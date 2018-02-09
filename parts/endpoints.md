---
currentMenu: parts-endpoints
parentMenu: parts
---
# Argentina Parts

## 6. Endpoints

A AGCO Parts API possui 6 endpoints disponíves para busca de informações relativas a peças de reposição como:

- **Details**
- **Price**
- **Availability**
- **Taxes**
- **Search**
- **Supersession**

</br>

### 6.1. Interface - Search
Este endpoint pode ser usado para retornar uma lista de possíveis peças de reposições da AGCO, baseado numa consulta de texto, ao qual será comparado à base de dados de partnumbers ou descriçoes da AGCO.

#### 6.1.1 Response

O exemplo a seguir representa a resposta do pedido acima, se ele tiver sido processado com sucesso:

	{
		"data": [
			{
				"id": "3012224X1",
				"description": "HEXAGON FLANGE BOLT M20 X 130 (2.5) ISO 8.8 ZN",
				"descriptionLanguage": "en"
			}
		],
		"meta": {
			"currentPage": 1,
			"nextPage": null,
			"totalPages": 1,
			"totalItems": 1
		}
	}

#### 6.1.2 Especificação dos atributos

|**ID**|**Campo**|**Pai**|**Tipo**|**Descrição**|**Obrigatório**|**Exemplo**|
|---|---|---|---|---|---|---|
|A01|data|Raiz|Tag raiz Lista| |Sim| |
|A02|id|A01|String|Número da peça|Sim|3012224X1|
|A03|description|A01|String|Descrição da peça|Sim|HEXAGON M20|
|A04|descriptionLanguage|A01|String|Linguagem da descrição|Sim|en|
|A05|meta|Raiz|Tag raiz||Não| | |
|A06|currentPage|A5|integer|Número da página|Sim|1|
|A07|nextPage|A5|integer|Próxima página|Não|null|
|A08|totalPages|A5|integer|Total de páginas|Sim|1|
|A09|totalItems|A5|integer|Total de itens da busca|Sim|1|
</br>

#### 6.1.3 Exemplo de request

GET /parts
GET /parts?dealerId=**{dealerId}**&query=3012224X1&lang={lang}

|**Parâmetro**|**Descrição**|**Tipo de parâmetro**|**Obrigatório**|**Tipo de dado**|**Valor padrão**|**Exemplo**|
|---|---|---|---|---|---|---|
|dealerId|Identificaçao do Dealer conforme sistema da AGCO|Query|Não|Number|Blank (null)|1481682|
|lang|Linguagem ao qual pode retornar com: pt-BR, es-AR, en-EN|Query|Não|String|Dealer default language|pt-BR|
|query|Insira consulta de texto para pesquisar no banco de dados|Query|Não|Query|Blank (null)|3012224X1|
|Página[item]|Máximo de número de item desejado para retornar por página|Query|Não|Number|10|100|
|Página[número]|Página desejada|Query|Não|Number|1|10|

</br>

### 6.2. Interface - Detail
Esse endpoint é utilizado para recuperar informações detalhadas sobre um partnumber específico:

#### 6.2.1 Response
O exemplo a seguir representa a resposta do pedido acima se ele tiver sido processado com sucesso:

	{
		"data": {
			"id": "3012224X1",
			"description": "HEXAGON FLANGE BOLT M20 X 130 (2.5) ISO 8.8 ZN",
			"descriptionLanguage": "en",
			"country": "BRA",
			"weight": 0,
			"minimumQuantity": 1,
			"movementCode": "Criticidade Muito Baixa",
			"fiscalCategory": "0",
			"directShipping": false,
			"superseded": false,
			"additionalInfo": []
		}
	}

