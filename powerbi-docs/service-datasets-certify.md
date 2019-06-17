---
title: Adathalmazok minősítése (előzetes verzió) – Power BI
description: Útmutató megbízható, kiemelkedő minőségű adathalmazok nagyvállalati felhasználóknak való felkínálásához.
author: maggiesMSFT
manager: kfile
ms.reviewer: chbraun
ms.service: powerbi
ms.subservice: powerbi-service
ms.topic: conceptual
ms.date: 05/31/2019
ms.author: maggies
LocalizationGroup: Share your work
ms.openlocfilehash: e790afee5b57b73a756ca3c1afd564b00e778186
ms.sourcegitcommit: 7c426a5209d4fdd1360fc3d0442d57991be1984d
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/03/2019
ms.locfileid: "66461327"
---
# <a name="certify-datasets-preview"></a>Adathalmazok minősítése (előzetes verzió)

Vállalata minősítheti azokat az adathalmazokat, amelyek a kritikus fontosságú információk hiteles forrásai. Ezek az adathalmazok kiemelt szerephez jutnak, amikor a jelentéskészítők megkezdik a jelentések létrehozását és megbízható adatokat keresnek. A minősítés szigorú válogatáson alapuló folyamat lehet, így csak a legértékesebb adathalmazok lesznek minősítve. A Power BI bérlői rendszergazdáinak új beállítás áll rendelkezésére, amellyel szigorúan szabályozhatják, hogy ki minősíthet adathalmazokat. A rendszergazdák így biztosíthatják, hogy az adathalmazok minősítése valóban megbízható és hiteles adathalmazokat eredményezzen, amelyeket az egész vállalatnál felhasználhatnak.

Lehetséges, hogy a Power BI-felhasználók jelenleg számos különböző adathalmazhoz férnek hozzá, ezért a vállalatoknak kell a megbízható, jó minőségű adathalmazokhoz irányítania őket. A Power BI két módot kínál az adathalmazok *támogatására*:

- **Meghirdetés**: Az adathalmaz-tulajdonosok meghirdethetik adathalmazaikat, amikor azok készen állnak a széles körű felhasználásra. Részleteket az [Adathalmaz meghirdetése](service-datasets-promote.md) című cikkben talál. 
- **Minősítés**: Az adathalmaz-tulajdonosok kérhetik a meghirdetett adathalmazok minősítését. Az **Adathalmaz-minősítés** bérlői rendszergazdai beállítás által meghatározott szűk felhasználói csoport dönti el, hogy mely adatbázisok lesznek minősítve.

## <a name="certify-a-dataset"></a>Adathalmaz minősítése

Bérlői rendszergazdája megadhat egy URL-címet a **Támogatás** beállítási lapján található **További információ** hivatkozáshoz.  A hivatkozás a minősítési eljárás dokumentációjára mutathat. Ha nem adják meg a **További információ** hivatkozás célját, akkor az alapértelmezés szerint erre a cikkre mutat.

![További információk az adathalmazok minősítéséről](media/service-datasets-certify-promote/power-bi-dataset-learn-more-certification.png)

Az adathalmazok minősítésére való jelölés óriási felelősséggel jár. A vizsgálati folyamat azzal kezdődik, hogy az adathalmaz létrehozója Önhöz fordul egy adott adathalmazzal kapcsolatban. Miután meggyőződik arról, hogy az adathalmaz eleget tesz a minősítés követelményeinek, megteheti az utolsó lépést.

1. Az adathalmaz tulajdonosának tagi jogosultságokat kell adnia ahhoz a munkaterülethez, ahol a jelentés elhelyezkedik.
1. Ha bérlői rendszergazdája adathalmazok minősítőjeként jelölte ki Önt, akkor elérhető lesz a **Minősített** lehetőség az adathalmaz **Beállításainak** **Támogatás** szakaszában. Válassza a **Minősített** lehetőséget.
1. Kattintson az **Alkalmaz** elemre.

Részletesebben is tájékozódhat arról, hogy a bérlői rendszergazdák hogyan [szabályozzák az adathalmazok használatát a munkaterületeken](service-datasets-admin-across-workspaces.md).

## <a name="next-steps"></a>Következő lépések

* További információ: [Adathalmazok használata több munkaterülettel](service-datasets-across-workspaces.md)
* Kérdése van? [Kérdezze meg a Power BI közösségét](http://community.powerbi.com/)