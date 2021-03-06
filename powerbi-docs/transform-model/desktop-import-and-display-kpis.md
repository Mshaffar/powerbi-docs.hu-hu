---
title: KPI-k importálása és megjelenítése a Power BI-ban
description: KPI-k importálása és megjelenítése
author: davidiseminger
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-desktop
ms.topic: conceptual
ms.date: 05/08/2019
ms.author: davidi
LocalizationGroup: Model your data
ms.openlocfilehash: 9f09dbabd82a43c15fbc59b3d357a424968c3fb6
ms.sourcegitcommit: 0e9e211082eca7fd939803e0cd9c6b114af2f90a
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83325506"
---
# <a name="import-and-display-kpis-in-power-bi"></a>KPI-k importálása és megjelenítése a Power BI-ban
A **Power BI Desktop** használatával KPI-ket importálhat és jeleníthet meg a táblákban, mátrixokban és kártyákon.

A KPI-k importálásához és megjelenítéséhez kövesse az alábbi lépéseket

1. Kezdje egy olyan Excel-fájllal, amely Power Pivot-modellel és KPI-kkel rendelkezik. Ebben a gyakorlatban egy *KPI-k* elnevezésű munkafüzetet használunk.

1. Importálja az Excel-munkafüzetet a Power BI-ba a **File -> Importálás -> Excel-munkafüzet tartalma** lehetőséggel. Így [a munkafüzetek importálásának módját is elsajátíthatja](../connect-data/desktop-import-excel-workbooks.md). 

1. A Power BI-ba történt importálás után a KPI megjelenik a **jelzőlámpa** ikonnal jelölt ![Mezők](media/desktop-import-and-display-kpis/traffic.png) panelen. Ahhoz, hogy a KPI-t felhasználhassa a jelentésben, ki kell bontania annak tartalmát, hogy megjelenjen az **Érték**, **Cél** és **Állapot** mező.

    ![](media/desktop-import-and-display-kpis/desktoppreviewfeatureon2.png)

1. Az importált KPI-ket érdemes szabványos vizualizáció-típusokban, például **Tábla** típusban felhasználni. A Power BI **KPI** vizualizáció-típust is tartalmaz, amely csak új KPI-k létrehozásához használandó.
   
    ![](media/desktop-import-and-display-kpis/desktoppreviewfeatureon3.png)

Ennyi az egész. Ezekkel a KPI-kkel trendeket, előrehaladást vagy egyéb jelentős mutatókat emelhet ki.
