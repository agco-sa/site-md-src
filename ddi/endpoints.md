---
currentMenu: ddi-endpoints
parentMenu: ddi
---
# Dealer Data Integration

## 5. Recursos e operações
Essa sessão contém os campos e regras das interfaces disponibilizadas para capturar informações de peças das concessionárias.
A API é composta de uma lista de recursos com possibilidade de diferentes operações dependendo do verbo HTTP utilizado, do caminho e dos parâmetros.

### 5.1. Interface DealerNFe

	Envia para a AGCO as informações de venda da revenda ao cliente final. no DMS a seleção de dados deverá atender a duas premissas importantes: </br>
	* Considerar as notas fiscais de Devolução(entrada), Saída e Transferência aptas a serem integradas e que contenham produtos a serem integrados conforme definido no cadastro de produto. </br>
	* Somente para as notas transmitidas e autorizadas pela SEFAZ, após o prazo máximo definido pelo cancelamento - não está previsto nenhum tratamento sobre o cancelamento de notas.  Recomenda-se a adoção de um parâmetro padrão que define o tempo máximo para cancelamento de nota fiscal SEFAZ para validar as notas aptas a integração DMS x AGCO. </br>
	A estrutura JSON contendo os dados é enviada no corpo da chamada. </br>
	Segue um exemplo do corpo da mensagem válida, no padrão JSON esperado, contendo TAGS do schema. </br>
	
