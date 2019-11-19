---
title: Vállalati vizualizációk a Power BI-ban
description: Vállalati vizualizációk használata, kezelése és létrehozása a Power BI-ban
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-desktop
ms.topic: conceptual
ms.date: 12/11/2018
LocalizationGroup: Visualizations
ms.openlocfilehash: 8c28c5ee89ffee37c09db8dc6ffcd6fb90274786
ms.sourcegitcommit: 08b73af260ded51daaa6749338cb85db2eab587f
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/15/2019
ms.locfileid: "74102088"
---
# <a name="organizational-visuals-in-power-bi"></a>Vállalati vizualizációk a Power BI-ban

A Power BI-ban a Power BI-vizualizációkkal személyre szabott, egyedi stílusú vizualizációkat hozhat létre. Ezeket a Power BI-vizualizációkat fejlesztők készítik, és azokat gyakran akkor hozzák létre, amikor a Power BI-ban található számos látványelem nem egészen felelt meg az igényeiknek.

Egyes szervezeteknél a Power BI-vizualizációk még ennél is fontosabbak – szükségesek lehetnek a szervezet bizonyos egyedi adatainak vagy elemzéseinek átadásához, speciális adatkövetelményeik lehetnek, vagy privát üzleti eljárásokat emelhetnek ki. Az ilyen szervezeteknek Power BI-vizualizációkat kell fejleszteniük, azokat meg kell osztaniuk az egész szervezetben, és gondoskodniuk kell azok megfelelő karbantartásáról. A Power BI vizualizációival a szervezetek pont ezt tehetik.

A következő képen az a folyamat látható, mely alapján a Power BI szervezeti Power BI-vizualizációi a rendszergazdától a fejlesztésen és a karbantartáson át végül eljutnak az adatelemzőkhöz.

![Egyéni vizualizáció képe](media/power-bi-custom-visuals-organizational/custom-visual-org-01.jpg)

A szervezeti vizualizációkat a Power BI rendszergazdája helyezi üzembe és kezeli a felügyeleti portálon. A szervezeti adattárban való üzembe helyezésük után a szervezet felhasználói könnyedén felderíthetik őket, és közvetlenül a Power BI Desktopból importálhatják a szervezeti Power BI-vizualizációkat.

A szervezeti Power BI-vizualizációk létrehozott jelentésekben való használatával kapcsolatban a következő cikkben találhat további információt: [További tudnivalók a szervezeti vizualizációk jelentésekbe importálásáról](power-bi-custom-visuals.md).

## <a name="administer-organizational-power-bi-visuals"></a>A szervezeti Power BI-vizualizációk felügyelete

A szervezeti Power BI-vizualizációknak a szervezetben való felügyeletével, üzembe helyezésével és kezelésével kapcsolatban a következő cikkben találhat további információt: [További információk a szervezeti Power BI-vizualizációk üzembe helyezésével és kezelésével kapcsolatban](https://go.microsoft.com/fwlink/?linkid=866790).

> [!WARNING]
> Az egyéni vizualizációk biztonsági és adatvédelmi kockázatokat tartalmazó kódot is tartalmazhatnak. Győződjön meg arról, hogy az egyéni vizualizációk szerzője és forrása megbízható, mielőtt üzembe helyezné őket a szervezet tárházban.

## <a name="considerations-and-limitations"></a>Megfontolandó szempontok és korlátozások

Több szempontot és korlátozást is figyelembe kell venni.

Rendszergazdák:

* Az örökölt Power BI-vizualizációk (mint például azok a Power BI-vizualizációk, melyek nem az új verzióval ellátott API-kra épülnek) használata nem támogatott

* Ha egy egyéni vizualizációt törölnek a tárházból, leáll minden olyan meglévő jelentés megjelenítése, mely a törölt vizualizációt használja. Az adattárból való törlés művelete nem vonható vissza. Az egyéni vizualizációk ideiglenes letiltásához használja a „Letiltás” funkciót.

Végfelhasználók:

* A szervezeti Power BI-vizualizációk a szervezeti adattárból importált privát vizualizációk. Ahogy a többi privát vizualizáció, ezek sem [exportálhatók a PowerPointba](https://docs.microsoft.com/power-bi/consumer/end-user-powerpoint), és nem jeleníthetők meg olyan e-mailekben, amelyek akkor érkeznek, amikor egy felhasználó [feliratkozik jelentésoldalakra](https://docs.microsoft.com/power-bi/consumer/end-user-subscribe). Ezeket a funkciókat csak a közvetlenül a piactérről importált, [minősített Power BI-vizualizációk](https://docs.microsoft.com/power-bi/power-bi-custom-visuals-certified) támogatják.

* Az AppSource piactérről származó Visio-vizualizáció, PowerApps-vizualizáció és GlobeMap-vizualizáció nem jelenik meg, ha a szervezet adattárának használatával lett üzembe helyezve.

## <a name="troubleshoot"></a>Hibaelhárítás

A hibaelhárítással kapcsolatban a [Power BI-vizualizációk hibáinak elhárítását](power-bi-custom-visuals-troubleshoot.md) ismertető cikkből tájékozódhat.

## <a name="faq"></a>Gyakori kérdések

További információt és válaszokat [a Power BI-vizualizációkkal kapcsolatos gyakori kérdések](power-bi-custom-visuals-faq.md#organizational-visuals) között talál.

További kérdései vannak? [Kérdezze meg a Power BI közösségét](https://community.powerbi.com/).