---
currentMenu: vmi-returncodes
parentMenu: vmi
---

# Integração VMI

## Códigos de Retorno
Ao enviar uma mensagem para o serviço, será retornado um código que varia de acordo com o resultado do processamento da mensagem na AGCO. A lista de possíveis retornos, assim como as ações a serem tomadas em cada caso de erro, são descritas na tabela a seguir.

|Código|Status|Descrição|Ação|
|------|------|---------|----|
|200|	Sucesso|	Dados atualizados com sucesso|	-|
|201|	Sucesso|	Dados inseridos com sucesso|	-|
|304|	Sucesso|	Mensagem descartada devido a dados já presentes no banco|	-|
|400|	Erro|	Requisição inválida|Rever formato dos dados enviados _(header incompleto, formato JSON incorreto, campos obrigatórios faltando, etc)_|
|401|Erro|Usuário não autenticado|Verificar usuário e senha|
|403|	Erro|	Usuário não autorizado|	Usuário não tem acesso aos dados ou token expirado|
|404|Erro|Endereço não encontrado|Revisar url de acesso ao serviço.|
|409|	Erro|	Conflito no banco de dados|	Rever dados enviados.|
|422|Erro|Dados inválidos|Rever dados enviados._(as validações realizadas pelo sistema estão na sessão 4.1)_|
|500|Erro|Erro inesperado|Entrar em contato com o DSS.|
|504|Erro|Problema de comunicação entre proxy e aplicação|Entrar em contato com o DSS.|

Referência: http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html

### 1. Validação de dados
Todos os dados enviados devem passar pela validação abaixo. Caso os critérios não sejam atendidos será retornado um erro **422**.
Neste caso, os dados incorretos devem ser corrigidos antes de serem re-enviados.

|Erro|Descrição|Mensagem de erro|Exemplo de valor enviado|
|----|---------|----------------|------------------------|
|001|Tipo de dado não está correto|Status: "422" – expected type: <tipo esperado>, found: <tipo recebido>|
|002|Formato da mensagem JSON enviada está incorreto|Status: "422" – Invalid JSON Format||
|003|A data enviada não está de acordo com o padrão definido P001|Status: "422" – string <data enviada> does not match pattern ^\\\\d{4}\\\\-(0?[1-9]\|1[012])\\\\-(0?[1-9]\|[12][0-9]\|3[01])$ |2005/10/30|
|004|Formato do número enviado não está correto| Status: "422" – <valor recebido> is not a multiple of 0.01|123.4512|
|005|Valor negativo enviado em campo que aceita apenas números positivos| Status: "422" – <valor recebido> is not higher or equal to 0|-123.45|
|006|Valor enviado com tamanho maior do que o esperado|Status: "422" – <campo> expected maxLength: <tamanho máximo esperado>, actual: <tamanho máximo enviado>|	|
|007|CNPJ do dealer não existe na base da AGCO ou está inativo|Status: "422" –  Invalid dealerLegalNumber provided. Dealer not found or is not currently active|	|
|008|Campo obrigatório não foi enviado na mensagem|Status: "422" – required key <campo> not found|	|
|009|Não foi atendida a regra R001|Status: "422" – <campo> is required when firstPurchase is true|	|
|010|O valor enviado não está de acordo com a lista de valores aceitos. Conforme item 5.2|Status: "422" – <valor recebido> is not a valid enum value"|	usd|
|011|O CNPJ enviado não é válido|Status: "422" – <campo> is an invalid legal number||
|012|Não foi atendida a regra R002|Status: "422" – <campo> is required when lineStatus is CLOSED| |
