---
currentMenu: parts-endpoints
parentMenu: parts
---
# Argentina Parts

## 6. Endpoints

A AGCO Parts API possui 6 endpoints disponíves para busca de informações relativas a peças de reposição como:
* Details
* Price
* Availability
* Taxes
* Search
* Supersession

### 6.1. Parts API - Search
Este endpoint pode ser usado para retornar uma lista de possíveis peças de reposições da AGCO, baseado numa consulta de texto, ao qual será comparado à base de dados de partnumbers ou descriçoes da AGCO.

#### 6.1.1 Request

GET /parts

| **Parâmetro** | **Descrição**                                               | **Tipo de parâmetro** | **Obrigatório** | **Tipo de dados** | **Valor padrão**       | **Exemplo**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| dealerId      | Identificaçao do Dealer conforme sistema da AGCO                 | Query              | Não           | Number        | Blank (null)            | 1481682        |
| lang          | Linguagem ao qual pode retornar com: pt-BR, es-AR, en-EN | Query              | Não           | String        | Dealer default language | pt-BR          |
| query         | Insira consulta de texto para pesquisar no banco de dados                | Query              | Não           | Query         | Blank (null)            | 3012224X1      |
| Página[item]    | Máximo de número de item desejado para retornar por página  | Query              | Não           | Number        | 10                      | 100            |
| Página[número]  | Página desejada                                                 | Query              | Não           | Number        | 1                       | 10             |
<br />
**Request Example:** 
GET /parts?dealerId={dealerId}&query=3012224X1&lang={lang}

#### 6.1.2 Response

O exemplo a seguir representa a resposta do pedido acima se ele tiver sido processado com sucesso:

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


| ID  | Parent ID | Campo               | Descrição                                                                                             | Obrigatório | Tipo de dado | Exemplo                |
|-----|-----------|---------------------|---------------------------------------------------------------------------------------------------------|----------|-----------|-------------------------|
| A01 | N/A       | id                  | Número da peça                                                                                           | Sim      | String    | 3012224X1               |
| A02 | N/A       | description         | Descrição da peça                                                                                      | Sim      | String    | HEXAGON M20             |
| A03 | N/A       | descriptionLanguage | Linguagem da descrição                                                                            | Sim      | String    | en                      |
<br />

### 6.2. Parts API - Detail


Esse endpoint é utilizado para recuperar informações detalhadas sobre um partnumber específico:

#### 6.2.1 Request

GET /parts/**{partnumber}**

| **Par** | **Descrição**                                               | **Tipo parâmetro** | **Obrigatório** | **Tipo de dado** | **Valor default**       | **Exemplo**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| partNumber    | AGCO Part Number                                              | Path               | Não           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Identificador do Dealer no sistema AGCO                | Query              | Não           | Number        | Blank (null)            | 1481682        |
| lang          | Linguagem que deve ser retornado: pt-BR, es-AR, en-EN | Query              | Não           | String        | Dealer default language | pt-BR          |
<br />
**Request Example:** 
GET /parts/{partNumber}?dealerId={dealerId}&lang={lang}

#### 6.2.2 Response

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


| ID  | Parent ID | Campo               | Descrição                                                                                             | Obrigatório | Tipo de dado | Exemplo                 |
|-----|-----------|---------------------|---------------------------------------------------------------------------------------------------------|----------|-----------|-------------------------|
| A01 | N/A       | id                  | Part number.                                                                                            | Sim      | String    | 3012224X1               |
| A02 | N/A       | description         | Descrição da peça                                                                                       | Sim      | String    | HEXAGON M20             |
| A03 | N/A       | descriptionLanguage | Linguagem da descrição                                                                           | Sim      | String    | en                      |
| A04 | N/A       | country             | País associado com a descrição da peça                                                           | Sim      | String    | BRA                     |
| A05 | N/A       | weight              | Peso em Kg                                                                                    | Sim      | Decimal   | 1.23456                 |
| A06 | N/A       | minimumQuantity     | Quantidade mínima de pedidos deste número de peça                                                         | Sim      | Decimal   | 1.23456                 |
| A07 | N/A       | movementCode        | Codigo do Movimento                                                                                          | Sim      | String    | Criticidade Muito Baixa |
| A08 | N/A       | fiscalCategory      | Categoria fiscal                                                                                        | Sim      | String    |                         |
| A09 | N/A       | directShipping      | Indica se esta parte tem transporte direto ou não                                              | Sim      | Boolean   | false                   |
| A10 | N/A       | superseded          | Indica que este número de peça é obsoleto e precisa procurar o número de peça de substituição mais recente | Sim      | Boolean   | true                    |
| A11 | N/A       | additionalInfo      | Informações adicionais                                                                       | Não       | Array     | []                      |
| A12 | A11       | name                | Nome do atributo                                                                                        | Não       | String    | BNDES                   |
| A13 | A11       | value               | Valor do atributo                                                                                        | Não       | Object    | true                    |
<br />

### 6.3. Parts API - Availability

Este endpoint é utilizado para recuperar informações sobre a disponibilidade de estoque de um número de peça específico.

#### 6.3.1 Request

GET /parts/**{partnumber}**/availability

