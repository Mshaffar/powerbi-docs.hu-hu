---
title: Power BI felügyeleti portál
description: A felügyeleti portál a Power BI bérlői felügyeletét teszi lehetővé a munkahelyen. Olyan lehetőségeket kínál, mint például a használati metrikák, hozzáférés a Microsoft 365 Felügyeleti központjához, valamint a beállítások.
author: kfollis
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: conceptual
ms.date: 04/27/2020
ms.author: kfollis
ms.custom: seodec18
LocalizationGroup: Administration
ms.openlocfilehash: b08184e92730bd3a42a91424883d07cecec82549
ms.sourcegitcommit: a72567f26c1653c25f7730fab6210cd011343707
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83564472"
---
# <a name="administering-power-bi-in-the-admin-portal"></a>A Power BI felügyelete a felügyeleti portálon

A felügyeleti portál segítségével kezelheti a szervezetéhez tartozó Power BI-*bérlőt*. A portál olyan lehetőségeket kínál, mint például a használati metrikák, hozzáférés a Microsoft 365 Felügyeleti központjához, valamint a beállítások.

Minden globális rendszergazda hozzáférhet a teljes felügyeleti portálhoz, valamint olyan felhasználók is, akik Power BI-szolgáltatásadminisztrátori szerepkört kaptak. Ha még nem kapott ilyen szerepkörbe, csak a **kapacitásbeállításokat** láthatja a portálon. A Power BI szolgáltatás rendszergazdai szerepkörére vonatkozó további információkat [a Power BI rendszergazdai szerepkörét ismertető](service-admin-role.md) témakör tartalmaz.

## <a name="how-to-get-to-the-admin-portal"></a>A felügyeleti portál elérése

A fiókját **Globális rendszergazda** fiókként kell megjelölni a Microsoft 365 vagy az Azure Active Directory (Azure AD) szolgáltatáson belül, vagy a Power BI szolgáltatás rendszergazdai szerepkörét kell hozzárendelni, hogy hozzá tudjon férni a Power BI felügyeleti portáljához. A Power BI szolgáltatás rendszergazdai szerepkörére vonatkozó további információkat [a Power BI rendszergazdai szerepkörét ismertető](service-admin-role.md) témakör tartalmaz. A Power BI felügyeleti portál eléréséhez tegye az alábbiakat.

1. Válassza ki a Beállítások fogaskereket a Power BI szolgáltatás jobb felső sarkában.

1. Válassza a **Felügyeleti portál** lehetőséget.

    ![A felügyeleti portál beállításai](media/service-admin-portal/powerbi-admin-settings.png)

A portálon kilenc lap található. A cikk további részében ezen lapokról olvashat.

![Navigálás a felügyeleti portálon](media/service-admin-portal/powerbi-admin-landing-page.png)

