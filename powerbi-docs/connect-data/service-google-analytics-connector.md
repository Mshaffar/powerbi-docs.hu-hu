---
title: 'Külső szolgáltatás: Google Analytics-összekötő'
description: 'Külső szolgáltatás: Google Analytics-összekötő a Power BI Desktophoz'
author: davidiseminger
ms.reviewer: ''
ms.custom: seodec18
ms.service: powerbi
ms.subservice: powerbi-desktop
ms.topic: conceptual
ms.date: 05/08/2019
ms.author: davidi
LocalizationGroup: Connect to data
ms.openlocfilehash: 4b279ebb1ae4ae34f1b9832883ddde5d804a7ace
ms.sourcegitcommit: 0e9e211082eca7fd939803e0cd9c6b114af2f90a
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83304047"
---
# <a name="use-the-google-analytics-connector-for-power-bi-desktop"></a>A Power BI Desktophoz készült Google Analytics-összekötő használata
> [!NOTE]
> A Power BI Destophoz készült Google Analytics tartalomcsomag és -összekötő a Google Analytics alapvető jelentéskészítő API-jára támaszkodik. Ennek következtében a funkciók és az elérhetőség az idő során változhatnak.

A Google Analytics adataihoz a **Google Analytics** összekötőjének használatával csatlakozhat. A csatlakozáshoz kövesse az alábbi lépéseket:

1. A **Power BI Desktop** **Kezdőlap** szalagján kattintson az **Adatok beolvasása** lehetőségre.
2. Az **Adatok beolvasása** ablak bal oldali ablaktábláján a kategóriák között válassza az **Online szolgáltatások** lehetőséget.
3. A jobb oldali listán kattintson a **Google Analytics** elemre.
4. Az ablak alján kattintson a **Csatlakozás** elemre.  
   ![](media/service-google-analytics-connector/tps_googleanalytics_1.png)

Ekkor egy párbeszédpanel tájékoztatja, hogy az összekötő egy külső szolgáltatás, és többek között arra figyelmezteti, hogy a funkciók és az elérhetőség idővel változhatnak.  
![](media/service-google-analytics-connector/tps_googleanalytics_2.png)

Ha a **Folytatás** elemre kattint, a rendszer arra kéri, hogy jelentkezzen be a Google Analytics-be.  
![](media/service-google-analytics-connector/tps_googleanalytics_3.png)

A hitelesítő adatok megadásakor a rendszer tájékoztatja, hogy a Power BI kapcsolat nélküli hozzáférést kér. Így férhet hozzá a Google Analytics-adataihoz a **Power BI Desktop** használatával.  

Az elfogadás után a **Power BI Desktop** jelzi, hogy Ön bejelentkezett.  
![](media/service-google-analytics-connector/tps_googleanalytics_5.png)

Ha a **Csatlakozás** lehetőségre kattint, a Google Analytics-adatok csatlakoznak a **Power BI Desktophoz**, és betöltődnek.  
![](media/service-google-analytics-connector/tps_googleanalytics_6.png)

## <a name="changes-to-the-api"></a>Az API módosításai
Bár minden változást igyekszünk követni a frissítések kibocsátásával, az API esetleges módosulásai befolyásolhatják az általunk létrehozott lekérdezések eredményeit. Egyes esetekben előfordulhat, hogy bizonyos lekérdezések már nem kapnak támogatást. E függőség miatt az említett összekötő használata esetén nem garantálhatjuk az eredményes lekérdezéseket.

A Google Analytics API módosulásainak további részletei az erre vonatkozó [változásnaplóban](https://developers.google.com/analytics/devguides/changelog) találhatók.