| **Parameter** | **Description**                                               | **Parameter Type** | **Required** | **Data Type** | **Default Value**       | **Example**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| partNumber    | AGCO Part Number                                              | Path               | No           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | No           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | No           | String        | Dealer default language | pt-BR          |
<br />
**Request Example:** GET /parts/{partNumber}/availability?dealerId={dealerId}&lang={lang}

#### 6.3.2 Response

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


| ID  | Parent ID | Campo          | Descrição                                                                             | Obrigatório | Tipo | Exemplo   |
|-----|-----------|----------------|-----------------------------------------------------------------------------------------|----------|-----------|-----------|
| A01 | N/A       | id             | Identificador da peça no sistema AGCO              | Sim      | String    | 036857N1  |
| A02 | N/A       | dealerId       | Identificador do Dealer no Sistema AGCO     | Sim      | Number    | 11571     |
| A03 | N/A       | availabilities | Array da informação de disponibilidade de cada warehouse acessível pelo revendedor solicitado | Sim      | Array     | []        |
| A04 | A03       | warehouseCode  | Identificador único do armazém retornado | Sim      | String    | REPVT06   |
| A05 | A03       | warehouseOrder | Ordem de prioridade do warehouse retornado| Sim      | Number    | 1         |
| A06 | A03       | warehouseName  | Nome das warehouse retornadas                   | Sim      | String    | ERNESTINA |
| A07 | A03       | available      | Representa se a peça está disponível para ser comprada deste warehouse  | Sim      | Boolean   | true      |
<br />

### 6.4. Parts API - Price
Este endpoint é utilizado para recuperar informações de preço de um número de peça específico.

#### 6.4.1 Request

GET /parts/**{partnumber}**/price

| **Parâmetro** | **Descrição**   | **Tipo parâmetro** | **Obrigatório** | **Tipo** | **Valor padrão**  | **Exemplo**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| partNumber    | Identificador da peça no sistema AGCO| Path  | Não       | String        | Blank (null)            | 3012224X1      |
| dealerId      | Identificador do Dealer no sistema AGCO  | Query    | Não   | Number    | Blank (null)            | 1481682        |
| lang         | Idioma que os dados devem ser devolvidos: pt-BR, es-AR, en-EN | Query | Não | String | Dealer default language | pt-BR|
<br />
**Request Example:** 
GET /parts/{partNumber}/price?dealerId={dealerId}&lang={lang}

#### 6.4.2 Response
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


| ID  | Parent ID | Campo         | Descrição                                                      | Obrigatório | Tipo | Exemplo  |
|-----|-----------|---------------|------------------------------------------------------------------|----------|-----------|----------|
| A01 | N/A       | id            | Identificador da peça no sistema da AGCO              | Sim      | String    | 040665R1 |
| A02 | N/A       | dealerId      | Identificado do Dealer no sistema AGCO                   | Sim      | Number    | 11571    |
| A03 | N/A       | prices        | Array com informação de preços disponíveisle para peça     | Sim      | Array     | []       |
| A04 | A03       | currency      | Código da moeda para peça selecionada                      | Sim      | String    | BRL      |
| A05 | A03       | type          | Informação de tipo de peça: Pública, Específica, Campanha, Safra | Sim      | String    | PUBLIC   |
| A06 | A03       | value         | Preço da peça                                                    | Sim      | Number    | 12.34567 |
| A07 | A03       | warehouseCode | Identificação do warehouse onde esses dados de preço foram encontrados  | Sim      | String    | REPVT03  |
<br />


