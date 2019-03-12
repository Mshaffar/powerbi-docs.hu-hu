---
title: A Power BI biztonsága – tanulmány
description: A Power BI biztonsági architektúráját és implementációját vizsgáló és ismertető tanulmány
author: davidiseminger
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-service
ms.topic: conceptual
ms.date: 02/28/2019
ms.author: davidi
LocalizationGroup: Conceptual
ms.openlocfilehash: 8415e731fd8749397b9604277f9f37f126b5413f
ms.sourcegitcommit: 76772a361e6cd4dd88824b2e4b32af30656e69db
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/27/2019
ms.locfileid: "56892990"
---
# <a name="power-bi-security-whitepaper"></a>A Power BI biztonsága – tanulmány

**Összefoglalás:** A Power BI a Microsoft egy online szoftverszolgáltatása (*SaaS* vagy szolgáltatott szoftver), amellyel könnyen és gyorsan létrehozhat önkiszolgáló üzletiintelligencia-irányítópultokat, jelentéseket, adatkészleteket és vizualizációkat. A Power BI szolgáltatással számos különböző adatforráshoz csatlakozhat, egyesítheti és formálhatja a kapcsolatokból származó adatokat, valamint másokkal megosztható jelentéseket és irányítópultokat hozhat létre.

**Szerző:** David Iseminger

**Műszaki véleményezők:** Pedram Rezaei, Cristian Petculescu, Siva Harinath, Tod Manning, Haydn Richardson, Adam Wilson, Ben Childs, Robert Bruckner, Sergei Gundorov, Kasper de Jonge

**A következőkre vonatkozik:** Power BI SaaS, Power BI Desktop, Power BI Embedded, Power BI Premium

> [!NOTE]
> A tanulmányt a böngésző **Nyomtatás** > **Mentés PDF-ként** lehetőségével mentheti vagy kinyomtathatja.

## <a name="introduction"></a>Bevezetés

A **Power BI** a Microsoft egy online szoftverszolgáltatása (_SaaS_ vagy szolgáltatott szoftver), amellyel könnyen és gyorsan létrehozhat önkiszolgáló üzletiintelligencia-irányítópultokat, jelentéseket, adatkészleteket és vizualizációkat. A Power BI szolgáltatással számos különböző adatforráshoz csatlakozhat, egyesítheti és formálhatja a kapcsolatokból származó adatokat, valamint másokkal megosztható jelentéseket és irányítópultokat hozhat létre.

