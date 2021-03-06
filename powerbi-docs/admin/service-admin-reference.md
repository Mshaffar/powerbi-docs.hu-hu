---
title: PowerShell-parancsmagok, REST API-k és a .NET SDK rendszergazdáknak
description: Ismerje meg a Power BI szkriptekkel és API-kkal való felügyeletének módjait.
author: kfollis
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: conceptual
ms.date: 09/09/2019
ms.author: kfollis
LocalizationGroup: Administration
ms.openlocfilehash: b4f4227a53a87cd831962bc5c944a569531b8232
ms.sourcegitcommit: bfc2baf862aade6873501566f13c744efdd146f3
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83136297"
---
# <a name="powershell-cmdlets-rest-apis-and-net-sdk-for-power-bi-administration"></a>PowerShell-parancsmagok, REST API-k és a .NET SDK a Power BI felügyeletéhez
A Power BI segítségével a rendszergazdák gyakori feladatokat végeztethetnek el PowerShell-parancsmagokkal. A Power BI emellett REST API-kkal is rendelkezik, valamint felügyeleti megoldások fejlesztésére is használható a .NET SDK-val. Ez a témakör parancsmagokat, valamint a hozzájuk tartozó SDK-módszert és REST API-végpontot ismerteti. További információ:

- PowerShell – [Letöltés](https://www.powershellgallery.com/packages/MicrosoftPowerBIMgmt/) és [dokumentáció](https://docs.microsoft.com/powershell/power-bi/overview?view=powerbi-ps)
- REST API – [dokumentáció](https://docs.microsoft.com/rest/api/power-bi/admin)
- .NET SDK – [Letöltés](https://www.nuget.org/packages/Microsoft.PowerBI.Api/)

> Az alábbi parancsmagokat a `-Scope Organization` hívhatja a bérlő kezeléséhez.

| **Parancsmag neve** | **Aliasnevek** | **SDK-módszer** | **REST API-végpont** | **Leírás** |
| --- | --- | --- | --- | --- |
| `Get-PowerBIDatasource` | N.A. | `Datasets_GetDataSourcesAsAdmin` | /v1.0/myorg/admin/datasets/{datasetkey}/datasources | Lekéri egy adott adatkészlet adatforrásait. |
| `Get-PowerBIDataset` | N.A. | `Datasets_GetDatasetsAsAdmin` | /v1.0/myorg/admin/datasets | Lekéri egy Power BI-bérlő összes adatkészletét. |
| `Get-PowerBIWorkspace` | `Get-PowerBIGroup` | `Groups_GetGroupsAsAdmin` | /v1.0/myorg/admin/groups | Lekéri egy Power BI-bérlő összes munkaterületét. |
| `Add-PowerBIWorkspaceUser` | `Add-PowerBIGroupUser` | `Groups_AddUserAsAdmin` | /v1.0/myorg/admin/groups/{groupId}/users | Tagként hozzáad egy felhasználót egy adott munkaterülethez. |
| `Remove-PowerBIWorkspaceUser` | `Remove-PowerBIGroupUser` | `Groups_DeleteUserAsAdmin` | /v1.0/myorg/admin/groups/{groupId}/users/{user} | Eltávolít egy felhasználót egy adott munkaterület tagjai közül. |
| `Restore-PowerBIWorkspace` |`Restore-PowerBIGroup` | `Groups_RestoreDeletedGroupAsAdmin` | /v1.0/myorg/admin/groups/{groupId}/restore | Visszaállít egy törölt munkaterületet. |
| `Set-PowerBIWorkspace` |`Set-PowerBIGroup` | `Groups_UpdateGroupAsAdmin` | /v1.0/myorg/admin/groups/{groupId} | Frissíti egy adott munkaterület tulajdonságait. |
| `Get-PowerBIDataset -WorkspaceId` | N.A. | `Groups_GetDatasetsAsAdmin` | /v1.0/myorg/admin/groups/{group\_id}/datasets | Lekéri egy adott munkaterület adatkészleteit. |
| `Get-PowerBIReport` | N.A. | `Reports_GetReportsAsAdmin` | /v1.0/myorg/admin/reports | Lekéri egy Power BI-bérlő összes jelentését. |
| `Get-PowerBIDashboard` | N.A. | `Dashboards_GetDashboardsAsAdmin` | /v1.0/myorg/admin/dashboards | Lekéri egy Power BI-bérlő összes irányítópultját. |
| `Get-PowerBIDashboard -WorkspaceId` | N.A. | `Groups_GetDashboardsAsAdmin` | /v1.0/myorg/admin/groups/{group\_id}/dashboards | Lekéri egy adott munkaterület irányítópultjait. |
| `Get-PowerBITile` | `Get-PowerBIDashboardTile` | `Dashboards_GetTilesAsAdmin` | /v1.0/myorg/admin/dashboards/{dashboard\_id}/tiles | Lekéri egy adott irányítópult csempéit. |
| `Get-PowerBIReport` | N.A. | `Groups_GetReportsAsAdmin` | /v1.0/myorg/admin/groups/{group\_id}/reports | Lekéri egy adott munkaterület jelentéseit. |
| `Get-PowerBIImport` | N.A. | `Imports_GetImportsAsAdmin` | /v1.0/myorg/admin/imports | Lekéri egy Power BI-bérlő összes importálását. |
| `Connect-PowerBIServiceAccount` | `Login-PowerBI` &  `Login-PowerBIServiceAccount` | N.A. | N.A. | Bejelentkezés a Power BI-ba és egy munkamenet elindítása. |
| `Disconnect-PowerBIServiceAccount` | `Logout-PowerBI` & `Logout-PowerBIServiceAccount` | N.A. | N.A. | Kijelentkezés a Power BI-ból és az aktuális munkamenet bezárása. |
| `Invoke-PowerBIRestMethod`| N.A. | N.A. | N.A. | Tetszőleges REST API-hívások küldése a Power BI-ba. |
| `Get-PowerBIAccessToken`| N.A. | N.A. | N.A. | A Power BI hozzáférési jogkivonatának beszerzése egy munkamenetben. |
| `Resolve-PowerBIError`| N.A. | N.A. | N.A. | Részletes hibaadatok lekérése sikertelen parancsmaghívások esetén. |
