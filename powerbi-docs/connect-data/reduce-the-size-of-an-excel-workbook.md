---
title: Excel-munkafüzet méretének csökkentése a Power BI-ban való megtekintéshez
description: Excel-munkafüzet méretének csökkentése a Power BI-ban való megtekintéshez
author: davidiseminger
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-service
ms.topic: conceptual
ms.date: 01/10/2019
ms.author: davidi
LocalizationGroup: Data from files
ms.openlocfilehash: 8c58c85ea46f9884586e1ff73f1ef9f7b1db9cdd
ms.sourcegitcommit: 0e9e211082eca7fd939803e0cd9c6b114af2f90a
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83327231"
---
# <a name="reduce-the-size-of-an-excel-workbook-to-view-it-in-power-bi"></a>Excel-munkafüzet méretének csökkentése a Power BI-ban való megtekintéshez
A Power BI-ba bármely, 1 GB-nál kisebb Excel-munkafüzetet feltölthet. Az Excel-munkafüzet két részből állhat: egy adatmodellből és a jelentés többi részéből – a munkalap alaptartalmából. Ha a jelentés megfelel a következő méretkorlátoknak, mentheti a **OneDrive Vállalati verzióba**, csatlakoztathatja a Power BI-ból, és megtekintheti az Excel Online-on:

* A teljes munkafüzet maximális terjedelme 1 GB lehet.
* Az alapvető munkalaptartalmak maximális terjedelme 30 MB lehet.

## <a name="what-makes-core-worksheet-contents-larger-than-30-mb"></a>Mely alapvető munkalaptartalmak növelhetik a terjedelmet 30 MB fölé
Többek között az alábbi elemek növelhetik 30 MB fölé a munkalap alaptartalmát:

* Képek.
* Árnyékolt cellák. [Cellaárnyékolási formátum eltávolítása](https://support.office.com/article/Add-or-change-the-background-color-of-cells-ac10f131-b847-428f-b656-d65375fb815e).
* Színes munkalapok. [Munkalapháttér eltávolítása](https://support.office.com/article/add-or-remove-a-sheet-background-3577a762-8450-4556-96a2-cc265abc00a8).
* Szövegmezők.
* Beilleszthető képek.

Lehetőség szerint fontolja meg a felsorolt elemek eltávolítását. 

Ha a jelentésben adatmodell van, más lehetőségek is kínálkoznak: 

* Eltávolíthatja az adatokat az Excel-munkafüzetekből, és az adatmodellben tárolhatja őket. Tekintse meg az „Adatok eltávolítása a munkalapokról” részt alább. 
* [Memóriahatékony adatmodell létrehozása](https://support.office.com/article/Create-a-memory-efficient-Data-Model-using-Excel-2013-and-the-Power-Pivot-add-in-951c73a9-21c4-46ab-9f5e-14a2833b6a70) révén csökkentheti a jelentés teljes méretét.

Az összes ilyen változás végrehajtásához Excelben kell szerkesztenie a munkafüzetet.

További információk: [ Excel-munkafüzetek fájlméretkorlátai a SharePoint Online szolgáltatásban](https://support.office.com/article/File-size-limits-for-workbooks-in-SharePoint-Online-9e5bc6f8-018f-415a-b890-5452687b325e).

## <a name="remove-data-from-worksheets"></a>Adatok eltávolítása a munkalapokról
Ha a Power Query vagy az Excel-adatok lapról importál adatokat az Excelbe, a munkafüzet ugyanazokat az adatokat egy Excel-táblában és az adatmodellben is tárolhatja. Az Excel-munkalapokon található nagy táblázatok 30 MB fölé emelhetik a munkalap alaptartamát. Ha eltávolítja a táblázatot az Excelből, és az adatokat az adatmodellben tartja meg, jelentősen csökkentheti a jelentés alaptartalmát. 

Amikor adatokat importál az Excelbe, kövesse az alábbi tanácsokat:

* **A Power Queryben**: Törölje a **Betöltés munkalapra** mezőt.
  
  Ekkor a rendszer csak az adatmodellbe importálja az adatokat, az adatok nem kerülnek Excel-munkalapokra.
* **Az Excel-adatok lapról**: ha korábban bejelölte az importálás varázsló **Tábla** négyzetét: Lépjen a **Meglévő kapcsolatok** területre \> kattintson a kapcsolatra \> válassza a **Csak kapcsolat létrehozása** elemet. Törölje a kezdeti importálás során létrehozott táblázatot vagy táblázatokat.
* **Az Excel-adatok lapról**: az **Adatimportálás** mezőben ne jelölje be a **Táblázat** elemet.

## <a name="workbook-size-optimizer"></a>Workbook Size Optimizer (munkafüzetméret-optimalizáló)
Adatmodellt tartalmazó munkafüzet esetén a munkafüzetméret-optimalizáló futtatásával csökkentheti a munkafüzet méretét. [A Workbook Size Optimizer letöltése](https://www.microsoft.com/download/details.aspx?id=38793).

## <a name="related-info"></a>Kapcsolódó információ
[Memóriahatékony Adatmodell létrehozása](https://support.office.com/article/Create-a-memory-efficient-Data-Model-using-Excel-2013-and-the-Power-Pivot-add-in-951c73a9-21c4-46ab-9f5e-14a2833b6a70)

[A OneDrive Vállalati verzió hivatkozásainak használata a Power BI Desktopban](desktop-use-onedrive-business-links.md)

