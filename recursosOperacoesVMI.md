![AGCO_logo](http://www.agco.com.br/content/agcocorp/pt_BR/_jcr_content/footermainparsys/footer/footerlogoimage.img.png/1485893878104.png)
# Integração VMI

## Recursos e operações
Essa sessão contém os campos e regras das interfaces disponibilizadas para capturar informações de peças das concessionárias.

### 1. Interface Inventory Data
Exemplo de JSON para a interface Inventory Data

        {
          "data": {
            "dealerLegalNumber": "99.999.999/0001-99",
            "extractionDateTime": "2016-11-23T10:45:00+03:00",
            "part": {
              "partNumber": "1444437P",
              "availableQuantity": 20,
              "onOrderQuantity": 1.5,
              "reservedQuantityWorkOrders": 1.5,
              "reservedQuantityPartTickets": 1.5,
              "openCustomerOrders": 1.5,
              "quantityReturnedByDealer": 10,
              "quantityReturnedByCustomerCounter": 1.5,
              "quantityReturnedByCustomerShop": 1.5,
              "quantityReturnedTotal": 1.5
            }
          }
        }



**Especificação dos atributos**

|**ID**|**Campo**|**Pai**|**Tipo**|**Descrição**|**Obrigatório**|**Regra**|**Exemplo**|
|----|-----|---|----|---------|-----------|-----|---------|
|A01	|data|	Raiz|	 |	TAG raiz da mensagem|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)	 	| ||
|A02	|dealerLegalNumber|	| 	varchar(50)|	CNPJ da concessionária|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)	||	"99.999.999/0001-99"|
|A03	|extractionDateTime	| 	|timestamp|	Data da extração dos dados da mensagem|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)	|P001|"2016-11-23T10:45:00+03:00"|
|A04	|parts|	A01|	| 	Grupo que contém as informações de peças|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	 |	| 
|A05| partsNumber	|A04|	varchar(50)|	Código do item vendido pela concessionária.Código original da concessionária|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	 |	"1444437P"|
|A06|	availableQuantity|	A04	|number(10,2)	|Quantidade de itens disponíveis no estoque para venda |![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	| 	20|
||||| - Excluir desse número peças que estão reservadas para ordens de serviços e que ainda não foram contadas como venda. ||||
||||| - Excluir desse número peças que estão reservadas para atender pedidos de venda. ||||
||||| - Excluir desse número peças pendentes de transferências||||
|A07|	onOrderQuantity|	A04|	number(10,2)	|Quantidade de itens com pedidos de compras em aberto ou transferências entre filiais pendentes e que não foram baixados no estoque.|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)	||15|
|||||1.1 Pedidos||||
|||||- Contar todas as peças em pedidos de compra, independente do tipo de pedido (emergência, estoque, etc), tirando os de compras realizados especificamente para um cliente.||||
|||||1.2 Transferências||||
|||||- Contar todos os pedidos pendentes de transferências internas, tirando os itens que já estão alocados para um cliente específico, assim como itens que estão em pedidos de balcão ou oficina||||
|A08	|reservedQuantityWorkOrders|	A04|	number(10,2)|	Itens reservados para ordens de serviços abertas na oficina e que ainda não foram contados como venda.|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)||	 	1.5|
|A09|	reservedQuantityPartTickets	|A04|	number(10,2)|	Itens reservados para pedidos de balcão e que ainda não foram contados como venda.	|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)	 |	|1.5|
|A10|	openCustomerOrders|	A04|	number(10,2)|	Soma de itens em pedidos em aberto para cliente final.|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	| 	1.5|
|A11	|quantityReturnedByDealer|	A04|	number(10,2)|	Itens retornados da concessionária para a AGCO.|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|| 	10|
|A12|	quantityReturnedByCustomerCounter|	A04|	number(10,2)|	Itens retornados por pedidos de balcão para a concessionária.|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |	1.5|
|A13	|quantityReturnedByCustomerShop|	A04|	number(10,2)|	Itens retornados por pedidos de oficina para a concessionária.|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	| 	1.5|
|A14|	quantityReturnedTotal|	A04|	number(10,2)|	Soma de itens retornados por pedidos de oficina e balcão para a concessionária.|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)	| |	1.5|