#### 6.2.2 Especificação de atributos
|**ID**|**Campo**|**Pai**| **Tipo**|**Descrição**|**Obrigatório**|**Exemplo**|
|---|---|---|---|---|---|---|
|B01|data|Raiz|Tag raiz||Sim| | |
|B02|additionalInfo|B01|Lista|Informações adicionais|Não|"Informações adicionais a incluir"|
|B03|name|B01|String|Nome do atributo|Não|BNDES|
|B04|value|B01|Object|Valor do atributo|Não|true|
|B05|country|B01|String|País associado com a descrição|Sim|BRA|
|B06|description|B01|String|Descrição da peça|Sim|HEXAGON M20|
|B07|descriptionLanguage|B01|String|Linguagem da descrição|Sim|en|
|B08|directShipping|B01|Boolean|Indica se esta parte tem transporte direto ou não|Sim|false|
|B09|fiscalCategory|B01|String|Categoria fiscal|Sim| |
|B10|id|B01|String|Part number|Sim|3012224X1|
|B11|minimunQuantity|B01|Decimal|Quantidade mínima de pedidos deste número de peça|Sim|1.23456|
|B12|movementCode|B01|String|Codigo do Movimento|Sim|Criticidade Muito Baixa|
|B13|superseded|B01|Boolean|Indica que este número de peça é obsoleto e precisa procurar o número de peça de substituição mais recente|Sim|true|
|B14|weigth|B01|Decimal|Peso em Kg|Sim|1.23456|

</br>

#### 6.2.3 Exemplo de request

GET /parts/**{partnumber}**
GET /parts/**{partNumber}**?dealerId={dealerId}&lang={lang}

|**Parâmetro**|**Descrição**|**Tipo de parâmetro**|**Obrigatório**|**Tipo de dado**|**Valor padrão**|**Exemplo**|
|---|---|---|---|---|---|---|
| partNumber    | AGCO Part Number                                              | Path               | Não           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Identificador do Dealer no sistema AGCO                | Query              | Não           | Number        | Blank (null)            | 1481682        |
| lang          | Linguagem que deve ser retornado: pt-BR, es-AR, en-EN | Query              | Não           | String        | Dealer default language | pt-BR          |

</br>

### 6.3. Interface - Availability

Este endpoint é utilizado para recuperar informações sobre a disponibilidade de estoque de um número de peça específico.

#### 6.3.1 Response

O exemplo a seguir representa a resposta do pedido acima se ele tiver sido processado com sucesso:

	{
		"data": {
			"id": "036857N1",
			"dealerId": 11571,
			"availabilities": [
				{
					"warehouseCode": "REPVT06",
					"warehouseOrder": 1,
					"warehouseName": "REPOSIÇÃO ERNESTINA",
					"available": false
				},
				{
					"warehouseCode": "REPVT03",
					"warehouseOrder": 2,
					"warehouseName": "REPOSIÇÃO JUNDIAI",
					"available": false
				}
			]
		}
	}
#### 6.3.2 Especificação de atributos

|**ID**|**Campo**|**Pai**|**Tipo**|**Descrição**|**Obrigatório**|**Exemplo**|
|---|---|---|---|---|---|---|
|C01|data|Raiz|Tag raiz| |Sim| |
|C02|availabilities|C01|Array|Lista|Array da informação de disponibilidade de cada warehouse acessível pelo revendedor solicitado|[]|
|C03|available|C02|Boolean|Representa se a peça está disponível para ser comprada deste warehouse|Sim|true|
|C04|warehouseCode|C02|String|Identificador único do armazém retornado|Sim|REPVT06|
|C05|warehouseName|C02|String|Nome das warehouse retornadas|Sim|ERNESTINA|
|C06|warehouseOrder|C02|Number|Ordem de prioridade do warehouse retornado|Sim|1|
|C07|dealerId|C01|Number|Identificador do Dealer no Sistema AGCO|Sim|11571|
|C08|id|C01|Boolean|Representa se a peça está disponível para ser comprada deste warehouse|Sim|true|

</br>

#### 6.3.3 Exemplo de request

GET /parts/**{partnumber}**/availability
GET /parts/**{partNumber}**/availability?dealerId={dealerId}&lang={lang}

