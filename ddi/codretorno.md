---
currentMenu: ddi-codretorno
parentMenu: ddi
---


# Dealer Data Integration
## 4. Códigos de Retorno

Ao enviar uma mensagem para o serviço, será retornado um código que varia de acordo com o resultado do processamento da mensagem AGCO. A lista de possíveis retornos, assim como as ações a serem tomadas em cada caso de erro, são descritas na tabela a seguir.

|CÓDIGO | STATUS |DESCRIÇÃO                  |AÇÃO|
|-------|--------|---------------------------|----|
| 201   | Sucesso| Dados criados com sucesso | \- |
| 400   | Erro   | Requisição inválida       | Rever formato dos dados enviados. Exemplo: Header incompleto, formato JSON incorreto, campos obrigatórios faltando, etc)|
| 401   | Erro   | Usuário não autorizado    | Verificar usuário e senha. Valores válidos corretamente convertidos em base64 no header. |
| 404   | Erro   | Endereço não encontrado   | Revisar URL de acesso ao serviço. |
| 422   | Erro   | Dados inválidos           | Entrar em contato com o DSS       |

Referência: http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html

### 4.1. Validação de dados
Todos os dados enviados devem passar pelas validações abaixo. Caso os critérios não sejam atendidos será retornado um erro **422**.
Neste caso, os dados incorretos devem ser corrigidos antes de serem re-enviados.

| ERRO | DESCRIÇÃO | TAG PAI | EXEMPLO DE ERRO |
| -----| --------- | ------- | --------------- |
| 1 | CNPJ do emitente não existe na base | NFe/infNFe/emit | "CNPJ": "99999999999999” *(CNPJ da filial deve existir na base)* |
| 2 | Informe apenas uma das opções: CPF ou CNPJ do destinatário | NFe/infNFe/dest | "CPF": "11111111111”, "CNPJ": "99999999999999” *(somente um dos dois deve ser enviado)*|
| 3 | O CNPJ do destinatário precisa ser válido | NFe/infNFe/dest | "CNPJ": "55555” *(CNPJ deve ser válido)*|
| 4 | O CPF do destinatário precisa ser válido | NFe/infNFe/dest | "CPF": "777” *(CPF deve ser válido)* |
| 5 | Informe apenas uma das opções: CPF ou CNPJ do emissor | NFe/infNFe/emit | "CPF": "11111111111”, "CNPJ": "99999999999999” *(somente um dos dois deve ser enviado)* |
| 6 | O CNPJ do emitente precisa ser válido | NFe/infNFe/emit | "CNPJ": "55555” *(CNPJ deve ser válido)* |
| 7 | O CPF do emitente precisa ser válido | NFe/infNFe/emit | "CPF": "777” *(CPF deve ser válido)*|
| 8 | O produto enviado não existe no estoque | ddi/prodDet/prod | "codigoItem": "42754F0913D", "serieComercial": "4275344889", "monobloco": " AAAT0012PCC002382" *(produto deve existir no estoque da filial)* |
| 9 | O tipo da nota fiscal não é válido | NFe/infNFe/ide | "tpNF": 9 *(deve ser 0 ou 1)* |
| 10 | O tipo da operação não é válido | ddi | "tipoOp": 9 *(deve ser 1, 4 ou 5)* |
| 11 | A data de emissão deve ser válida e menor do que a data atual | NFe/infNFe/ide | "dhEmi": "2099-01-01T00:00:00.000Z" *(data deve ser menor que a atual)* |
| 12 | Município do destinatário não existe na base | NFe/infNFe/dest /enderDest | "cMun": 111111 *(código do município deve existir na base)* |
| 13 | Produto não pode ser devolvido | ddi/prodDet/prod | "codigoItem": "42754F0913D", "serieComercial": "4275344889", "monobloco": " AAAT0012PCC002382" *(produto não está com status disponível para devolução)* |
| 14 | CNPJ do destinatário não existe na nota | NFe/infNFe/dest | "CNPJ": "” *(CNPJ está vazio ou não existe a tag)* |
| 15 | CNPJ do emitente não existe na nota | NFe/infNFe/emit | "CNPJ": "” *(CNPJ está vazio ou não existe a tag)* |
| 16 | CNPJ da nota é diferente do CNPJ da concessionária | NFe/infNFe/dest ou NFe/infNFe/emit | "CNPJ": "99999999999999” *(CNPJ enviado é diferente do CNPJ que está com o produto em estoque)* |
| 17 | CNPJ do destinatário não existe na base | NFe/infNFe/dest | "CNPJ": "99999999999999” *(CNPJ enviado não existe na base)* |
| 18 | Produtos duplicados na nota fiscal | ddi/prodDet/prod | "codigoItem": "42754F0913D", "serieComercial": "4275344889", "monobloco": " AAAT0012PCC002382" *(produto aparece duas vezes na mesma nota fiscal)* |
| 19 | CNPJ não existe na base | NFe/infNFe/emitNFe/infNFe/dest | "CNPJ": "02050252” (CNPJ não está cadastrado na AGCO) |
| 20 | O Xml da nota é obrigatório ao informar uma campanha | xml | Informação de campanha informada, mas XML não foi informado |
| 21 | Nota Fiscal já cadastrada | NFe/infNFe/ide | "nNF": 14253 (nota fiscal já está informada com base no CNPJ, número da nota e série) |
| 22 | Já existe uma nota fiscal mais recente no sistema para esse produto. | NFe/infNFe/ide | "dhEmi": "2018-01-01T00:00:00.000Z" (se já existir uma nota para o produto a nova nota deve ter data maior do que a data da nota anterior) |














