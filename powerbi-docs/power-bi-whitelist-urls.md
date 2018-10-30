---
title: Power BI URL-címek
description: Ez a cikk ismerteti azokat a végpontokat, amelyeket az online Power BI szolgáltatást használó ügyfeleknek el kell tudniuk érni.
author: mgblythe
ms.author: mblythe
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.component: powerbi-service
ms.topic: conceptual
ms.date: 10/22/2018
ms.openlocfilehash: cc7b24d273f8e83854f7e316f0c761e710e48160
ms.sourcegitcommit: a764e4b9d06b50d9b6173d0fbb7555e3babe6351
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/22/2018
ms.locfileid: "49641965"
---
# <a name="power-bi-urls"></a>Power BI URL-címek

A Power BI SaaS (szolgáltatott szoftver) alkalmazás néven is ismert **online Power BI szolgáltatáshoz** internetkapcsolatra van szükség. Az online Power BI szolgáltatást használó ügyfeleknek el kell érniük az alábbi végpontokat.

A Power BI online szolgáltatás használatához hozzá kell férnie az alábbi táblázatokban **kötelezőként** megjelölt végpontokhoz, és a hivatkozott webhelyeken **kötelezőként** megjelölt végpontokhoz is, hogy csatlakozni tudjon. Ha egy külső webhelyre mutató hivatkozás egy adott bekezdésre mutat, akkor csak az abban a bekezdésben lévő végpontokat kell megvizsgálnia.

Bizonyos funkciók működése érdekében a **választhatóként** megjelölt végpontok is **szerepelhetnek az engedélyezési listán**.

Az online Power BI szolgáltatás csak a 443-as TCP-port megnyitását igényli a felsorolt végpontokhoz.

A helyettesítő karakterek (*) a gyökértartomány alatti összes szintet jelentik. Ha nincs elérhető információ, azt az N/A jelölés mutatja. A **Cél(ok)** oszlop teljes tartománynevek/tartományok listája, és olyan külső webhelyekre hivatkozik, amelyek további információkat tartalmaznak a végpontokról.

>[!Important]
>Az alábbi táblázatok információi nem vonatkoznak az **Egyesült államok kormányzati felhőszolgáltatására**, **a németországi felhőre** és a **kínai felhőre**.

## <a name="authentication"></a>Hitelesítés

A Power BI működése függ az Office 365 hitelesítés és identitás szakaszban feltüntetett végpontoktól. A Power BI használatához tudnia kell csatlakozni az alább hivatkozott webhelyen található végpontokhoz.

| Sor | Szerep | Cél(ok) | Port(ok) |
| --- | --- | --- | --- |
| 1 | **Kötelező:** Hitelesítés és identitás | Tekintse meg az [Office Online szolgáltatást és a közös URL-címeket](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online) bemutató Office 365-dokumentációt  | N.A. |

## <a name="general-site-usage"></a>Általános webhelyhasználat

A Power BI használatához tudnia kell csatlakozni az alábbi táblázatban és a hivatkozott webhelyeken megadott végpontokhoz.

| Sor | Szerep | Cél(ok) | Port(ok) |
| --- | --- | --- | --- |
| 1 | **Kötelező:** Háttérbeli API-k | *.analysis.windows.net | TCP 443 |
| 2 | **Kötelező:** Office 365-integráció | Tekintse meg az [Office Online szolgáltatást és a közös URL-címeket](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online) bemutató Office 365-dokumentációt | N.A. |
| 3 | **Kötelező:** Portál | app.powerbi.com | TCP 443 |
| 4 | **Kötelező:** Szolgáltatási telemetria | dc.services.visualstudio.com | TCP 443 |
| 5 | **Választható:** Tájékoztató üzenetek | dynmsg.modpim.com | TCP 443 |
| 6 | **Választható:** NPS felmérések | nps.onyx.azure.net | TCP 443 |
| | | |

## <a name="administration"></a>Felügyelet

Ahhoz, hogy rendszergazdai funkciókat végezzen el a Power BI-ban, tudnia kell csatlakozni az alább hivatkozott webhelyeken megadott végpontokhoz.

| Sor | Szerep | Cél(ok) | Port(ok) |
| --- | --- | --- | --- |
| 1 | **Kötelező:** A felhasználók kezeléséhez és auditnaplók megtekintéséhez | Tekintse meg az [Office Online szolgáltatást és a közös URL-címeket](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online) bemutató Office 365-dokumentációt | N.A. |
| | | |

## <a name="getting-data"></a>Adatok beolvasása

Ahhoz, hogy adatokat kérhessen le bizonyos adatforrásokból, például a OneDrive-ból, tudnia kell csatlakozni az alábbi táblázatban megadott végpontokhoz. Előfordulhat, hogy további internetes tartományok és URL-címek elérése szükséges a vállalatnál használt egyes adatforrásokhoz.

