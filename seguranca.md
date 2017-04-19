---
currentMenu: seguranca
---

# Segurança
A fim de garantir a segurança das informações transmitidas, todas as chamadas devem ser feitas com SSL.
Além da criptografia da comunicação, o uso da API exige que as chamadas sejam autenticadas. O modo de autenticação é o Basic Auth, e ele é feito através do uso de headers nas chamadas das operações.
Além das informações de segurança, mais headers são especificados conforme a tabela a seguir.

|  PROPRIEDADE  | DESCRIÇÃO  | EXEMPLO  |
|---|---|---|
| Authorization| Inserir no header a seguinte propriedade: “**Authorization**: Basic <token>" Onde <**token**> é a conversão da concatenação <**usuario**>:<**senha**> em base64. Como auxílio, pode-se usar a função btoa(“usuario:senha”) no modo debug de algum navegador, sendo retornado o valor em base64. Pode-se também utilizar sites que convertem para base64, por exemplo: [http://base64-encoder-online.waraxe.us/](http://base64-encoder-online.waraxe.us/) | Authorization: Basic dGVzdGU6dGVzdGU=   |
| Content-Type |Inserir no header a seguinte propriedade: “**Content-Type: application/json**”|Content-Type: application/json |


