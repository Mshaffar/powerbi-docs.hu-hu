---
title: Adatforrások kezelése – Importálás/ütemezett frissítés
description: A helyszíni adatátjáró és az átjáróhoz tartozó adatforrások kezelésének módja. Ez a cikk az importálás/ütemezett frissítés szolgáltatással használható adatforrásokra vonatkozik.
author: arthiriyer
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 07/15/2019
ms.author: arthii
LocalizationGroup: Gateways
ms.openlocfilehash: c77194c2599e518481276024ae1afc2b00524226
ms.sourcegitcommit: 0e9e211082eca7fd939803e0cd9c6b114af2f90a
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83320676"
---
# <a name="manage-your-data-source---importscheduled-refresh"></a>Adatforrások kezelése – Importálás/ütemezett frissítés

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

Miután [telepítette a helyszíni adatátjárót](/data-integration/gateway/service-gateway-install), [fel kell vennie az átjáróval használható adatforrásokat](service-gateway-data-sources.md#add-a-data-source). Ez a cikk bemutatja, hogyan lehet használni az ütemezett frissítéshez használt átjárókat és az adatforrásokat a DirectQuery vagy az élő kapcsolatok helyett.

## <a name="add-a-data-source"></a>Adatforrás hozzáadása

Az [Adatforrás hozzáadása](service-gateway-data-sources.md#add-a-data-source) című témakörben további információt talál adatforrások hozzáadásáról. Válassza ki az adatforrás típusát.

Az összes felsorolt adatforrástípus használható ütemezett frissítéshez a helyszíni átjáróval. Az Analysis Services, az SQL Server és az SAP HANA használható ütemezett frissítéshez vagy DirectQuery/élő kapcsolatokhoz is.

![Az adatforrás kiválasztása](media/service-gateway-enterprise-manage-scheduled-refresh/datasourcesettings2.png)

Ezután kell megadni az információkat az adatforráshoz. Ebbe beletartoznak a forrásra vonatkozó információk és az adatforrás eléréséhez használt hitelesítő adatok.

> [!NOTE]
> Az adatforrás felé irányuló összes lekérdezés ezen hitelesítő adatok segítségével fut. A [Titkosított hitelesítő adatok tárolása a felhőben](service-gateway-data-sources.md#store-encrypted-credentials-in-the-cloud) című témakörben további információt talál a hitelesítő adatok tárolásáról.

![Adatforrás-beállítások kitöltése](media/service-gateway-enterprise-manage-scheduled-refresh/datasourcesettings3-oracle.png)

Az [Elérhető adatforrástípusok listájában](service-gateway-data-sources.md#list-of-available-data-source-types) megtalálja azokat az adatforrástípusokat, amelyek használhatók az ütemezett frissítéssel.

Miután mindent kitöltött, válassza a **Hozzáadás** lehetőséget. Mostantól használhatja ezt az adatforrást ütemezett frissítéshez a helyszíni adataival. Ha sikerrel járt, megjelenik a *Sikeres csatlakozás* üzenet.

![A kapcsolat állapotának megjelenítése](media/service-gateway-enterprise-manage-scheduled-refresh/datasourcesettings4.png)

### <a name="advanced-settings"></a>Speciális beállítások

Ha szeretné, konfigurálhatja az adatforrás adatvédelmi szintjét is. Ez a beállítás vezérli, hogy hogyan lesznek egyesítve az adatok. Ez csak ütemezett frissítéshez használható. Az adatforrás adatvédelmi szintjeiről az [Adatvédelmi szintek (Power Query)](https://support.office.com/article/Privacy-levels-Power-Query-CC3EDE4D-359E-4B28-BC72-9BEE7900B540) című témakörben olvashat részletesebben.

![Az adatvédelem szintjének beállítása](media/service-gateway-enterprise-manage-scheduled-refresh/datasourcesettings9.png)

## <a name="use-the-data-source-for-scheduled-refresh"></a>Az adatforrás használata ütemezett frissítéshez

Miután létrehozta az adatforrást, használhatja azt DirectQuery-kapcsolatokkal vagy ütemezett frissítéssel is.

> [!NOTE]
> A kiszolgáló és az adatbázis nevének egyeznie kell a Power BI Desktopban és az adatforrásban a helyszíni adatátjárón belül.

Az adatkészlet és az adatforrás közötti kapcsolat az átjárón belül a kiszolgáló nevén és az adatbázis nevén alapul. A neveknek egyezniük kell. Ha például egy IP-címet ad meg a kiszolgáló nevének, a Power BI Desktopban azt az IP-címet kell használnia az adatforráshoz az átjáró konfigurációján belül. Ha a Power BI Desktopban a *KISZOLGÁLÓ\PÉLDÁNY* formát használta, az átjáró konfigurációjában is ezt kell megadnia az adatforráshoz.

Ha szerepel az átjárón belül konfigurált adatforrás **Felhasználók** lapján, és a kiszolgáló és az adatbázis neve egyezik, az átjáró megjelenik lehetőségként az ütemezett frissítésnél.

![A felhasználók megjelenítése](media/service-gateway-enterprise-manage-scheduled-refresh/powerbi-gateway-enterprise-schedule-refresh.png)

> [!WARNING]
> Ha az adatkészlet több adatforrást tartalmaz, az egyes adatforrásokat hozzá kell adni az átjárón belül. Ha egy vagy több adatforrást nem ad hozzá az átjáróhoz, az átjáró nem lesz elérhető ütemezett frissítésre.

## <a name="limitations"></a>Korlátozások

Az OAuth nem támogatott hitelesítési séma a helyszíni adatátjáróval. Nem vehet fel olyan adatforrásokat, amelyekhez OAuth szükséges. Ha az adatkészlet egy adatforrásához OAuth szükséges, nem fogja tudni ütemezett frissítéshez használni az átjárót.

## <a name="next-steps"></a>További lépések

* [A helyszíni adatátjáró hibaelhárítása](/data-integration/gateway/service-gateway-tshoot)
* [Átjárók hibaelhárítása – Power BI](service-gateway-onprem-tshoot.md)

Több kérdése van? Kérdezze meg [a Power BI közösségét](https://community.powerbi.com/).
