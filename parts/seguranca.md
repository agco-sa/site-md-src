---
currentMenu: parts-seguranca
parentMenu: parts
---

# Argentina Parts

## 3. Segurança
A fim de garantir a segurança das informações transmitidas, todas as chamadas devem ser feitas com SSL/TLS.<br/>
Além da criptografia da comunicação, o uso da API exige que as chamadas sejam autenticadas através de token utilizando-se do padrão OAuth2.

### 3.1. Como gerar o token
Para gerar o token deve-se enviar uma requisição POST para a URL:

|Ambiente|URL|
|--------|---|
|Teste|https://appsqa.agcoonline.com.br/SecurityApi/Token |
|Produção|https://apps.agcoonline.com.br/SecurityApi/Token |

Com as seguintes informações no cabeçalho:

|Header|Informação|
|------|----------|
|X-OpenAM-Username|	usuário|
|X-OpenAM-Password|	senha|

Caso a requisição seja efetuada com sucesso, o servidor de autenticação enviará o código HTTP 200 (OK) e o corpo da resposta com o token, como exemplificado abaixo:

    {
      "tokenId": "<TOKEN>",
      "successUrl": ""
    }

Caso contrário o servidor irá responder com um código HTTP 400 (Bad Request) ou 401 (Unauthorized), sem corpo na resposta.<br/>
Após o recebimento do token, o mesmo deverá ser enviado em todas as requisições para o serviço do VMI através do seguinte cabeçalho:

|Header|Informação|
|------|----------|
|Authorization|	Bearer <TOKEN\>|
|Content-Type|	application/json|

### 3.2. Observações
O token gerado poderá ser invalidado conforme regras internas, como tempo de ociosidade (tempo após o último uso). Caso isso aconteça, é responsabilidade da aplicação cliente gerar um novo token e continuar com o processo. O código de resposta que será enviado pela aplicação VMI caso o token tenha sido invalidado será o código HTTP 401 (Unauthorized).
