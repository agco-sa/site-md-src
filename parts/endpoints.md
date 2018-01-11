---
currentMenu: parts-endpoints
parentMenu: parts
---

# Argentina Parts

## 7. Endpoints

The AGCO Parts API has six endpoints available for retriving part information such as details, pricing, availability information, taxes and supersession.

### 7.1. Parts API - Search

This endpoint can be used to retrieve a list of possible AGCO parts based on a query text which will be compared to AGCO database part numbers or description.

#### 7.1.1 Request

GET /parts

| **Parameter** | **Description**                                               | **Parameter Type** | **Required** | **Data Type** | **Default Value**       | **Example**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| Authorization | Authorization Token (Using OAuth2) - See Security for Details | Header             | No           | String        | Blank (null)            | Bearer <Token> |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | No           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | No           | String        | Dealer default language | pt-BR          |
| query         | Input text query to search on database.                       | Query              | No           | Query         | Blank (null)            | 3012224X1      |
| page[size]    | Maximum number of items desired to be returned on each page.  | Query              | No           | Number        | 10                      | 100            |
| page[number]  | Desired page                                                  | Query              | No           | Number        | 1                       | 10             |
<br />
**Request Example:** GET /parts?dealerId=1481682&query=3012224X1&lang=en-EN

#### 7.1.2 Response

The following example represents the response of the above request if it has has been processed successfully:

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


| ID  | Parent ID | Field               | Description                                                                                             | Required | Data Type | Example                 |
|-----|-----------|---------------------|---------------------------------------------------------------------------------------------------------|----------|-----------|-------------------------|
| A01 | N/A       | id                  | Part number.                                                                                            | Yes      | String    | 3012224X1               |
| A02 | N/A       | description         | Part description.                                                                                       | Yes      | String    | HEXAGON M20             |
| A03 | N/A       | descriptionLanguage | Language of the description.                                                                            | Yes      | String    | en                      |
<br />

### 7.2. Parts API - Detail

This endpoint is used to retrieve detailed information about a specific part number.

#### 7.2.1 Request

GET /parts/**{partnumber}**

| **Parameter** | **Description**                                               | **Parameter Type** | **Required** | **Data Type** | **Default Value**       | **Example**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| Authorization | Authorization Token (Using OAuth2) - See Security for Details | Header             | No           | String        | Blank (null)            | Bearer <Token> |
| partNumber    | AGCO Part Number                                              | Path               | No           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | No           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | No           | String        | Dealer default language | pt-BR          |
<br />
**Request Example:** GET /parts/3012224X1?dealerId=1481682&lang=en-EN

#### 7.2.2 Response

The following example represents the response of the above request if it has has been processed successfully:

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


| ID  | Parent ID | Field               | Description                                                                                             | Required | Data Type | Example                 |
|-----|-----------|---------------------|---------------------------------------------------------------------------------------------------------|----------|-----------|-------------------------|
| A01 | N/A       | id                  | Part number.                                                                                            | Yes      | String    | 3012224X1               |
| A02 | N/A       | description         | Part description.                                                                                       | Yes      | String    | HEXAGON M20             |
| A03 | N/A       | descriptionLanguage | Language of the description.                                                                            | Yes      | String    | en                      |
| A04 | N/A       | country             | Country associated with the part description.                                                           | Yes      | String    | BRA                     |
| A05 | N/A       | weight              | Weight in kilograms.                                                                                    | Yes      | Decimal   | 1.23456                 |
| A06 | N/A       | minimumQuantity     | Minimum ordering quantity of this part number.                                                          | Yes      | Decimal   | 1.23456                 |
| A07 | N/A       | movementCode        | Movement code.                                                                                          | Yes      | String    | Criticidade Muito Baixa |
| A08 | N/A       | fiscalCategory      | Fiscal Category.                                                                                        | Yes      | String    |                         |
| A09 | N/A       | directShipping      | Indicates whether this part has direct shipping or not.                                                 | Yes      | Boolean   | false                   |
| A10 | N/A       | superseded          | Indicates that this part number is obsolete and need to search for more recent replacement part number. | Yes      | Boolean   | true                    |
| A11 | N/A       | additionalInfo      | Additional Information (Optional)                                                                       | No       | Array     | []                      |
| A12 | A11       | name                | Attribute name.                                                                                         | No       | String    | BNDES                   |
| A13 | A11       | value               | Attribute value.                                                                                        | No       | Object    | true                    |
<br />

### 7.3. Parts API - Availability

This endpoint is used to retrieve information about stock availability of a specific part number.

#### 7.3.1 Request

GET /parts/**{partnumber}**/availability

