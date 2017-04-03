![AGCO_logo](http://www.agco.com.br/content/agcocorp/pt_BR/_jcr_content/footermainparsys/footer/footerlogoimage.img.png/1485893878104.png)
# Integração VMI

## Padrões e lista de valores
Essa sessão contém os padrões e lista de valores utilizados no contrato de dados.
### 1. Padrões utilizados no campos
Abaixo estão os padrões existentes no contrato de dados.

|Código|Padrão|Exemplo|Referência|
|------|------|-------|----------|
|P001	|ISO 8601|	YYYY-MM-DDThh:mm:ss+03:00|	 |
|P002	|ISO 4217|	BRL	 | |
|P003	|ISO 3166-2	|"BR"|	https://www.iso.org/obp/ui/#search/code/|
|P004	|ISO 3166-2|"BR-RS"	| No final da url https://www.iso.org/obp/ui/#iso:code:3166: coloque o código do país da ISO 3166-2. Exemplo: https://www.iso.org/obp/ui/#iso:code:3166:BR|


### 2. Lista de valores
Abaixo estão as listas de valores utilizadas em alguns campos no contrato de dados.

|Código|Valores|Descrição|
|------|-------|---------|
|V001	|true|true: item original AGCO|
||false|false: item não original AGCO|
|V002	|true|true: item estocável|
| | false|false: item não estocável|
|V003	|true|true: registro representa uma primeira compra do item|
| | false|false: registro não representa uma primeira compra do item|
|V004	|"STOCK_ORDER" | STOCK_ORDER: pedido de estoque, semanal, etc|
||"VOR"|VOR: pedidos emergenciais ou de máquina parada|
||"SERVICE"|SERVICE: pedidos de garantia|
||"TRANSFER"|TRANSFER: pedidos de transferência entre filiais|
|V005	|"REPVT03"|REPVT03: pedidos atendidos por Jundiaí|
||"REPVT06"|REPVT06: pedidos atendidos por Ernestina|
||""|Vazio: pedidos não atendidos pela AGCO|
|V006	|"OPEN"|OPEN: linha do pedido está pendente de atendimento|
||"CLOSED"|CLOSED: linha do pedido entrou no estoque da concessionária|
||"CANCELLED"|CANCELLED: linha do pedido foi cancelada|
|V007	|"S"|S: venda|
||"W"|W: oficina|
||"T"|T: transferência|
||"R"|R: devolução|
|V008	|"REGULAR"|REGULAR:|
||"EXPEDITE"|EXPEDITE:|
|V009	|"OPEN"|OPEN: linha da venda está pendente de atendimento|
||"RESERVED"|RESERVED: linha da venda tem reserva no estoque|
||"CLOSED"|CLOSED: linha da venda foi enviado para o cliente|
||"CANCELLED"|CANCELLED: linha da venda foi cancelada pelo cliente|
|V010	|"RC"|RC: cliente regular|
||"GE"|GE: orgão público|
||"IN"|IN: indústria|
||"FO"|FO: frotista|


### 3. Regras
Abaixo estão as regras aplicadas em alguns campos do contrato de dados

|Código|Regra|
|------|-----|
|R001	|Quando o campo firstPurchase = true esse campo deve estar preenchido|
|R002	|Quando o campo lineStatus = "CLOSED" esse campo deve estar preenchido|