---
title: A Power BI-vizualizációk speciális szerkesztési módja
description: Ez a cikk bemutatja, hogyan adhat meg speciális felületi vezérlőket a Power BI-vizualizációkban.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: conceptual
ms.date: 06/18/2019
ms.openlocfilehash: 97242883fe90c8f5e115818a24e4bb1c49f69b77
ms.sourcegitcommit: 7aa0136f93f88516f97ddd8031ccac5d07863b92
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/05/2020
ms.locfileid: "79380558"
---
# <a name="advanced-edit-mode-in-power-bi-visuals"></a>A Power BI-vizualizációk speciális szerkesztési módja

Ha speciális felületi vezérlőkre van szüksége egy Power BI-vizualizációban, használja a Speciális szerkesztési módot. A jelentés szerkesztési módjában a **Szerkesztés** gombbal **Speciális** értékre állíthatja a szerkesztési módot. A vizualizáció az `EditMode` jelzővel állapítja meg, hogy megjelenítse-e a felületi vezérlőt.

A vizualizáció alapértelmezés szerint nem támogatja a Speciális szerkesztési módot. Eltérő viselkedés igénye esetén ezt explicit módon fel kell tüntetni a vizualizáció *capabilities.json* fájljában a `advancedEditModeSupport` tulajdonság beállításával.

Lehetséges értékek:

- `0` – NotSupported

- `1` – SupportedNoAction

- `2` – SupportedInFocus

## <a name="enter-advanced-edit-mode"></a>A Speciális szerkesztési mód megnyitása

A **Szerkesztés** gomb a következő esetekben jelenik meg:

* Az `advancedEditModeSupport` tulajdonság a *capabilities.json* fájlban `SupportedNoAction` vagy `SupportedInFocus` értékre van állítva.

* A vizualizáció jelentésszerkesztési módban van megnyitva.

Ha az `advancedEditModeSupport` tulajdonság hiányzik a *capabilities.json* fájlból, vagy `NotSupported` értékre van állítva, a **Szerkesztés** gomb eltűnik.

![A szerkesztési mód megnyitása](media/advanced-edit-mode/edit-mode.png)

Amikor a **Szerkesztés** lehetőséget választja, a vizualizáció frissítési hívást kap, `Advanced` értékre állított EditMode beállítással. A *capabilities.json* fájlban beállított értékek alapján a következő műveletek mennek végbe:

* `SupportedNoAction`: Nincs szükség további lépésre a gazdagéptől.
* `SupportedInFocus`: A gazdagép fókusz módban jeleníti meg a vizualizációt.

## <a name="exit-advanced-edit-mode"></a>Kilépés a Speciális szerkesztési módból

A **Vissza a jelentéshez** gomb a következő esetekben jelenik meg:

* Az `advancedEditModeSupport` tulajdonság a *capabilities.json* fájlban `SupportedInFocus` értékre van állítva.
