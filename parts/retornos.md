---
currentMenu: parts-retornos
parentMenu: parts
---

# Argentina Parts

## 4. Códigos de Retorno
Se efetuar uma requisição com retorno de sucesso ou se efetuar uma requisição com alguma inconsistência na sua formulação ou no seu retorno poderão ser apresentados os seguintes status:

|Código|Status|Descrição|Ação|
|------|------|---------|----|
|200|	Sucesso|	Busca realizada com sucesso|	-|
|400|	Erro|	Requisição inválida|Rever formato dos dados enviados<br/><br/>_(header incompleto, formato JSON incorreto, campos obrigatórios faltando, etc)_|
|401|	Erro|	Usuário não autenticado|Verificar usuário e senha|
|403|	Erro|	Usuário não autorizado|	Usuário não tem acesso aos dados ou token expirado|
|404|	Erro|	Endereço não encontrado|Revisar url de acesso ao serviço.|
|409|	Erro|	Conflito no banco de dados|	Rever dados enviados.|

Referência: http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html


