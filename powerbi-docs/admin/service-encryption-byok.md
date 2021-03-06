---
title: Saját titkosítási kulcsok használata a Power BI-hoz
description: Útmutató saját titkosítási kulcsok Power BI Premiumban való használatához.
author: davidiseminger
ms.author: davidi
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: conceptual
ms.date: 02/20/2020
LocalizationGroup: Premium
ms.openlocfilehash: c3d95e6cc10f01a09fe93d31012652e741eb077c
ms.sourcegitcommit: 0e9e211082eca7fd939803e0cd9c6b114af2f90a
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83274420"
---
# <a name="bring-your-own-encryption-keys-for-power-bi"></a>Saját titkosítási kulcsok használata a Power BI-hoz

A Power BI az _inaktív_ és _feldolgozás alatt álló_ adatokat titkosítja. A Power BI alapértelmezés szerint a Microsoft által felügyelt kulcsokkal titkosítja az adatokat. A Power BI Premiumban saját kulcsait is használhatja az adathalmazba importált inaktív adatokhoz (További információ: [Adatforrásokkal kapcsolatos és tárolási szempontok](#data-source-and-storage-considerations)). Ezt nevezik _Bring Your Own Key_ (BYOK) megközelítésnek.

## <a name="why-use-byok"></a>Miért érdemes BYOK-t használni?

BYOK használatával egyszerűbben eleget tehet a kulcsokkal kapcsolatban a felhőszolgáltatóval (ebben az esetben a Microsofttal) kötött megállapodás követelményeinek. BYOK használatával Ön adhatja meg és szabályozhatja alkalmazásszinten a Power BI-beli inaktív adatok titkosítási kulcsait. Ennek eredményeként ön szabályozza, és vissza is vonhatja vállalati kulcsait, ha a szolgáltatás elhagyása mellett dönt. Az adatok kulcsok visszavonása után 30 percen belül olvashatatlanná válnak a szolgáltatás számára.

## <a name="data-source-and-storage-considerations"></a>Adatforrásokkal kapcsolatos és tárolási szempontok

BYOK használatához adatokat kell feltöltenie a Power BI szolgáltatásba egy Power BI Desktop- (PBIX-) fájlból. Nem használhat BYOK-t a következő helyzetekben:

- Élő Analysis Services-kapcsolat
- Excel-munkafüzetek (ha az adatok nincsenek a Power BI Desktopba importálva)
- [Leküldéses adathalmazok](/rest/api/power-bi/pushdatasets)
- [Streamelési adathalmazok](../connect-data/service-real-time-streaming.md#set-up-your-real-time-streaming-dataset-in-power-bi)
- [Nagyméretű modellek](service-premium-large-models.md)

A saját kulcsok használata (BYOK) csak adathalmazokra vonatkozik. A leküldéses adathalmazok, valamint a felhasználók által a szolgáltatásba feltöltött Excel-fájlok és CSV-fájlok nem a saját kulcsával lesznek titkosítva. A munkaterületein tárolt összetevőket az alábbi PowerShell-paranccsal azonosíthatja:

```PS C:\> Get-PowerBIWorkspace -Scope Organization -Include All```

> [!NOTE]
> Ehhez a parancsmaghoz a Power BI v1.0.840 felügyeleti modulja szükséges. A futtatott verziót a Get-InstalledModule -Name MicrosoftPowerBIMgmt parancs futtatásával állapíthatja meg. A legújabb verzió telepítéséhez futtassa az Install-Module -Name MicrosoftPowerBIMgmt parancsot. A Power BI-parancsmagról és annak paramétereiről a [Power BI PowerShell-parancsmag modul](https://docs.microsoft.com/powershell/power-bi/overview) című cikkből juthat információhoz.

## <a name="configure-azure-key-vault"></a>Az Azure Key Vault konfigurálása

Ebben a szakaszban megtudhatja, hogyan konfigurálhatja az Azure Key Vaultot, amely egy titkos kódok, köztük titkosítási kulcsok biztonságos tárolására és elérésére szolgáló eszköz. Titkosítási kulcsok tárolásához használhat meglévő kulcstartót, vagy újat is létrehozhat, amelyet csak a Power BI-hoz használ.

Az ebben a szakaszban leírtak feltételezik az Azure Key Vault alapszintű ismeretét. További információ: [Mi az Azure Key Vault?](/azure/key-vault/key-vault-whatis). Kulcstartóját az alábbi módon konfigurálhatja:

1. Vegye fel a Power BI szolgáltatást szolgáltatásnévként a kulcstartóhoz, Wrap és Unwrap engedélyekkel.

1. Hozzon létre 4096 bites RSA-kulcsot (vagy használjon ilyen típusú meglévő kulcsot) Wrap és Unwrap engedélyekkel.

    > [!IMPORTANT]
    > A Power BI BYOK csak 4096 bites RSA-kulcsokat támogat.

1. Ajánlott: Ellenőrizze, hogy a kulcstárolóhoz engedélyezve van-e a _Helyreállítható törlés_ beállítás.

### <a name="add-the-service-principal"></a>A szolgáltatásnév hozzáadása

1. Az Azure Portalon a kulcstartóban a **Hozzáférési szabályzatok** alatt válassza az **Új hozzáadása** lehetőséget.

1. A **Rendszerbiztonsági tag kijelölése** alatt keresse meg és válassza ki a Microsoft.Azure.AnalysisServices elemet.

    > [!NOTE]
    > Ha nem találja a „Microsoft.Azure.AnalysisServices” elemet, az valószínűleg azért van, mert az Azure Key Vaulthoz társított Azure-előfizetéséhez nem rendeltek Power BI-erőforrást. Próbáljon meg a következő sztringre keresni: 00000009-0000-0000-c000-000000000000.

1. A **Kulcsengedélyek** területen jelölje ki a **Kulcs kicsomagolása** és a **Kulcs kicsomagolása** engedélyt.

    ![PBIX-fájl összetevői](media/service-encryption-byok/service-principal.png)

1. Válassza az **OK**, majd a **Mentés** lehetőséget.

> [!NOTE]
> Ha a jövőben meg szeretné vonni a Power BI-nak az adatokhoz való hozzáférését, távolítsa el az adott szolgáltatásnév hozzáférési jogosultságait az Azure Key Vaultból.

### <a name="create-an-rsa-key"></a>RSA-kulcs létrehozása

1. Kulcstartójában a **Kulcsok** alatt válassza a **Generálás/Importálás** lehetőséget.

1. Válassza az RSA **Kulcstípust** és a 4096 **RSA-kulcsméretet**.

    ![PBIX-fájl összetevői](media/service-encryption-byok/create-rsa-key.png)

1. Válassza a **Létrehozás** lehetőséget.

1. A **Kulcsok** alatt jelölje ki a létrehozott kulcsot.

1. Válassza a kulcs **Aktuális verziójának** GUID-azonosítóját.

1. Ellenőrizze, hogy a **Kulcs becsomagolása** és a **Kulcs kicsomagolása** is ki van-e jelölve. Másolja ki a BYOK Power BI-beli engedélyezéséhez szükséges **Kulcsazonosítót**.

    ![PBIX-fájl összetevői](media/service-encryption-byok/key-properties.png)

### <a name="soft-delete-option"></a>Helyreállítható törlés beállítás

A kulcstartóhoz a kulcs – vagy a kulcstartó – véletlen törléséből eredő adatvesztés elkerülése érdekében ajánlott engedélyezni a [Helyreállítható törlés](/azure/key-vault/key-vault-ovw-soft-delete) beállítást. A kulcstartóhoz [a PowerShell használatával kell engedélyeznie a „Helyreállítható törlés” tulajdonságot](/azure/key-vault/key-vault-soft-delete-powershell), mert ez a beállítás egyelőre nem érhető el az Azure Portalon.

Az Azure Key Vault megfelelő konfigurálása után már engedélyezheti bérlőjében a BYOK-t.

## <a name="enable-byok-on-your-tenant"></a>BYOK engedélyezése a bérlőben

BYOK úgy engedélyezhető a bérlői szinten a [PowerShell](https://www.powershellgallery.com/packages/MicrosoftPowerBIMgmt.Admin) használatával, hogy először bevezeti Power BI-bérlőjében a létrehozott és az Azure Key Vaultban tárolt titkosítási kulcsait. Ez után prémium szintű kapacitásonként kioszthatja ezeket a titkosítási kulcsokat a kapacitásbeli tartalom titkosításához.

### <a name="important-considerations"></a>Fontos szempontok

BYOK engedélyezése előtt vegye figyelembe a következőket:

- Jelenleg nem tilthatja le a BYOK-ot, miután engedélyezte azt. Az `Add-PowerBIEncryptionKey` parancshoz megadott paraméterektől függően szabályozni tudja, hogy hogyan legyen használva a BYOK egy vagy több kapacitáshoz. A kulcsok bérlőbeli bevezetését azonban nem vonhatja vissza. További információ: [BYOK engedélyezése](#enable-byok).

- Egy BYOK-t használó munkaterületet nem helyezhet át _közvetlenül_ megosztott kapacitásba egy Power BI Premiumbeli dedikált kapacitásból. A munkaterületet először olyan dedikált kapacitásba kell áthelyeznie, amelyen nincs engedélyezve BYOK.

- Ha egy BYOK-t használó munkaterületet helyez át egy dedikált kapacitásból egy megosztottba a Power BI Premiumban, a jelentések és adatkészletek nem lesznek elérhetők, mivel ezek a kulccsal vannak titkosítva. Ennek elkerülése érdekében a munkaterületet először olyan dedikált kapacitásba kell áthelyeznie, amelyen nincs engedélyezve BYOK.

### <a name="enable-byok"></a>BYOK engedélyezése

BYOK engedélyezéséhez bérlői rendszergazdának kell lennie a Power BI szolgáltatásban, a `Connect-PowerBIServiceAccount` parancsmag használatával bejelentkezve. Ez után az [`Add-PowerBIEncryptionKey`](/powershell/module/microsoftpowerbimgmt.admin/Add-PowerBIEncryptionKey) paranccsal engedélyezheti a BYOK-ot, az alábbi példán bemutatott módon:

```powershell
Add-PowerBIEncryptionKey -Name'Contoso Sales' -KeyVaultKeyUri'https://contoso-vault2.vault.azure.net/keys/ContosoKeyVault/b2ab4ba1c7b341eea5ecaaa2wb54c4d2'
```

Több kulcs hozzáadásához futtassa az `Add-PowerBIEncryptionKey` parancsmagot különböző értékeket megadva a -`-Name` és a `-KeyVaultKeyUri` számára. 

A parancsmag két kapcsolóparamétert fogad el, amelyek a jelenlegi és jövőbeli kapacitások titkosítását befolyásolják. Alapértelmezés szerint a kapcsolók egyike sincs beállítva:

- `-Activate`: Azt jelzi, hogy a rendszer ezt a kulcsot fogja használni a bérlőben meglévő minden olyan kapacitáshoz, amely még nem lett titkosítva.

- `-Default`: Azt jelzi, hogy ez a kulcs mostantól az egész bérlőben alapértelmezett. Új kapacitás létrehozásakor a kapacitás örökli ezt a kulcsot.

> [!IMPORTANT]
> A `-Default` kapcsoló megadása esetén a bérlőben ettől kezdve létrehozott összes kapacitás a megadott kulccsal (vagy egy frissített alapértelmezett kulccsal) lesz titkosítva. Az alapértelmezett művelet nem vonható vissza, így többé nem tud olyan prémium szintű kapacitást létrehozni a bérlőben, amely nem használ BYOK-t.

Miután engedélyezte a BYOK-t a bérlőben, állítsa be a titkosítási kulcsot egy vagy több Power BI-kapacitáshoz:

1. A következő lépéshez szükséges kapacitásazonosítót a [`Get-PowerBICapacity`](/powershell/module/microsoftpowerbimgmt.capacities/get-powerbicapacity) paranccsal kaphatja meg.

    ```powershell
    Get-PowerBICapacity -Scope Individual
    ```

    A parancsmag az alábbihoz hasonló kimenetet eredményez:

    ```
    Id              : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    DisplayName     : Test Capacity
    Admins          : adam@sometestdomain.com
    Sku             : P1
    State           : Active
    UserAccessRight : Admin
    Region          : North Central US
    ```

1. Állítsa be a titkosítási kulcsot a [`Set-PowerBICapacityEncryptionKey`](/powershell/module/microsoftpowerbimgmt.admin/set-powerbicapacityencryptionkey) paranccsal:

    ```powershell
    Set-PowerBICapacityEncryptionKey-CapacityId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -KeyName 'Contoso Sales'
    ```

Azt szabályozni tudja, hogy hogyan használja a BYOK-ot a bérlőben. Egyetlen kapacitás titkosításához például hívja meg az `Add-PowerBIEncryptionKey` parancsot az `-Activate` vagy a `-Default` kapcsoló nélkül. Ez után hívja meg a `Set-PowerBICapacityEncryptionKey` parancsot arra a kapacitásra, amelyen engedélyezni kívánja a BYOK-ot.

## <a name="manage-byok"></a>BYOK felügyelete

A Power BI további parancsmagokat kínál a BYOK egyszerű bérlőbeli felügyeletéhez:

- A [`Get-PowerBICapacity`](/powershell/module/microsoftpowerbimgmt.capacities/get-powerbicapacity) használatával lekérheti a kapacitás által jelenleg használt kulcsot:

    ```powershell
    Get-PowerBICapacity -Scope Organization -ShowEncryptionKey
    ```

- A [`Get-PowerBIEncryptionKey`](/powershell/module/microsoftpowerbimgmt.admin/get-powerbiencryptionkey) használatával lekérheti a bérlő által jelenleg használt kulcsot:

    ```powershell
    Get-PowerBIEncryptionKey
    ```

- A [`Get-PowerBIWorkspaceEncryptionStatus`](/powershell/module/microsoftpowerbimgmt.admin/get-powerbiworkspaceencryptionstatus) használatával megállapíthatja, hogy a munkaterületen lévő adathalmazok titkosítva vannak-e, és hogy titkosítási állapotuk szinkronban van-e a munkaterülettel:

    ```powershell
    Get-PowerBIWorkspaceEncryptionStatus -Name'Contoso Sales'
    ```

    Lényeges, hogy a titkosítás a kapacitás szintjén van engedélyezve, de a titkosítás állapotát az adathalmaz szintjén kapja meg a megadott munkaterülethez.

- A titkosításhoz használt kulcs verziója a [`Switch-PowerBIEncryptionKey`](/powershell/module/microsoftpowerbimgmt.admin/switch-powerbiencryptionkey) paranccsal váltható (vagy _forgatható_). A parancsmag csak a `-Name` kulcs `-KeyVaultKeyUri` értékét módosítja:

    ```powershell
    Switch-PowerBIEncryptionKey -Name'Contoso Sales' -KeyVaultKeyUri'https://contoso-vault2.vault.azure.net/keys/ContosoKeyVault/b2ab4ba1c7b341eea5ecaaa2wb54c4d2'
    ```



## <a name="next-steps"></a>Következő lépések

* [Power BI PowerShell-parancsmag modul](https://docs.microsoft.com/powershell/power-bi/overview) 

* [A munka megosztásának módjai a Power BI-ban](../collaborate-share/service-how-to-collaborate-distribute-dashboards-reports.md)

* [Jelentés szűrése lekérdezésisztring-paraméterek URL-címben való használatával](../collaborate-share/service-url-filters.md)

* [Beágyazás jelentéskijelzővel a SharePoint Online-ban](../collaborate-share/service-embed-report-spo.md)

* [Webes közzététel a Power BI-ból](../collaborate-share/service-publish-to-web.md)

