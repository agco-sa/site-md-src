---
currentMenu: parts-padroes-listas
parentMenu: parts
---

# Argentina Parts

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

|Código|Valores|Descrição|
|------|-------|---------|
|V001|pt-BR<br>es-AR|Se não informado o parâmetro 'lang' o sistema detecta a localização do Dealer para definir linguagem|
|V002|pt<br/>es<br/>en|pt = Português<br/>es = Espanhol<br/>en = Inglês<br/>|
|V003|Y<br/>N|Y = Yes<br/>N = No|
|V004|A<br/>B<br/>D<br/>vazio<br/>null|A = Ativa<br/>B = Broken<br/>D = Desativada<br/>" "<br/>null|
|V005|SP<br/>SI<br/>IN<br/>CO<br/>CS<br/>SS|SP = Simples Parcial<br/>SI = Simples<br/>IN = Informativa<br/>CO = Composta</br>CS = Composta Seletiva<br/>SS = Simples Seletiva|

<br/>

### 5.3. Regras
Abaixo estão as regras aplicadas em alguns campos do contrato de dados

|Código|Regra|
|------|-----|
|R001	|Quando parâmetro "null" retorna vazio|
|R002	|Quando não for encontrado nenhum registro retorna vazio|

#### 5.3.1. Fluxo e regras tipos de substituições
![Fluxo Tipos Substituições](https://github.com/agco-sa/site-md-src/blob/parts/images/tipos-substituicoes.png)
