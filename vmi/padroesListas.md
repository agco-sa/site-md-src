---
currentMenu: vmi-padroes-listas
parentMenu: vmi
---


# Vendor Management Inventory Integration

## 5. Padrões e lista de valores
Essa sessão contém os padrões e lista de valores utilizados no contrato de dados.
### 5.1. Padrões utilizados no campos
Abaixo estão os padrões existentes no contrato de dados.

|Código|Padrão|Exemplo|Referência|
|------|------|-------|----------|
|P001	|ISO 8601|	YYYY-MM-DDThh:mm:ss+03:00|	 |
|P002	|ISO 4217|	BRL	 | |
|P003	|ISO 3166-2	|"BR"|	https://www.iso.org/obp/ui/#search/code/|
|P004	|ISO 3166-2|"BR-RS"	| No final da url https://www.iso.org/obp/ui/#iso:code:3166: coloque o código do país da ISO 3166-2.<br/> Exemplo: [https://www.iso.org/obp/ui/#iso:code:3166:BR](https://www.iso.org/obp/ui/#iso:code:3166:BR)|


### 5.2. Lista de valores
Abaixo estão as listas de valores utilizadas em alguns campos no contrato de dados.

|Código|Valores|Descrição|
|------|-------|---------|
|V001|true<br/>false|true: item original AGCO<br/>false: item não original AGCO|
|V002|true<br/>false|true: item estocável<br/>false: item não estocável|
|V003|true<br/>false|true: registro representa uma primeira compra do item<br/>false: registro não representa uma primeira compra do item|
|V004|"STOCK_ORDER"<br/>"VOR"<br/>"SERVICE"<br/>"TRANSFER"|STOCK_ORDER: pedido de estoque, semanal, etc<br/>VOR: pedidos emergenciais ou de máquina parada<br/>SERVICE: pedidos de garantia<br/>TRANSFER: pedidos de transferência entre filiais|
|V005|"REPVT03"<br/>"REPVT06"<br/>""|REPVT03: pedidos atendidos por Jundiaí<br/>REPVT06: pedidos atendidos por Ernestina<br/>Vazio: pedidos não atendidos pela AGCO|
|V006|"OPEN"<br/>"CLOSED"<br/>"CANCELLED"|OPEN: linha do pedido está pendente de atendimento<br/>CLOSED: linha do pedido entrou no estoque da concessionária<br/>CANCELLED: linha do pedido foi cancelada|
|V007|"S"<br/>"W"<br/>"T"<br/>"R"|S: venda<br/>W: oficina<br/>T: transferência<br/>R: devolução|
|V008|"REGULAR"<br/>"EXPEDITE"|REGULAR: entrega normal<br/>EXPEDITE: entrega expressa|
|V009|"OPEN"<br/>"RESERVED"<br/>"CLOSED"<br/>"CANCELLED"|OPEN: linha da venda está pendente de atendimento<br/>RESERVED: linha da venda tem reserva no estoque<br/>CLOSED: linha da venda foi enviado para o cliente<br/>CANCELLED: linha da venda foi cancelada pelo cliente|
|V010|"RC"<br/>"GE"<br/>"IN"<br/>"FO"|RC: cliente regular<br/>GE: orgão público<br/>IN: indústria<br/>FO: frotista|
|V011|true<br/>false|true: é uma venda atípica<br/>false: não é uma venda atípica|


### 5.3. Regras
Abaixo estão as regras aplicadas em alguns campos do contrato de dados

|Código|Regra|
|------|-----|
|R001	|Quando o campo firstPurchase = true esse campo deve estar preenchido|
|R002	|Quando o campo lineStatus = "CLOSED" esse campo deve estar preenchido|