| Sor | Szerep | Cél(ok) | Port(ok) |
| --- | --- | --- | --- |
| 1 | **Kötelező:** AppSource (belső vagy külső alkalmazások a Power BI-ban) | appsource.microsoft.com </br> *.s-microsoft.com  | TCP 443 |
| 2 | **Kötelező:** Bejelentkezés és adatok lekérése tartalomcsomagokhoz | *.github.com  | TCP 443 |
| 3 | **Választható:** Fájlok importálása személyes OneDrive-ból | Lásd: [A OneDrive webhelyhez megkövetelt URL-címek és portok](https://docs.microsoft.com/en-us/onedrive/required-urls-and-ports) | N.A. |
| 4 | **Választható:** Power BI 60 másodperc alatt – bemutató videó | *.doubleclick.net </br> *.ggpht.com </br> *.google.com </br> *.googlevideo.com </br> *.youtube.com </br> *.ytimg.com </br> fonts.gstatic.com | TCP 443 |
| 5 | **Választható:** PubNub streamelési adatforrások | Lásd: [PubNub dokumentáció](https://support.pubnub.com/support/solutions/articles/14000043522) | N.A. |
| | | |

## <a name="dashboard-and-report-integration"></a>Irányítópultok és jelentések integrálása

A Power BI-nak szüksége van bizonyos végpontokra az irányítópultok és jelentések támogatásához. Tudnia kell csatlakozni az alábbi táblázatban és a hivatkozott webhelyeken megadott végpontokhoz.

| Sor | Szerep | Cél(ok) | Port(ok) |
| --- | --- | --- | --- |
| 1 | **Kötelező:** Excel-integráció | Tekintse meg az [Office Online szolgáltatást és a közös URL-címeket](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online) bemutató Office 365-dokumentációt | N.A. |
| | | |

## <a name="custom-visuals"></a>Egyéni vizualizációk

A Power BI-nak szüksége van bizonyos végpontokra az egyéni vizualizációkhoz való hozzáféréshez és azok megjelenítéséhez. Tudnia kell csatlakozni az alábbi táblázatban és a hivatkozott webhelyeken megadott végpontokhoz.

| Sor | Szerep | Cél(ok) | Port(ok) |
| --- | --- | --- | --- |
| 1 | **Kötelező:** Egyéni vizualizáció importálása a Marketplace felületéről vagy egy fájlból | *.azureedge.net </br> *.blob.core.windows.net </br> store.office.com | TCP 443 |
| 2 | **Választható:** Bing Térképek | bing.com </br> platform.bing.com </br> *.dynamic.tiles.virtualearth.net </br> *.virtualearth.net | TCP 443 |
| 3 | **Választható:** PowerApps | Lásd a [Szükséges szolgáltatások szakaszt](https://docs.microsoft.com/powerapps/maker/canvas-apps/limits-and-config#required-services) a PowerApps rendszerkövetelményeinek webhelyén | N.A. |
| 4 | **Választható:** Visio | Tekintse meg az [Office Online szolgáltatást és a közös URL-címeket](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online), valamint a [SharePoint Online szolgáltatást és a OneDrive Vállalati verziót](https://docs.microsoft.com/en-us/office365/enterprise/urls-and-ip-address-ranges#sharepoint-online-and-onedrive-for-business) bemutató Office 365-dokumentációt | N.A. |
| | | |

## <a name="related-external-sites"></a>Kapcsolódó külső webhelyek

A Power BI más webhelyekre is hivatkozik. Ezek közé tartoznak a dokumentációkat tartalmazó, a támogatást nyújtó, az új funkciókéréseket kezelő stb. webhelyek. Ezek a webhelyek nem befolyásolják a Power BI működését, ezért tetszés szerint felvehetők az engedélyezési listára.

| Sor | Szerep | Cél(ok) | Port(ok) |
| --- | --- | --- | --- |
| 1 | **Választható:** Közösségi webhely | community.powerbi.com </br> oxcrx34285.i.lithium.com | TCP 443 |
| 2 | **Választható:** Dokumentációs webhely | docs.microsoft.com </br> img-prod-cms-rt-microsoft-com.akamaized.net </br> statics-uhf-eas.akamaized.net </br> cdnssl.clicktale.neting-district.clicktale.net | TCP 443 |
| 3 | **Választható:** Letöltési webhely (Power BI Desktophoz stb.) | download.microsoft.com | TCP 443 |
| 4 | **Választható:** Külső átirányítások | aka.ms </br> go.microsoft.com | TCP 443 |
| 5 | **Választható:** Ötletek visszajelzési webhelye| ideas.powerbi.com </br> powerbi.uservoice.com | TCP 443 |
| 6 | **Választható:** A Power BI webhelye – kezdőlap, további információs hivatkozások, támogatási webhely, letöltési hivatkozások, partnerek bemutatása stb. | powerbi.microsoft.com | TCP 443 |
| 7 | **Választható:** Power BI Fejlesztői központ | dev.powerbi.com | TCP 443 |
| 8 | **Választható:** Támogatási webhely | support.powerbi.com </br> s3.amazonaws.com </br> *.olark.com </br> logx.optimizely.com </br> mscom.demdex.net </br> tags.tiqcdn.com | TCP 443 |
| | | |