* [Használati metrikák](#usage-metrics)
* [Felhasználók](#users)
* [Auditnaplók](#audit-logs)
* [Bérlői beállítások](#tenant-settings)
* [Kapacitásbeállítások](#capacity-settings)
* [Beágyazási kódok](#embed-codes)
* [Szervezeti vizualizációk](#organizational-visuals)
* [Adatfolyam-tárolás (előzetes verzió)](#dataflowStorage)
* [Munkaterületek](#workspaces)
* [Egyéni védjegyzés](#custom-branding)

## <a name="usage-metrics"></a>Használati metrikák

A **Használati metrikák** segítségével nyomon követheti a szervezet Power BI-használatát. Ezenkívül azt is mutatja, hogy mely munkahelyi felhasználók és csoportok a legaktívabbak a Power BI-ban. 

> [!NOTE]
> Az irányítópult első használatakor, vagy ha hosszú idő elteltével keresi fel újra az irányítópultot, egy betöltési képernyő jelenik meg az irányítópult betöltése során.

Miután az irányítópult betöltődött, két szakaszba sorolt csempék jelennek meg. Az első szakasz tartalmazza az egyes felhasználók használati adatait, míg a második szakaszban a munkahelyi csoportok hasonló információi láthatók.

Az alábbiakban az egyes csempéknél megjelenő részletes információkat ismertetjük:

* A felhasználói munkaterület összes irányítópultjának, jelentésének és adatkészletének egyedi darabszáma.
  
    ![Az irányítópultok, jelentések és adatkészletek eltérő darabszáma](media/service-admin-portal/powerbi-admin-usage-metrics-number-tiles.png)

* A legtöbbet használt irányítópult az ahhoz hozzáférő felhasználók száma szerint. Például ha 3 felhasználóval oszt meg egy irányítópultot, és olyan tartalomcsomaghoz is hozzáadja azt, amelyhez két különböző felhasználó kapcsolódik, a számláló értéke 6 (1 + 3 + 2).
  
    ![Legtöbbet felhasznált irányítópultok](media/service-admin-portal/powerbi-admin-usage-metrics-top-dashboards.png)

* A legnépszerűbb tartalom, amelyhez a felhasználók kapcsolódtak. Ez bármi lehet, amelyhez a felhasználók hozzáférhetnek az adatbeolvasási folyamaton keresztül, például szolgáltatott szoftveres tartalomcsomagok, munkahelyi tartalomcsomagok, fájlok vagy adatbázisok.
  
    ![Legtöbbet felhasznált csomagok](media/service-admin-portal/powerbi-admin-usage-metrics-top-connections.png)

* A legaktívabb felhasználókat mutatja az irányítópultok száma alapján, beleértve a felhasználók által létrehozott és a velük megosztott irányítópultok számát.
  
    ![Legaktívabb felhasználók – irányítópultok](media/service-admin-portal/powerbi-admin-usage-metrics-top-users-dashboards.png)

* A legaktívabb felhasználókat mutatja a jelentéseik száma alapján.
  
    ![Legaktívabb felhasználók – jelentések](media/service-admin-portal/powerbi-admin-usage-metrics-top-users-reports.png)

A második szakasz ugyanezeket az információkat tartalmazza – a csoportok alapján. Lehetővé teszi annak megtekintését, hogy a munkahely mely csoportjai a legaktívabbak, és milyen típusú tartalmakat használnak fel.

Ezek az információk valós betekintést nyújtanak abba, hogy a felhasználók miként használják a Power BI-t a munkahelyen, és mely munkahelyi felhasználók és csoportok számítanak különösen aktívnak.

## <a name="control-usage-metrics"></a>Használati metrikák szabályozása

A használati metrikai jelentés olyan funkció, amelyet a Power BI vagy Microsoft 365 rendszergazdája kapcsolhat be vagy ki. A rendszergazdák részletesen szabályozhatják, hogy mely felhasználók férnek hozzá használati metrikákhoz. Ezek alapértelmezés szerint minden vállalati felhasználó számára **engedélyezve** vannak.

A rendszergazdák azt is meghatározhatják, hogy a tartalomkészítők láthatják-e a felhasználónkénti adatokat a használati metrikák között. 

Magukról a jelentésekről a [Power BI-irányítópultok és -jelentések használati metrikáinak figyelése](../collaborate-share/service-usage-metrics.md) című szakaszban olvashat részleteket.

### <a name="usage-metrics-for-content-creators"></a>Használati metrikák tartalomkészítők számára

1. A Felügyeleti portálon válassza a **Bérlői beállítások** > **Tartalomkészítőknek szánt használati metrikák** lehetőséget.

    ![Felügyeleti portál, bérlői beállítások, használati metrikák](media/service-admin-portal/power-bi-admin-usage-metrics.png)

1. Engedélyezze (vagy tiltsa le) a használati metrikákat > **Alkalmaz**.

    ![Használati metrikák engedélyezve](../collaborate-share/media/service-usage-metrics/power-bi-tenant-settings-updated.png)


### <a name="per-user-data-in-usage-metrics"></a>Felhasználónkénti adatok a használati metrikákban

Alapértelmezés szerint a felhasználónkénti adatok engedélyezve vannak a használati metrikákhoz, a tartalomfelhasználói fiókadatok pedig szerepelnek a metrikajelentésekben. Ha ezt az információt nem szeretné belefoglalni egyes felhasználók esetében, tiltsa le a funkciót megadott biztonsági csoportok, vagy a teljes szervezet számára. A fiókadatok ekkor *névtelenként* jelennek meg a jelentésben.

![Felhasználónkénti használati adatok](media/service-admin-portal/power-bi-admin-per-user-usage-data.png)

### <a name="delete-all-existing-usage-metrics-content"></a>Az összes meglévő használati metrikai tartalom törlése

Ha letiltják a használati metrikákat az egész vállalat számára, a rendszergazdák az alábbi két lehetőség egyikét, vagy mindkettőt is kiválaszthatják:

- Az **összes meglévő használati metrikai tartalom törlése** lehetőséggel törölni tudnak minden meglévő jelentést és irányítópult-csempét, amely a használati metrikai jelentések és adathalmazok használatával készült. Ezen a módon minden használati metrikai adat hozzáférhetetlenné válik a szervezet valamennyi felhasználója számára, akik esetleg már használják is azokat. 
- Az **összes meglévő felhasználói adat törlése az aktuális használati metrikai tartalomban** lehetőséggel minden felhasználónkénti adat hozzáférhetetlenné válik a szervezet valamennyi felhasználója számára, akik esetleg már használják is azokat. 

Fontolja meg ezt a lépést, mert a meglévő használati és felhasználónkénti metrikai tartalom törlése nem vonható vissza.

## <a name="users"></a>Felhasználók

A Power BI-felhasználókat, -csoportokat és -rendszergazdákat a Microsoft 365 Felügyeleti központjában kezelheti. A **Felhasználók** lap tartalmaz egy hivatkozást a bérlő felügyeleti központjára.

![A Microsoft 365 Felügyeleti központ megnyitása](media/service-admin-portal/powerbi-admin-manage-users.png)

## <a name="audit-logs"></a>Auditnaplók

A Power BI-naplókat az Office 365 Security & Compliance Centerben kezelheti. A **Auditnaplók** lap tartalmaz egy, a bérlőhöz tartozó Security & Compliance centerre mutató hivatkozást. [További információ](service-admin-auditing.md)

Az auditnaplók használatához engedélyezze a [**Vizsgálati naplók létrehozása belső tevékenységek és megfelelőség vizsgálatához**](#create-audit-logs-for-internal-activity-auditing-and-compliance) beállítást.

## <a name="tenant-settings"></a>Bérlői beállítások

A **Bérlői beállítások** lap lehetővé teszi a szervezet számára elérhetővé tett funkciók finomhangolt szabályozását. Ha aggályai vannak a bizalmas adatokkal kapcsolatban, a funkciók némelyike esetlegesen nem megfelelő a munkahely számára, vagy csak egy adott funkciót szeretne engedélyezni egy adott csoportnak.

Az alábbi képen a **Bérlői beállítások** lap néhány beállítása látható.

![Bérlői beállítások](media/service-admin-portal/powerbi-admin-tenant-settings.png)

> [!NOTE]
> A beállítás módosításának érvénybe léptetése a bérlő összes felhasználója számára akár 10 percet is igénybe vehet.

A beállítások állapota háromféle lehet:

* **A szervezeten belül sehol nem engedélyezett**: A szervezeten belül senki sem használhatja ezt a funkciót.

    ![Az összes le van tiltva beállítás](media/service-admin-portal/powerbi-admin-tenant-settings-disabled.png)

* **A szervezeten belül mindenhol engedélyezett**: A szervezeten belül mindenki használhatja ezt a funkciót.

    ![Az összes engedélyezve van beállítás](media/service-admin-portal/powerbi-admin-tenant-settings-enabled.png)

* **A szervezet egy alegysége számára engedélyezett**: A szervezet felhasználóinak egy adott részhalmaza vagy csoportjai használhatják az adott funkciót.

    Engedélyezhet egy funkciót az egész munkahelyen a felhasználók egy adott csoportja kivételével.

    ![Engedélyezett részhalmaz beállítás](media/service-admin-portal/powerbi-admin-tenant-settings-enabled-except.png)

    Engedélyezhet egy funkciót a felhasználók egy adott csoportjában, és letilthatja azt a felhasználók egy másik csoportjában. Ezzel a módszerrel garantálható, hogy egyes felhasználók még akkor sem férhetnek hozzá az adott funkcióhoz, ha egyébként benne vannak az engedélyezett csoportban.

    ![Kivéve engedélyezése beállítás](media/service-admin-portal/powerbi-admin-tenant-settings-enabled-except2.png)

A következő néhány bekezdés a bérlői beállítások különböző típusainak áttekintését nyújtja.

## <a name="help-and-support-settings"></a>Súgó és támogatás beállításai

### <a name="publish-get-help-information"></a>Súgóinformációk közzététele

A vállalati felhasználók belső súgó és támogatási forrásokhoz fordulhatnak a Power BI súgó menüjében. Ezek a paraméterek pontosabban a Tanulás, Közösség és Segítség kérése menüelemek viselkedését módosítják.

Emellett a licenckérések URL-címének megadásával testreszabhatja a **Fiók bővítése** gomb célként megadott URL-címét. Ez a gomb a **Frissítés a Power BI Pro kiadásra** párbeszédpanelen, valamint a **Személyes tárhely kezelése** lapon jelenik meg a Power BI Pro-licenccel nem rendelkező felhasználók számára. Emellett a Power BI-ban már nem érhető el **A Pro kiadás ingyenes kipróbálása** gomb ezen a párbeszédpanelen és tárhelylapon. Ez biztosítja, hogy a Power BI megbízhatóan vezesse végig a felhasználókat a szervezetben a licenckezelési megoldással definiált folyamaton.

![Kivéve engedélyezése beállítás](media/service-admin-portal/powerbi-admin-tenant-settings-gethelp.png)

### <a name="receive-email-notifications-for-service-outages-or-incidents"></a>E-mail-értesítések fogadása szolgáltatásbeli kimaradásokról vagy incidensekről

Az e-mail-küldést engedélyező biztonsági csoportok e-mail-értesítéseket fognak kapni, ha ezt a bérlőt érinti egy szolgáltatáskimaradás vagy egy incidens. További információ a [Szolgáltatáskimaradásokkal kapcsolatos értesítésekről](service-interruption-notifications.md).

## <a name="workspace-settings"></a>Munkaterület beállításai

A felügyeleti portál **Bérlői beállítások** területén két szakaszban vezérelhetőek a munkaterületek:

- Új munkaterületi felhasználói felületek létrehozása.
- Adatkészletek használata munkaterületek között.

### <a name="create-the-new-workspaces"></a>Új munkaterületek létrehozása

A munkaterületeken a felhasználók együttműködhetnek az irányítópultokon, a jelentéseken és más tartalmakon. A rendszergazdák a **Munkaterületek létrehozása (új munkaterületi felhasználói felület)** beállítással jelzik, hogy a szervezet mely felhasználói hozhatnak létre munkaterületeket. A rendszergazdák dönthetnek úgy, hogy egy szervezetben mindenkinek engedélyezik vagy senkinek nem engedélyezik új munkaterületi felhasználói felületek létrehozását. Korlátozhatják is meghatározott biztonsági csoportok tagjaira a létrehozást. További tudnivalók a [munkaterületekről](../collaborate-share/service-new-workspaces.md).

:::image type="content" source="media/service-admin-portal/power-bi-admin-workspace-settings.png" alt-text="Új munkaterületi felhasználói felületek létrehozása":::

A Microsoft 365-csoportokon alapuló klasszikus munkaterületek felügyelete továbbra is a felügyeleti portálon és az Azure Active Directoryban történik.

> [!NOTE]
> A **Munkaterületek létrehozása (új munkaterületi felhasználói felület)** beállítás alapértelmezett értéke, hogy csak a Microsoft 365-csoportok létrehozására jogosult felhasználóknak engedélyezett új Power BI-munkaterületek létrehozása. A Power BI felügyeleti portálján a megfelelő érték beállításával gondoskodjon arról, hogy a megfelelő felhasználók hozhassanak létre munkaterületeket.

**Munkaterületek listája**

A felügyeleti portálon egy másik szakasz is tartalmaz a bérlőbeli munkaterületekre vonatkozó beállításokat. Ebben a szakaszban rendezheti és szűrheti a munkaterületek listáját, és minden munkaterület adatait megjelenítheti. Ennek részleteit a cikk [Munkaterületek](#workspaces) című szakasza ismerteti.

**Tartalomcsomagok és alkalmazások közzététele**

A felügyeleti portálon azt is szabályozhatja, hogy mely felhasználók rendelkezzenek engedéllyel alkalmazások vállalaton belüli terjesztésére. A részleteket ennek a cikknek [Tartalomcsomagok és alkalmazások közzététele a teljes vállalat számára](#publish-content-packs-and-apps-to-the-entire-organization) című fejezetében találhatja meg.

### <a name="use-datasets-across-workspaces"></a>Adathalmazok használata több munkaterülettel

A rendszergazdák szabályozhatják, hogy a szervezet mely felhasználói használhatják az adathalmazokat a munkaterületeken. Ha ez a beállítás engedélyezve van, a felhasználóknak továbbra is összeállítási engedélyre van szükségük az adott adathalmazhoz.

:::image type="content" source="media/service-admin-portal/power-bi-admin-datasets-workspaces.png" alt-text="Adatkészletek használata munkaterületek között":::

További tudnivalókat az [adatkészletek munkaterületeken való használatának bevezetőjében](../connect-data/service-datasets-across-workspaces.md) olvashat.


## <a name="export-and-sharing-settings"></a>Exportálási és megosztási beállítások

### <a name="share-content-with-external-users"></a>Tartalom megosztása külső felhasználókkal

A vállalat felhasználói megoszthatnak irányítópultokat, jelentéseket és alkalmazásokat külső felhasználókkal. További információ a [külső megosztásról](../collaborate-share/service-share-dashboards.md#share-a-dashboard-or-report-outside-your-organization).

![Külső felhasználók beállítás](media/service-admin-portal/powerbi-admin-sharing-external-02.png)

Az alábbi képen azon üzenet látható, amely akkor jelenik meg, ha külső felhasználóval oszt meg tartalmat.

![Megosztás külső felhasználóval](media/service-admin-portal/powerbi-admin-sharing-external.png)  

> [!IMPORTANT]
> Ez a beállítás azt szabályozza, hogy a Power BI felhasználói meghívhatnak-e külső felhasználókat, mint Azure Active Directory B2B- (Azure AD B2B-) felhasználókat a szervezetbe a Power BI-on keresztül. Ha ez a beállítás engedélyezve van, a Vendég meghívója szerepkörrel rendelkező felhasználók külső e-mail-címeket vehetnek fel jelentések, irányítópultok és Power BI-alkalmazások megosztásakor. A külső címzett meghívást kap a szervezethez való csatlakozásra, mint Azure AD B2B-vendégfelhasználó. Ha ezt a beállítást kikapcsolja, a már Azure AD B2B-vendégfelhasználóként meghívottak továbbra is megjelennek a Power BI személyválasztó felületein, és hozzáférést kaphatnak elemekhez, munkaterületekhez és alkalmazásokhoz.

### <a name="publish-to-web"></a>Webes közzététel

A Power BI-bérlő rendszergazdái a **Webes közzététel** beállítással szabályozhatják, hogy mely felhasználók hozhatnak létre beágyazási kódokat a jelentések webes közzétételéhez. Ez a funkció a jelentést és annak adatait is bárki számára elérhetővé teszi a weben. További tudnivalók a [webes közzétételről](../collaborate-share/service-publish-to-web.md).

> [!NOTE]
> Új webes közzétételi beágyazási kódok létrehozását csak a Power BI-rendszergazdák engedélyezhetik. A vállalatok rendelkezhetnek meglévő beágyazási kódokkal. Az aktuálisan közzétett jelentések a felügyeleti portál [Beágyazási kódok](service-admin-portal.md#embed-codes) szakaszában tekinthetők meg.

Az alábbi ábrán egy jelentés **További lehetőségek (...)** menüje látható a **Webes közzététel** beállítás engedélyezése esetén.

![Webes közzététel a További lehetőségek menüben](media/service-admin-portal/power-bi-more-options-publish-web.png)

A felügyeleti portálon elérhető **Webes közzététel** beállítással megadható, hogy mely felhasználók hozhatnak létre beágyazási kódokat.

![Webes közzététel beállítás](media/service-admin-portal/powerbi-admin-publish-to-web-setting.png)

A rendszergazdák a **Webes közzététel** **Engedélyezésével**, valamint **A beágyazási kódok működési módjának kiválasztásával** megtehetik, hogy **Csak a meglévő beágyazási kódokat engedélyezik**. Ebben az esetben a felhasználók létrehozhatnak beágyazási kódokat, de ennek engedélyezését a Power BI-rendszergazdától kell kérniük.

![Webes közzétételi kérés](../collaborate-share/media/service-publish-to-web/publish_to_web_admin_prompt.png)

A **Webes közzététel** beállításától függően a felhasználók különféle lehetőségeket láthatnak a felhasználói felületen.

|Funkció |A teljes cég számára engedélyezve |A teljes cég számára letiltva |Speciális biztonsági csoportok   |
|---------|---------|---------|---------|
|Egy jelentés **További lehetőségek (...)** menüjének **Webes közzététel** pontja|Mindenki számára engedélyezve|Nem mindenki számára látható|Csak az arra jogosult felhasználók vagy csoportok láthatják.|
|A **Beágyazási kódok kezelése** funkció a **Beállítások** közt|Mindenki számára engedélyezve|Mindenki számára engedélyezve|Mindenki számára engedélyezve<br><br>* A **Törlés** parancsot csak az arra jogosult felhasználók vagy csoportok érik el.<br>* A **Kód lekérése** mindenki számára engedélyezve van.|
|**Beágyazási kódok** a felügyeleti portálon|Az állapot a következő értékek egyikét jeleníti meg:<br>* Aktív<br>* Nem támogatott<br>* Blokkolva|Állapotként a **Letiltva** jelenik meg|Az állapot a következő értékek egyikét jeleníti meg:<br>* Aktív<br>* Nem támogatott<br>* Blokkolva<br><br>Ha egy felhasználónak nincs megfelelő jogosultsága a bérlői beállítások alapján, akkor a **Megsértve** állapot jelenik meg.|
|Meglévő közzétett jelentések|Minden engedélyezve|Minden letiltva|A jelentések továbbra is megjelennek mindenki számára.|

### <a name="export-data"></a>Adatok exportálása

A munkahelyi felhasználók adatokat exportálhatnak egy csempéről vagy vizualizációból. Ez vezérli az elemzést az Excelben, a .csv-be történő exportálást, az adatkészlet letöltését (.pbix) és a Power BI szolgáltatás Live Connect-funkcióit. További információ [adatok csempéről vagy vizualizációból való exportálásáról](../visuals/power-bi-visualization-export-data.md).

>[!NOTE]
> Az Exportálás Excelbe beállítás bevezetése előtt ez a beállítás szabályozta az Excel-fájlba való exportálást is. A részletekért tekintse meg az [Exportálás Excelbe megjegyzését](#export-to-excel).

![Adatexportálási beállítások](media/service-admin-portal/powerbi-admin-portal-export-data-setting.png)

Az alábbi képen az adatok exportálásának lehetősége látható egy csempén.

![Adatok exportálása egy csempéből](media/service-admin-portal/powerbi-admin-export-data.png)

> [!NOTE]
> Az **Adatok exportálása** lehetőség letiltásával azt is megakadályozhatja, hogy a felhasználók az [Elemzés az Excelben](../collaborate-share/service-analyze-in-excel.md) funkciót vagy a Power BI szolgáltatás élő kapcsolatát használják.

### <a name="export-to-excel"></a>Exportálás Excelbe

A szervezeten belüli felhasználók exportálhatják az adatokat egy vizualizációból egy Excel-fájlba.

![Exportálás Excelbe beállítás](media/service-admin-portal/powerbi-admin-portal-export-to-excel-setting.png)

>[!IMPORTANT]
> Az Exportálás Excelbe beállítás bevezetése előtt az Excel-fájlba való exportálást az Adatexportálási beállítások vezérelték. Ezért azoknál a bérlőknél, amelyek az Exportálás Excelbe bevezetését megelőzően léteztek, az első alkalommal, amikor a bérlői rendszergazdák megtekintik az Exportálás Excelbe beállítást, látni fogják, hogy *nem alkalmazott módosításokat* is tartalmaz. Ezeket a módosításokat alkalmazniuk kell ahhoz, hogy az új beállítás érvénybe lépjen. Ellenkező esetben az Excel-fájlba való exportálás továbbra is az Adatexportálási beállításokkal lesz vezérelve.

### <a name="export-reports-as-powerpoint-presentations-or-pdf-documents"></a>Jelentések exportálása PowerPoint-bemutatóként vagy PDF-dokumentumként

A szervezeten belüli felhasználók PowerPoint-fájlként és PDF-dokumentumként is exportálhatnak Power BI-jelentéseket. [További információ](../consumer/end-user-powerpoint.md)

Az alábbi képen látható a **Fájl** menü egy jelentéshez, ha a **Jelentések exportálása PowerPoint-bemutatóként vagy PDF-fájlként** beállítás engedélyezve van.

![Jelentések exportálása PowerPoint-bemutatóként](media/service-admin-portal/powerbi-admin-powerpoint.png)

### <a name="print-dashboards-and-reports"></a>Irányítópultok és jelentések nyomtatása

A munkahelyi felhasználók irányítópultokat és jelentéseket nyomtathatnak. [További információ](../consumer/end-user-print.md)

Az alábbi képen az irányítópult nyomtatásának lehetősége látható.

![Irányítópult nyomtatása](media/service-admin-portal/powerbi-admin-print-dashboard.png)

Az alábbi képen a jelentéshez tartozó **Fájl** menü látható, ha az **Irányítópultok és jelentések nyomtatása** beállítás engedélyezve van.

![Jelentés nyomtatása](media/service-admin-portal/powerbi-admin-print-report.png)

### <a name="allow-external-guest-users-to-edit-and-manage-content-in-the-organization"></a>Annak engedélyezése, hogy külső vendégfelhasználók is szerkeszthessék és kezelhessék a szervezeti tartalmakat

Az Azure AD B2B-vendégfelhasználók szerkeszthetik és kezelhetik a szervezeti tartalmakat. [További információ](service-admin-azure-ad-b2b.md)

A következő képen az „Annak engedélyezése, hogy külső vendégfelhasználók is szerkeszthessék és kezelhessék a szervezeti tartalmakat” beállítás látható.

![Annak engedélyezése, hogy külső vendégfelhasználók is szerkeszthessék és kezelhessék a szervezeti tartalmakat](media/service-admin-portal/powerbi-admin-tenant-settings-b2b-guest-edit-manage.png)

A felügyeleti portálon azt is szabályozhatja, hogy mely felhasználók rendelkezzenek engedéllyel külső felhasználók a szervezetbe való meghívására. További részletekért tekintse meg a [Tartalom megosztása külső felhasználókkal](#export-and-sharing-settings) című részt.

### <a name="email-subscriptions"></a>E-mail-feliratkozások
A vállalati felhasználók e-mail-feliratkozásokat hozhatnak létre és használhatnak. További tudnivalók a [feliratkozásokról](../collaborate-share/service-publish-to-web.md).

![E-mail-feliratkozások engedélyezése](media/service-admin-portal/power-bi-manage-email-subscriptions.png)

### <a name="featured-content"></a>Kiemelt tartalom

A szervezet néhány vagy minden jelentéskészítőjének engedélyezheti, hogy kiemeljék tartalmukat a Power BI kezdőlapjának Kiemelt szakaszában. Az új felhasználók a Power BI kezdőlapjának tetején láthatják a kiemelt tartalmakat. A kiemelt tartalom egyre lejjebb kerül a kezdőlapon, ahogy a felhasználók **kedvenceket**, **gyakori elemeket**, és **legutóbbi elemeket** adnak hozzá. 

Azt javasoljuk, hogy elsőként csak néhány reklámozót alkalmazzon. Ha a teljes szervezet számára lehetővé teszi, hogy tartalmat emeljen ki a kezdőlapon, nehéz lesz nyomon követni az összes kiemelt tartalmat. 

A kiemelt tartalom engedélyezése után a Felügyeleti portálon is kezelheti. További információt a tartomány kiemelt tartalmairól a cikk [Kiemelt tartalom kezelése](#manage-featured-content) című szakaszában találhat.

## <a name="content-pack-and-app-settings"></a>Tartalomcsomag és alkalmazás beállításai

### <a name="publish-content-packs-and-apps-to-the-entire-organization"></a>Tartalomcsomagok és alkalmazások közzététele a teljes szervezet számára

A rendszergazdák ezzel a beállítással határozzák meg, hogy mely felhasználók tehetnek közzé tartalomcsomagokat és alkalmazásokat a teljes vállalat, és nem csak adott csoportok számára. További tudnivalók az [alkalmazások közzétételéről](../collaborate-share/service-create-distribute-apps.md).

Az alábbi képen a **Teljes saját szervezet** lehetőség látható a tartalomcsomag létrehozásakor.

![Tartalomcsomag közzététele a szervezet számára](media/service-admin-portal/powerbi-admin-publish-entire-org.png)

### <a name="create-template-apps-and-organizational-content-packs"></a>Vállalati tartalomcsomagok és alkalmazások sablonjainak létrehozása

A munkahelyi felhasználók sablonalkalmazásokat és vállalati sablon tartalomcsomagokat készíthetnek, amelyek a Power BI Desktop adott adatforrására épülő adathalmazokat használják. További információ a [sablonalkalmazásokról](../connect-data/service-template-apps-create.md).

### <a name="push-apps-to-end-users"></a>Alkalmazások küldése a végfelhasználóknak

A jelentéskészítők közvetlenül is megoszthatnak alkalmazásokat a végfelhasználókkal, anélkül, hogy telepíteni kellene azokat az [AppSource](https://appsource.microsoft.com)-ból. További információ: [alkalmazások automatikus telepítése a végfelhasználók számára](../collaborate-share/service-create-distribute-apps.md#automatically-install-apps-for-end-users).

## <a name="integration-settings"></a>Integrálási beállítások

### <a name="use-analyze-in-excel-with-on-premises-datasets"></a>Az Elemzés az Excelben helyszíni adathalmazokon való használata

A munkahelyi felhasználók az Excel használatával megtekinthetik és használhatják a helyszíni Power BI-adatkészleteket. [További információ](../collaborate-share/service-analyze-in-excel.md)

> [!NOTE]
> Az **Adatok exportálása** lehetőség letiltásával azt is megakadályozhatja, hogy a felhasználók az **Elemzés az Excelben** funkciót használják.

### <a name="use-arcgis-maps-for-power-bi"></a>Az ArcGIS Maps for Power BI használata

A vállalati felhasználók használhatják az Esri által biztosított ArcGIS Maps for Power BI vizualizációt. [További információ](../visuals/power-bi-visualization-arcgis.md)

### <a name="use-global-search-for-power-bi-preview"></a>A globális keresés használata a Power BI-ban (előzetes verzió)

A vállalati felhasználók használhatják az Azure Searchre épülő külső keresési funkciókat.

## <a name="power-bi-visuals-settings"></a>Power BI-vizualizációk beállításai

### <a name="add-and-use-power-bi-visuals"></a>Power BI-vizualizációk hozzáadása és használata

A munkahelyi felhasználók Power BI-vizualizációkat használhatnak és oszthatnak meg. [További információ](../developer/visuals/power-bi-custom-visuals.md)

> [!NOTE]
> Ez a beállítás az egész munkahelyre vonatkozhat, de korlátozható meghatározott csoportokra.

A Power BI Desktop (a 2019. márciusi kiadással kezdődően) támogatja a **Csoportházirendek** használatát a Power BI-vizualizációk letiltásához a cég összes üzembe helyezett számítógépén.

<table>
<tr><th>Attribútum</th><th>Érték</th>
</tr>
<td>key</td>
    <td>Software\Policies\Microsoft\Power BI Desktop\</td>
<tr>
<td>valueName</td>
<td>EnableCustomVisuals</td>
</tr>
</table>

Az 1 (decimális) érték engedélyezi a Power BI-vizualizációk használatát a Power BI-ban (ez az alapértelmezett beállítás).

A 0 (decimális) érték letiltja a Power BI-vizualizációk használatát a Power BI-ban.

### <a name="allow-only-certified-visuals"></a>Csak hitelesített vizualizációk engedélyezése

A szervezet azon felhasználói, akik engedélyt kaptak Power BI-vizualizációk hozzáadására és használatára (őket „Power BI-vizualizációk hozzáadása és használata” beállítás jelzi), csak a [hitelesített Power BI-vizualizációkat](https://go.microsoft.com/fwlink/?linkid=2002010) használhatják (a nem hitelesített vizualizációk le lesznek tiltva, használatuk esetén hibaüzenet jelenik meg). 


A Power BI Desktop (a 2019. márciusi kiadással kezdődően) támogatja a **Csoportházirendek** használatát a tanúsítvány nélküli Power BI-vizualizációk letiltásához a cég összes üzembe helyezett számítógépén.

<table>
<tr><th>Attribútum</th><th>Érték</th>
</tr>
<td>key</td>
    <td>Software\Policies\Microsoft\Power BI Desktop\</td>
<tr>
<td>valueName</td>
<td>EnableUncertifiedVisuals</td>
</tr>
</table>

Az 1 (decimális) érték engedélyezi a tanúsítvány nélküli Power BI-vizualizációk használatát a Power BI-ban (ez az alapértelmezett beállítás).

A 0 (decimális) érték letiltja a tanúsítvány nélküli Power BI-vizualizációk használatát a Power BI-ban (ez a beállítás csak a [tanúsítvánnyal rendelkező Power BI-vizualizációkat engedélyezi](https://go.microsoft.com/fwlink/?linkid=2002010)).

## <a name="r-visuals-settings"></a>R-vizualizációk beállításai

### <a name="interact-with-and-share-r-visuals"></a>R-vizualizációk kezelése és megosztása

A munkahelyi felhasználók R-szkriptekkel készült vizualizációkat használhatnak és oszthatnak meg. [További információ](../visuals/service-r-visuals.md)

> [!NOTE]
> Ez a beállítás az egész munkahelyre vonatkozik, és nem lehet korlátozni meghatározott csoportokra.

## <a name="audit-and-usage-settings"></a>Naplózási és használati beállítások

### <a name="create-audit-logs-for-internal-activity-auditing-and-compliance"></a>Auditnaplók létrehozása a belső tevékenységek vizsgálatához és a megfelelőség biztosításához

A felhasználók a naplózással nyomon követhetik, hogy a munkahely más felhasználói milyen műveleteket hajtottak végre a Power BI-ban. [További információ](service-admin-auditing.md)

Az auditnapló bejegyzéseinek rögzítéséhez engedélyezni kell ezt a beállítást. Akár 48 órás késés is lehet a naplózás engedélyezése és a naplózási adatok megtekinthetővé válása között. Ha nem látja azonnal adatokat, ellenőrizze később az auditnaplókat. Hasonló késés lehet az auditnaplók megtekintési engedélyének megkapása és a naplók elérésének lehetővé válása között.

> [!NOTE]
> Ez a beállítás az egész munkahelyre vonatkozik, és nem lehet korlátozni meghatározott csoportokra.

### <a name="usage-metrics-for-content-creators"></a>Használati metrikák tartalomkészítők számára

A munkahelyi felhasználók láthatják az általuk létrehozott jelentések és irányítópultok használati metrikáit. [További információ](../collaborate-share/service-usage-metrics.md)

### <a name="per-user-data-in-usage-metrics-for-content-creators"></a>Felhasználónkénti adatok a használati metrikákban a tartalmak szerzői számára

A tartalmak szerzőinek használati metrikáiban szerepel a tartalmakhoz hozzáférő felhasználók megjelenítendő neve és e-mail-címe. [További információ](../collaborate-share/service-usage-metrics.md)

A felhasználónkénti adatok alapértelmezés szerint engedélyezve vannak a használati metrikákhoz, a tartalomkészítői fiókadatok pedig szerepelnek a metrikák jelentéseiben. Ha ezt az információt nem szeretné összegyűjteni az összes felhasználó esetében,letilthatja a funkciót megadott biztonsági csoportok vagy a teljes szervezet számára. A fiókadatok a kizárt felhasználók esetén ekkor *névtelenként* jelennek meg a jelentésben.

## <a name="dashboard-settings"></a>Irányítópult beállításai

### <a name="data-classification-for-dashboards"></a>Irányítópultok adatainak besorolása

A munkahelyi felhasználók a biztonsági szint besorolását jelző címkékkel láthatják el az irányítópultokat. [További információ](../create-reports/service-data-classification.md)

> [!NOTE]
> Ez a beállítás az egész munkahelyre vonatkozik, és nem lehet korlátozni meghatározott csoportokra.

## <a name="developer-settings"></a>Fejlesztői beállítások

### <a name="embed-content-in-apps"></a>Tartalom beágyazása alkalmazásokba

A munkahelyi felhasználók beágyazhatnak Power BI-irányítópultokat és -jelentéseket szolgáltatott szoftveres (SaaS-) alkalmazásokba. A beállítás kikapcsolásával megakadályozhatja, hogy a felhasználók a REST API-k használatával Power BI-tartalmakat ágyazzanak be saját alkalmazásukba. [További információ](../developer/embedded/embedding.md)

### <a name="allow-service-principals-to-use-power-bi-apis"></a>A Power BI API-k használatának engedélyezése szolgáltatásneveknek

Az Azure Active Directoryban (Azure AD-ben) regisztrált webalkalmazások hozzárendelt szolgáltatásnevet használnak a Power BI API-k elérésére anélkül, hogy a felhasználónak be kellene jelentkeznie. Egy alkalmazás számára akkor lehet engedélyezni a szolgáltatásnévvel történő hitelesítést, ha a szolgáltatásneve szerepel egy engedélyezett biztonsági csoportban. [További információ](../developer/embedded/embed-service-principal.md)

> [!NOTE]
> A szolgáltatásnevek a biztonsági csoportjukból öröklik az engedélyeket a Power BI összes bérlői beállításához. Az engedélyek korlátozásához hozzon létre egy külön biztonsági csoportot a szolgáltatásneveknek, majd adja hozzá az Egyes biztonsági csoportok kivételével listához a vonatkozó, engedélyezett Power BI-beállítások esetében.

## <a name="dataflow-settings"></a>Adatfolyam-beállítások

### <a name="create-and-use-dataflows"></a>Adatfolyamok létrehozása és használata

A vállalati felhasználók létrehozhatnak és használhatnak adatfolyamokat. További információ az adatfolyamokról: [Önkiszolgáló adatelőkészítés a Power BI-ban](../transform-model/service-dataflows-overview.md). Az adatfolyamok prémium szintű kapacitásban való engedélyezéséről lásd: [Számítási feladatok konfigurálása](service-admin-premium-workloads.md).

> [!NOTE]
> Ez a beállítás az egész munkahelyre vonatkozik, és nem lehet korlátozni meghatározott csoportokra.

## <a name="template-apps-settings"></a>Sablonalkalmazások beállításai

Három beállítás szabja meg, hogy egy sablonalkalmazás képes-e sablonalkalmazásokat közzétenni vagy telepíteni.

![A sablonalkalmazások beállításai a Power BI felügyeleti portálon](media/service-admin-portal/power-bi-admin-portal-template-apps.png)

### <a name="publish-template-apps"></a>Sablonalkalmazások közzététele

A vállalati felhasználók sablon alkalmazás-munkaterületeket hozhatnak létre. Az [AppSource](https://appsource.microsoft.com) vagy más terjesztési mód segítségével szabályozható, hogy mely felhasználók tehetnek közzé vagy terjeszthetnek a vállalaton kívüli ügyfelek között sablonalkalmazásokat.

![Power BI felügyeleti portál, Sablonalkalmazások létrehozása beállítás](media/service-admin-portal/power-bi-admin-portal-template-app-settings.png)

### <a name="install-template-apps-listed-on-appsource"></a>Az AppSource-on megjelenő sablonalkalmazások telepítése

A vállalati felhasználók **csak** az [AppSource](https://appsource.microsoft.com)-ról tölthetnek le és telepíthetnek alkalmazásokat. Megadható, hogy mely felhasználók vagy biztonsági csoportok telepíthetnek sablonalkalmazásokat az AppSource-ról.

![Power BI felügyeleti portál, Sablonalkalmazások telepítése beállítás](media/service-admin-portal/power-bi-admin-portal-template-app-settings-installer-appsource.png)

### <a name="install-template-apps-not-listed-on-appsource"></a>Az AppSource-on nem megjelenő sablonalkalmazások telepítése

Megadható, hogy mely vállalati felhasználók tölthetnek le és telepíthetnek **az [AppSource](https://appsource.microsoft.com)-on nem megjelenő** sablonalkalmazásokat.

![Power BI felügyeleti portál, Sablonalkalmazások telepítése beállítás](media/service-admin-portal/power-bi-admin-portal-template-app-settings-installer-nonappsource.png)

## <a name="capacity-settings"></a>Kapacitásbeállítások

### <a name="power-bi-premium"></a>Power BI Premium

A **Power BI Premium** lapon a munkahely által megvásárolt bármely Power BI Premium-kapacitás (EM vagy P termékváltozat) felügyelhető. A munkahely minden felhasználója láthatja a **Power BI Premium** lapot, de annak tartalma csak akkor jelenik meg, ha az adott felhasználó *kapacitás-rendszergazda* vagy rendelkezik a szükséges engedélyekkel. Ha a felhasználó nem rendelkezik ilyen engedéllyel, az alábbi üzenet jelenik meg.

![Nincs hozzáférés a Premium-beállításokhoz](media/service-admin-portal/premium-settings-no-access.png)

### <a name="power-bi-embedded"></a>Power BI Embedded

A **Power BI Embedded** lapon megtekintheti az ügyfél számára vásárolt Power BI Embedded (A termékváltozat) kapacitásait. Mivel az A termékváltozatot csak az Azure-tól szerezheti be, a [beágyazott kapacitások Azure-ban való kezelésére](../developer/embedded/azure-pbie-create-capacity.md)**az Azure Portalt** kell használnia.

A Power BI Embedded (A termékváltozat) beállításainak kezeléséről további információért lásd a [Mi a Power BI Embedded](../developer/embedded/azure-pbie-what-is-power-bi-embedded.md) szakaszt.

## <a name="embed-codes"></a>Beágyazási kódok

A rendszergazdák megnézhetik a bérlő számára generált beágyazási kódokat a jelentések nyilvános megosztásához. A kódokat vissza is vonhatja, vagy törölheti. [További információ](../collaborate-share/service-publish-to-web.md)

![Beágyazási kódok a Power BI felügyeleti portálon](media/service-admin-portal/embed-codes.png)

 ## <a name=""></a><a name="organizational-visuals">Szervezeti vizualizációk</a> 

A **Szervezeti vizualizációk** lapon Power BI-vizualizációkat helyezhet üzembe és kezelhet a cégen belül. A szervezeti vizualizációk segítségével egyszerűen helyezhet üzembe szellemi tulajdont képező vizualizációkat, a szerzők pedig láthatják a jelentéseket és importálhatják a saját jelentéseikbe a Power BI Desktopból. [További információ](../developer/visuals/power-bi-custom-visuals-organization.md)

> [!WARNING]
> Az egyéni vizualizációk biztonsági vagy adatvédelmi kockázatot jelentő kódokat tartalmazhatnak, ezért az adattárban való üzembe helyezés előtt ellenőrizze, hogy megbízható-e a vizualizáció szerzője és forrása.

A következő képen látható az összes olyan Power BI-vizualizáció, amely jelenleg megtalálható a szervezet adattárában.

![Szervezeti rendszergazdai visualizáció](media/service-admin-portal/power-bi-custom-visuals-organizational-admin-01.png)

### <a name="add-a-new-custom-visual"></a>Új egyéni vizualizáció hozzáadása

Új egyéni vizualizáció hozzáadásához kövesse az alábbi lépéseket. 

1. A jobb oldali ablaktáblán válassza ki az **Egyéni vizualizáció hozzáadása** lehetőséget.

    ![Power BI-vizualizációk – űrlap](media/service-admin-portal/power-bi-custom-visuals-organizational-admin-02.png)

1. Töltse ki az **Egyéni vizualizáció hozzáadása** űrlapot:

    * **Válasszon egy .pbiviz-fájlt** (kötelező): Válasszon ki egy feltöltendő egyéni vizualizációs fájlt. Csak a verziószámmal ellátott API-s Power BI-vizualizációk támogatottak (itt elolvashatja, ez mit jelent).

    Az egyéni vizualizációk feltöltése előtt át kell tekintenie a vizualizációt biztonsági és adatvédelmi szempontból, hogy biztosan megfeleljen a szervezet igényeinek.

    * **Nevezze el az egyéni vizualizációkat** (kötelező): Adjon egy rövid címet a vizualizációnak, hogy a Power BI Desktop felhasználói könnyen megértsék a rendeltetését.

    * **Ikon**: A Power BI Desktop felhasználói felületén megjelenő ikonfájl.

    * **Leírás**: A vizualizáció rövid leírása, amely több információt szolgáltat a felhasználónak

1. Kattintson a **Hozzáadás** lehetőségre a feltöltés kérelmezéséhez. Ha ez sikeres, az új elem megjelenik a listában. Ha nem, egy ennek megfelelő hibaüzenet jelenhet meg

### <a name="delete-a-custom-visual-from-the-list"></a>Egyéni látványelem törlése a listából

A vizualizáció végleges törléséhez kattintson az adattárban lévő vizualizációhoz tartozó kuka ikonra.

> [!IMPORTANT]
> A törlés nem vonható vissza. A törölt vizualizációk azonnal abbahagyják a renderelést a meglévő jelentésekben. A törölt változatot még ugyanazon vizualizáció ismételt feltöltése sem helyettesíti. A felhasználók azonban újraimportálhatják a vizualizációt, és pótolhatják azt a jelentéseikben.

### <a name="disable-a-custom-visual-in-the-list"></a>Egyéni látványelem letiltása a listában

A vizualizáció szervezeti áruházból való letiltásához válassza a fogaskerék ikont. A **Hozzáférés** szakaszban, tiltsa le az egyéni vizualizációt.

Miután letiltja a vizualizációt, az nem fog megjelenni a meglévő jelentésekben, és az alábbi hibaüzenet jelenik meg.

*Ez az egyéni vizualizáció már nem érhető el. További információért forduljon a rendszergazdához.*

Azonban a könyvjelzőzött vizualizációk továbbra is működnek.

Frissítés vagy rendszergazdai módosítás után a Power BI felhasználóinak újra kell indítaniuk az alkalmazást, vagy a Power BI szolgáltatás használata esetén frissíteniük kell a böngészőt a frissítések megjelenítéséhez.

### <a name="update-a-visual"></a>Vizualizáció frissítése

A vizualizáció munkahelyi áruházból való feltöltéséhez kattintson a fogaskerék ikonra. Keresse meg és töltse fel a vizualizáció új verzióját.

Győződjön meg róla, hogy a vizuális azonosító ugyanaz maradt. Az új fájl az előző fájlt helyére kerül a jelentésekben az egész vállalatnál. Ha azonban a vizualizáció új verziója megbontja az előző verziójának valamely használati vagy adatstruktúráját, akkor ne cserélje le az előző verziót. Ehelyett hozzon létre egy új listázást a vizualizáció új verziójához. Például adjon hozzá egy új verziószámot (X.X verzió) az új listázott vizualizáció címéhez. Ezáltal nyilvánvalóvá válik, hogy ez ugyanaz a vizualizáció, de frissített verziószámmal, így a meglévő jelentések működése nem hibásodik meg. Most is győződjön meg róla, hogy a vizuális azonosító ugyanaz maradt. Így amikor a felhasználók legközelebb belépnek a szervezeti adattárba a Power BI Desktopból, importálhatják az új verziót, amely kérni fogja őket, hogy cseréljék le a jelentésben található jelenlegi verziót.

További információt [a vállalati Power BI-vizualizációkkal kapcsolatos gyakori kérdések](../developer/visuals/power-bi-custom-visuals-faq.md#organizational-power-bi-visuals) között találhat

## <a name=""></a><a name="dataflowStorage">Adatfolyam-tárolás (előzetes verzió)</a>

A Power BI-jal használt adatok alapértelmezés szerint a Power BI által biztosított belső tárolóban helyezkednek el. Az adatfolyamok és az Azure Data Lake Storage Gen2 (ADLS Gen2) integrációjának köszönhetően adatfolyamait vállalata Azure Data Lake Storage Gen2-fiókjában is tárolhatja. További információt az [Adatfolyamok és az Azure Data Lake integrációja (előzetes verzió)](../transform-model/service-dataflows-azure-data-lake-integration.md) című cikkben talál.

## <a name="workspaces"></a>Munkaterületek

Rendszergazdaként megtekintheti a bérlőjében meglévő munkaterületeket. Rendezheti és szűrheti a munkaterületek listáját, és minden munkaterület adtait megjelenítheti. A táblázat oszlopai a munkaterületek a [Power BI felügyeleti Rest API](/rest/api/power-bi/admin) által visszaadott tulajdonságainak felelnek meg. A személyes munkaterületek típusa **PersonalGroup**, a klasszikus munkaterületeké **Group**, az új felületű munkaterületek pedig **Workspace** típusúak. További információkért lásd a [Munka szervezése az új munkaterületeken](../collaborate-share/service-new-workspaces.md) című részt.

A rendszergazdák kezelhetik és helyre is állíthatják a munkaterületeket a felügyeleti portálon vagy a PowerShell-parancsmagokkal. 

![Munkaterületek listája](media/service-admin-portal/workspaces-list.png)

A **Munkaterületek** lapon megtekintheti az egyes munkaterületek *állapotát*. Az alábbi táblázat részletesebben is ismerteti ezen állapotok jelentését.

|Állam  |Leírás  |
|---------|---------|
| Aktív | Normál munkaterület. Nem árul el semmit a felhasználásról vagy a tartalomról, csak annyit, hogy maga a munkaterület „normális”. |
| Árva | Rendszergazda-jogú felhasználó nélküli munkaterület. |
| Törölve | Törölt munkaterület. 90 napig elég metaadatot tartunk meg ahhoz, hogy a munkaterületet szükség esetén helyreállítsa. |
| Eltávolítás folyamatban | A munkaterület törlése folyamatban van, de még nem szűnt meg. A felhasználók törölhetik saját munkaterületeiket, először Eltávolítás folyamatban, majd végül Törölve állapotba léptetve azokat. |

## <a name="custom-branding"></a>Egyéni védjegyzés

Rendszergazdaként a teljes szervezet számára testreszabhatja a Power BI kinézetét. Jelenleg három fő lehetőség közül választhat:

![Egyéni védjegyzési lehetőségek](media/service-admin-portal/power-bi-custom-branding.png)

* **Embléma feltöltése**: Az ideális eredmény érdekében .png formátumú, 10 KB vagy kisebb, legalább 200 x 30 képpont méretű fájlt töltsön fel.

* **Borítókép feltöltése**: Az ideális eredmény érdekében .jpg .png formátumú, 1 MB vagy kisebb, legalább1920 x 160 képpont méretű fájlt töltsön fel.

* **Témaszín kiválasztása**: Témaszínt hexadecimális, RGB, érték, vagy színskála alapján választhat.


További információ: [Céges egyéni védjegyzés](https://aka.ms/orgBranding).

![Munkaterületek listája](media/service-admin-portal/workspaces-list.png)

## <a name="manage-featured-content"></a>A kiemelt tartalom kezelése

Bérlői rendszergazdaként kezelheti az összes olyan jelentést, irányítópultot és alkalmazást, amelyek a Power BI kezdőlapjának Kiemelt szakaszában jelennek meg a szervezetben.

- A Felügyeleti portálon válassza a **Kiemelt tartalom** lehetőséget.

Itt áttekintheti, hogy ki emelte ki a tartalmat, mikor, valamint megtekintheti a vonatkozó metaadatokat. Ha valami gyanúsnak tűnik, vagy ha törölni szeretné a Kiemelt szakaszt, igény szerint törölheti a kiemelt tartalmat.

További információt a kiemelt tartalmak használatáról a cikk [Kiemelt tartalom](#featured-content) című szakaszában találhat.

## <a name="next-steps"></a>Következő lépések

[A Power BI felügyelete a munkahelyen](service-admin-administering-power-bi-in-your-organization.md)  
[A Power BI rendszergazdai szerep ismertetése](service-admin-role.md)  
[A Power BI-naplózás használata a munkahelyen](service-admin-auditing.md)  

További kérdései vannak? [Kérdezze meg a Power BI közösségét](https://community.powerbi.com/)