### 2. Interface Parts Data
Exemplo de JSON para a interface Parts Data

        {
          "data": {
            "dealerLegalNumber": "99.999.999/0001-99",
            "extractionDateTime": "2016-11-23T10:45:00+03:00",
            "part": {
              "partNumber": "1444437P",
              "agcoPartNumber": "1480626M1",
              "originalPart": true,
              "description": "REPARO PLATO  C/ ALAVANCA 8 VELOCIDADE",
              "dealerNote": "Parafuso 12X70 MM Locação Obsoletos",
              "stockable": true,
              "lastSaleDate": "2016-11-23",
              "mainBinLocation": "E 03 03",
              "alternateBinLocation": "E 03 03",
              "minimumThreshold": 1.5,
              "maximumThreshold": 1.5,
              "preferredSupplierLegalNumber": "00.000.000/0001-00",
              "preferredSupplierName": "NOME FANTASIA DO FORNECEDOR",
              "netPrice": 200.00,
              "averageCost": 200.00,
              "unitOfMeasure": "M",
              "dealerPartsPerPackage": 1.5,
              "currencyCode": "BRL",
              "lastPurchasePrice": 200.00,
              "openPurchaseOrders": 10,
              "vendorPackageQuantity": 10,
              "segmentationCode01": "FLT",
              "segmentationCode02": "",
              "segmentationCode03": "",
              "segmentationCode04": "",
              "firstAvailableDate": "2016-11-23",
              "firstPurchase": false
            }
          }
        }



**Especificação dos atributos**

