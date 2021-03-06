---
title: Teljes jelentések exportálása PowerPointba
description: Ismerje meg, hogyan exportálhat jelentést a Power BI-ból a PowerPointba.
author: mihart
ms.reviewer: ''
ms.custom: contperfq4
ms.service: powerbi
ms.subservice: powerbi-consumer
ms.topic: conceptual
ms.date: 05/12/2020
ms.author: mihart
LocalizationGroup: Share your work
ms.openlocfilehash: f70c41e40ff2da385b2f63798b93dec3fcd7b7c5
ms.sourcegitcommit: a72567f26c1653c25f7730fab6210cd011343707
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83565741"
---
# <a name="export-reports-to-powerpoint"></a>Jelentések exportálása PowerPointba

[!INCLUDE[consumer-appliesto-yyny](../includes/consumer-appliesto-yyny.md)]


A Power BI szolgáltatás (app.powerbi.com) segítségével közzéteheti jelentését a Microsoft PowerPointban, és könnyedén létrehozhat bemutatót a Power BI-jelentés alapján. A PowerPointba történő exportáláskor a következő történik:

* A PowerPointban a Power BI-jelentés minden lapjából külön dia lesz.
* A rendszer a Power BI-jelentés minden oldalát egyetlen nagyfelbontású képként exportálja a PowerPointba.
* A jelentéshez adott szűrők és szeletelők beállításai megmaradnak.
* A PowerPointban létrejön egy hivatkozás, amely a Power BI-jelentésre mutat.

A **Power BI-jelentést** gyorsan exportálhatja a **PowerPointba**. Kövesse az alábbi szakaszban leírt lépéseket.

Másolhat egyszerre egy vizualizációt is a Power BI szolgáltatásból, és beillesztheti a PowerPointba (vagy bármely más, a beillesztést támogató programba). A vágólapra másoláshoz válassza a **Másolás képként** ikont. Ezután nyissa meg a PowerPointot, és illessze be a vizualizációt. További információt a [vizualizációk statikus képként történő másolását](../visuals/power-bi-visualization-copy-paste.md) ismertető cikkben tekinthet meg.

![Válassza a Másolás képként ikont](media/end-user-powerpoint/power-bi-copy.png)

## <a name="export-your-power-bi-report-to-powerpoint"></a>Power BI-jelentés exportálása a PowerPointba
A **Power BI szolgáltatásban** jelöljön ki egy jelentést a vásznon való megjelenítéshez. Egy jelentést a **kezdőlapon**, az **Alkalmazások** között, vagy a navigációs panel bármely más tárolójában is kijelölhet.

[!INCLUDE [power-bi-service-new-look-include](../includes/power-bi-service-new-look-include.md)]

Amikor a PowerPointba exportálandó jelentés megjelenik a vásznon, válassza az **Exportálás** > **PowerPoint** elemet a menüsávon.

![Az Exportálás lehetőség kiválasztása a menüsávon](media/end-user-powerpoint/power-bi-export.png)

Megjelenik egy előugró ablak, ahol kiválaszthatja az **Aktuális értékek** vagy az **Alapértelmezett értékek** lehetőséget. Az **Aktuális értékek** az aktuális állapotban exportálja a jelentést, amely tartalmazza a szeletelő és a szűrő értékein végzett aktív módosításokat.  A legtöbb felhasználó ezt a beállítást választja. Ha görgetett, az **Aktuális értékek** nem tartalmazza a vizualizáció görgetési állapotát, a rendszer pedig az adatok felső részét exportálja. Azt is megteheti, hogy az **Alapértelmezett értékek** lehetőség választásával az eredeti állapotában exportálja a jelentést, ahogyan azt a *tervezője* megosztotta, így az eredeti állapoton végzett semmilyen változtatás sem fog tükröződni.

![Exportálandó elem kiválasztása](media/end-user-powerpoint/power-bi-current-values.png)
 
Emellett egy jelölőnégyzetet is bejelölhet, amellyel kiválaszthatja, hogy exportálja-e vagy sem a jelentés rejtett lapjait. Jelölje be ezt a négyzetet, ha csak a böngészőben az Ön számára látható jelentésoldalakat szeretné exportálni. Ha inkább szeretné belefoglalni az exportba az összes rejtett oldalt is, akkor hagyja bejelöletlenül ezt a négyzetet. Ha a jelölőnégyzet ki van szürkítve, akkor nincsnek rejtett lapok a jelentésben. Egy rejtett lapra jó példa az elemleírások lapja. Az [egyéni elemleírásokat](../create-reports/desktop-tooltips.md) a *jelentéstervezők* hozzák létre, a Power BI szolgáltatás *felhasználói* számára pedig nem jelentéslapként jelennek meg. 

Miután elvégezte a kijelöléseket, válassza az **Exportálás** gombot a folytatáshoz. Ekkor a Power BI szolgáltatás böngészőablakának jobb felső sarkában megjelenik egy értesítés, hogy folyamatban van a jelentés exportálása a PowerPointba. 



![Értesítés – Exportálás PowerPointba folyamatban](media/end-user-powerpoint/power-bi-export-progress.png)

Az exportálás néhány percig is eltarthat. Az exportálás időtartamát többek között a jelentés szerkezete és a Power BI szolgáltatás aktuális terhelése befolyásolhatja. A jelentés exportálása közben Ön tovább dolgozhat a Power BI-ban.

Miután a Power BI szolgáltatás befejezte az exportálási folyamatot, erről az értesítési fejléc megváltozása tájékoztatja Önt. A fájl mostantól elérhető azon a helyen, ahol a böngésző megjeleníti a letöltött fájlokat. Az alábbi képen ez egy letöltési szalag formájában látható a böngészőablak alján.

