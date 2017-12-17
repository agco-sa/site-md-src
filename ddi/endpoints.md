---
currentMenu: ddi-endpoints
parentMenu: ddi
---

#Dealer Data Integration

##5. Recursos e operações
Essa sessão contém os campos e regras das interfaces disponibilizadas para capturar informações de peças das concessionárias.
A API é composta de uma lista de recursos com possibilidade de diferentes operações dependendo do verbo HTTP utilizado, do caminho e dos parâmetros.

###5.1. Interface DealerNFe
Envia para a AGCO as informações de venda da revenda ao cliente final. no DMS a seleção de dados deverá atender a duas premissas importantes:
	+ Considerar as notas fiscais de Devolução(entrada), Saída e Transferência aptas a serem integradas e que contenham produtos a serem integrados conforme definido no cadastro de produto.
	+ Somente para as notas transmitidas e autorizadas pela SEFAZ, após o prazo máximo definido pelo cancelamento - não está previsto nenhum tratamento sobre o cancelamento de notas.
Recomenda-se a adoção de um parâmetro padrão que define o tempo máximo pra cancelamento da nota fiscal SEFAZ para validar as notas aptas a integração DMS x AGCO. 
A estrutura JSON contendo os dados é enviada no corpo da chamada. Segue um exemplo do corpo de uma mensagem válida, no padrão JSON esperado, contendo TAGS do schema.
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

####5.1.1. Especificação de atributos grupo “nfe”

| TAG | Tipo | Descrição | Regra | Mandatório | Exemplo |	
|---|---|---|---|---|-|	
|   | numeric(4,2) | Versão do layout |  | ![check](/images/check.png) | "versao": 3.00 |
|   | varchar(47)) | Identificador da TAG a ser  assinada | Informar a chave de acesso da NFe precedida do literal ‘NFe’, acrescentada a validação do formato | ![check](/images/check.png) | "Id": " NFe43150395437281000312550030000296371002180066" |

####5.1.2. Especificação de atributos grupo “XMLFile”

####5.1.3. Especificação de atributos grupo “ddi”

###5.2. Interface Stock

###5.3. Interface Campaign

**\* Se existir a informação de CPF o campo CNPJ deve vir vazio. O mesmo acontece para o caso contrário.**
