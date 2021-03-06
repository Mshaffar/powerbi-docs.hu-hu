---
title: Power BI-adatkészlet tulajdonságai
description: A Power BI-adatkészlet API-k tulajdonságainak megismerése
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: conceptual
ms.date: 06/08/2018
ms.openlocfilehash: 7dad7071fbf887c36443cacdb9be83d83e0b89be
ms.sourcegitcommit: a72567f26c1653c25f7730fab6210cd011343707
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83561501"
---
# <a name="dataset-properties"></a>Adatkészlet tulajdonságai

Az adatkészletek API-jának jelenlegi v1 verziójában az adatkészlet létrehozása csak névvel és táblák gyűjteményével engedélyezett. Minden egyes tábla rendelkezhet névvel és oszlopok gyűjteményével. Minden oszlop rendelkezik egy névvel és adattípussal. Jelenleg bővítjük ezeket a tulajdonságokat, melyek közül a legfigyelemreméltóbb a mértékek és a táblák közötti kapcsolatok támogatása. Ebben a kiadásban támogatott tulajdonságok teljes listája a következő:

> [!IMPORTANT]
> Ez a [Datasets Operation Groups](https://docs.microsoft.com/rest/api/power-bi/datasets) (Adatkészletek, műveletcsoportok) oldalon érhető el.

## <a name="dataset"></a>Adathalmaz

Name (Név)  |Típus  |Description (Leírás)  |Csak olvasható  |Kötelező
---------|---------|---------|---------|---------
id     |  Guid       | Az adatkészlet egész rendszerre kiterjedő, egyedi azonosítója.        | Igaz        | Hamis        
név     | Sztring        | Az adatkészlet felhasználó által meghatározott neve.        | Hamis        | Igaz        
táblák     | Table[]        | Táblagyűjtemény.        |  Hamis       | Hamis        
kapcsolatok     | Relationship[]        | Táblák közti kapcsolatok gyűjteménye.        | Hamis        |  Hamis  
defaultMode     | Sztring        | A „Push” és „Streaming” értékekkel meghatározza, hogy az adatkészlet továbbítása leküldéssel, streameléssel vagy mindkettővel történjen-e.         | Hamis        |  Hamis

## <a name="table"></a>Tábla

Name (Név)  |Típus  |Description (Leírás)  |Csak olvasható  |Kötelező
---------|---------|---------|---------|---------
név     | Sztring        |  A tábla felhasználó által meghatározott neve. A tábla azonosítójaként is szolgál.       | Hamis        |  Igaz       
oszlopok     |  column[]       |  Oszlopgyűjtemény.       | Hamis        |  Igaz       
mértékek     | measure[]        |  Mértékgyűjtemény.       | Hamis        |  Hamis       
isHidden     | Logikai érték        | Ha az értéke igaz, a tábla rejtett lesz az ügyféleszközök elől.        | Hamis        | Hamis        

## <a name="column"></a>Oszlop

Name (Név)  |Típus  |Description (Leírás)  |Csak olvasható  |Kötelező
---------|---------|---------|---------|---------
név     |  Sztring        | Az oszlop felhasználó által meghatározott neve.        |  Hamis       | Igaz       
dataType     |  Sztring       |  Támogatott [EDM-adattípusok](/dotnet/framework/data/adonet/entity-data-model-primitive-data-types) és korlátozások. Lásd: [Adattípus-korlátozások](#data-type-restrictions).      |  Hamis       | Igaz        
formatString     | Sztring        | Egy sztring, amely leírja, hogyan kell formázni az értéket a megjelenésekor. A sztringek formázásáról további információért olvassa el a [FORMAT_STRING tartalmakat](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents).      | Hamis        | Hamis        
sortByColumn    | Sztring        |   Ugyanazon tábla oszlopának a sztringneve, amelyet a jelenlegi oszlop elrendezésére használ.     | Hamis        | Hamis       
dataCategory     | Sztring        |  Az ebben az oszlopban lévő adatokat leíró adatkategóriához használható sztringérték. Néhány gyakori érték például: Address, City, Continent, Country, Image, ImageUrl, Latitude, Longitude, Organization, Place, PostalCode, StateOrProvince, WebUrl       |  Hamis       | Hamis        
isHidden    |  Logikai érték       |  Tulajdonság, amely azt jelzi, hogy az oszlop rejtett-e a nézetben. Az alapértelmezett érték a false.       | Hamis        | Hamis        
summarizeBy     | Sztring        |  Alapértelmezett aggregációs módszer az oszlophoz. Értékek többek között: default, none, sum, min, max, count, average, distinctCount     |  Hamis       | Hamis

## <a name="measure"></a>Mérték

Name (Név)  |Típus  |Description (Leírás)  |Csak olvasható  |Kötelező
---------|---------|---------|---------|---------
név     | Sztring        |  A mérték felhasználó által meghatározott neve.       |  Hamis       | Igaz        
kifejezés     | Sztring        | Egy érvényes DAX-kifejezés.        | Hamis        |  Igaz       
formatString     | Sztring        |  Egy sztring, amely leírja, hogyan kell formázni az értéket a megjelenésekor. A sztringek formázásáról további információért olvassa el a [FORMAT_STRING tartalmakat](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents).       | Hamis        | Hamis        
isHidden     | Sztring        |  Ha az értéke igaz, a tábla rejtett lesz az ügyféleszközök elől.       |  Hamis       | Hamis       

## <a name="relationship"></a>Kapcsolat

Name (Név)  |Típus  |Description (Leírás)  |Csak olvasható  |Kötelező 
---------|---------|---------|---------|---------
név     | Sztring        | A kapcsolat felhasználó által meghatározott neve. A kapcsolat azonosítójaként is szolgál.        | Hamis       | Igaz        
crossFilteringBehavior     | Sztring        |    A kapcsolat szűrési iránya: OneDirection (alapértelmezett), BothDirections, Automatic       | Hamis        | Hamis        
fromTable     | Sztring        | A külső kulcs tábla neve.        | Hamis        | Igaz         
fromColumn    | Sztring        | A külső kulcs oszlop neve.        | Hamis        | Igaz         
toTable    | Sztring        | Az elsődleges kulcs tábla neve.        | Hamis        | Igaz         
toColumn     | Sztring        | Az elsődleges kulcs oszlop neve.        | Hamis        | Igaz        

## <a name="data-type-restrictions"></a>Adattípusokra vonatkozó korlátozások

Ezek a korlátozások a dataType tulajdonságra vonatkoznak.

Adattípus  |Korlátozások  
---------|---------
Int64     |   Az Int64.MaxValue és Int64.MinValue érték nem engedélyezett.      
Double     |  A Double.MaxValue és Double.MinValue érték nem engedélyezett. A számtól eltérő értékek (NaN) nem támogatottak. +Infinity és -Infinity értékek nem támogatottak egyes függvényekben (pl.: Min, Max).       
Logikai érték     |   Igaz vagy hamis.
Datetime    |   Az adatok betöltése során kvantáljuk az értékeket a napok törtrészével az 1/300 másodperc (3,33 ms) egész többszörösévé.      
Sztring     |  Jelenleg akár 4000 karaktert is lehetővé tesz sztringértékenként.
Tizedes tört|precision=28, scale=4

## <a name="example"></a>Példa
A következő mintakód tartalmaz néhányat ezek közül a tulajdonságok közül:

```json
{

  "name": "PushAdvanced",

  "tables": [

    {

      "name": "Date",

      "columns": [

        {

          "name": "Date",

          "dataType": "dateTime",

          "formatString": "dddd\\, mmmm d\\, yyyy",

          "summarizeBy": "none"

        }

      ]

    },

    {

      "name": "sales",

      "columns": [

        {

          "name": "Date",

          "dataType": "dateTime",

          "formatString": "dddd\\, mmmm d\\, yyyy",

          "summarizeBy": "none"

        },

        {

          "name": "Sales",

          "dataType": "int64",

          "formatString": "0",

          "summarizeBy": "sum"

        }

      ],

      "measures": [

        {

          "name": "percent to forecast",

          "expression": "SUM(sales[Sales])/SUM(forecast[forecast])",

          "formatString": "0.00 %;-0.00 %;0.00 %"

        }

      ]

    },

    {

      "name": "forecast",

      "columns": [

        {

          "name": "date",

          "dataType": "dateTime",

          "formatString": "m/d/yyyy",

          "summarizeBy": "none"

        },

        {

          "name": "forecast",

          "dataType": "int64",

          "formatString": "0",

          "summarizeBy": "sum"

        }

      ]

    }

  ],

  "relationships": [

    {

      "name": "2ea345ce-b147-436e-8ac2-9d3c4d82af8d",

      "fromTable": "sales",

      "fromColumn": "Date",

      "toTable": "Date",

      "toColumn": "Date",

      "crossFilteringBehavior": "bothDirections"

    },

    {

      "name": "5d95f419-e589-4345-9581-6e70670b1bba",

      "fromTable": "forecast",

      "fromColumn": "date",

      "toTable": "Date",

      "toColumn": "Date",

      "crossFilteringBehavior": "bothDirections"

    }

  ]

}
```