A Power BI szolgáltatást a [Microsoft Online Services használati feltételei](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=31) és a [Microsoft nagyvállalati adatvédelmi nyilatkozata](http://www.microsoft.com/privacystatement/OnlineServices/Default.aspx) szabályozza. Az adatfeldolgozás helyéről tájékozódjon a Microsoft Online Services használati feltételei között található Adatfeldolgozási hely feltételei között. A Power BI megfelelőségi információival kapcsolatban az elsődleges forrás a [Microsoft Adatvédelmi központ](https://www.microsoft.com/trustcenter). A Power BI csapata keményen dolgozik azért, hogy az ügyfeleknek a legújabb innovációkat és termékeket nyújtsa. A Power BI jelenleg az [Office 365 megfelelőségi keretrendszerének](http://go.microsoft.com/fwlink/p/?LinkID=618494) D szintjén található.

Ez a cikk a Power BI biztonságát ismerteti. Ennek keretében bemutatja a Power BI-architektúrát, majd a felhasználói hitelesítést és az adatkapcsolatok létrehozását, végül pedig ismerteti, hogy a Power BI hogyan tárolja és mozgatja az adatokat a szolgáltatáson belül. Az utolsó szakasz biztonsággal kapcsolatos kérdéseket és válaszokat tartalmaz.

## <a name="power-bi-architecture"></a>A Power BI-architektúra

A **Power BI** szolgáltatás az **Azure**-ra épül, amely a Microsoft [felhőalapú számítástechnikai platformja](http://azure.microsoft.com/overview/what-is-azure/). A Power BI-t jelenleg a világ számos adatközpontjában alkalmazzák – számos aktív példány érhető el az adatközpontok régióinak ügyfelei számára, valamint ugyanennyi passzív példány, amelyek az aktív példányok biztonsági másolatait képezik.

Minden Power BI-példány két fürtből áll – egy webes előtérrendszer (**WFE-**) fürtből és egy **Back End-** fürtből. Ezeket a következő képen tekintheti meg, és a cikk további részének hátterét képezik. 

![A WFE és a Back End](media/whitepaper-powerbi-security/powerbi-security-whitepaper_01.png)

A Power BI az Azure Active Directoryval (**AAD**) végez fiókhitelesítést és -kezelést. A Power BI az **Azure Traffic Managert (ATM-et)** is használja arra, hogy a felhasználói forgalmat – a kapcsolódást megkísérlő ügyfél DNS-rekordja alapján – a legközelebbi adatközponthoz irányítsa a hitelesítési elvégzéséhez és statikus tartalom és fájlok letöltéséhez. A Power BI a szükséges statikus tartalmat és fájlokat az **Azure Content Delivery Network (CDN)** használatával osztja el hatékonyan a felhasználók között a földrajzi helyzet alapján.

### <a name="the-wfe-cluster"></a>A WFE-fürt

A **WFE**-fürt kezeli a kezdeti kapcsolódást és a Power BI hitelesítési folyamatát az AAD-val hitelesítve a felhasználókat, és hozzáférési jogkivonatokat ad ki a Power BI szolgáltatással való további felhasználói kapcsolatokhoz.

![A WFE-fürt](media/whitepaper-powerbi-security/powerbi-security-whitepaper_02.png)

Amikor a felhasználók megpróbálnak csatlakozni a Power BI szolgáltatáshoz, az ügyfél DNS-szolgáltatása az **Azure Traffic Managerrel** kommunikálva keresi meg a legközelebbi, Power BI-példánnyal rendelkező adatközpontot. További információ erről a folyamatról: [Az Azure Traffic Manager „Teljesítmény” forgalom-útválasztási módja](https://azure.microsoft.com/documentation/articles/traffic-manager-routing-methods/#performance-traffic-routing-method).

A felhasználóhoz legközelebbi WFE-fürt kezeli a bejelentkezési és hitelesítési műveletsort (amelyet a cikk későbbi szakaszaiban ismertetünk), majd egy AAD-tokent szolgáltat a felhasználónak a hitelesítést követően. A WFE-fürt ASP.NET összetevője elemzi a kérelmet, és meghatározza, hogy a felhasználó mely szervezethez tartozik, majd kommunikál a Power BI **globális szolgáltatásával**. A globális szolgáltatás egy minden WFE- és Back End-fürttel megosztott Azure-tábla, amely leképezi a felhasználókat és az ügyfélszervezeteket a Power BI-bérlőjüket tartalmazó adatközpontra. A WFE adja meg a böngésző számára, hogy mely Back End-fürt tartalmazza a szervezet bérlőjét. A felhasználó hitelesítését követően a rendszer további ügyfél-interakciókat végez közvetlenül a Back End-fürttel, amely kérelmekben nincs közvetítő szerepe a WFE-nek.

### <a name="the-power-bi-back-end-cluster"></a>A Power BI Back End-fürtje

A hitelesített ügyfelek a **Back End**-fürt által lépnek kapcsolatba a Power BI szolgáltatással. A **Back End**-fürt kezeli a vizualizációkat, a felhasználói irányítópultokat, adatkészleteket, jelentéseket, adattárolókat, adatkapcsolatokat, adatfrissítéseket és sok mást, ami együtt jár a Power BI szolgáltatás használatával.

![A Back End-fürt](media/whitepaper-powerbi-security/powerbi-security-whitepaper_03.png)

Az **átjárói szerepkör** átjáróként szolgál a felhasználói kérelmek és a Power BI szolgáltatás között. A felhasználók nem kerülnek közvetlen kapcsolatba más szerepkörrel, csak az átjárói szerepkörrel.

**Fontos:** Fontos tisztában lenni azzal, hogy a nyilvános interneten keresztül _csak_ az Azure API Management (**APIM**) és az Átjáró (**GW**) szerepkörök érhetők el. Ezek biztosítják a hitelesítést, az engedélyezést, a DDoS-védelmet, a szabályozást, a terheléselosztást, az útválasztást és más funkciókat.

A fenti ábrán a **Back End-** fürt képén lévő szaggatott vonal a felhasználók által egyedül elérhető két szerepkör (a szaggatott vonaltól balra) és a csak a rendszer által elérhető szerepkörök közötti határvonalat jelzi. Amikor egy hitelesített felhasználó a Power BI szolgáltatáshoz kapcsolódik, akkor a kapcsolatot és az ügyfél minden kérelmét az **átjárói szerepkör** és az **Azure API Management** fogadja és kezeli, amely aztán a felhasználó nevében használja a Power BI szolgáltatás többi elemét. Amikor egy ügyfél például egy irányítópultot próbál megtekinteni, az **átjárói szerepkör** fogadja a kérelmet, majd külön kérelmet küld a **bemutatási szerepkörnek**, hogy lekérje az adatokat, amelyekre a böngészőnek az irányítópult megjelenítéséhez szüksége van.

![Az átjárói szerepkör](media/whitepaper-powerbi-security/powerbi-security-whitepaper_04.png)

### <a name="power-bi-premium"></a>Power BI Premium

A **Power BI Premium** egy dedikált, kiépített és particionált szolgáltatás-munkaterületet kínál olyan előfizetőknek, akiknek dedikált erőforrásokra van szüksége a Power BI-tevékenységeikhez. Amikor egy ügyfél Power BI Premium-előfizetésre regisztrál, az **Azure Resource Manager** létrehozza a Premium kapacitást. Az előfizetés bevezetése egy, az előfizetés szintjével arányos virtuálisgép-készletet rendel a Power BI-bérlőt tartalmazó adatközponthoz (kivéve a multi-geo környezeteket, amelyekről később esik szó), amelyet **Azure Service Fabric**-példányként indít el.

![Power BI Premium](media/whitepaper-powerbi-security/powerbi-security-whitepaper_05.png)

A Premium fürt létrehozása után annak minden kommunikációja a Power BI Back End-fürtön halad át, ahol létrejön a kapcsolat az ügyfél dedikált, **Power BI Premium** előfizetésű virtuális gépeivel.

### <a name="data-storage-architecture"></a>Adattárolási architektúra

A Power BI két elsődleges adattárat használ adatok tárolására és kezelésére: A felhasználóktól feltöltött adatokat általában **Azure Blob**-tárolóra küldi, a metaadatokat és magának a rendszernek az összetevőit pedig egy tűzfal mögött, az **Azure SQL Database**-ben tárolja.

![Adattárolás](media/whitepaper-powerbi-security/powerbi-security-whitepaper_06.png)

Például amikor egy felhasználó egy Excel-munkafüzetet importál a Power BI szolgáltatásba, létrejön egy memóriabeli, táblázatos Analysis Services-adatbázis, amely az adatokat a memóriában tárolja legfeljebb egy óráig (vagy amíg a rendszer memóriaterhelést nem tapasztal). Az adatokat az **Azure Blob** Storage-nak is elküldi.

A felhasználók Power BI-előfizetéseivel kapcsolatos metaadatokat (például az irányítópultokat, jelentéseket, legutóbbi adatforrásokat, munkaterületeket, szervezeti adatokat, bérlői adatokat és egyéb metaadatokat) az **Azure SQL Database** tárolja és frissíti. Az Azure SQL Database minden tárolt adatot teljes mértékben titkosít az [Azure SQL transzparens adattitkosítási](https://msdn.microsoft.com/library/dn948096.aspx) (TDE) technológiával. Az Azure Blob Storage-ban tárolt adatok is titkosítva vannak. További információt az adatok beöltéséről, tárolásáról és áthelyezéséről az **Adatok tárolása és áthelyezése** című szakaszban találhat.

## <a name="tenant-creation"></a>Bérlőlétrehozás

A bérlő az Azure AD szolgáltatás egy dedikált példánya, amelyet a szervezetek megkapnak és a tulajdonukban áll, amikor regisztrálnak egy Microsoft-felhőszolgáltatásra, például az Azure, a Microsoft Intune, a Power BI vagy az Office 365 szolgáltatásra. Mindegyik Azure AD-bérlő önálló, és elkülönül a többi Azure AD-bérlőtől.

A bérlő a cég felhasználóit és a hozzájuk tartozó adatokat – a jelszavakat, a felhasználói profil adatait, az engedélyeket és hasonlókat – tárolja. Emellett a céghez és annak biztonságához kapcsolódó csoportokat, alkalmazásokat és egyéb adatokat is tartalmaz. További információ: [Az Azure AD-bérlő ismertetése](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).

A Power BI-bérlő az Azure Active Directoryban megadott országhoz (vagy régióhoz) és államhoz legközelebbi adatközpontban jön létre. Ezeket az adatokat az Office 365 vagy a Power BI szolgáltatás első kiépítésekor adhatta meg. A Power BI-bérlő ezután nem hagyja el a megadott adatközpontot.

### <a name="multiple-geographies-multi-geo---preview"></a>Több földrajzi hely (multi-geo) – előzetes verzió

Egyes szervezeteknek az üzleti igények alapján több földrajzi helyen vagy régióban is Power BI-jelenlétre van szükségük. Például előfordulhat, hogy egy cég Power BI-bérlője az Egyesült Államokban található, a cég azonban más földrajzi helyeken (például Ausztráliában) is végez üzletet, amihez Power BI-szolgáltatásokra és -adatokra van szüksége.  2018 második felétől az egy földrajzi helyen található bérlővel rendelkező szervezetek – megfelelő kiépítés mellett – más földrajzi helyen lévő Power BI-erőforrásokhoz is hozzáférhetnek. Ezt a funkciót az egyszerűség és a hivatkozások kedvéért a dokumentumban **multi-geónak** nevezzük.

Különböző földrajzi helyeken való működés közben észben kell tartani bizonyos technikai szempontokat. Ezeket ebben a dokumentumban tisztázzuk. Fontos szempontok:

- Egy távoli régióban tárolt, gyorsítótárazott lekérdezés inaktív állapotban marad a régióban, más átvitt adatok azonban oda-vissza mozoghatnak több földrajzi hely között.
- Egy távoli régió PBIX vagy XLSX formátumú, Power BI-ban közzétett jelentései esetenként egy másolattal vagy árnyékmásolattal rendelkeznek a Power BI Azure Blob Storage-tárolójában. Ilyen esetekben az Azure Storage Service Encryption (SSE) titkosítja az adatokat.
- Ha multi-Geo-környezetben adatot helyez át egy régióból egy másikba, az adatok eredeti helyén történő szemétgyűjtés 7–10 napon belül történik meg. Ez megsemmisíti az eredeti régióból áthelyezett adatok másolatát.

Az alábbi kép bemutatja, hogy a távoli, multi-geo környezettel rendelkező régió Power BI-szolgáltatásait hogyan irányítja át a rendszer a **Power BI Back End**-fürtön keresztül, amelyben létrejön a kapcsolat az ügyfél távoli Power BI-előfizetéséhez tartozó virtuális gépével.

![Multi-geo](media/whitepaper-powerbi-security/powerbi-security-whitepaper_07.png)

### <a name="datacenters-and-locales"></a>Adatközpontok és területi beállítások

A Power BI bizonyos régiókban érhető el, attól függően, hogy hol vannak üzemelő Power BI-fürtök a regionális adatközpontokban. A Microsoft tervezi, hogy további adatközpontokra is kiterjeszti a Power BI-infrastruktúrát.

A következő hivatkozásokra kattintva további információt kaphat az Azure adatközpontjairól.

- [Azure-régiók](http://azure.microsoft.com/regions/) – információ az Azure globális jelenlétéről és helyszíneiről
- [Azure-szolgáltatások régiók szerint](http://azure.microsoft.com/regions/#services) – az Azure a Microsofttól elérhető szolgáltatásainak (infrastruktúra-szolgáltatások és platformszolgáltatások egyaránt) teljes listája minden régióban.

A Power BI szolgáltatás jelenleg a következő régiókban érhető el, amelyeket a következő elsődleges adatközpontok szolgáltatnak:

- Egyesült Államok
  - USA keleti régiója
  - USA 2. keleti régiója
  - USA északi középső régiója
  - USA déli középső régiója
  - USA nyugati régiója
  - USA 2. nyugati régiója
- Kanada
  - Közép-Kanada
  - Kelet-Kanada
- Egyesült Királyság
  - Egyesült Királyság nyugati régiója
  - Egyesült Királyság déli régiója
- Brazília
  - Dél-Brazília
- Németország
  - Közép-Németország
  - Északkelet-Németország
- Európa
  - Észak-Európa
  - Nyugat-Európa
- Japán
  - Kelet-Japán
  - Nyugat-Japán
- India
  - Közép-India
  - Dél-India
  - Nyugat-India
- Kelet-Ázsia
  - Kelet-Ázsia
  - Délkelet-Ázsia
- Ausztrália
  - Kelet-Ausztrália
  - Délkelet-Ausztrália

A Microsoft önálló jogi személyek számára is biztosít adatközpontokat. A Power BI szolgáltatás szuverén felhőkben való elérhetőségéről a [Power BI szuverén felhőkről](https://powerbi.microsoft.com/clouds/) szóló oldalán tájékozódhat.

Adatai tárolási helyével és használatának módjáról a [Microsoft Adatvédelmi központban](https://www.microsoft.com/TrustCenter/Transparency/default.aspx#_You_know_where) talál további információt. Az inaktív ügyféladatok elhelyezésével kapcsolatos kötelezettségvállalások az **Adatfeldolgozási feltételek** vagy az [Online Microsoft-szolgáltatások feltételei](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=31) között vannak megadva.

## <a name="user-authentication"></a>Felhasználók hitelesítése

A Power BI szolgáltatásban a felhasználó hitelesítése a felhasználó böngészője és a Power BI szolgáltatás vagy a Power BI által használt Azure-szolgáltatások közötti kérések, válaszok és átirányítások sorozatából áll. Ez a műveletsor írja le a felhasználó Power BI-beli hitelesítésének folyamatát. A vállalati felhasználók számára választható hitelesítési (bejelentkezési) modellekről a [Bejelentkezési modell választása az Office 365-höz](https://blogs.office.com/2014/05/13/choosing-a-sign-in-model-for-office-365/) című cikkből tájékozódhat.

### <a name="authentication-sequence"></a>Hitelesítési műveletsor

A felhasználó Power BI szolgáltatásban történő hitelesítésnek műveletsora az alább ismertetett, ábrákkal illusztrált lépésekben zajlik.

1. A felhasználó egy böngészőből kezdeményezi a Power BI szolgáltatással való kapcsolatot azzal, hogy a címsorba begépeli a Power BI címét (például https://app.powerbi.com)), vagy hogy a _Bejelentkezés_ lehetőséget választja a Power BI kezdőlapján (https://powerbi.microsoft.com)). A kapcsolat TLS 1.2 és HTTPS használatával lesz létrehozva, és a böngésző és a Power BI szolgáltatás közötti minden további kommunikáció HTTPS-t használ. A kérés az **Azure Traffic Manager** felé lesz továbbítva.

2. Az **Azure Traffic Manager** a felhasználó DNS-rekordjának ellenőrzésével meghatározza a legközelebbi olyan adatközpontot, ahol a Power BI üzembe van helyezve, és annak a WFE-fürtnek az IP-címét adja meg válaszul a DNS-nek, amelyre a felhasználót irányítani kell.

3. A WFE (előtér-webkiszolgáló) ezután a Microsoft online szolgáltatásainak bejelentkezési oldalára irányítja a kiszolgálót.

    ![Hitelesítési műveletsor](media/whitepaper-powerbi-security/powerbi-security-whitepaper_08.png)

1. A felhasználó hitelesítését követően a bejelentkezési oldal a korábban meghatározott legközelebbi Power BI szolgáltatás **WFE-fürtjére** irányítja át a felhasználót.

2. A böngésző átad egy, a Microsoft Online szolgáltatások oldalára való sikeres bejelentkezéskor beszerzett cookie-t, amelyet a **WFE-fürtön** belüli **ASP.NET** szolgáltatás vizsgál meg.

3. A WFE-fürt az **Azure Active Directory** ( **AAD** ) szolgáltatással egyeztetve hitelesíti a felhasználó Power BI-szolgáltatás-előfizetését, és beszerez egy AAD-jogkivonatot. Amikor az AAD a felhasználó sikeres hitelesítésével válaszol, és visszaad egy AAD-jogkivonatot, a WFE-fürt a bérlők listáját és azok Power BI-háttérfürtjeinek helyét kezelő **Globális Power BI szolgáltatással** egyeztetve meghatározza a felhasználó bérlőjét tartalmazó Power BI szolgáltatásfürtöt. A WFE-fürt ezután ahhoz a Power BI-fürthöz irányítja a felhasználót, amelyen a bérlője elhelyezkedik, majd egyszerre több mindent ad vissza a felhasználó böngészőjének:


      - Az **AAD-jogkivonatot**
      - **A munkamenetadatokat**
      - Annak a **háttérfürtnek** a webcímét, amellyel a felhasználó kommunikálhat


1. A felhasználó böngészője ekkor a megadott Azure CDN-hez, bizonyos fájlok esetében pedig a WFE-hez fordulva letölti a böngészőnek a Power BI szolgáltatással való együttműködéséhez szükséges megadott közös fájlok gyűjteményét. A böngészőlap így a Power BI szolgáltatás böngésző-munkamenetének időtartamára tartalmazza az AAD-jogkivonatot, a munkamenetadatokat, a társított háttérfürt helyét, valamint az Azure CDN-ből és a WFE-fürtből letöltött fájlok gyűjteményét.

![Párbeszéd az Azure CDN-nel](media/whitepaper-powerbi-security/powerbi-security-whitepaper_09.png)

Ha ezek az elemek készen állnak, a böngésző kapcsolatot kezdeményez a megadott háttérfürttel, és megkezdődik a felhasználónak a Power BI szolgáltatással végzett tevékenysége. Ettől kezdve a Power BI szolgáltatáshoz irányuló összes hívás a megadott háttérfürttel történik, és minden hívás tartalmazza a felhasználó AAD-jogkivonatát. Az AAD-jogkivonat élettartama egy óra; ha a felhasználó munkamenete nyitva marad; a WFE a hozzáférés fenntartása érdekében rendszeresen frissíti a jogkivonatot.

## <a name="data-storage-and-movement"></a>Adatok tárolása és áthelyezése

A Power BI szolgáltatásban az adatok lehetnek _inaktívak_ (a Power BI-felhasználó számára elérhető adatok, amelyekkel éppen nem végez munkát) vagy _használatban lévők_ (például: éppen futtatott lekérdezések, éppen használt adatkapcsolatok és -modellek, a Power BI szolgáltatásba éppen feltöltött adatok és/vagy modellek, vagy más műveletek, amelyeket egy felhasználó vagy a Power BI szolgáltatás végez az aktívan elért és módosított adatokon). Az éppen használt adatokat _használatban lévő adatoknak_ nevezzük. Az inaktív adatok titkosítva vannak a Power BI-ban. Az átvitel alatt álló, vagyis a Power BI szolgáltatás által éppen küldött vagy fogadott adatok szintén titkosítottak.

A Power BI szolgáltatás az alapján is eltérően kezeli az adatokat, hogy azokhoz **DirectQuery** használatával lehet hozzáférni, vagy _nem_ lehet elérni őket DirectQueryvel. A felhasználói adatok tehát két kategóriába vannak sorolva a Power BI-ban: DirectQueryvel elért adatok, és DirectQueryvel nem elért adatok.

A **DirectQuery** olyan lekérdezés, amelyhez egy Power BI-felhasználó lekérdezése a Microsoft's Data Analysis Expressions (DAX) nyelvről – a Power BI és más Microsoft-termékek által lekérdezések létrehozására használt nyelv –, amely az adatforrás natív adatnyelvére (például T-SQL-re vagy más natív adatbázis-nyelvre) van lefordítva. A DirectQuery-lekérdezésekhez társított adatok csak hivatkozás alapján vannak tárolva, tehát amikor a DirectQuery nem aktív, a forrásadatok nincsenek a Power BI-ban tárolva (a vizualizációknak az irányítópultok és jelentések megjelenítéséhez használt adatait kivéve – a későbbi, a _Használatban lévő adatok (adatáthelyezés)_ című szakaszban leírtak szerint). Ehelyett a DirectQuery-adatokra való hivatkozások vannak tárolva, amelyek lehetővé teszik ezeknek az adatoknak az elérését a DirectQuery futtatásakor. Egy DirectQuery a lekérdezés futtatásához szükséges összes információt, így a kapcsolati sztringet és az adatforrások eléréséhez használt hitelesítő adatokat is tartalmazza, ezáltal a DirectQuery kapcsolódni tud a benne foglalt adatforrásokhoz az automatikus frissítéshez. DirectQuery használata esetén a DirectQuery-lekérdezésbe a mögöttes adatmodell információi is be vannak építve.

A DirectQuery-t **nem** használó lekérdezések olyan DAX-lekérdezések gyűjteményei, amelyek _nincsenek_ közvetlenül lefordítva egy mögöttes adatforrás natív nyelvére. A nem DirectQuery lekérdezések nem tartalmazzák a mögöttes adatokhoz tartozó hitelesítő adatokat, és a mögöttes adatok be vannak töltve a Power BI szolgáltatásba, kivéve a [Power BI Gateway](https://powerbi.microsoft.com/documentation/powerbi-gateway-enterprise/) szolgáltatáson keresztül elért helyszíni adatokat, amelyek esetében a lekérdezés csak a helyszíni adatokra való hivatkozásokat tárolja.

A DirectQuery és a más lekérdezések közötti megkülönböztetés határozza meg, hogyan kezeli a Power BI szolgáltatás az inaktív adatokat, és hogy maga a lekérdezés titkosítva van-e. A következő szakaszok az inaktív és mozgásban lévő adatokat írják le, valamint az adatok titkosítását, elhelyezkedését és kezelésük módját ismertetik.

### <a name="data-at-rest"></a>Inaktív adatok

Inaktív adatok esetén a Power BI szolgáltatás az alábbi alpontokban ismertetett módon tárolja az adathalmazokat, jelentéseket és irányítópult-csempéket. Korábban már volt szó arról, hogy a Power BI-ban az inaktív adatok titkosítva vannak. Az ETL betűszó az alábbiakban a kinyerés, az átalakítás és a betöltés (Extract, Transform and Load) műveleteket jelenti.

#### <a name="encryption-keys"></a>Titkosítási kulcsok

- Az Azure Blob-kulcsok titkosítási kulcsai titkosítva vannak tárolva egy Azure Key Vaultban.
- Az Azure SQL Database TDE (transzparens adattitkosítás) technológiájának titkosítási kulcsait maga az Azure SQL kezeli.
- A Data Movement (adatáthelyezési) szolgáltatás és a helyszíni adatátjáró titkosítási kulcsai a következő helyeken vannak tárolva:
  - Az ügyfél infrastruktúrájában a helyszíni adatátjáróban – helyszíni adatforrások esetén
  - Az adatáthelyezési szerepkörben – felhőalapú adatforrások esetén

A Windows Azure Blob Storage titkosításához használt tartalomtitkosítási kulcs (Content Encryption Key, CEK) egy véletlenszerűen generált 256-bites kulcs. A CEK által a tartalom titkosításához használt algoritmus az AES\_CBC\_256.

A CEK titkosításához ezután használt kulcstitkosítási kulcs (Key Encryption Key, KEK) egy előre definiált 256-bites kulcs. A KEK által a CEK titkosításához használt algoritmus az A256KW.

A helyreállítási kulcson alapuló átjárótitkosítási kulcsok sohasem hagyják el a helyszíni infrastruktúrát. A Power BI nem fér hozzá a titkosított helyszíni hitelesítő adatok értékeihez, és nem tudja elfogni őket; a webes ügyfelek által a hitelesítő adatok titkosításához használt nyilvános kulcs ahhoz az adott átjáróhoz való, amellyel éppen kommunikál.

Felhőalapú adatforrások esetén az adatáthelyezési szerepkör [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) (mindig titkosított) metódusokkal titkosítja a titkosítási kulcsokat. További információ az [Always Encrypted adatbázis-funkcióról](https://msdn.microsoft.com/library/mt163865.aspx).

#### <a name="datasets"></a>Adathalmazok

1. Metaadatok (táblák, oszlopok, mértékek, számítások, kapcsolati sztringek stb.)
      
    a. Helyszíni Analysis Services esetén a szolgáltatásban semmi sincs tárolva az adott, az Azure SQL-ben titkosítva tárolt adatbázisra mutató hivatkozáson kívül.
 
    b. Az ETL, a DirectQuery és a Push Data összes többi metaadata titkosítva van és Azure Blob-tárolóban van tárolva.

1. Az eredeti adatforrásokhoz való hitelesítő adatok
  
      a. Helyszíni Analysis Services – Hitelesítő adatokra nincs szükség, ezért nincsenek tárolt hitelesítő adatok.

      b. DirectQuery – Attól függ, hogy a modellt közvetlenül a szolgáltatásban hozták-e létre, amely esetben azt a rendszer a kapcsolati sztringben tárolja, és az Azure Blobban titkosítja, ha pedig a modellt a Power BI Desktopból importálták, a titkosított hitelesítő adatokat az adatáthelyezési erőforrás Azure SQL Database szolgáltatása tárolja. A titkosítási kulcsot az átjárót futtató számítógép tárolja az ügyfél infrastruktúráján.

      c. Leküldéses adatok – Nem alkalmazható

      d. ETL

      - A **Salesforce**, illetve a **OneDrive** esetében a titkosított frissítési jogkivonatokat a Power BI-szolgáltatás Azure SQL Database szolgáltatása tárolja.
      - Egyéb esetben:
        - Ha az adatkészlet frissítésre van konfigurálva, a hitelesítő adatokat az adatáthelyezési erőforrás Azure SQL Database szolgáltatása tárolja. A titkosítási kulcsot az átjárót futtató számítógép tárolja az ügyfél infrastruktúráján.
        - Ha az adatkészlet nincsen frissítésre konfigurálva, a rendszer nem tárol hitelesítő adatokat az adatforrásokhoz

1. Adatok

    a. Helyszíni Analysis Services és DirectQuery – semmi nincs tárolva a Power BI-szolgáltatásban.

    b. ETL – titkosítva az Azure Blob-tárolóban, de jelenleg a Power BI-szolgáltatások által használt Azure Blob-tároló [Azure Storage Service Encryption (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) titkosítást, másnéven kiszolgálóoldali titkosítást használ. A Multi-geo is SSE-t használ.

    c. Leküldéses adat 1. verzió – Azure Blob-tárolóban titkosítva tárolva, de jelenleg a Power BI-szolgáltatásokban használt Azure Blob-tároló [Azure Storage Service Encryption (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) titkosítást, másnéven kiszolgálóoldali titkosítást használ. A Multi-geo is SSE-t használ.

    d. Leküldéses adat 2. verzió – titkosítva tárolva az Azure SQL-ben.

A Power BI a titkosítás ügyféloldali megközelítését alkalmazza, és az Azure Blob-tároló titkosításához cipher block chaining (CBC) módú advanced encryption standard (AES) titkosítást használ. További információ az [ügyféloldali titkosítással kapcsolatban](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/).

A Power BI a következő módon biztosítja az adatok adatintegritási monitorozását:

* Az Azure SQL-ben tárolt inaktív adatok esetében a Power BI az SQL-ben natív módon elérhető dbcc, transzparens adattitkosítás és konstans lap-ellenőrzőösszeg funkciókat alkalmazza.

* Az Azure Blob-tárolóban tárolt inaktív adatok esetében a Power BI ügyféloldali titkosítást és HTTPS protokollt használ az adatok tárba való átviteléhez, és a lekérést követően adatintegritás-ellenőrzést is végrehajt rajtuk. Itt többet is megtudhat [az Azure Blob-tároló biztonsági megoldásairól](https://azure.microsoft.com/documentation/articles/storage-security-guide/).

#### <a name="reports"></a>Jelentések

1. Metaadatok (jelentésdefiníció)

   a. A jelentések lehetnek Office 365-höz készült Excel-, illetve Power BI-jelentések. Az alábbiak érvényesek a metaadatokra a jelentés típusától függően:

       a. Excel Report metadata is stored encrypted in SQL Azure. Metadata is also stored in Office 365.
       
       b. Power BI reports are stored encrypted in Azure SQL database.

2. Statikus adatok

   A statikus adatok közé tartoznak az olyan összetevők, mint a háttérképek és az egyéni vizualizációk.

    a. Az Office 365-höz készült Excel esetében semmit nem tárol a rendszer.

    b. A Power BI-jelentések esetében a statikus adatok titkosítva vannak tárolva az Azure Blob-tárolóban.

3. Gyorsítótárak a. Az Office 365-höz készült Excel-jelentések esetében semmit nem gyorsítótáraz a rendszer.

    b. A Power BI-jelentések esetében a megjelenített vizualizációk adatainak gyorsítótárazása titkosítva történik az Azure SQL Database szolgáltatásban.
 

4. A Power BI-ban közzétett eredeti Power BI Desktop (.pbix) vagy Excel (.xlsx) fájlok

    Előfordulhat, hogy az .xlsx- vagy .pbix-fájlok másolatát, vagy árnyékmásolatát a rendszer eltárolja a Power BI Azure Blob-tárolójában; ebben az esetben az adatokat titkosítva tárolja. Minden ilyen a Power BI-szolgáltatás Azure Blob-tárolójában tárolt jelentés [Azure Storage Service Encryption (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) titkosítást, másnéven kiszolgálóoldali titkosítást használ. A Multi-geo is SSE-t használ.

#### <a name="dashboards-and-dashboard-tiles"></a>Irányítópultok és irányítópult-csempék

1. Gyorsítótárak – Az irányítópultok vizualizációihoz szükséges adatok általában az Azure SQL Database szolgáltatásban vannak titkosítva gyorsítótárazva és tárolva. Más csempéket, mint például az Excelből vagy SQL Server Reporting Services-ből (SSRS) kitűzött vizualizációkat a rendszer kép formájában, szintén titkosítva tárolja az Azure Blobban.

2. Statikus adatok – ide tartoznak az olyan összetevők, mint a háttérképek és az egyéni vizualizációk, ezeket a rendszer az Azure Blob-tárolóban titkosítva tárolja.

Az alkalmazott titkosítási módszertől függetlenül, az ügyfelek nevében a Microsoft a kulcstitkosítás felügyeletéhez vagy egy titkoskód-tárolót, vagy az Azure Key Vaultot használja.

### <a name="data-transiently-stored-on-non-volatile-devices"></a>Permanens eszközökön tárolt ideiglenes adatok

A következők a permanens eszközökön tárolt ideiglenes adatokra vonatkoznak.

#### <a name="datasets"></a>Adathalmazok

1. Metaadatok (táblák, oszlopok, mértékek, számítások, kapcsolati sztringek stb.)

2. Előfordulhat, hogy néhány sémához kapcsolódó összetevőt a rendszer korlátozott ideig a számítási csomópont merevlemezén tárol. Ezenkívül előfordul, hogy a rendszer néhány összetevőt korlátozott ideig az Azure Redis Cache-ben titkosítatlanul tárol.

3. Az eredeti adatforrásokhoz való hitelesítő adatok

    a. Helyszíni Analysis Services – a rendszer semmit nem tárol

    b. DirectQuery – Attól függ, hogy a modellt közvetlenül a szolgáltatásban hozták-e létre, amely esetben azt a rendszer a kapcsolati sztringben tárolja titkosított formában, a titkosítási kulcsot pedig ugyanitt egyszerű szöveges formában tárolja (a titkosított adat mellett), ha pedig a modellt a Power BI Desktopból importálták, permanens eszközökön a rendszer nem tárolja a hitelesítő adatokat.

    c. Leküldéses adatok – Nincs (nem alkalmazható)

    d. ETL – nincs (a rendszer semmit sem tárol a számítási csomóponton, minden az **Inaktív adatok** szekcióban fentebb leírtak szerint történik)
4. Adatok

    Előfordulhat, hogy néhány adatösszetevőt a rendszer korlátozott ideig a számítási csomópont merevlemezén tárol.

### <a name="data-in-process"></a>Feldolgozás alatt álló adatok

Az adatok akkor tekinthetők feldolgozás alatt állónak, ha azokat a felhasználó aktívan használja, vagy azokhoz aktívan hozzáfér. Például, az adatok feldolgozás alatt állónak tekinthetők, amikor a felhasználó megnyitja az adatkészletet, javítja vagy módosítja az irányítópultot vagy jelentést, vagy amikor frissítés, vagy más adatelérési tevékenység történik. Amikor bekövetkezik ezen események bármelyike, és az adat feldolgozás alá kerül, az **Adatszerepkör** a Power BI szolgáltatásban létrehoz egy Analysis Services-adatbázist (AS-adatbázis) a memóriában, és ebbe tölti be az adatkészletet. Függetlenül attól, hogy az adatkészlet DirectQuery-n alapszik-e, az AS-adatbázis nincsen titkosítva, hogy az **Adatszerepkör** hozzáférhessen, és a memóriában tárolódik mindaddig, amíg a Power BI szolgáltatásnak már nincs szüksége az adatkészletre. A Power BI Premium-előfizetéssel rendelkező ügyfelek esetén a Power BI a memórián belüli Analysis Services-adatbázist (AS-adatbázis) az ügyfél számára elkülönített Power BI-virtuálisgépek gyűjteményében hozza létre.

Amint az adatok használtba vannak véve, beleértve azt is, hogy betöltik őket a Power BI-ba, előfordulhat, hogy a Power BI szolgáltatás a vizualizációs adatokat egy titkosított **Azure SQL Database** típusú adatbázisban tárolja, függetlenül attól, hogy az adatbázis DirectQuery-n alapszik-e.

A használatba vett adatok adatintegritásának monitorozásához a Power BI a HTTPS, TCP/IP és TLS protokollokat használja annak érdekében, hogy biztosítsa az adatok titkosítását és az adatintegritás megőrzését adattovábbítás közben is.

## <a name="user-authentication-to-data-sources"></a>Az adatforrások felhasználói hitelesítése

Mindegyik adatforrás esetén, a felhasználó egy, a saját bejelentkezési adatain alapuló kapcsolatot hoz létre, és ezeket a hitelesítő adatokat használja az adatokhoz való hozzáféréshez. A felhasználók a mögöttes adatok alapján lekérdezéseket, irányítópultokat és jelentéseket készíthetnek.

Amikor a felhasználó megosztja a lekérdezést, irányítópultot, jelentést vagy bármelyik vizualizációt, az ezekhez az adatokhoz vagy vizualizációkhoz való hozzáférés annak függvénye, hogy az alapul szolgáló adatforrások támogatják-e a szerepkörszintű biztonságot (RLS).

Ha az alapul szolgáló adatforrás támogatja a **Power BI **** szerepkörszintű biztonság funkcióját (RLS)**, a Power BI szolgáltatás alkalmazni fogja a megfelelő szerepkörszintű biztonságot, és azok a felhasználók, akik nem rendelkeznek az alapul szolgáló adatokhoz való hozzáféréshez szükséges hitelesítő adatokkal (mely hozzáférés lehet egy irányítópultban vagy más adatösszetevőben használt lekérdezés), nem fogják látni azokat az adatokat, amelyekhez nem rendelkeznek jogosultsággal. Ha a felhasználó alapul szolgáló adatokhoz való hozzáférése eltér az irányítópultot vagy jelentést létrehozó felhasználóétól, a vizualizációk és egyéb összetevők csak a felhasználó hozzáférési szintjének megfelelő adatokat fogják megjeleníteni.

Ha az adatforrás **nem** használ RLS-t, az alapul szolgáló adatforráshoz való hozzáférés a Power BI-bejelentkezés hitelesítő adatai alapján történik, illetve, ha kapcsolódás közben más hitelesítő adatokat adnak meg, akkor azok alapján. Amikor egy felhasználó RLS-t nem használó adatforrásból tölt adatokat a Power BI szolgáltatásba, az adatokat a Power BI a dokumentum **Adattárolás és továbbítás** szakaszában leírtak szerint tárolja. Az RLS-t nem használó adatforrások esetében az adatok más felhasználókkal történő megosztásakor (például amikor irányítópult vagy jelentés használatával osztják meg őket), illetve adatfrissítéskor, az adatokhoz való hozzáféréshez, vagy azok megjelenítéséhez az eredeti hitelesítő adatokat használja a rendszer.

![Szerepkörszintű biztonság (RLS)](media/whitepaper-powerbi-security/powerbi-security-whitepaper_10.png)

Az RLS-t használó és nem használó adatforrások összehasonlításához példaként képzeljük el, hogy Sam létrehoz egy jelentést és egy irányítópultot, majd megosztja őket Abby-vel és Ralph-al. Ha a jelentésben és az irányítópulton használt adatforrások **nem** támogatják az RLS-t, Abby és Ralph látni fogja az összes adatot, amit Sam az irányítópultba felvett (amelyet feltöltött a Power BI szolgáltatásba), továbbá Abby és Ralph az összes adatot kezelheti is. Ezzel szemben, ha Sam a jelentést és az irányítópultot olyan adatforrások használatával hozza létre, amelyek támogatják az RLS-t, majd ezután megosztja azt Abby-vel és Ralph-al, a következő fog történni, amikor Abby megpróbálja megtekinteni az irányítópultot:

1. Mivel az irányítópult RLS-t használó adatforráson alapul, az irányítópult vizualizációi rövid időre a &quot;betöltés&quot; üzenetet fogják megjeleníteni, miközben a Power BI szolgáltatás lekérdezést küld az adatforrás felé, hogy lekérje az irányítópult mögöttes lekérdezésére vonatkozó kapcsolati sztringben megadott jelenlegi adatkészletet.

2. Az adatokhoz Abby a hitelesítő adatai és szerepköre alapján fér hozzá, és a rendszer csak azokat az adatokat tölti be az irányítópultba és a jelentésbe, amelyek eléréséhez megfelelő engedélyekkel rendelkezik.

3. Az irányítópult és a jelentés vizualizációi Abby szerepkörszintjének megfelelően jelennek meg.

Amikor Ralph nyitja meg az irányítópultot vagy jelentést, ugyanez a folyamat játszódik le az ő szerepkörszintjének megfelelően.

## <a name="power-bi-and-expressroute"></a>A Power BI és az ExpressRoute

A Power BI és az ExpressRoute használatával egyéni privát kapcsolatot hozhat létre a vállalat és a Power BI között (vagy egy internetszolgáltató együttes elhelyezési létesítményét használva), így megkerülheti az internetet, és nagyobb védelmet biztosíthat Power BI-beli bizalmas adatai és kapcsolatai számára.

Az ExpressRoute egy olyan Azure-szolgáltatás, amellyel privát kapcsolatokat hozhat létre az Azure-adatközpontok (ahol a Power BI is található) és helyszíni infrastruktúrája között, illetve az Azure-adatközpontok és együttes elhelyezési környezete között. További információt [A Power BI és az ExpressRoute](https://powerbi.microsoft.com/documentation/powerbi-admin-power-bi-expressroute/) című cikkben talál.

## <a name="power-bi-mobile"></a>Power BI Mobile

A Power BI Mobile a három elsődleges mobilplatformhoz készült alkalmazások gyűjteménye: Android, iOS és Windows Mobile. A Power BI Mobile alkalmazásainak biztonsági megfontolásai két kategóriába sorolhatók:

* Eszközkommunikáció
* Az eszközön található alkalmazás és adatok

Az **eszközkommunikáció** esetén minden Power BI Mobile-alkalmazás kommunikál a Power BI szolgáltatással, és a böngészők által is használt kapcsolati és hitelesítési műveletsorokat alkalmazza. Ezeket a tanulmány korábbi szakaszaiban ismertettük. Az iOS és az Android rendszerű Power BI-mobilalkalmazások az alkalmazáson belül nyitnak meg egy böngészőablakot, míg a Windows rendszerű mobilalkalmazás egy közvetítő segítségével hoz létre egy kommunikációs csatornát a Power BI-hoz.

Az alábbi táblázat a Power BI Mobile tanúsítványalapú hitelesítésének (CBA) támogatását listázza mobileszközplatform szerint:

| **CBA-támogatás** | **iOS** | **Android** | **Windows** |
| --- | --- | --- | --- |
| **Power BI** (bejelentkezés a szolgáltatásba) | támogatott | támogatott | Nem támogatott |
| **SSRS ADFS** (csatlakozás az SSRS-kiszolgálóhoz) | Nem támogatott | Támogatott | Nem támogatott |

A Power BI Mobile-alkalmazások aktívan kommunikálnak a Power BI szolgáltatással. A szolgáltatás telemetrikai adatokkal gyűjt használati statisztikákat és hasonló adatokat, amelyeket használatot és egyéb tevékenységeket monitorozó szolgáltatásoknak továbbít. Ezek nem tartalmaznak személyes azonosításra alkalmas információkat (PII-t).

A Power BI **eszközön található alkalmazása** az alkalmazás használatát elősegítő eszközön tárolja az adatokat:

* Az Azure Active Directory- és frissítési tokenek az eszköz egy biztonságos mechanizmusában tárolódnak, amely iparági szabványnak megfelelő biztonsági intézkedéseket alkalmaz.

* Az eszköz tárhelye gyorsítótárazza az adatokat, amelyet nem titkosít az alkalmazás

* Az eszköz titkosítás nélkül tárolja a beállításokat is, azonban valós felhasználói adatokat nem.

A Power BI Mobile adatgyorsítótára két hétig marad az eszközön, vagy a következő események egyikéig: az alkalmazás eltávolítása; a felhasználó kijelentkezése a Power BI Mobile-ból; a felhasználó nem jelentkezik be (például lejár a token vagy megváltozik a jelszó). Az adatgyorsítótár tartalmazza a Power BI Mobile alkalmazásban korábban megnyitott irányítópultokat és jelentéseket.

A Power BI Mobile-alkalmazások nem vizsgálják a mappákat az eszközön. [További információ az offline adatokról a Power BI Mobile-alkalmazásokban](https://powerbi.microsoft.com/documentation/powerbi-mobile-offline-android/).

A Power BI Mobile mindhárom elérhető platformja támogatja a Microsoft Intune-t, amely egy mobileszköz- és alkalmazáskezelési szoftverszolgáltatás. Az Intune engedélyezésével és konfigurálásával a mobileszköz adatai titkosítva vannak, a Power BI alkalmazás pedig nem telepíthető SD-kártyákra. [További információ a Microsoft Intune-ról](http://www.microsoft.com/cloud-platform/microsoft-intune).

## <a name="power-bi-security-questions-and-answers"></a>Power BI – biztonsággal kapcsolatos kérdések és válaszok

Az alábbiak Power BI-jal kapcsolatos gyakori biztonsági kérdések, valamint azok válaszai. Ezeket a tanulmányhoz való hozzáadás ideje szerint rendeztük, így a tanulmány frissítésekor könnyen megtalálhatja az új kérdéseket és válaszokat. A legújabb kérdések a lista végére kerülnek.

**Hogyan csatlakoznak a felhasználók a Power BI-ban az adatforrásokhoz, illetve hogyan férhetnek hozzájuk?**

* **Power BI-hitelesítő adatok és tartományi hitelesítő adatok:** A felhasználók egy e-mail-címmel jelentkeznek be a Power BI szolgáltatásba. Amikor egy felhasználó megpróbál egy adatforráshoz csatlakozni, a Power BI a hozzá használt e-mail-címet adja meg hitelesítő adatként. Tartományhoz csatlakozó (helyszíni vagy felhőalapú) erőforrások esetén a bejelentkezési e-mail-címhez egy _egyszerű felhasználónevet_ ([UPN-t](https://msdn.microsoft.com/library/windows/desktop/aa380525(v=vs.85).aspx)) is társít a címtárszolgáltatás, amellyel meghatározza, hogy megfelelőek-e a hitelesítő adatok a hozzáféréshez. A Power BI-ba való bejelentkezéshez munkahelyi e-mail-címeket (ugyanazt az e-mail-címet, mint amelyet munkahelyi erőforrások eléréséhez használnak, például _david@contoso.com_) használó szervezetek esetén a leképezés gördülékeny. Az olyan szervezetek esetén, amelyek nem munkahelyi e-mail-címeket használnak (például _david@contoso.onmicrosoft.com_), címtárleképezést kell alkalmazni, hogy a felhasználók Power BI-hitelesítő adatokkal hozzáférést kaphassanak a helyszíni erőforrásokhoz.

* **SQL Server Analysis Services és a Power BI:** Helyszíni SQL Server Analysis Servicest használó szervezetek a Power BI helyszíni adatátjáróját (a korábbi szakaszokban **átjáró**) használhatják.  A Power BI helyszíni adatátjárója szerepkörszintű biztonságot (RLS-t) képes kényszeríteni az adatforrásokon. További információt az RLS-ről a dokumentum korábbi, **Az adatforrások felhasználói hitelesítése** című szakaszában találhat. Emellett egy részletes cikket is elolvashat a [Power BI Gatewayről](https://powerbi.microsoft.com/documentation/powerbi-gateway-enterprise/).

  A szervezetek az **egyszeri bejelentkezéshez** (SSO-hoz) a Kerberost is használhatják, amellyel zökkenőmentesen csatlakozhatnak a Power BI-ból a helyszíni adatforrásokhoz, például az SQL Serverhez, az SAP HANA-hoz és a Teradatához. További információ és a konkrét konfigurációs követelmények: [**A Kerberos használata a Power BI-ból a helyszíni adatforrásokba történő egyszeri bejelentkezéshez (SSO)**](https://docs.microsoft.com/power-bi/service-gateway-kerberos-for-sso-pbi-to-on-premises-data).

* **Nem tartományi kapcsolatok**: A nem tartományhoz kapcsolódó, RLS-t biztosítani képtelen adatkapcsolatok esetén a felhasználónak a kapcsolódási műveletsor során kell megadnia a hitelesítő adatokat, amelyeket a Power BI ezután továbbít az adatforrásnak a kapcsolat létrehozásához. Ha megfelelőek az engedélyek, az adatok betöltődnek az adatforrásból a Power BI szolgáltatásba.

**Hogyan helyezhetők át az adatok a Power BI-ba?**

* A Power BI által kért és közvetített adatok átvitel közben HTTPS protokollal vannak titkosítva az adatforrás és a Power BI szolgáltatás összekapcsolása között. A rendszer biztonságos kapcsolatot hoz létre az adatszolgáltatóval, és csak ezután indítja meg az adatátvitelt.

**Hogyan gyorsítótárazza a Power a jelentések, irányítópultok és modellek adatait? Ez a folyamat megbízható?**

* Egy adatforrás használatakor a Power BI szolgáltatás a dokumentum korábbi, **Adatok tárolása és áthelyezése** című szakaszában ismertetett eljárást követi.

**Az ügyfelek helyben gyorsítótárazzák a weblapadatokat?**

* Amikor a böngészőügyfelek megnyitják a Power BI-t, annak webkiszolgálói a _Cache-Control_ direktívát _no-store_ beállításra állítják. A _no-store_ direktíva arra utasítja a böngészőket, hogy ne gyorsítótárazzák a felhasználó által megtekintett weblapot, és ne tárolják a weblapot az ügyfél gyorsítótárában.

**Mi a helyzet a szerepkör alapú biztonsággal, a jelentések és irányítópultok megosztásával, valamint az adatkapcsolatokkal? Hogyan működnek ezek a funkciók az adathozzáférés, az irányítópultok megtekintése és a jelentés-hozzáférés és -frissítés szempontjából?**

* A **nem szerepkör szintű biztonsággal (RLS)** rendelkező adatforrások esetén ha valaki a Power BI-on keresztül megoszt egy irányítópultot jelentést vagy adatmodellt más felhasználókkal, az adatok elérhetővé válnak ezen további felhasználók számára. A Power BI *nem* hitelesíti újra a felhasználókat az eredeti adatforráshoz. Miután az adatok feltöltődtek a Power BI-ba, az adatforrást hitelesítő felhasználó felelős azok megtekintési jogosultságaiért.

  Amikor **RLS**-kompatibilis adatforrásokhoz (például egy Analysis Services-adatforráshoz) jönnek létre adatkapcsolatok, a Power BI csak az irányítópult adatait gyorsítótárazza. Minden alkalommal, amikor valaki a Power BI-ban megtekint vagy megnyit egy RLS-kompatibilis adatforrásból származó jelentést vagy adatkészletet, a Power BI szolgáltatás lekéri az adatokat az adatforrásból a felhasználó hitelesítő adatai alapján, majd ha a felhasználó megfelelő engedélyekkel rendelkezik, betölti számára az adatokat a jelentésbe vagy az adatmodellbe. Ha a hitelesítés nem sikerül, a felhasználó hibaüzenetet kap.

  További információt a dokumentum korábbi, **Felhasználói hitelesítés az adatforrásokhoz** című szakaszában találhat.

**A felhasználók bármikor csatlakozhatnak ugyanazokhoz az adatforrásokhoz, amelyek némelyike a tartományi hitelesítő adatoktól eltérő hitelesítő adatokat követel meg. Hogyan kerülhetik el, hogy ne kelljen minden alkalommal megadniuk ezeket a hitelesítő adatokat, amikor létrehoznak egy adatkapcsolatot?**

* A Power BI [Power BI Personal Gateway](https://support.powerbi.com/knowledgebase/articles/649846) funkciója lehetővé teszi a felhasználók számára, hogy több különböző adatforráshoz hozzanak létre hitelesítő adatokat, amelyeket automatikusan használhatnak az adatforrások ismételt megnyitásakor. További információ: [Power BI Personal Gateway](https://support.powerbi.com/knowledgebase/articles/649846).

**Hogyan működnek a Power BI-csoportok?**

* A Power BI-csoportokkal a felhasználók gyorsan és könnyen, saját csapatokban működhetnek együtt irányítópultok, jelentések és adatmodellek létrehozásán. Ha például egy olyan Power BI-csoportja van, amely a közvetlen csapatának minden tagját tartalmazza, könnyen együttműködhet velük, ha kiválasztja a Csoport elemet a Power BI-ban. A Power BI-csoportok egyenértékűek az Office 365 univerzális csoportjaival (amelyeket itt [ismerhet meg](https://support.office.com/Article/Find-help-about-Groups-in-Office-365-7a9b321f-b76a-4d53-b98b-a2b0b7946de1), [hozhat létre](https://support.office.com/Article/View-create-and-delete-Groups-in-the-Office-365-admin-center-a6360120-2fc4-46af-b105-6a04dc5461c7) és [kezelhet](https://support.office.com/Article/Manage-Group-membership-in-the-Office-365-admin-center-e186d224-a324-4afa-8300-0e4fc0c3000a)), és az Azure Active Directoryval megegyező hitelesítési mechanizmusokat alkalmazzák. [Létrehozhat csoportokat a Power BI-ban](https://support.powerbi.com/knowledgebase/articles/654250), vagy egy univerzális csoportot az Office 365 felügyeleti központjában – a Power BI-beli csoportalkotás szempontjából mindkettőnek ugyanaz az eredménye.

  A Power BI-csoportokkal megosztott adatokra ugyanazok a biztonsági megfontolások vonatkoznak, mint a Power BI-ban megosztott bármilyen más adatokra. **Nem RLS**-kompatibilis adatforrások esetén a Power BI **nem** hitelesíti újra a felhasználókat az eredeti adatforráshoz. Miután az adatok feltöltődtek a Power BI-ba, az adatforrást hitelesítő felhasználó felelős azok megtekintési jogosultságaiért. További információt a dokumentum korábbi, **Felhasználói hitelesítés az adatforrásokhoz** című szakaszában találhat.

  További információ a [Power BI-csoportokról](https://support.powerbi.com/knowledgebase/articles/654247).

**Milyen portokat használ a helyszíni adatátjáró és a személyes adatátjáró? Vannak bizonyos tartománynevek, amelyeket a könnyebb csatlakozáshoz engedélyezni kell?**

* Erre a kérdésre a részletes válasz a következő hivatkozáson érhető el: [https://powerbi.microsoft.com/documentation/powerbi-gateway-enterprise](https://powerbi.microsoft.com/documentation/powerbi-gateway-enterprise)

**Hogyan kell használni a helyreállítási kulcsokat a helyszíni adatátjáróban, és hol tárolja ezeket a rendszer? Mi a helyzet a biztonságos hitelesítőadat-kezeléssel?**

* Az átjárók telepítése és konfigurálása során a rendszergazda egy átjáró **helyreállítási kulcsában** gépel. A **helyreállítási kulccsal** két, még erősebb típusú kulcskészlet hozható létre:

  - Egy **RSA** aszimmetrikus kulcs
  - Egy **AES** aszimmetrikus kulcs

  Ezek a létrehozott kulcsok (**RSA** és **AES**) a helyi számítógépen egyik fájljában találhatók. Ez a fájl titkosítva van. A fájl tartalmát csak ez a Windows-gép fejtheti vissza, és csak ezzel az átjárószolgáltatás-fiókkal.

  Amikor egy felhasználó megadja az adatforrás hitelesítő adatait a Power BI szolgáltatás felületén, a rendszer a böngészőben titkosítja ezeket a nyilvános kulccsal. Az átjáró újra titkosítja a már titkosított hitelesítő adatokat egy AES aszimmetrikus kulccsal, mielőtt a Power BI-ba kerülnének. A Power BI szolgáltatás így soha nem fér hozzá a titkosítatlan adatokhoz.

**Milyen kommunikációs protokollokat alkalmaz a helyszíni adatátjáró, és hogyan biztosítja ezeket?**

* Az átjáró a következő két kommunikációs protokollt támogatja:

  - **AMQP 1.0 – TCP + TLS** : Ehhez a protokollhoz a következő portokat kell megnyitni a kimenő kommunikációhoz: 443, 5671–5672 és 9350–9354. Az átjáró ezt a protokollt részesíti előnyben, mivel ennek kisebb a kommunikációs terhelése.

  - **HTTPS – WebSocket és HTTPS + TLS** : Ez a protokoll csak a 443-as portot használja. A WebSocketet egyetlen HTTP CONNECT üzenet indítja el. A csatorna létrejötte után a kommunikáció gyakorlatilag kizárólag TCP+TLS. Ha az átjárót ezen protokoll használatára szeretné kényszeríteni, ahhoz módosítania kell egy beállítást [a helyszíni átjáróról szóló cikk](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/) útmutatása szerint.

**Mi az Azure CDN szerepe a Power BI-ban?**

* Ahogyan korábban említettük, a Power BI a szükséges statikus tartalmat és fájlokat az **Azure Content Delivery Network** (CDN) használatával osztja el hatékonyan a felhasználók között a földrajzi helyzet alapján. Pontosabban, a Power BI szolgáltatás több **CDN-t** használ ahhoz, hogy a szükséges statikus tartalmakat és fájlokat a felhasználók számára hatékonyan oszthassa el a nyilvános interneten keresztül. A statikus fájlok között megtalálhatók termékek letöltési fájljai (például a **Power BI Desktop**, a **helyszíni adatátjáró** vagy a különböző független szolgáltatóktól származó Power BI-alkalmazások), böngészőkonfigurációs fájlok, amelyek a Power BI szolgáltatás felé irányuló egymást követő kapcsolatok kezdeményezésére és kialakításához szükségesek, illetve megtalálható a Power BI kezdeti biztonságos bejelentkezési oldala is.

  Egy kezdeti Power BI-kapcsolatból származó információ alapján a felhasználó böngészője a megadott Azure **CDN**-hez, bizonyos fájlok esetében pedig a **WFE**-hez fordulva letölti a böngészőnek a Power BI szolgáltatással való együttműködéséhez szükséges megadott közös fájlok gyűjteményét. A böngészőlap így a Power BI szolgáltatás böngésző-munkamenetének időtartamára tartalmazza az AAD-jogkivonatot, a munkamenetadatokat, a társított **háttérfürt** helyét, valamint az Azure **CDN**-ből és a **WFE**-fürtből letöltött fájlok gyűjteményét.

**Egyéni vizualizációknál elvégzi-e a Microsoft az egyéni vizualizációkód biztonsági vagy adatvédelmi kiértékelését a Katalógusban való közzététel előtt?**

* Nem. Az ügyfél felelős az egyéni vizualizáció kódjának átvizsgálásáért és annak megállapításáért, hogy az megbízható-e. Minden egyéni vizualizáció kódja tesztkörnyezetben van működtetve, hogy egy egyéni vizualizáció esetleg hibás kódja ne lehessen káros hatással a Power BI szolgáltatás egészére.

**Léteznek más Power BI-vizualizációk, amelyek információt küldenek az ügyfélhálózaton kívülre?**

* Igen. A Bing Térképek és az ESRI-vizualizációk a Power BI szolgáltatáson kívülre küldenek adatokat az ezeket a szolgáltatásokat felhasználó vizualizációk esetén. További információk mellett a Power BI-on kívüli bérlői adatforgalom részletes leírását is megtalálja [**A Power BI és az ExpressRoute**](https://powerbi.microsoft.com/documentation/powerbi-admin-power-bi-expressroute/) ismertetésében.

**Mi a helyzet az adatok elkülönítésével? Üzembe helyezhetjük a bérlőket megadott földrajzi helyen lévő adatközpontokban, hogy az adatok ne kerülhessenek az országhatáron túlra?**

* Egyes ügyfeleknek bizonyos földrajzi helyeken lehetősége van bérlőt létrehozni egy szuverén felhőben, ahol az adatok tárolása és feldolgozása minden más adatközponttól elkülönítve történik. A szuverén felhők némileg eltérő biztonsággal rendelkeznek, mivel a szuverén felhő Power BI szolgáltatását külön adatkezelő működteti a Microsoft nevében.

  Az ügyfelek úgy is dönthetnek, hogy egy adott régióban állítanak be bérlőt, az ilyen bérlőknek azonban nem lesz a Microsofttól elkülönített adatkezelője. A szuverén felhők díjszabása eltér az általánosan elérhető kereskedelmi Power BI szolgáltatásétól. A Power BI szolgáltatás szuverén felhőkben való elérhetőségéről a [Power BI szuverén felhőkről](https://powerbi.microsoft.com/clouds/) szóló oldalán tájékozódhat.

**Hogyan kezeli a Microsoft a Power BI Premium-előfizetésekkel rendelkező ügyfelek kapcsolatait? Mások ezek a kapcsolatok, mint a nem prémium szintű Power BI szolgáltatáshoz létrehozottak?**

* A Power BI Premium-előfizetésekkel rendelkező ügyfelek számára létrehozott kapcsolatok [Azure Business-to-Business (B2B)](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) hitelesítési eljárást alkalmaznak, Azure Active Directory (AD) használatával lehetővé téve a hozzáférés-vezérlést és a hitelesítést. A Power BI Premium-előfizetők és a Power BI Premium-erőforrások közötti kapcsolatokat a Power BI ugyanúgy kezeli, mint minden más Azure AD-felhasználót.

## <a name="conclusion"></a>Összegzés

A Power BI szolgáltatás architektúrája két fürtön alapul – a webes előtérrendszer (WFE-) fürtön és a háttérbeli fürtön. A WFE-fürt feladata a kezdeti kapcsolódás és a Power BI szolgáltatásba történő hitelesítés, hitelesítés után pedig a Back End kezeli a további felhasználói tevékenységeket. A Power BI a felhasználói identitásokat az Azure Active Directory (AAD) használatával tárolja és kezeli, az adatok és metaadatok tárolását pedig az Azure Blob, illetve az Azure SQL Database használatával kezeli.

A Power BI-beli adattárolás és adatfeldolgozás más az alapján, hogy az adatok elérése DirectQuery használatával történik-e, és attól is függ, hogy az adatforrások a felhőben vannak-e, vagy helyszíniek. A Power BI szerepkörszintű biztonság (RLS) érvényre juttatására is képes, és együttműködik a helyszíni adatokhoz hozzáférést biztosító átjárókkal.

## <a name="feedback-and-suggestions"></a>Visszajelzések és javaslatok

Visszajelzéseit nagyra értékeljük. Szívesen fogadjuk a tanulmány vagy a Power BI-jal kapcsolatos más tartalom javítására, bővítésére vagy egyértelműbbé tételére vonatkozó javaslatait. Javaslatait a következő címre küldheti: [pbidocfeedback@microsoft.com](mailto:pbidocfeedback@microsoft.com).

## <a name="additional-resources"></a>További források

A Power BI-ról az alábbi forrásanyagokban talál további információt.

- [Csoportok a Power BI-ban](https://support.powerbi.com/knowledgebase/articles/654247)
- [Első lépések a Power BI Desktopban](https://support.powerbi.com/knowledgebase/articles/471664)
- [Power BI Gateway](https://powerbi.microsoft.com/documentation/powerbi-gateway-enterprise/)
- [Power BI REST API – Áttekintés](https://msdn.microsoft.com/library/dn877544.aspx)
- [A Power BI API referenciája](https://msdn.microsoft.com/library/mt147898.aspx)
- [Helyszíni adatátjáró](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
- [A Power BI és az ExpressRoute](https://powerbi.microsoft.com/documentation/powerbi-admin-power-bi-expressroute/)
- [Power BI szuverén felhők](https://powerbi.microsoft.com/clouds/)
- [Power BI Premium](https://aka.ms/pbipremiumwhitepaper)
- [A Kerberos használata a Power BI-ból a helyszíni adatforrásokba történő egyszeri bejelentkezéshez (SSO)](https://docs.microsoft.com/power-bi/service-gateway-kerberos-for-sso-pbi-to-on-premises-data)