|**Parâmetro**|**Descrição**|**Tipo de parâmetro**|**Obrigatório**|**Tipo de dado**|**Valor padrão**|**Exemplo**|
|---|---|---|---|---|---|---|
| partNumber    | AGCO Part Number                                              | Path               | No           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | No           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | No           | String        | Dealer default language | pt-BR          |

</br>

### 6.4. Interface - Price
Este endpoint é utilizado para recuperar informações de preço de um número de peça específico.

#### 6.4.1 Response
O exemplo a seguir representa a resposta do pedido acima se ele tiver sido processado com sucesso:

	{
		"data": {
			"id": "040665R1",
			"dealerId": 11571,
			"prices": [
				{
					"currency": "BRL",
					"type": "PUBLIC",
					"value": 82.3478,
					"warehouseCode": "REPVT03"
				},
				{
					"currency": "BRL",
					"type": "SPECIFIC",
					"value": 48.55,
					"warehouseCode": "REPVT03"
				},
				{
					"currency": "BRL",
					"type": "CAMPAIGN",
					"value": 60.45,
					"warehouseCode": "REPVT03"
				},
				{
					"currency": "BRL",
					"type": "HARVEST",
					"value": 60.45,
					"warehouseCode": "REPVT03"
				}
			]
		}
	}
	
#### 6.4.2 Especificação de atributos

|**ID**|**Campo**|**Pai**|**Tipo**|**Descrição**|**Obrigatório**|**Exemplo**|
|---|---|---|---|---|---|---|
|D01|data|Raiz|Tag raiz| | | |
|D02|dealerId|D01|Number|Identificador do Dealer no sistema AGCO|Sim|11571|
|D03|id|D01|String|Identificador da peça no sistema da AGCO|Sim|040665R1|
|D04|prices|D01|Lista|Array com informação de preços disponíveisle para peça|Sim|[]|
|D05|currency|D04|String|Código da moeda para peça selecionada|Sim|BRL|
|D06|type|D04|String|Informação de tipo de peça: Pública, Específica, Campanha, Safra|Sim|PUBLIC|
|D07|value|D04|Number|Preço da peça|Sim|12.34567|
|D08|warehouseCode|D04|String|Identificação do warehouse onde esses dados de preço foram encontrados|Sim|REPVT03|

</br>

#### 6.4.3 Exemplo Request

GET /parts/**{partnumber}**/price
GET /parts/**{partNumber}**/price?dealerId={dealerId}&lang={lang}

|**Parâmetro**|**Descrição**|**Tipo de parâmetro**|**Obrigatório**|**Tipo de dado**|**Valor padrão**|**Exemplo**|
|---|---|---|---|---|---|---|
| partNumber    | Identificador da peça no sistema AGCO| Path  | Não       | String        | Blank (null)            | 3012224X1      |
| dealerId      | Identificador do Dealer no sistema AGCO  | Query    | Não   | Number    | Blank (null)            | 1481682        |
| lang         | Idioma que os dados devem ser devolvidos: pt-BR, es-AR, en-EN | Query | Não | String | Dealer default language | pt-BR|
<br />

### 6.5. Interface - Supersession

Este endpoint é utilizado para recuperar informações se a parte especificada foi substituída e quais são as peças de reposição.

#### 6.5.1 Response

O exemplo a seguir representa a resposta do pedido acima se ele tiver sido processado com sucesso:

	{
		"data": [
			{
				"supersededId": "036857N1",
				"supersededDescription": "LEVER RH / LD",
				"supersedingId": "195910M1",
				"supersedingDescription": "BUSH",
				"condition": null,
				"reversibility": "N",
				"status": "A",
				"supersessionDescription": "",
				"descLang": "en",
				"type": "CO",
				"quantity": 1
			},
			{
				"supersededId": "036857N1",
				"supersededDescription": "LEVER RH / LD",
				"supersedingId": "036858P1",
				"supersedingDescription": "LEVER",
				"condition": null,
				"reversibility": "N",
				"status": "A",
				"supersessionDescription": "",
				"descLang": "en",
				"type": "CO",
				"quantity": 1
			}
		]
	}
#### 6.5.2 Especificação de atributos

