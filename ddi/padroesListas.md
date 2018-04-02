---
currentMenu: ddi-padroes-listas
parentMenu: ddi
---

# DDI

## 5. Padrões e lista de valores
Essa sessão contém os padrões e lista de valores utilizados no contrato de dados.
### 5.1. Padrões utilizados no campos
Abaixo estão os padrões existentes no contrato de dados.

|Código|Padrão|Exemplo|Referência|
|------|------|-------|----------|
|P001|ISO 3166-2|"pt-BR"|No final da url https://www.iso.org/obp/ui/#iso:code:3166: coloque o código do país da ISO 3166-2.<br/> Exemplo: [https://www.iso.org/obp/ui/#iso:code:3166:BR](https://www.iso.org/obp/ui/#iso:code:3166:BR)|
<br/>

### 5.2. Lista de valores
Abaixo estão as listas de valores utilizadas em alguns campos no contrato de dados.

|Código|Valores|
|------|-------|
|V001|Ativa = ? / Inativa = ?|
|V002|Pattern yyyy-MM-dd’T’HH:mm:ss.SSS’Z’|
|V003|Pattern yyyy-MM-dd'T'HH:mm:ss.SSS'Z'|
|V004|I= Interno, E = Externo|
|V005|Tamanho Min = 1 Max = 12|

<br/>

### 5.3. Regras
Abaixo estão as regras aplicadas em alguns campos do contrato de dados

|Código|Regra|
|------|-----|
|R001|Informar a chave de acesso da NFe precedida do literal ‘NFe’, acrescentada a validação do formato|
|R002|Se existir a informação de CPF o campo CNPJ deve vir vazio|
|R003|Se existir a informação de CPF o campo CNPJ deve vir vazio|
|R004|Se existir a informação de CPF o campo CNPJ deve vir vazio|
|R005|Se existir a informação de CNPJ o campo CPF deve vir vazio|
|R006|Preencher com zeros na hipótese de a NF-e não possuir série|
|R007|O XML da NF é obrigatório ao informar uma campanha. O valor da nota é obrigatório ao informar uma campanha|
|R008|Brand must not be Empty or null|
|R009|ID must not be Empty or null|
|R010|Model must not be Empty or null|
|R011|Não pode ser vazio ou null|
|R012|Não pode ser vazio ou null|
|R013|ProductType must not be Empty or null|
|R014|Utilizar código 55 para identificação da NF-e, emitida em substituição ao modelo 1 ou 1A|


<br/>