Exemplo de JSON para interface DealerNFe:

    {
    "NFe": {
        "infNFe": {
            "dest": {
                "CNPJ": "",
                "CPF": "29896908087",
                "enderDest": {
                    "UF": "RS",
                    "cMun": 4307807,
                    "cPais": 1058,
                    "xMun": "ESTRELA"
                },
                "xNome": "ANTONIO WELTER"
            },
            "det": [
                {
                    "nItem": 1,
                    "prod": {
                        "cProd": "EN02219",
                        "qCom": 1,
                        "vProd": 287000,
                        "vUnCom": 287000,
                        "xProd": "COLHEITADEIRA AGRIC. MF 5650 MHC"
                    }
                }
            ],
            "emit": {
                "CNPJ": "91495457000170",
                "enderEmit": {
                    "UF": "RS",
                    "xMun": "SANTANA DO LIVRAMENTO",
                    "xPais": "BRASIL"
                },
                "xFant": "CONCESSIONARIA X",
                "xNome": "CONCESSIONARIA X"
            },
            "id": "NFe43150495437281000312550030000301351002205802",
            "ide": {
                "dhEmi": "2017-11-27T03:00:00.000Z",
                "dhSaiEnt": "2017-11-27T03:00:00.000Z",
                "mod": "55",
                "nNF": 30283,
                "natOp": "5102 VENDA DE MERCADORIA",
                "serie": 3,
                "tpNF": 1
            },
            "infAdic": {
                "infCpl": ""
            },
            "total": {
                "ICMSTot": {
                    "vNF": 2700
                }
            },
            "versao": 3
        }
    },
    "XMLFile": {
        "base64": "",
        "filename": "43150495437281000312550030000301351002205802-nfe.xml",
        "filesize": 8013,
        "filetype": "text/xml"
    },
    "ddi": {
        "campaign": {
            "active": true,
            "beginDate": "2017-11-23",
            "brand": "MF",
            "endDate": "2017-12-28",
            "id": 43,
            "market": "I",
            "models": [
                {
                    "id": 107,
                    "idWholegoodsCampaign": 43,
                    "model": "71804K",
                    "updaDate": null,
                    "userLogin": "loginuser"
                }
            ],
            "name": "Teste_Aug",
            "productType": "TA"
        },
        "prodDet": [
            {
                "nItem": 1,
                "prod": {
                    "codigoItem": "71804KH467A",
                    "modelo": "71804K",
                    "monobloco": "AAAT0017VGC004107",
                    "serieComercial": "7180466020"
                }
            }
        ],
        "tipoOp": 1,
        "vend": {
            "CPF": "99999999900",
            "telefone": "",
            "xNome": "Nome Vendedor"
        }
    }

</br>

#### 5.1.1. Especificação de atributos grupo “nfe”

|TAG|Tipo|Descrição|Regra|Obrigatório|Exemplo|
|---|---|---|---|---|---|
|   |numeric(4,2)|Versão do layout|  |![check](/images/check.png)|"versao": 3.00| |
|   |varchar(47)|Identificador da TAG a ser  assinada|R001|![check](/images/check.png)|"Id": " NFe43150395437281000312550030000296371002180066"|
|infNFe/dest/CNPJdest|varchar(14)|CNPJ do destinatário|R002|*|"CNPJ": "95485281000312"|
|infNFe/dest/CPF|varchar(11)|CPF do destinatário|R003|*|"CPF": "29896908087"|
|infNFe/dest/xNome|varchar(60)|Razão social ou nome do destinatário|-|![check](/images/check.png)|"xNome": "ANTONIO DA SILVA"|
|infNFe/dest/enderDest/UF|varchar(2)|Sigla UF do destinatário|-|![check](/images/check.png)|"UF": "RS"|
|infNFe/dest/enderDest/cMun|int|Código do Município|-|![check](/images/check.png)|"cMun": 4306205| 
|infNFe/dest/enderDest/xMun|varchar(60)|Nome do Município|-|![check](/images/check.png)|"xMun": "CRUZEIRO DO SUL"|
|infNFe/dest/enderDest/cPais|int|Código do País do destinatário|-|![error](/images/error.png)|"cPais": 1058|
|infNFe/dest/enderDest/xPais|varchar(60)|Nome do País do destinatário|-|![error](/images/error.png)|"xPais": "BRASIL"|
|infNFe/det/nItem|int|Índice do item na nota|-|![check](/images/check.png)|"nItem": 1|
|infNFe/det/prod/cProd|varchar(60)|Código do produto|-|![check](/images/check.png)|"cProd": "5650MHCL876/409489"|
|infNFe/det/prod/qCom|numeric(15,4)|Quantidadecomercial|-|![check](/images/check.png)|"qCom": 1.0000|
|infNFe/det/prod/vProd|numeric(15,2)|Valor total bruto dos produtos|-|![check](/images/check.png)|"vProd": 287000.00|
|infNFe/det/prod/vUnCom|numeric(15,4)|Quantidadecomercial|-|![check](/images/check.png)|"qCom": 1.0000|
|infNFe/det/prod/xProd|varchar(120)|Descrição do produto|-|![check](/images/check.png)|"xProd": "COLHEITADEIRA"|
|infNFe/emit/CNPJ|varchar(14)|CNPJ do emitente|R004|*|"CNPJ": "95437281000312"|
|infNFe/emit/CPF|varchar(11)|CPF do emitente|R005|* |"CPF": "29895508087"|
|infNFe/emit/xFant|varchar(60)|Nome fantasia do emitente|-|![error](/images/error.png)|"xFant": "EXEMPLO FANT EMIT"|
|infNFe/emit/xNome|varchar(60)|Razão Social ou nome do emitente|-|![check](/images/check.png)|"xNome": "EXEMPLO EMIT"|
|infNFe/emit/enderEmit/UF|varchar(2)|Sigla da UF do emitente|-|![check](/images/check.png)|"UF": "RS"|
|infNFe/emit/enderEmit/xMun|varchar(60)|Nome do município do emitente|-|![check](/images/check.png)|"xMun": "CRUZEIRO DO SUL"|
|infNFe/emit/enderEmit/xPais|varchar(60)|Nome do País do emitente|-|![error](/images/error.png)|"xPais": "BRASIL"|
|infNFe/id/|varchar(47)|Identificador da TAG a ser assinada. (informar a chave de acesso da NF-e precedida do literal ‘NFe’, acrescentada a validação do formato)|-|![check](/images/check.png) |"Id": " NFe43150395437281000312550030000296371002180066"|
|infNFe/ide/dhEmi|datetime|Data de emissão da nota. *(formato" yyyy-MM-dd'T'HH:mm:ssX")*|-| ![check](/images/check.png)|"dhEmi": "2015-03-30T03:00:00-03:00"|
|infNFe/ide/dhSaiEnt|datetime|Data de Saída ou da Entradada Mercadoria/Produto. *(formato"yyyy-MM-dd'T'HH:mm:ssX")*|-|![check](/images/check.png)|"dhSaiEnt": "2015-03-30T03:00:00-03:00"|
|infNFe/ide/mod|varchar(2)|Código do modelo da nota. (utilizar código 55 para identificação da NF-e, emitida em substituição ao modelo 1 ou 1A)|-|![check](/images/check.png)|"mod":"55"|
|infNFe/ide/nNf|int|Número da nota|-|![check](/images/check.png)|"nNF": 29637|
|infNFe/ide/natOp|varchar(60)|Descrição da Natureza da Operação|-|![check](/images/check.png)|“natOp”: “TRANSFERENCIA ENTRE FILIAIS”|
|infNFe/ide/serie|int|Série da nota|R006|![check](/images/check.png)|"serie": 3|
|infNFe/ide/tpNF|int|Tipo de operação. |V001|![check](/images/check.png)|"tpNF": 1|
|infNFe/infAdic/infCpl|Varchar(5000)|Informações complementares da NF|-|![check](/images/check.png)|“infCpl”:  “Informações complementares sobre a NF”|
|infNFe/total/ICMSTot/vNF |numeric(15,2)|Valor Total da NF-e|-|![check](/images/check.png)|"vNF": 287000.00|
|infNfe/versao|numeric(4,2)|Versão do layout|-|![check](/images/check.png)|"versao": 2.00|
</br>

#### 5.1.2. Especificação de atributos grupo “XMLFile”

|TAG|Tipo|Descrição|Regra|Mandatório|Exemplo|	
|---|---|---|---|---|---|	
|/base64 |Byte array|Arquivo XML em bytes|R007|![check](/images/check.png)|  |
|/filename|varchar|Nome do arquivo| -  |![check](/images/check.png)|“filename “ : “NFe43170492197540000125550030000587641000818289.xml”|
|/filesize|int|Tamanho do arquivo em bytes| -  |![check](/images/check.png)|“filesize” : 9765|
|/filetype|varchar|Tipo de arquivo| -  |![check](/images/check.png)|“filetype” : “text/xml”| 
</br>

#### 5.1.3. Especificação de atributos grupo “ddi”

| TAG | Tipo | Descrição | Regra | Obrigatório | Exemplo |	
|---|---|---|---|---|---|	
|/campaign/active|boolean|Campo booleano informa se a campanha está ativa ou não. Padrão false caso não informado|V002| ![check](/images/check.png)|"active": true|
|/campaign/beginDate/|Datetime|Data de inicio da campanha|V003|![check](/images/check.png)|"beginDate": "2017-12-20T09:44:48.416Z"|
|/campaign/brand/|varchar(4)|Marca dos tratores|R008|![check](/images/check.png)|  |
|/campaign/endDate/|Datetime|Data final da campanha|V004| ![check](/images/check.png) |"endDate": "2017-12-20T09:44:48.417Z"|
|/campaign/id/ | int|Identificador da campanha|R009|![check](/images/check.png)|"id": 0|
|/campaign/market/|varchar(2)|Informa o tipo de mercado interno.|V005| ![check](/images/check.png) |"market": "string",|
|/campaign/models|Grupo|Campanhas envelope do grupo de Campanhas|R010|![check](/images/check.png)|"models":[{"id": 0, "idWholegoodsCampaign": 0, "model": "string", "updateDate": "2017-12-19T10:55:21.256Z", "userLogin": "string"}]|
|/campaign/models/model/|varchar(250)|Modelo da campanha|R011|![check](/images/check.png) | "model": "string"| 
|/campaign/name/|varchar(50)|Nome da campanha|R012   V006| ![check](/images/check.png)|"name": "string"|
|/campaign/productType/|varchar(4)|Tipo do produto|R013|![check](/images/check.png)| "productType": "string"| 
|/prodDet/nItem/|int|Índice do item na nota| -  |![check](/images/check.png)|"nItem": 1|
|/prodDet/prod/codigoItem/|varchar(25)|Código do item - AGCO| -  |![check](/images/check.png)|"codigoItem": "42754F0913D"|
|/prodDet/prod/modelo/|varchar(2)|Código do modelo da nota |R014|![check](/images/check.png)|"modelo": "MF"|
| /prodDet/prod/TipoProd | varchar(3)  |  Tipo de produto AGCO, onde: Trator = “TA”, Colheitadeira = “CO”, Pulverizador: “PU” | -  | ![error](/images/error.png) |"tipoProd": "TA"|
| /prodDet/prod/monobloco/ |  varchar(30) |  Número do Monobloco – AGCO  | -  |  ![error](/images/error.png) | "monobloco": " AAAT0012PCC002382" |
| /prodDet/prod/serieComercial/ | varchar(20) | Código da Série Comercial - AGCO | - | ![check](/images/check.png)  | serieComercial": "4275344889" |
| /tipoOp/vend/CPF | varchar(11) | CPF de vendedor | - | ![error](/images/error.png) | "CPF": "29896908085" |
| /tipoOp/vend/CNPJ |  varchar(14) | CNPJ do vendedor  | - | ![error](/images/error.png) |  "CNPJ": "95485281000312" |
| /tipoOp/vend/telefone |  varchar(15) | Número do telefone celular do vendedor  | - |  ![error](/images/error.png) |  "telefone": "5199999999" |
| /tipoOp/vend/xNome | varchar(60) | Nome completo do vendedor | -  | ![error](/images/error.png) | "xNome": "NOME VENDEDOR" |
</br>

### 5.2. Interface Stock

Envia para a AGCO as informações de negociação do produto/monobloco em estoque. Os dados da Concessionária e do produto devem ser adicionados diretamente no endereço da API.</br>

Exemplo de JSON para interface STOCK </br>
Endereço </br>
    https://appsqa.agcoonline.com.br/portal/ddi/Stock/Tipo_empresa/Cod_Dealer/Monobloco/Serie_Comercial/Item

Body

  `{"available":"S","availableCpfCnpj":"999.999.999-00"}` 

|Tipo Empresa|Código Dealer|Monobloco|Série Comercial|Item|	
|------------|-------------|---------|---------------|----|
|6|11571|000BO3020CI0004|BP03330255|BP0302E1021|

Detalhe: O parâmetro token deve ser setado via Bearer para essa interface. </br>

| Propriedade | Descrição | Exemplo |
|-----------|---------|-------|
|Authorization|Inserir no header a seguinte propriedade: “Authorization: Bearer”.|Authorization: Bearer <token>|
|Content-Type|Inserir no header a seguinte propriedade: **"Content-Type:application/json"**|Content-Type:application/json|

</br>

### 5.3. Interface Campaign

Através do método GET no DMS é possível buscar uma lista das Campanhas existentes na AGCO. 
</br>

#### 5.3.1. Response Body
	{
 	 "data": [
    {
      "id": "1",
      "type": "wholegoodsCampaign",
      "attributes": {
        "id": 1,
        "brand": "VT",
        "market": "I",
        "productType": "TA",
        "name": "Campanha tes",
        "models": [
          {
            "id": 5,
            "idWholegoodsCampaign": 1,
            "model": "7180KFA",
            "updateDate": null,
            "userLogin": "avier"
          }
        ],
</br>

#### 5.3.2. Request Headers

	{
  		"Accept": "application/json;charset=UTF-8"
	}

* Se existir a informação de CPF o campo CNPJ deve vir vazio. O mesmo acontece para o caso contrário.

