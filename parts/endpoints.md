---
currentMenu: parts-endpoints
parentMenu: parts
---

# Argentina Parts

## 7. Recursos e operações
Os campos e as regras das interfaces disponibilizadas para capturar informações de peças são:

### 7.1. Interface - Search

GET /parts/

parameters:
produces:
      parameters:
        - in: header
          name: Authorization
          description: Authorization Header
          required: true
          type: string
        - in: query
          name: query
          description: Query text
          required: false
          type: string
          collectionFormat: multi
        - in: query
          name: dealerId
          description: Dealer identifier from AGCO internal systems
          required: false
          type: number
        - in: query
          name: lang
          description: Desired language of the description
          required: false
          type: string
        - in: query
          name: page
          description: Page number
          required: false
          type: number

### 7.2. Interface - Detail

GET /parts/{partnumber}

      parameters:
        - in: header
          name: Authorization
          description: Authorization Header
          required: true
          type: string
        - in: path
          name: partnumber
          description: Part number
          required: true
          type: string
        - in: query
          name: dealerId
          description: Dealer identifier from AGCO internal systems
          required: false
          type: number
        - in: query
          name: lang
          description: Desired language of the description
          required: false
          type: string


### 7.3. Interface - Availability

GET /parts/{partnumber}/availability

      parameters:
        - in: header
          name: Authorization
          description: Authorization Header
          required: true
          type: string
        - in: path
          name: partnumber
          description: Part number
          required: true
          type: string
        - in: query
          name: dealerId
          description: Dealer identifier from AGCO internal systems
          required: false
          type: number
        - in: query
          name: lang
          description: Desired language of the description
          required: false
          type: string


### 7.4. Interface - Price

GET /parts/{partnumber}/price

      parameters:
        - in: header
          name: Authorization
          description: Authorization Header
          required: true
          type: string
        - in: path
          name: partnumber
          description: Part number
          required: true
          type: string
        - in: query
          name: dealerId
          description: Dealer identifier from AGCO internal systems
          required: false
          type: number


### 7.5. Interface - Supersession

GET /parts/{partnumber}/supersession

      parameters:
        - in: header
          name: Authorization
          description: Authorization Header
          required: true
          type: string
        - in: path
          name: partnumber
          description: Part number
          required: true
          type: string

### 7.6. Interface - Tax

GET /parts/{partnumber}/taxes

      parameters:
        - in: header
          name: Authorization
          description: Authorization Header
          required: true
          type: string
        - in: path
          name: partnumber
          description: Part number
          required: true
          type: string