|ID|Campo|Pai|Tipo|Descrição|Obrigatório|Regra|Exemplo|
|--|-----|---|----|---------|-----------|-----|-------|
|B01|data|Raiz| |TAG raiz da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | | 
|B02|dealerLegalNumber|B01|varchar(50)|CNPJ da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"99.999.999/0001-99"|
|B03|extractionDateTime|B01|timestamp|Data da extração dos dados da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|P001|"2016-11-23T10:45:00+03:00"|
|B04|part|B01||Grupo que contém as informações de peças|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|B05|partsNumber|B04|varchar(50)|Código do item. Código original da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"1444437P"|
|B06|agcoPartNumber|B04|varchar(50)|Código do item AGCO. Se o item não for um item original AGCO a concessionária deve ter um código AGCO que corresponda ao item em questão|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"1480626M1"|
|B07|originalPart|B04|boolean|Informação que define se o item é um item original AGCO ou não|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|V001|true|
|B08|description|B04|varchar(60)|Descrição da peça da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"REPARO PLATO  C/ ALAVANCA 8 VELOCIDADES"|
|B09|dealerNote|B04|varchar(60)|Observações da concessionária para o item|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |"Parafuso 12X70 MM Locação Obsoletos"|
|B10|stockable|B04|boolean|É um item estocável ou não|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|V002|true|
|B11|lastSaleDate|B04|date|Última data de venda da peça (data de nota fiscal)|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |"2016-11-23"|
|B12|mainBinLocation|B04|varchar(60)|Local principal de armazenamento da peça na concessionária. Se não existe a informação para o item enviar apenas os delimitador|	R001|	|"E   03  03"|
|B13|alternateBinLocation|B04|varchar(60)|Local secundário de armazenamento da peça na concessionária.|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |"E   03  03"|
|B14|minimumThreshold|B04|number(10,2)|Estoque mínimo para o item na concessionária|R001| |1,5|
|B15|maximumThreshold|B04|number(10,2)|Estoque máximo para o item na concessionária|R001| |1,5|
|B16|preferredSupplierLegalNumber|B04|varchar(50)|CNPJ do fornecedor do item|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"00.000.000/0001-00"|
|B17|preferredSupplierName|B04|varchar(100)|Nome fantasia do fornecedor preferencial para o item|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |"NOME FANTASIA DO FORNECEDOR"|
|B18|netPrice|B04|number(14,2)|Preço de lista do item na concessionária|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |200,00|
|B19|averageCost|B04|number(14,2)|Custo médio do item na concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |200,00|
|B20|unitOfMeasure|B04|varchar(3)|Unidade de medida de armazenamento do item|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"M"|
|B21|dealerPartsPerPackage|B04|number(14,2)| |![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |1,5|
|B22|currencyCode|B04|varchar(3)|Código da moeda|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|P002|"BRL"|
|B23|lastPurchasePrice|B04|number(14,2)|Último preço de venda pago|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	|200.00|
|B24|openPurchaseOrders|B04|number|Quantidade de itens em pedidos de compras abertos|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|10|
|B25|vendorPackageQuantity|B04|number|Informação apenas para itens não AGCO:Embalagem mínima que o item é solicitado no fornecedor|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |10|
|B26|segmentationCode01|B04|varchar(30)|Campo para informações de segmentação da concessionária|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	|"FLT"|
|B27|segmentationCode02|B04|varchar(30)|Campo para informações de segmentação da concessionária|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|B28|segmentationCode03|B04|varchar(30)|Campo para informações de segmentação da concessionária|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|B29|segmentationCode04|B04|varchar(30)|Campo para informações de segmentação da concessionária|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|B30|firstAvailableDate|B04|date|Data da primeira movimentação do item na filial. Opção 1: enviar a data que a peça foi recebida pela primeira vez no estoque. Opção 2: se não tiver a informação da opção 1 enviar a data que a peça foi solicita pela primeira vez pela oficina. Opção 3: se não tiver a informação das opções 1 e 2 enviar a data que a peça foi adicionada pela primeira vez no estoque. Opção 4: se não tiver a informação das opções 1, 2 e 3 enviar a data 1900-01-01|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"2016-11-23"|
|B31|firstPurchase|B04|boolean|Esse campo identifica se essa peça nunca esteve em estoque porque é um registro de primeira compra|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|V003|false|


### 3. Interface Purchase Order
Exemplo de JSON para a interface Purchase Order

    {
      "data": {
        "dealerLegalNumber": "99.999.999/0001-99",
        "extractionDateTime": "2016-11-23T10:45:00+03:00",
        "order": {
          "orderId": "34562",
          "orderAgco": "AOL-123456",
          "orderIdOriginal": "4567",
          "deliveredDealerLegalNumber": "11.000.000/0001-00",
          "orderDate": "2016-11-23",
          "orderType": "STOCK_ORDER",
          "supplierLegalNumber": "00.000.000/0001-00",
          "supplierName": "NOME FANTASIA DO FORNECEDOR",
          "filter1": "",
          "filter2": "",
          "filter3": "",
          "items": [
            {
              "sourceLocation": "REPVT03",
              "orderLineNumber": "1",
              "partNumber": "1444437P",
              "receivedDate": "2016-11-23",
              "requestedQuantity": 1.5,
              "receivedQuantity": 1.5,
              "openQuantity": 1.5,
              "canceledQuantity": 1.5,
              "lineStatus": "OPEN"
            }
          ]
        }
      }
    }


**Especificação dos atributos**

|ID|Campo|Pai|Tipo|Descrição|Obrigatório|Regra|Exemplo|
|--|-----|---|----|---------|-----------|-----|-------|
|C01|data|Raiz| |TAG raiz da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|C02|dealerLegalNumber|C01|varchar(50)|CNPJ da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"99.999.999/0001-99"|
|C03|extractionDateTime|C01|timestamp|Data da extração dos dados da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|P001|"2016-11-23T10:45:00+03:00"|
|C04|order|C01||Grupo que contém as informações de pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|C05|orderID|C04|varchar(50)|Número do pedido na concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"34562"|
|C06|orderAgco|C04|varchar(10)|Número do pedido AGCO|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |"AOL-123456"|
|C07|orderIdOriginal|C04|varchar(50)|Número original do pedido na concessionária. O valor desse campo nunca pode mudar. Deve sempre manter o primeiro número recebido pelo pedido|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	|"4567"|
|C08|deliveredDealerLegalNumber|C04|varchar(50)|CNPJ da filial que receberá o pedido|	![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"11.000.000/0001-00"|
|C09|orderDate|C04|date|Data da abertura do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"2016-11-23"|
|C10|orderType|C04|varchar(50)|Tipo do pedido|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|V004|"STOCK_ORDER"|
|C11|supplierLegalNumber|C04|varchar(50)|CNPJ do fornecedor do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"00.000.000/0001-00"|
|C12|supplierName|C04|varchar(100)|Nome fantasia do fornecedor do pedido|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |"NOME FANTASIA DO FORNECEDOR"|
|C13|filter1|C04|varchar|Campo utilizado para filtro de informações|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|C14|filter2|C04|varchar|Campo utilizado para filtro de informações|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|C15|filter3|C04|varchar|Campo utilizado para filtro de informações|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|C16|items|C04||Grupo que contém as informações de peças do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|C17|sourceLocation|C16|varchar(20)|Informação do armazém em que o pedido foi colocado na AGCO|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|V005|"REPVT03"|
|C18|orderLineNumber|C16|varchar(10)|Linha única do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"1"|
|C19|partNumber|C16|varchar(20)|Código do item vendido. Código original da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"1444437P"|
|C20|receivedDate|C16|date|Data que o item foi recebimento pela concessionária|R002| |"2016-11-23"|
|C21|requestedQuantity|C16|number(14,2)|Quantidade solicitada no pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|1,5|
|C22|receivedQuantity|C16|number(14,2)|Quantidade recebida pela filial da concessionária|R002| |1,5|
|C23|openQuantity|C16|number(14,2)|Quantidade pendentes de recebimento pela concessionária. Diferença entre a quantidade solicitada e recebida|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|1,5|
|C24|canceledQuantity|C16|number(14,2)|Quantidade de itens cancelados no pedido|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |1,5|
|C25|lineStatus|C16|varchar(20)|Status da linha do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|V006|"OPEN"|

### 4. Interface Sales Order
Exemplo de JSON para a interface Sales Order

    {
      "data": {
        "dealerLegalNumber": "99.999.999/0001-99",
        "extractionDateTime": "2016-11-23T10:45:00+03:00",
        "order": {
          "orderDate": "2016-11-23",
          "orderType": "W",
          "orderId": "1233",
          "customerLegalNumber": "000.000.000-00",
          "deliveryType": "REGULAR",
          "dealerFilter1": "",
          "dealerFilter2": "",
          "dealerFilter3": "",
          "items": [
            {
              "orderLineNumber": "1A2B3C4D5E",
              "partNumber": "1444437P",
              "firstPassFill": false,
              "demandDate": "2016-11-23",
              "requestedDate": "2016-11-23",
              "requestedQuantity": 1.5,
              "reservedQuantity": 1.5,
              "shippedQuantity": 15,
              "returnedQuantity": 10,
              "canceledQuantity": 0,
              "shippedDate": "2016-11-23",
              "quantityAvailable": 20,
              "lineStatus": "OPEN",
              "serialNumber": ""
            }
          ]
        }
      }
    }


**Especificação dos atributos**

|ID|Campo|Pai|Tipo|Descrição|Obrigatório|Regra|Exemplo|
|--|-----|---|----|---------|-----------|-----|-------|
|D01|data|Raiz| |TAG raiz da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|D02|dealerLegalNumber|D01|varchar(50)|CNPJ da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"99.999.999/0001-99"|
|D03|extractionDateTime|D01|timestamp|Data da extração dos dados da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|P001|"2016-11-23T10:45:00+03:00"|
|D04|order|D01||Grupo que contém as informações de pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|D05|orderDate|D04|date|Data que o pedido foi coloca no sistema|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"2016-11-23"|
|D06|orderType|D04|varchar(1)|Tipo do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|V007|"W"|
|D07|orderId|D04|varchar(50)|Número do pedido na concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"1233"|
|D08|customerLegalNumber|D04|varchar(50)|CPF ou CNPJ do cliente|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"000.000.000-00"|
|D09|deliveryType|D04|varchar(20)|Tipo de entrega do pedido|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|V008|"REGULAR"|
|D10|dealerFilter1|D04|varchar(100)|Campo utilizado para filtro de informações|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|D11|dealerFilter2|D04|varchar(100)|Campo utilizado para filtro de informações|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|D12|dealerFilter3|D04|varchar(100)|Campo utilizado para filtro de informações|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |
|D13|items|D04||Grupo que contém as informações de peças do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|D14|orderLineNumber|D13|varchar(10)|Linha única do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"1A2B3C4D5E"|
|D15|partNumber|D13|varchar(50)|Código do item vendido. Código original da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"1444437P"|
|D16|firstPassFill|D13|boolean|Identifica se o pedido foi atendido por completo no momento da solicitação|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	|false|
|D17|demandDate|D13|date|Data que surgiu a demanda do item. Por exemplo, data que a máquina quebrou|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	|"2016-11-23"|
|D18|requestedDate|D13|date|Data que foi solicitada a entrega do pedido|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |"2016-11-23"|
|D19|requestedQuantity|D13|number(14,2)|Quantidade que foi solicitada no pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |1.5|
|D20|reservedQuantity|D13|number(14,2)|Quantidades de itens que estão reservados e que ainda não estão contando como venda|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |1.5|
|D21|shippedQuantity|D13|number(14,2)|Quantidade de itens que já foram enviados para o cliente|R002|	|15|
|D22|returnedQuantity|D13|number(14,2)|Quantidade de itens que foram retornados do cliente para a concessionária|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	|10|
|D23|canceledQuantity|D13|number(14,2)|Quantidade de itens que foram cancelados pelo clinte na concessionária|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |0|
|D24|shippedDate|D13|date|Data que o pedido foi enviado para o cliente|R002| |"2016-11-23"|
|D25|quantityAvailable|D13|number(14,2)|Quantidade de itens disponíveis na data que o pedido foi solicitado|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	|20|
|D26|lineStatus|D13|varchar(20)|Status da linha do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|V009|"OPEN"|
|D27|serialNumber|D13|varchar(30)|Série comercial da maquina que esse item será utilizado|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| | |

### 5. Interface Lost Sales
Exemplo de JSON para a interface Lost Sales

    {
      "data": {
        "dealerLegalNumber": "99.999.999/0001-99",
        "extractionDateTime": "2016-11-23T10:45:00+03:00",
        "order": {
          "customerLegalNumber": "000.000.000-00",
          "partNumber": "1444437P",
          "lostSalesQuantity": 10,
          "lostSalesType": "W",
          "lostSalesDate": "2016-11-23"
        }
      }
    }


**Especificação dos atributos**

|ID|Campo|Pai|Tipo|Descrição|Obrigatório|Regra|Exemplo|
|--|-----|---|----|---------|-----------|-----|-------|
|E01|data|Raiz| |TAG raiz da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|E02|dealerLegalNumber|E01|varchar(50)|CNPJ da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"99.999.999/0001-99"|
|E03|extractionDateTime|E01|timestamp|Data da extração dos dados da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|P001|"2016-11-23T10:45:00+03:00"|
|E04|order|E01||Grupo que contém as informações de pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|E05|customerLegalNumber|E04|varchar(50)|CPF ou CNPJ do cliente|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)| |"000.000.000-00"|
|E06|partNumber|E04|varchar(50)|Código do item. Código original da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"1444437P"|
|E07|lostSalesQuantity|E04|number(14,2)|Quantidade de itens perdidos por falta de estoque|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|10|
|E08|lostSalesType|E04|varchar(1)|Tipo do pedido|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|V007|"W"|
|E09|lostSalesDate|E04|date|Data da perda da venda|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"2016-11-23"|

### 6. Interface Customer
Exemplo de JSON para a interface Customer

    {
      "data": {
        "dealerLegalNumber": "99.999.999/0001-99",
        "extractionDateTime": "2016-11-23T10:45:00+03:00",
        "customer": {
          "customerLegalNumber": "00.000.000/0001-00",
          "customerId": "AAA-12345678",
          "customerName": "NOME DO CLIENTE",
          "countryCode": "BR",
          "stateCode": "BR-RS",
          "cityName": "Canoas",
          "lastSalesDate": "2016-11-23T10:45:00+03:00",
          "type": "RC"
        }
      }
    }


**Especificação dos atributos**

|ID|Campo|Pai|Tipo|Descrição|Obrigatório|Regra|Exemplo|
|--|-----|---|----|---------|-----------|-----|-------|
|F01|data|Raiz| | |![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| | |
|F02|dealerLegalNumber|F01|varchar(50)|CNPJ da concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"99.999.999/0001-99"|
|F03|extractionDateTime|F01|timestamp|Data da extração dos dados da mensagem|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|P001|"2016-11-23T10:45:00+03:00"|
|F04|customer|F01| |	|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	| |
|F05|customerLegalNumber|F04|varchar(50)|CPF ou CNPJ do cliente|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"00.000.000/0001-00"|
|F06|customerId|F04|varchar(50)|Código do cliente na concessionária|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"AAA-12345678"|
|F07|customerName|F04|varchar(100)|Nome do cliente|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)| |"NOME DO CLIENTE"|
|F08|countryCode|F04|varchar(60)|País do cliente|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|P003|"BR"|
|F09|stateCode|F04|varchar(60)|Estado do cliente|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|P004|"BR-RS"|
|F10|cityName|F04|varchar(60)|Cidade do cliente|![check](https://github.com/agco-sa/site-md-src/blob/master/check.png?raw=true)|	|"Canoas"|
|F11|type|F04|varchar(60)|Tipo do cliente|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|	|"RC"|
|F12|lastSalesDate|F04|date|Data da última venda para o cliente|![error](https://github.com/agco-sa/site-md-src/blob/master/error.png?raw=true)|P001|2016-11-23T10:45:00+03:00|