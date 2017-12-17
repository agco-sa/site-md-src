---
currentMenu: ddi-seguranca
parentMenu: ddi
---
# Dealer Data Integration

## 3. Segurança
A fim de garantir a segurança das informações transmitidas, todas as chamadas devem ser feitas com SSL.
Além da criptografia da comunicação, o uso da API exige que as chamadas sejam autenticadas através do padrão BasicAuth, e ele é realizado através do uso de headers nas chamadas das operações. Além das informações de segurança, mais headers são especificados conforme a tabela a seguir.

###3.1 Como gerar o token
Para gerar o token deve-se enviar uma requisição POST para a URL:
| Ambiente | URL |
|---|---|
| Teste | https://appsqa.agcoonline.com.br/SecurityApi/Token |
| Produção| https://appsqa.agcoonline.com.br/SecurityApi/Token |

Com as seguintes informações de cabeçalho:
| Header | Informação |
|---|---|
| X-OpenAM-Username | Usuário |
| X-OpenAM-Password | Senha |
Caso a requisição seja realizada com sucesso, o servidor de autenticação enviará o código HTTP 200 (OK) e o corpo da resposta com o token, como exemplificado abaixo:

     "tokenId": "<TOKEN>",
     "successUrl": ""

Caso contrário o servidor irá responder com um código HTTP 400 (Bad Request) ou 401 (Unauthorized), sem corpo na resposta.
Após o recebimento do token, o mesmo deverá ser enviado em todas as requisições para o serviço do DDI através do seguinte cabeçalho:

|  Propriedade | Descrição  | Exemplo  |
|---|---|---|
| Authorization| Inserir no header a seguinte propriedade: “**Authorization**: Basic <token>" Onde <**token**> é a conversão da concatenação <**usuario**>:<**senha**> em base64. Como auxílio, pode-se usar a função btoa(“usuario:senha”) no modo debug de algum navegador, sendo retornado o valor em base64. Pode-se também utilizar sites que convertem para base64, por exemplo: [http://base64-encoder-online.waraxe.us/](http://base64-encoder-online.waraxe.us/) | Authorization: Basic dGVzdGU6dGVzdGU=   |
| Content-Type |Inserir no header a seguinte propriedade: “**Content-Type:application/json**”|Content-Type:application/json |

###3.2 Observações
O token gerado poderá ser invalidado conforme regras internas, como tempo de ociosiodade (tempo após o último uso). Caso isso aconteça, é responsabilidade da aplicação do cliente gerar um novo token e continuar o processo. 
O código de resposta que será enviado pela aplicação VMI caso o token tenha sido invalidado será o código HTTP 401 (Unauthorized).