| **Parameter** | **Description**                                               | **Parameter Type** | **Required** | **Data Type** | **Default Value**       | **Example**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| Authorization | Authorization Token (Using OAuth2) - See Security for Details | Header             | No           | String        | Blank (null)            | Bearer <Token> |
| partNumber    | AGCO Part Number                                              | Path               | No           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | No           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | No           | String        | Dealer default language | pt-BR          |
<br />
**Request Example:** GET /parts/036857N1/availability?dealerId=1481682&lang=en-EN

#### 7.3.2 Response

The following example represents the response of the above request if it has has been processed successfully:

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


| ID  | Parent ID | Field          | Description                                                                             | Required | Data Type | Example   |
|-----|-----------|----------------|-----------------------------------------------------------------------------------------|----------|-----------|-----------|
| A01 | N/A       | id             | Part number.                                                                            | Yes      | String    | 036857N1  |
| A02 | N/A       | dealerId       | Dealer identifier from AGCO internal systems.                                           | Yes      | Number    | 11571     |
| A03 | N/A       | availabilities | Array of availability information of each warehouse accessible by the requested dealer. | Yes      | Array     | []        |
| A04 | A03       | warehouseCode  | Unique identifier of the retrieved warehouse.                                           | Yes      | String    | REPVT06   |
| A05 | A03       | warehouseOrder | Priority order of the retrieved warehouse.                                              | Yes      | Number    | 1         |
| A06 | A03       | warehouseName  | Name of the retrieved warehouse.                                                        | Yes      | String    | ERNESTINA |
| A07 | A03       | available      | Represents whether the part is available to be brought from this warehouse.             | Yes      | Boolean   | true      |
<br />

### 7.4. Parts API - Price

This endpoint is used to retrieve price information of a specific part number.

#### 7.4.1 Request

GET /parts/**{partnumber}**/price

| **Parameter** | **Description**                                               | **Parameter Type** | **Required** | **Data Type** | **Default Value**       | **Example**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| Authorization | Authorization Token (Using OAuth2) - See Security for Details | Header             | No           | String        | Blank (null)            | Bearer <Token> |
| partNumber    | AGCO Part Number                                              | Path               | No           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | No           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | No           | String        | Dealer default language | pt-BR          |
<br />
**Request Example:** GET /parts/040665R1/price?dealerId=1481682&lang=en-EN

#### 7.4.2 Response

The following example represents the response of the above request if it has has been processed successfully:

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


| ID  | Parent ID | Field         | Description                                                      | Required | Data Type | Example  |
|-----|-----------|---------------|------------------------------------------------------------------|----------|-----------|----------|
| A01 | N/A       | id            | Part number.                                                     | Yes      | String    | 040665R1 |
| A02 | N/A       | dealerId      | Dealer identifier from AGCO internal systems.                    | Yes      | Number    | 11571    |
| A03 | N/A       | prices        | Array of available price information for this part number.       | Yes      | Array     | []       |
| A04 | A03       | currency      | Currency code of this price.                                     | Yes      | String    | BRL      |
| A05 | A03       | type          | Price type information. (PUBLIC, SPECIFIC, CAMPAIGN or HARVEST). | Yes      | String    | PUBLIC   |
| A06 | A03       | value         | Price value                                                      | Yes      | Number    | 12.34567 |
| A07 | A03       | warehouseCode | Warehouse identification where this price data has been found.   | Yes      | String    | REPVT03  |
<br />