### 6.5. Parts API - Supersession

Este endpoint é utilizado para recuperar informações se a parte especificada foi substituída e quais são as peças de reposição.

#### 6.5.1 Request

GET /parts/**{partnumber}**/supersession

| **Parâmetro** | **Descrição**                                               | **Tipo** | **Obrigatório** | **Tipo** | **Valor padrão**       | **Exemplo**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| partNumber    | Identificador da peça no Sistema AGCO                                              | Path               | Não           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Identificador do Dealer no Sistema AGCO                 | Query              | Não           | Number        | Blank (null)            | 1481682        |
| lang          | Linguagem com que deve retornar: pt-BR, es-AR, en-EN | Query              | Não           | String        | Linguagem padrão do Dealer | pt-BR          |
<br />
**Exemplo de requisição:** GET /parts/036857N1/supersession?dealerId=1481682&lang=en-EN

#### 6.5.2 Resposta

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


| ID  | Parent ID | Campo                   | Descrição                           | Obrigatório | Tipo      | Exemplo       |
|-----|-----------|-------------------------|-------------------------------------|-------------|-----------|---------------|
| A01 | N/A       | supersededId            | AGCO Part number                    | Sim         | String    | 036857N1      |
| A02 | N/A       | supersededDescription   | AGCO Part description               | Sim         | String    | LEVER RH / LD |
| A03 | N/A       | supersedingId           | AGCO Substitution Part number       | Sim         | String    | 195910M1      |
| A04 | N/A       | supersedingDescription  | AGCO Substitution Part description  | Sim         | String    | BUSH          |
| A05 | N/A       | condition               | Supersession condition              | Sim         | String    | null          |
| A06 | N/A       | reversibility           | Supersession reversibility          | Sim         | String    | N             |
| A07 | N/A       | status                  | Supersession status                 | Sim         | String    | A             |
| A08 | N/A       | supersessionDescription | Supersession description            | Sim         | String    | Test          |
| A09 | N/A       | descLang                | Language of the description         | Sim         | String    | en            |
| A10 | N/A       | type                    | Supersession type                   | Sim         | String    | CO            |
| A11 | N/A       | quantity                | Supersession quantity               | Sim         | Number    | 1             |
<br />


### 6.6. Parts API - Taxes

Este ponto final é usado para recuperar informações fiscais de um número de peça específico.

#### 6.6.1 Request

GET /parts/**{partnumber}**/taxes

| **Parâmetro** | **Descrição**                                               | **Tipo de parâmetro** | **Obrigatório** | **Tipo de dado** | **Valor padrão**       | **Exemplo**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| partNumber    | AGCO Part Number                                              | Path               | Não           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | Não           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | Não           | String        | Dealer default language | pt-BR          |
<br />
**Exemplo de resposta:** 
GET /parts/{partNumber}/taxes?dealerId={dealerId}&lang={lang}

#### 6.6.2 Resposta
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


| ID  | Parent ID | Campo             | Descrição                                       | Obrigatório | Tipo| Exemplo  |
|-----|-----------|-------------------|-------------------------------------------------|----------|-----------|----------|
| A01 | N/A       | partNumber        | Número da peça                                    | Sim      | String    | 036857N1 |
| A02 | N/A       | taxClassification | Classificação de taxas                            | Sim      | String    | 0        |
| A03 | N/A       | taxes             | Conjunto de informação de taxas do partnumber | Sim      | Array     | []       |
| A04 | A03       | name              | Identificador exclusivo de taxas                           | Sim      | String    | IPI      |
| A05 | A03       | currency          | Moeda                                    | Sim      | String    | BRL      |
| A06 | A03       | value             | Valor                                     | Sim      | Number    | 27.50    |
<br />
