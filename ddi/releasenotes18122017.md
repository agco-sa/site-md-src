---
currentMenu: ddi-releasenotes18122017
parentMenu: ddi
---


# Dealer Data Integration

# Release Notes - 18 Dez 2017

## O que temos de novo?
+ Inclusão campo Campanha
+ Inclusão campo XMLFile

## Objetivo
Para que seja contemplada a inclusão/seleção da Campanha inserida na tela de Cadastro de Nota Fiscal na tela de "Consulta Estoque > Cadastrar Nota Fiscal", reflita as mesmas informações, estamos incluindo os campos para informar Campanha e o XML da Nota Fiscal no endpoint 'DealerNfe'.

## Inclusão "ddi/campaign" ?

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

## Inclusão "XMLFile"

    "XMLFile": {
        "base64": "",
        "filename": "43150495437281000312550030000301351002205802-nfe.xml",
        "filesize": 8013,
        "filetype": "text/xml"
    },

## API Changes 

> + ddi/campaign
> + XMLFile





