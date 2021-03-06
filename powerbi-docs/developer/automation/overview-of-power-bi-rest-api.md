---
title: Mire használhatom a Power BI API-t?
description: Mire használhatom a Power BI API-t?
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: overview
ms.date: 03/25/2019
ms.openlocfilehash: 1a74d856ad46dc6843546919aa4234dc86d2be5c
ms.sourcegitcommit: 7aa0136f93f88516f97ddd8031ccac5d07863b92
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/05/2020
ms.locfileid: "79488432"
---
# <a name="what-can-developers-do-with-the-power-bi-api"></a>Mire használhatják a fejlesztők a Power BI API-t?

A Power BI REST API-val Power BI-jelentéseket, irányítópultokat és csempéket beágyazó alkalmazásokat hozhat létre.

A Power BI REST API-val kezelési feladatokat is végezhet olyan Power BI-objektumokon, mint a jelentések, az adatkészletet és a munkaterületek.

Íme néhány, a Power BI API-k használatával elvégezhető feladat.

| **További információ** | **Hivatkozás erre az információra** |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Irányítópultok, jelentések és csempék beágyazása Power BI- és nem Power BI-felhasználók részére. | [Power BI-irányítópultok, -jelentések és -csempék beágyazása ](../embedded/embed-sample-for-customers.md) |
| Kezelési feladatok végrehajtása Power BI-objektumokon. | [A Power BI REST API-jainak leírása](https://docs.microsoft.com/rest/api/power-bi/) |
| Kulcsfontosságú adatok küldése Power BI-irányítópultokra a meglévő üzleti munkafolyamatok kiterjesztésével. | [Adatok küldése az irányítópultokra ](walkthrough-push-data.md) |
| Hitelesítés a Power BI-ban. | [Hitelesítés a Power BI-ban ](../embedded/get-azuread-access-token.md) |

> [!NOTE]
> A Power BI API-k továbbra is csoportokként hivatkoznak a munkaterületekre. Bármely csoportokra való utalás munkaterületek használatát jelöli.

## <a name="api-developer-tools"></a>API-fejlesztői eszközök

| Eszköz(ök) | Description (Leírás) |  |  |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|---|---|
| [Demókörnyezeti eszközök](https://microsoft.github.io/PowerBI-JavaScript/demo) | A Power BI JavaScript API-jainak használatát bemutató minták használata. Ez az eszköz lehetőséget ad a Power BI Embedded különböző mintáinak gyors kipróbálására. |  |  |
| [Power BI JavaScript wiki](https://github.com/Microsoft/powerbi-javascript/wiki) | További információ a Power BI JavaScript API-jairól. |  |  |
| [Postman](https://www.getpostman.com/) | Kérelmek futtatása, tesztelés, hibakeresés, monitorozás, automatizált tesztek futtatása és egyéb lehetőségek. |

## <a name="push-data-into-power-bi"></a>Adatok leküldése a Power BI szolgáltatásba

A Power BI API lehetővé teszi az [adatok leküldését az adatkészletekbe](walkthrough-push-data.md). A funkció segítéségével sorokat adhat hozzá az adatkészletekben lévő táblákhoz. Az irányítópultok csempéi vagy a jelentésekben lévő vizualizációk ezután tükrözik az új adatokat.

![Adatminta leküldése](media/overview-of-power-bi-rest-api/powerbi-push-data.png)

## <a name="github-repositories"></a>GitHub-adattárak

* [Power BI fejlesztői minták](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [.NET SDK](https://github.com/Microsoft/PowerBI-CSharp)
* [JavaScript API](https://github.com/Microsoft/PowerBI-JavaScript)

## <a name="next-steps"></a>Következő lépések

* [Adatok küldése adatkészletekbe](walkthrough-push-data.md)
* [Power BI-vizualizáció fejlesztése](../visuals/custom-visual-develop-tutorial.md)
* [A Power BI REST API-jainak leírása](rest-api-reference.md)
* [Power BI REST API-k](https://docs.microsoft.com/rest/api/power-bi/)

Több kérdése van? [Kérdezze meg a Power BI-közösséget](https://community.powerbi.com/)