![a képernyő alján megjelenő, böngészőbeli értesítés](media/end-user-powerpoint/power-bi-browsers.png)

Ennyi az egész! A fájlt letöltheti, megnyithatja a PowerPointban, módosíthatja és kibővítheti, mint minden más PowerPoint-bemutatót.

## <a name="open-the-powerpoint-file"></a>A PowerPoint-fájl megnyitása
Amikor megnyitja a Power BI-ból exportált PowerPoint-fájlt, számos remek és praktikus elemet talál. Tekintse meg az alábbi képet, és nézze végig a számozott elemek által szemléltetett nagyszerű funkciókat. A PowerPoint lapjai, függetlenül a Power BI-jelentés eredeti oldalméreteitől és dimenzióitól, mindig a szabványos 9:16 méretben jönnek létre.

![megnyílik a PowerPoint](media/end-user-powerpoint/power-bi-powerpoint-numbered.png)

1. A bemutató első oldalán a jelentés neve és egy hivatkozás látható, amelynek segítségével a bemutató alapjául szolgáló jelentést **megtekintheti a Power BI-ban**.
2. A jelentésről is hasznos információkhoz juthat. Az **Utolsó adatfrissítés** azt a dátumot és időt mutatja meg, amelyen az exportált jelentés alapul. A **Letöltés** azt a dátumot és időt mutatja, amikor a Power BI-jelentés PowerPoint-fájlba lett exportálva. A **Letöltés** által megjelenített idő a számítógép időzónája szerinti idő az exportálás időpontjában.


3. A jelentés minden oldala külön dián jelenik meg, ahogy azt a navigációs panel is mutatja. 
4. A közzétett jelentést a Power BI a saját nyelvi beállításainak megfelelően, vagy a böngésző nyelve szerint rendereli. A nyelvi beállításokat megtekintheti vagy módosíthatja a fogaskerék ikon ![Fogaskerék ikon](media/end-user-powerpoint/power-bi-settings-icon.png) > **Beállítások** > **Általános** > **Nyelv** lehetőség választásával. Nyelvi információk: [A Power BI által támogatott nyelvek és országok vagy régiók](../fundamentals/supported-languages-countries-regions.md).


Amikor megtekint egy adott diát, láthatja, hogy minden egyes jelentésoldal egy külön kép. A PowerPointban nem görgethet, mivel minden dia statikus kép.

![A vizualizációkat külön képekként mutató képernyő](media/end-user-powerpoint/power-bi-images.png)

Most már csak Önön múlik, hogy miképpen használja fel a PowerPoint-bemutatót vagy a nagyfelbontású képeket.

## <a name="considerations-and-troubleshooting"></a>Megfontolandó szempontok és hibaelhárítás
Az **Exportálás a PowerPointba** funkció használatakor figyelembe kell vennie néhány megfontolást és korlátozást.
 

* Az [URL-szűrők](../collaborate-share/service-url-filters.md) jelenleg nem érvényesek az exportálás **Aktuális értékek** beállítása esetén.

* Ha a PowerPointba való exportáláskor a jelentés egyéni betűkészletet használ, a rendszer az alapértelmezett betűkészletre cseréli az egyéni betűkészletet.

* Az alábbi vizualizációtípusok nem támogatottak, és nem lesznek a PowerPointba exportálva:
   - A [nem minősített egyéni vizualizációk](../developer/visuals/power-bi-custom-visuals-certified.md) nem támogatottak. 
   - Az [ESRI ArcGIS vizualizáció](../visuals/power-bi-visualizations-arcgis.md) nem támogatott
   - Az R- és a Python-vizualizációk nem támogatottak.
   - A háttérképek szélét a program a diagram határoló területével együtt levágja. A PowerPointba való exportálás előtt ajánlott eltávolítani a háttérképeket.

* Egyes jelentések nem exportálhatók. Ezek a következők:
    - A Power BI bérlői tartományán kívüli felhasználók jelentései, például olyan felhasználóké, akik nem a vállalat munkatársai, de megosztották Önnel a jelentést.
    - Ha egy irányítópultot cégen kívüli felhasználóval oszt meg (tehát olyasvalakivel, aki nincs jelen a Power BI-bérlőn), akkor az a felhasználó nem tudja a PowerPointba exportálni a megosztott irányítópulthoz kapcsolódó jelentéseket. Például ha Ön aaron@contoso.com, megoszthatja a munkáját a következővel: david@cohowinery.com. david@cohowinery.com viszont nem exportálhatja a kapcsolódó jelentéseket a PowerPointba.
    - A több mint 30 jelentésoldalt tartalmazó jelentések. Csak az első 30 oldal lesz exportálva.
    - Azok a jelentések, amelyek exportálása a PowerPoint régebbi verzióiba történik.

* Ha az **Exportálás a PowerPointba** menüpont nem érhető el a Power BI szolgáltatásban, valószínűleg a bérlői rendszergazda tiltotta le a funkciót. Részletekért lépjen kapcsolatba a bérlői rendszergazdával.
* A Power BI szolgáltatás a PowerPoint-exportálásnál a Power BI nyelvi beállításait alkalmazza. A nyelvi beállításokat megtekintheti vagy módosíthatja a fogaskerék ikon ![Fogaskerék ikon](media/end-user-powerpoint/power-bi-settings-icon.png) > **Beállítások** > **Általános** > **Nyelv** lehetőség választásával.



## <a name="next-steps"></a>Következő lépések
[Vizualizációk másolása statikus képként](../visuals/power-bi-visualization-copy-paste.md)    
[Jelentés nyomtatása](end-user-print.md)
