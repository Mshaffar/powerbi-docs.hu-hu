---
title: Elemzések futtatása és megtekintése irányítópult-csempéken
description: Power BI-végfelhasználóként érdemes elsajátítania az irányítópult-csempék elemzési eredményeinek megállapítását.
author: mihart
ms.reviewer: ''
featuredvideoid: et_MLSL2sA8
ms.service: powerbi
ms.subservice: powerbi-consumer
ms.topic: conceptual
ms.date: 03/11/2020
ms.author: mihart
LocalizationGroup: Dashboards
ms.openlocfilehash: 891a9b1a5afee26bdb2d6b363ccd2cee5f2461cb
ms.sourcegitcommit: 7aa0136f93f88516f97ddd8031ccac5d07863b92
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/05/2020
ms.locfileid: "79377284"
---
# <a name="view-data-insights-on-dashboard-tiles-with-power-bi"></a>Adatelemzési eredmények megtekintése irányítópult-csempéken a Power BI-jal

[!INCLUDE[consumer-appliesto-yyny](../includes/consumer-appliesto-yyny.md)]

Az irányítópulton található vizualizációs [csempék](end-user-tiles.md) mindegyike nagyszerű lehetőséget kínál az adatfeltárással való ismerkedéshez. Ha rákattint egy csempére, megnyílik egy jelentés vagy a [Q&A](end-user-q-and-a.md), amelyben szűrheti és rendezheti a jelentés alapjául szolgáló adathalmazt, és részletes elemzést végezhet rajta. Elemzések futtatásakor pedig a Power BI elvégzi Ön helyett az adatok felderítését.

![három pont menü mód](./media/end-user-insights/power-bi-insight.png)

Elemzéseket futtatva érdekes interaktív vizualizációkat hozhat létre adataiból. Elemzéseket futtathat az irányítópult adott csempéin, és még az elemzéseken is futtathat elemzést!

A megállapítási szolgáltatás a Microsoft Researchcsel együttműködésben fejlesztett, növekvő számú [haladó szintű elemzési algoritmusra épül](end-user-insight-types.md). A Microsoft Research egyre több felhasználó számára teszi lehetővé megállapítások kinyerését az adatokból újszerű és intuitív módszerekkel.

## <a name="run-insights-on-a-dashboard-tile"></a>Irányítópult csempére vonatkozó elemzések futtatása
Ha az irányítópult egyik csempéjén futtat elemzéseket, a Power BI megkeresi az adott csempe létrehozásához használt adatokat. 

1. [Nyisson meg egy irányítópultot](end-user-dashboards.md).
2. Vigye az egérmutatót egy csempe fölé. Válassza a **További beállítások** (...) lehetőséget, majd az **Elemzések megtekintése** elemet. 

    ![három pont menü mód](./media/end-user-insights/power-bi-hovers.png)


3. A csempe [Fókusz módban](end-user-focus.md) nyílik meg, és a jobb oldalán jelennek meg az elemzéskártyák.    
   
    ![Fókusz mód](./media/end-user-insights/power-bi-insights-tile.png)    
4. Felkeltette valamelyik elemzés az érdeklődését? Az adott elemzéskártyát kiválasztva az adatok mélyebb szintjére is leáshat. A kiválasztott elemzés a bal oldalon fog megjelenni, az új, kizárólag az adott elemzés adatain alapuló új elemzéskártyák pedig a jobb oldalon.    

 ## <a name="interact-with-the-insight-cards"></a>Az elemzéseket megjelenítő kártyák interaktív használata
Egy elemzés megnyitása után folytathatja a felderítést.

   * A vizualizációt a vásznon szűrheti.  A szűrők megjelenítéshez a jobb felső sarokban látható nyilat választva nyithatja meg a Szűrők panelt.

      ![elemzés és a Szűrők menü kibontva](./media/end-user-insights/power-bi-filters.png)
   
   * Elemzést magára az elemzés kártyájára vonatkozóan is futtathat. Ezt gyakran **kapcsolódód elemzésnek** is nevezik. Kijelöléssel tegyen aktívvá egy elemzéskártyát. Az megjelenik a jelentésvásznon.
   
      ![elemzés és a Szűrők menü kibontva](./media/end-user-insights/power-bi-insight-card.png)
   
   * Válassza a jobb felső sarokban látható villanykörte ikont ![Elemzések lekérése ikon](./media/end-user-insights/power-bi-bulb-icon.png) vagy az **Elemzések lekérése** lehetőséget. A bal oldalon megjelennek az elemzések, a jobb oldalon pedig új kártyák láthatók, melyeket kizárólag az adott elemzésben szereplő adatok alapján készített a rendszer.
     
     ![az Elemzések lekérése ikon a menüsávon](./media/end-user-insights/power-bi-related.png)
     
A jelentéshez a bal felső sarokban látható **Kilépés a fókusz módból** lehetőséget választva léphet vissza.

## <a name="considerations-and-troubleshooting"></a>Szempontok és hibaelhárítás
- Az **Elemzések megtekintése** az irányítópult nem minden csempetípusával használható. Például Power BI-vizualizációkhoz nem érhető el.<!--[Power BI visuals](end-user-custom-visuals.md)-->


## <a name="next-steps"></a>További lépések
További tudnivalók a [Gyors elemzések típusaival kapcsolatban](end-user-insight-types.md)