### 7.5. Parts API - Supersession

This endpoint is used to retrieve information if the specified part has been replaced and what the replacement parts are.

#### 7.5.1 Request

GET /parts/**{partnumber}**/supersession

| **Parameter** | **Description**                                               | **Parameter Type** | **Required** | **Data Type** | **Default Value**       | **Example**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| Authorization | Authorization Token (Using OAuth2) - See Security for Details | Header             | No           | String        | Blank (null)            | Bearer <Token> |
| partNumber    | AGCO Part Number                                              | Path               | No           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | No           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | No           | String        | Dealer default language | pt-BR          |
<br />
**Request Example:** GET /parts/036857N1/supersession?dealerId=1481682&lang=en-EN

#### 7.5.2 Response

The following example represents the response of the above request if it has has been processed successfully:

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


| ID  | Parent ID | Field                   | Description                         | Required | Data Type | Example       |
|-----|-----------|-------------------------|-------------------------------------|----------|-----------|---------------|
| A01 | N/A       | supersededId            | AGCO Part number                    | Yes      | String    | 036857N1      |
| A02 | N/A       | supersededDescription   | AGCO Part description               | Yes      | String    | LEVER RH / LD |
| A03 | N/A       | supersedingId           | AGCO Substitution Part number       | Yes      | String    | 195910M1      |
| A04 | N/A       | supersedingDescription  | AGCO Substitution Part description  | Yes      | String    | BUSH          |
| A05 | N/A       | condition               | Supersession condition              | Yes      | String    | null          |
| A06 | N/A       | reversibility           | Supersession reversibility          | Yes      | String    | N             |
| A07 | N/A       | status                  | Supersession status                 | Yes      | String    | A             |
| A08 | N/A       | supersessionDescription | Supersession description            | Yes      | String    | Test          |
| A09 | N/A       | descLang                | Language of the description         | Yes      | String    | en            |
| A10 | N/A       | type                    | Supersession type                   | Yes      | String    | CO            |
| A11 | N/A       | quantity                | Supersession quantity               | Yes      | Number    | 1             |
<br />


### 7.6. Parts API - Tax

This endpoint is used to retrieve tax information of a specific part number.

#### 7.6.1 Request

GET /parts/**{partnumber}**/taxes

| **Parameter** | **Description**                                               | **Parameter Type** | **Required** | **Data Type** | **Default Value**       | **Example**    |
|---------------|---------------------------------------------------------------|--------------------|--------------|---------------|-------------------------|----------------|
| Authorization | Authorization Token (Using OAuth2) - See Security for Details | Header             | No           | String        | Blank (null)            | Bearer <Token> |
| partNumber    | AGCO Part Number                                              | Path               | No           | String        | Blank (null)            | 3012224X1      |
| dealerId      | Dealer identifier from AGCO internal systems.                 | Query              | No           | Number        | Blank (null)            | 1481682        |
| lang          | Language which data should be returned (pt-BR, es-AR, en-EN). | Query              | No           | String        | Dealer default language | pt-BR          |
<br />
**Request Example:** GET /parts/3012224X1/taxes?dealerId=1481682&lang=en-EN

#### 7.6.2 Response

The following example represents the response of the above request if it has has been processed successfully:

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


| ID  | Parent ID | Field             | Description                                     | Required | Data Type | Example  |
|-----|-----------|-------------------|-------------------------------------------------|----------|-----------|----------|
| A01 | N/A       | partNumber        | Part number                                     | Yes      | String    | 036857N1 |
| A02 | N/A       | taxClassification | Tax classification                              | Yes      | String    | 0        |
| A03 | N/A       | taxes             | Array of taxes information for this part number | Yes      | Array     | []       |
| A04 | A03       | name              | Tax unique identifier                           | Yes      | String    | IPI      |
| A05 | A03       | currency          | Tax currency                                    | Yes      | String    | BRL      |
| A06 | A03       | value             | Tax value                                       | Yes      | Number    | 27.50    |
<br />
