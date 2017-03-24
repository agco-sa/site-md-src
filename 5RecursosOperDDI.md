![AGCO_logo](http://www.agco.com.br/content/agcocorp/pt_BR/_jcr_content/footermainparsys/footer/footerlogoimage.img.png/1485893878104.png)
# Dealer Data Integration

## Recursos e operações
A API é composta de uma lista de recursos com possibilidade de diferentes operações dependendo do verbo HTTP utilizado, do caminho e dos parâmetros.

### 1. POST /ddi/DealerNFe
Envia para a AGCO de informações de venda da revenda ao cliente final. 
No DMS a seleção de dados deverá atendar a duas premissas importantes:
   
*  Considerar as notas fiscais de entrada (devoluções), saída e transferência aptas a ser integradas e que contenham produtos a serem integrados conforme definido no cadastro de produto.
*  Somente para notas transmitidas e autorizadas pela SEFAZ, após o prazo máximo definido para o cancelamento – não está previsto nenhum tratamento sobre o cancelamento de notas.
    *  Recomenda-se a adoção de um parâmetro padrão que defini o tempo máximo para cancelamento da nota fiscal na SEFAZ para validar as notas aptas a integração DMS x AGCO.
    
A estrutura JSON contendo os dados é enviada no corpo da chamada.
Segue um exemplo do corpo de uma mensagem válida, no padrão JSON esperado, contendo todas as TAGs do schema.
    
  

    {
     "NFe": {
       "infNFe": {
         "versao": 3.1,
         "id": "",
         "ide": {
           "natOp": "5102 VENDA DE MERCADORIA",
           "mod": "55",
           "serie": 10,
           "nNF": 445512,
           "dhEmi": "2015-08-18T03:00:00.000Z",
           "dhSaiEnt": "2015-08-20T03:00:00.000Z",
           "tpNF": 1
         },
         "emit": {
           "CNPJ": "92028224000391",
           "xNome": "CONCESSIONARIA X",
           "xFant": "CONCESSIONARIA X",
           "enderEmit": {
             "xMun": "SANTANA DO LIVRAMENTO",
             "UF": "RS",
             "xPais": "BRASIL"
           }
         },
         "dest": {
           "CPF": "23518456091",
           "CNPJ": "",
           "xNome": "MARCOS DA SILVA",
           "enderDest": {
             "cMun": 4305108,
             "xMun": "BAGE",
             "UF": "RS",
             "cPais": 1058
           }
         },
         "det": [
           {
             "nItem": 1,
             "prod": {
               "cProd": "42654F01338",
               "xProd": "TRATOR AGRICOLA MF4265 4RM",
               "qCom": 1,
               "vUnCom": 86064.35,
               "vProd": 86064.35
             }
           }
         ],
         "total": {
           "ICMSTot": {
             "vNF": 86064.35
           }
         },
         "infAdic": {
           "infCpl": ""
         }
       }
     },
     "ddi": {
       "tipoOp": 1,
       "vend": {
         "CPF": "68037503020",
         "xNome": "FRANCISCO DA SILVA",
         "telefone": "5499999999"
       },
       "prodDet": [
         {
           "nItem": 1,
           "prod": {
             "modelo": "42654F",
             "codigoItem": "42654F01338",
             "serieComercial": "4265395723",
             "monobloco": "AAAT0011CEC001305"
           }
         }
       ]
     }
    }

    

### Especificação dos atributos (grupo "NFe")
| TAG PAI | TAG | TIPO | DESCRIÇÃO | OBRIGATÓRIO | EXEMPLO |
| :------- | :--- | :---- | :--------- | :----------- | :------- |
| | **versão** | numeric(4,2) | Versão do layout | Sim | "versao": 2.00 |
| | **id** | varchar(47) | Identificador da TAG a ser assinada. *(informar a chave de acesso da NF-e precedida do literal ‘NFe’, acrescentada a validação do formato)* | Sim | "Id": " NFe43150395437281000312550030000296371002180066" |
| ide | **natOp** | varchar(60) | Descrição da Natureza da Operação | Sim | “natOp”: “TRANSFERENCIA ENTRE FILIAIS”|
| ide | **mod** | varchar(2) | Código do modelo da nota. *(utilizar código 55 para identificação da NF-e, emitida em substituição ao modelo 1 ou 1A)* | Sim | "mod":"55" |
| ide | **serie** | int | Série da nota. *(preencher com zeros na hipótese de a NF-e não possuir série)* | Sim | "serie": 3 |
| ide | **nNF** | int | Número da nota | Sim | "nNF": 29637 |
| ide | **dhEmi** | datetime | Data de emissão da nota. *(formato" ***yyyy-MM-dd'T'HH:mm:ssX***")* | Sim | "dhEmi": "2015-03-30T03:00:00-03:00" |
| ide | **dhSaiEnt** | datetime | Data de Saída ou da Entradada Mercadoria/Produto. *(formato"***yyyy-MM-dd'T'HH:mm:ssX***")*|
| ide | **tpNF** | int | Tipo de operação. (0 = entrada, 1 = saída) | Sim | "tpNF": 1 |
| emit | **CNPJ** | varchar(14) | CNPJ do emitente | \* | "CNPJ": "95437281000312" |
| emit | **CPF** | varchar(11) | CPF do emitente | \* | "CPF": "29895508087" |
| emit | **xNome** | varchar(60) | Razão social ou nome do emitente | Sim | "xNome": "EXEMPLO EMIT" |
| emit | **xFant** | varchar(60) | Nome fantasia do emitente | Não | "xFant": "EXEMPLO FANT EMIT" |
| emitenderEmit | **xMun** | varchar(60) | Nome do município do emitente | Sim | "xFant": "EXEMPLO FANT EMIT" |
| emitenderEmit | **UF** | varchar(2) | Sigla da UF do emitente | Sim | "UF": "RS" |
| emitenderEmit | **xPais** | varchar(60) | Nome do País do emitente | Não | "xPais": "BRASIL" |
| dest | **CNPJ** | varchar(14) | CNPJ do destinatário | /* | "CNPJ": "95485281000312" |
| dest | **CPF** | varchar(11) | CPF do destinatário | /* | "CPF": "29896908087" |
| dest | **xNome** | varchar(60) | Razão social ou nome do destinatário | Sim | "xNome": "ANTONIO DA SILVA" |
| destenderDest |	**cMun** | int |	Código do município |	Sim	| "cMun": 4306205 |
| destenderDest | **xMun**	| varchar(60) |	Nome do município do destinatário |	Sim	| "xMun": "CRUZEIRO DO SUL" |
| destenderDest | **UF** |	varchar(2)	| Sigla da UF do destinatário |	Sim	| "UF": "RS" |
| destenderDest | **cPais**	| int	| Código do País |	Não	| "cPais": 1058 |
| destenderDest | **xPais**	| varchar(60)	| Nome do País do destinatário |	Não	| "xPais": "BRASIL" |
| det	| **nItem** |	int	| Índice do item na nota	| Sim	| "nItem": 1 |
| detprod | **cProd**	| varchar(60) |	Código do produto	| Sim	| "cProd": "5650MHCL876/409489" |
| detprod | **xProd** |	varchar(120)	| Descrição do produto |	Sim	| "xProd": "COLHEITADEIRA" |
| detprod | **qCom** |	numeric(15,4)	| Quantidadecomercial |	Sim |	"qCom": 1.0000|
| detprod | **vUnCom** |	numeric(21,10) |	Valor UnitáriodeComercialização |	Sim |	"vUnCom": 287000.00 |
| detprod | **vProd** |	numeric(15,2) |	Valor total bruto dos produtos |	Sim	| "vProd": 287000.00 |
| totalICMSTot |	**vNF** |	numeric(15,2) |	Valor Total da NF-e |	Sim |	"vNF": 287000.00 |



### Especificação dos atributos (grupo “ddi”)
| TAG PAI | TAG | TIPO | DESCRIÇÃO | OBRIGATÓRIO | EXEMPLO |
| :------- | :--- | :---- | :--------- | :----------- | :------- |
| | **tipoOp** | int | Código do tipo de operação *( ***1***=venda, ***4***=devolução, ***5***=transferência)* | Sim | "tipoOp": 1 |
| vend | **CPF** |	varchar(11) |	CPF do Vendedor |	Não |	"CPF": "29896908085"|
| vend | **xNome** |	varchar(60) |	Nome completo do Vendedor	| Não |	"xNome": "NOME VENDEDOR" |
| vend | **telefone** |	varchar(15) |	Número do telefone celular do Vendedor	| Não |	"telefone": "5199999999" |
| prodDet |	**nItem** |	int	| Índice do item na nota	| Sim |	"nItem": 1 |
| prodDetprod | **codigoItem**	| varchar(25)	| Código do Item - AGCO |	Sim	| "codigoItem": "42754F0913D" |
| prodDetprod | **serieComercial**	| varchar(20) |	Código da Série Comercial - AGCO |	Sim	| "serieComercial": "4275344889" |
| prodDetprod | **monobloco**	| varchar(30) |	Número do monobloco - AGCO |	Não |	"monobloco": " AAAT0012PCC002382" |
| prodDetprod | **tipoProd** |	varchar(3) |	Tipo de produto AGCO, onde: Trator = “TA”, Colheitadeira = “CO”, Pulverizador: “PU” |	Não |	"tipoProd": "TA" |
| prodDetprod | **cPrograma** |	int	| Controle do Programa Mais Alimentos. (0 = Não, 1 = Sim) |	Não |	"cPrograma": 0 |

**\* Se existir a informação de CPF o campo CNPJ deve vir vazio. O mesmo acontece para o caso contrário.**
