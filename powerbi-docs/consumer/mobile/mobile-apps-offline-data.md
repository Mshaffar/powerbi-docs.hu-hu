---
title: Adatok megtekintése offline módban a Power BI-mobilalkalmazásokban
description: 'Megtudhatja, milyen előnyökkel jár, ha a mobilböngésző helyett a mobilalkalmazásban tekinti meg a Power BI-t: akkor is hozzáférhet az adataihoz, ha épp nem csatlakozik hálózathoz.'
author: paulinbar
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-mobile
ms.topic: conceptual
ms.date: 12/09/2019
ms.author: painbar
ms.openlocfilehash: cfb5e4f1f75437db6235ece0d8661bab3f008649
ms.sourcegitcommit: bfc2baf862aade6873501566f13c744efdd146f3
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83148414"
---
# <a name="view-your-data-offline-in-the-power-bi-mobile-apps"></a>Adatok megtekintése offline módban a Power BI-mobilalkalmazásokban
Hatóköre:

| ![iPhone](./media/mobile-apps-offline-data/iphone-logo-50-px.png) | ![iPad](./media/mobile-apps-offline-data/ipad-logo-50-px.png) | ![Android rendszerű telefon](./media/mobile-apps-offline-data/android-phone-logo-50-px.png) | ![Android rendszerű táblagép](./media/mobile-apps-offline-data/android-tablet-logo-50-px.png) | ![Windows 10](./media/mobile-apps-offline-data/win-10-logo-50-px.png) |
|:--- |:--- |:--- |:--- |:--- |
| iPhone-ok |iPadek |Android rendszerű telefonok |Android-táblagépek |Windows 10 rendszerű eszközök |

>[!NOTE]
>A Power BI-mobilalkalmazás támogatása a **Windows 10 Mobile rendszerű telefonokhoz** 2021. március 16-án megszűnik. [További tudnivalók](https://go.microsoft.com/fwlink/?linkid=2121400)

Ha a mobilböngésző helyett a mobilalkalmazásban tekinti meg a Power BI-t, kihasználhatja annak előnyeit, hogy akkor is hozzáférhet az adataihoz, amikor éppen nem csatlakozik hálózathoz. 

![Nincs hálózat üzenet](./media/mobile-apps-offline-data/power-bi-iphone-no-network.png)

Alapértelmezés szerint a Power BI gyakran frissíti az adatokat, így munkába menet vagy utazás közben is bármikor naprakész válaszokat kaphat az üzletmenettel kapcsolatos kérdéseire.

## <a name="data-access-while-youre-offline"></a>Adathozzáférés kapcsolat nélküli üzemmódban
Ha kapcsolat nélküli üzemmódban van, elérheti és használhatja a korábban a mobilalkalmazásból megnyitott irányítópultokat.

A korábban a mobilalkalmazásból megnyitott Power BI-jelentésekhez is van csak olvasási jogosultságokat biztosító hozzáférése. Megtekintheti a teljes jelentést, de nem szűrhet, nem végezhet keresztszűrést, nem rendezheti, és nem használhat rajta szeletelőt.

## <a name="background-data-refresh"></a>Háttérben futó adatfrissítés
A háttérben futó frissítés frissíti a kedvenc irányítópultjait, valamint az utolsó két hétben megtekintett irányítópultokat és jelentéseket a Power BI szolgáltatás (nem az adatforrás) adataival. Ha Wi-Fi-hálózathoz csatlakozik, a háttérben futó frissítés 2 óránként frissíti az adatokat. Ha 3G-hálózatot használ, a Power BI 24 óránként frissíti a tartalmakat.

A háttérben futó frissítéseket ki is kapcsolhatja, például ha kerülni szeretné a hálózaton keresztüli adatforgalmat. Ellenőrizze a beállításokat az eszközén.

> [!NOTE]
> Ha a Power BI mobilalkalmazást egy iOS-eszközön használja, és a cége konfigurálta a Microsoft Intune MAM felügyeletet, a háttérben futó adatfrissítés ki van kapcsolva. A Power BI a weben futó Power BI szolgáltatásból frissíti az adatokat, amikor legközelebb belép az alkalmazásba.
> 
> További információt a [Power BI-mobilalkalmazások Microsoft Intune-nal történő konfigurálásával](../../admin/service-admin-mobile-intune.md) foglalkozó témakörben talál. 
> 
> 

## <a name="offline-indicators"></a>Kapcsolat nélküli állapot jelzése
A Power BI egyértelműen jelzi, amikor kapcsolat nélküli üzemmódba lép vagy kilép belőle, és jelzi a kapcsolat nélküli üzemmódban nem elérhető hiányzó irányítópultokat, jelentéseket és csempéket is.

## <a name="limitations"></a>Korlátozások
Amikor kapcsolat nélküli üzemmódban használja a Power BI-t a mobileszközén, a következő korlátokba ütközhet:

* A Power BI legfeljebb 250 MB adatot képes kapcsolat nélküli üzemmódban gyorsítótárazni.
* Néhány csempetípushoz aktív kiszolgálókapcsolat szükséges, tehát kapcsolat nélküli üzemmódban nem érhetők el. Ilyenek például a Bing térkép csempéi és az egyéni csempék.
* A Power BI-ban a teljes Excel-munkafüzetek nem érhetők el kapcsolat nélküli üzemmódban.
* A Reporting Services mobiljelentések és KPI-k megtekinthetők kapcsolat nélküli üzemmódban, ha csatlakoztatott állapotban egyszer már használta őket, de nem frissülnek a háttérben. Csak akkor frissülnek, amikor megnyitja őket.
* A Power BI mobilalkalmazásaiban nem jelennek meg a Power BI jelentéskészítő kiszolgálón mentett Power BI Desktop-fájlok (.pbix-fájlok). 
* A lapszámozott jelentések (RDL) nem érhetők el kapcsolat nélkül.

## <a name="next-steps"></a>További lépések
A visszajelzése segít eldönteni, hogy milyen fejlesztésekre koncentráljunk a jövőben, ezért kérjük, ne mulasszon el szavazni más szolgáltatásokra, amelyeket szívesen látna a Power BI-mobilalkalmazásokban. 

* [Power BI-alkalmazások mobileszközökre](mobile-apps-for-mobile-devices.md)
* @MSPowerBI követése Twitteren
* Vegyen részt [a Power BI-közösség](https://community.powerbi.com/) beszélgetéseiben
* [Mi az a Power BI?](../../fundamentals/power-bi-overview.md)