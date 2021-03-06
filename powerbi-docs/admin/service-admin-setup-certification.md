---
title: Adathalmaz- és adatfolyam-minősítés beállítása (előzetes verzió)
description: Útmutató a vállalati adathalmaz- és adatfolyam-minősítési eljárás kialakításához.
author: paulinbar
ms.service: powerbi
ms.subservice: powerbi-service
ms.topic: conceptual
ms.date: 03/22/2020
ms.author: painbar
LocalizationGroup: Share your work
ms.openlocfilehash: ae47c6ea0c7b9bf629f55701ba4242a195dc164d
ms.sourcegitcommit: 0e9e211082eca7fd939803e0cd9c6b114af2f90a
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83274397"
---
# <a name="set-up-dataset-and-dataflow-certification-preview"></a>Adathalmaz- és adatfolyam-minősítés beállítása (előzetes verzió)

Vállalata minősítheti azokat az adathalmazokat és adatfolyamokat, amelyek a kritikus fontosságú információk hiteles forrásai.

A Power BI-bérlő rendszergazdájaként az Ön feladata a vállalati minősítési eljárás kialakítása. Ez a következőkkel jár:
* Minősítés engedélyezése a bérlőben.
* Az adathalmazok és adatfolyamok minősítésére jogosult csoportok és felhasználók listájának meghatározása.
* Az adathalmazok esetében a vállalat adathalmaz-minősítési szabályzatára mutató URL-cím megadása, ha van ilyen.

Az adathalmazok és adatfolyamok minősítése az adathalmazok és adatfolyamok *ellenőrzésének* része. Erről az [adathalmazok ellenőrzését](../connect-data/service-datasets-promote.md) és az [adatfolyamok ellenőrzését](../transform-model/service-dataflows-promote-certify.md) ismertető cikkekben található további információ.


## <a name="set-up-certification"></a>A minősítés beállítása

1. Nyissa meg a Bérlői beállításokat a felügyeleti portálon.
1. Az Exportálási és megosztási beállítások szakaszban bontsa ki a Minősítés szakaszt.

   ![Adatkészlet és adatfolyam-tanúsítvány beállítása](media/service-admin-setup-certification/service-admin-certification-setup-dialog.png)

1. Állítsa a kapcsolót az **Engedélyezve** állásba.
1. Ha a vállalat rendelkezik közzétett minősítési szabályzattal, annak URL-címét is itt adhatja meg az adathalmazok minősítéséhez. Ez lesz az **adatfolyam-ellenőrzési beállítások párbeszédpanel** [További tudnivalók](../connect-data/service-datasets-promote.md#request-dataset-certification) hivatkozása 
1. Adja meg az adathalmazok és adatfolyamok minősítésére jogosult felhasználók vagy csoportok listáját. Ezek a feljogosított minősítők használhatják majd az [adathalmaz](../connect-data/service-datasets-promote.md#request-dataset-certification) vagy [adatfolyam](../transform-model/service-dataflows-promote-certify.md#certify-a-dataflow) ellenőrzési beállításainak párbeszédpaneljén, a minősítési szakaszban található Minősítés gombot.
1. Kattintson az **Alkalmaz** gombra.

## <a name="next-steps"></a>További lépések
* [Adathalmazok meghirdetése](../connect-data/service-datasets-promote.md)
* [Adathalmazok minősítése](../connect-data/service-datasets-certify.md)
* [Adatfolyamok meghirdetése](../transform-model/service-dataflows-promote-certify.md#promote-a-dataflow)
* [Adatfolyamok minősítése](../transform-model/service-dataflows-promote-certify.md#certify-a-dataflow)
* Kérdései vannak? [Kérdezze meg a Power BI-közösséget](https://community.powerbi.com/)