|**ID**|**Campo**|**Pai**|**Tipo**|**Descrição**|**Obrigatório**|**Exemplo**|
|---|---|---|---|---|---|---|
|E01|data|Raiz|Tag raiz Lista| |Sim| |
|E02|condition|E01|String|Condição da substituição|Sim|null|
|E03|descLang|E01|String|Linguagem da descrição|Sim|en|
|E04|reversibility|E01|String|Reversão da substituição|Sim|N|
|E05|status|E01|String|Status da substituição|Sim|A|
|E06|supersededId|E01|String|Substituição do partnumber AGCO|Sim|195910M1|
|E07|supersededDescription|E01|String|Descrição partnumber AGCO|Sim|LEVER RH / LD|
|E08|supersedingDescription|E01|String|Descrição do partnumber AGCO|Sim|BUSH|
|E09|supersedingId|E01|String|Identificador do partnumber de substituição|Sim|195910M1|
|E10|supersessionDescription|E01|String|Descrição da substituição|Sim|Test|
|E11|type|E01|String|Tipo de substituição|Sim|CO|
|E12|quantity|E01|number|Quantidade|Sim|1|

</br>

#### 6.5.3 Exemplo de request

GET /parts/**{partnumber}**/supersession
GET /parts/**{partnumber}**/supersession?dealerId=1481682&lang=en-EN

|**Parâmetro**|**Descrição**|**Tipo de parâmetro**|**Obrigatório**|**Tipo de dado**|**Valor padrão**|**Exemplo**|
|---|---|---|---|---|---|---|
| partNumber    | Identificador da peça no Sistema AGCO                                              | Path               | Não           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Identificador do Dealer no Sistema AGCO                 | Query              | Não           | Number        | Blank (null)            | 1481682        |
| lang          | Linguagem com que deve retornar: pt-BR, es-AR, en-EN | Query              | Não           | String        | Linguagem padrão do Dealer | pt-BR          |

</br>

### 6.6. Interface - Taxes

Este endpoint é utilizado para recuperar informações fiscais de um número de peça específico.

#### 6.6.1 Response
O exemplo a seguir representa a resposta do pedido acima se ele tiver sido processado com sucesso:

	{
		"data": {
			"partNumber": "3012224X1",
			"taxClassification": "0",
			"taxes": [
				{
					"name": "IPI",
					"currency": "BRL",
					"value": 10
				},
				{
					"name": "PISCOFINS",
					"currency": "BRL",
					"value": 27.25
				}
			]
		}
	}

#### 6.6.2 Especificação de atributos

|**ID**|**Campo**|**Pai**|**Tipo**|**Descrição**|**Obrigatório**|**Exemplo**|
|---|---|---|---|---|---|---|
|F01|data|Raiz|Tag raiz| |Sim| |
|F02|partnumber|F01|String|Número da peça|Sim|036857N1|
|F03|taxClassification|F01|String|Classificação de taxas|Sim|0(zero)|
|F04|taxes|F01|Lista|Conjunto de informação de taxas do partnumber|Sim|[]|
|F05|currency|F04|String|Moeda|Sim|BRL|
|F06|name|F04|String|Identificador exclusivo de taxas|Sim|IPI|
|F07|value|F04|Number|Valor|Sim|27.50|

</br>

#### 6.6.3 Exemplo de request

GET /parts/**{partnumber}**/taxes
GET /parts/**{partNumber}**/taxes?dealerId={dealerId}&lang={lang}

|**Parâmetro**|**Descrição**|**Tipo de parâmetro**|**Obrigatório**|**Tipo de dado**|**Valor padrão**|**Exemplo**|
|---|---|---|---|---|---|---|
|partNumber|AGCO Part Number| Path|Não|String|Blank (null)|3012224X1|
|dealerId|Identificador do Dealter no sistema AGCO| Query|Não|Number|Blank (null)|1481682|
|lang|Idioma que os dados devem ser devolvidos: pt-BR, es-AR, en-EN|Query|Não|String|Idioma padrão da Concessionária|pt-BR|
</br>
