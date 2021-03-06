---
title: 'Többoldalas jelentések a Power BI-ban: Gyakori kérdések'
description: Ez a cikk a lapszámozott jelentésekkel kapcsolatos gyakori kérdésekre ad választ. Ezek a jelentések magas szinten formázott, tökéletesen pontos jelentések, amelyek nyomtatáshoz vagy PDF-készítéshez vannak optimalizálva.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: report-builder
ms.topic: conceptual
ms.date: 04/29/2020
ms.openlocfilehash: 0089a38c852d82acaebc8cab0f0fb653c6a304cb
ms.sourcegitcommit: a72567f26c1653c25f7730fab6210cd011343707
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83565626"
---
# <a name="paginated-reports-in-power-bi-faq"></a>Többoldalas jelentések a Power BI-ban: Gyakori kérdések 

Ez a cikk a lapszámozott jelentésekkel kapcsolatos gyakori kérdésekre ad választ. Ezek a jelentések magas szinten formázott, tökéletesen pontos jelentések, amelyek nyomtatáshoz vagy PDF-készítéshez vannak optimalizálva. Lapszámozottnak hívjuk őket, mert több oldalon megjeleníthetők. A lapszámozott jelentések az SQL Server Reporting Services RDL-jelentéseinek technológiáján alapulnak. 

Ez a cikk számos, a Power BI Premium lapszámozott jelentéseivel, valamint a Jelentéskészítővel (a lapszámozott jelentések készítéséhez használt különálló eszközzel) kapcsolatos gyakori kérdést megválaszol. A szolgáltatásban csak Power BI Pro-licenccel tehet közzé jelentéseket. Oldalakra osztott jelentéseket a Saját munkaterületen vagy a munkaterületeken tehet közzé, ha az adott munkaterület egy Power BI Premium-kapacitáshoz tartozik. 

## <a name="administration"></a>Felügyelet

### <a name="what-size-premium-capacity-do-i-need-for-paginated-reports"></a>Milyen méretű Prémium szintű kapacitás szükséges a lapszámozott jelentésekhez?

A lapszámozott jelentések számítási feladatai a P1–P3 termékváltozatokon érhetők el.  Beágyazási vagy tesztelési/fejlesztési helyzetekben az A4–A6 termékváltozatokkal is használható.

### <a name="what-is-the-maximum-memory-threshold-i-can-put-for-paginated-reports-in-my-capacity"></a>Mi a kapacitásom lapszámozott jelentéseihez megadható maximális memóriaküszöb?

A memóriának akár 100%-át is felhasználhatja ehhez a számítási feladathoz.

### <a name="how-does-user-access-work-for-paginated-reports"></a>Hogyan működik a felhasználói hozzáférés lapszámozott jelentések esetén?

A lapszámozott jelentések felhasználói hozzáférése megegyezik a Power BI szolgáltatás minden egyéb tartalmának felhasználói hozzáférésével 

### <a name="how-do-i-turn-onoff-my-paginated-reports-workload"></a>Hogyan kapcsolhatom be és ki a lapszámozott jelentések számítási feladatát?

A kapacitás-rendszergazda engedélyezheti vagy letilthatja a lapszámozott jelentések számítási feladatait a kapacitás-rendszergazdai portálon.  A számítási feladat alapértelmezés szerint az összes létrehozott új kapacitáshoz be lesz kapcsolva, de az első többoldalas jelentés feltöltéséig nem használ memóriát.  

### <a name="how-can-i-monitor-usage-of-paginated-reports-in-my-tenant"></a>Hogyan tudom monitorozni a bérlőm lapszámozott jelentéseinek használatát?

Az auditnaplók a részletesen tartalmazzák ennek a jelentéstípusnak a használatát a következő eseményeknél:

- Power BI-jelentés megtekintése
- Power BI-jelentés törlése
- Power BI-jelentés létrehozása
- Letöltött Power BI-jelentés

A ReportType mező „PaginatedReport” értéke megkülönbözteti a lapszámozott jelentéseket a Power BI-jelentésektől.

A naplók továbbá a következő eseményeket teszik elérhetővé a lapszámozott jelentésekhez:

- Power BI-adatkészlet kötése egy átjáróhoz
- Power BI-adatforrás feltárása
- TakeOverDatasource (Adatforrás átvétele)

### <a name="can-i-monitor-this-workload-through-the-premium-capacity-monitoring-app"></a>Figyelhetem a számítási feladatot a Prémium szintű kapacitás Monitoring Appjával?

Igen, a monitoring új lapként elérhető ugyanazokkal a releváns információkkal, amelyek az Power BI-adatkészleteknél is elérhetőek.

### <a name="do-i-need-a-pro-license-to-create-and-publish-paginated-reports"></a>Pro-licencre van szükségem lapszámozott jelentések létrehozásához és közzétételéhez?

Lapszámozott jelentéseket Pro-licenc nélkül is feltölthet a saját munkaterületére, ha az prémium szintű kapacitásban van.  Más munkaterületek esetén Pro-licenccel kell rendelkeznie, hogy tartalmat készítsen és tegyen közzé bennük. Ajánljuk, hogy Pro-licenc nélkül is töltse le és használja a Power BI Jelentéskészítőt, de a létrehozott lapszámozott jelentéseket így nem tudja közzétenni. 

### <a name="what-if-i-have-a-paginated-report-in-a-workspace-and-the-paginated-report-workload-is-turned-off"></a>Mi történik, ha van egy lapszámozott jelentésem egy munkaterületen, és a lapszámozott jelentés számítási feladata ki van kapcsolva?

Hibaüzenetet kap, a jelentést pedig nem tekintheti meg, amíg be nem kapcsolja a számítási feladatot. A jelentés továbbra is törölhető a munkaterületről.

### <a name="what-is-the-default-memory-for-each-of-the-premium-skus-that-support-paginated-reports"></a>Mennyi a lapszámozott jelentéseket támogató Prémium termékváltozatok alapértelmezett memóriája?

A lapszámozott jelentéseket támogató Prémium termékváltozatok alapértelmezett memóriája:

- **P1/A4**: Alapértelmezés szerint 20%; minimum 10%
- **P2/A5**: Alapértelmezés szerint 20%; minimum 5%
- **P3/A6**: Alapértelmezés szerint 20%; minimum 2,5%

A Power BI-bérlők rendszergazdái a Felügyeleti portálon módosíthatják a maximális memória alapértelmezett százalékos arányát. Tekintse meg a **Többoldalas jelentések** számítási feladatának szakaszát a **Power BI Premium** területen a **Kapacitás beállításai** lapon.

:::image type="content" source="media/paginated-reports-faq/paginated-reports-capacity-settings.png" alt-text="Többoldalas jelentések kapacitásának beállításai lap":::

## <a name="general"></a>Általános

### <a name="when-should-i-use-a-paginated-report-vs-a-power-bi-report"></a>Mikor érdemes lapszámozott, illetve Power BI-jelentést használnom?

A lapszámozott jelentések olyan forgatókönyvekhez ideálisak, amelyek magas szinten formázott, tökéletesen pontos jelentéseket igényelnek, amelyek nyomtatáshoz vagy PDF-készítéshez vannak optimalizálva.  Erre jó példa lehet egy havi eredménybeszámoló.  

A Power BI-jelentések áttekintéshez és interaktivitáshoz tökéletesek.  Például egy Power BI-jelentés a legmegfelelőbb választás egy olyan értékesítési jelentés esetében, amelyben különböző értékesítők saját régiójuk/iparáguk/ügyfeleik szerint szeretnék szeletelni ugyanazon jelentés adatait, és megtekinteni, hogyan változnak a számok.

További információ: [Többoldalas jelentések használata a Power BI-ban](../guidance/report-paginated-or-power-bi.md).

### <a name="the-documentation-says-power-bi-report-builder-is-the-preferred-authoring-tool-can-i-create-paginated-reports-in-sql-server-data-tools-for-power-bi"></a>A dokumentáció szerint a Power BI Jelentéskészítő az előnyben részesített jelentéskészítő eszköz. Létrehozhatok lapszámozott jelentéseket az SQL Server Data Tools for Power BI szolgáltatással is?

Igen, azonban a Power BI szolgáltatással egyszerre csak egy elem tölthető fel, így számos SQL Server Data Tools- (SSDT-) forgatókönyve még nem támogatott. A [nem támogatott funkciók teljes listáját](#what-paginated-report-features-in-ssrs-arent-yet-supported-in-power-bi) a gyakori kérdések későbbi egy szakaszában tekintheti meg.  

### <a name="what-versions-of-report-builder-do-you-support"></a>A Jelentéskészítő mely verziói támogatottak?

A Power BI Jelentéskészítőt a lapszámozott jelentések Power BI szolgáltatásban való elkészítésének elsődleges eszközeként adtuk ki. [A Power BI Jelentéskészítő telepítése a Microsoft letöltőközpontból](https://go.microsoft.com/fwlink/?linkid=2086513).

### <a name="how-do-i-move-existing-reports-i-have-saved-in-sql-server-reporting-services-to-power-bi"></a>Hogyan helyezhetek át meglévő mentett jelentéseket az SQL Server Reporting Servicesből a Power BI-ba?

Egy projekt a GitHubon mostantól támogatja a tartalom SQL Server Reporting Services-ből Power BI-ból való migrálását.  Itt talál további részleteket és töltheti le az eszközt: [https://github.com/microsoft/RdlMigration](https://github.com/microsoft/RdlMigration)

### <a name="can-i-open-reports-and-publish-directly-to-the-service"></a>Megnyithatok jelentéseket, majd közzétehetem őket közvetlenül a szolgáltatásban?

Igen. Támogatni kezdtük a jelentések megnyitását és közvetlenül a szolgáltatásba való közzétételét a Power BI Jelentéskészítőből.

### <a name="what-paginated-report-features-in-ssrs-arent-yet-supported-in-power-bi"></a>Az SSRS mely lapszámozott jelentéssekkel kapcsolatos funkciói nem támogatottak még a Power BI-ban?

A lapszámozott jelentések jelenleg a következő elemeket nem támogatják:

- Megosztott adatforrások
- Megosztott adathalmazok
- Részletezés és átkattintás más jelentésekbe
- Csatolt jelentések
- Egyéni betűtípusok

Ha egy nem támogatott funkcióval rendelkező fájlt próbál meg feltölteni a Power BI szolgáltatásba, hibaüzenetet kap egy átváltás/rendezés elem helyett.

### <a name="what-data-sources-do-you-support-currently-for-paginated-reports"></a>Milyen adatforrásokat támogatnak jelenleg a lapszámozott jelentések?

Az adatforrások listáját [A Power BI többoldalas jelentéseihez használható támogatott adatforrások](paginated-reports-data-sources.md) című cikkben találhatja meg. 

### <a name="what-authentication-methods-do-you-support"></a>Milyen hitelesítési módszerek támogatottak?

Az egyszeri bejelentkezést az Azure Analysis Services, az Azure SQL Database és a Power BI-adatforrások esetén támogatjuk.  Az Azure SQL Database és az Azure Analysis Services esetén az OAuth szolgáltatást is támogatjuk.  Más adatforrások esetén egyelőre tárolnia kell az adatforráshoz tartozó felhasználónevet és jelszót a portálon vagy az átjárón.  

### <a name="can-i-use-a-power-bi-dataset-as-a-data-source-for-my-paginated-report"></a>Használhatok Power BI-adatkészletet a lapszámozott jelentés adatforrásaként?

Igen, támogatjuk a Power BI-adatkészletek többoldalas jelentések adatforrásaiként való használatát.

### <a name="can-i-use-stored-procedures-through-the-gateway"></a>Használhatok tárolt eljárásokat az átjárón keresztül?

Igen, a tárolt eljárások átjárón keresztüli használata támogatott az SQL Server-adatforrásokhoz, beleértve a paramétereket használókat is.

### <a name="what-export-formats-are-available-for-my-report-in-the-power-bi-service"></a>Milyen exportálási formátumokat használhatok a jelentéshez a Power BI szolgáltatásban?

Microsoft Excel, Microsoft Word, Microsoft PowerPoint, PDF, .CSV, XML, és MHTML formátumokban exportálhat.

### <a name="can-i-print-paginated-reports"></a>Nyomtathatok lapszámozott jelentéseket?

Igen, nyomtatás is lehetséges a lapszámozott jelentéseknél, és egy új, továbbfejlesztett előnézet is használható. 

### <a name="are-e-mail-subscriptions-available-for-paginated-reports"></a>Léteznek e-mailes feliratkozások a többoldalas jelentésekhez?

Igen, az e-mail-feliratkozások teljes mértékben támogatottak a lapszámozott jelentésekre, és ehhez hat különböző fájlformátum és paraméterérték támogatása is járul.

### <a name="can-i-run-custom-code-in-my-report"></a>Futtathatok egyéni kódot a jelentésben?

Igen, az SSRS-hez hasonlóan itt is támogatjuk kódok futtatását.

### <a name="can-i-use-power-bi-embedded-to-embed-my-paginated-reports-into-an-app-im-hosting"></a>Használhatom a Power BI Embedded szolgáltatást lapszámozott jelentések egy általam üzemeltetett alkalmazásba történő beágyazásához?

Már elérhető a SaaS-beágyazás, beleértve a biztonságos beágyazás támogatását. A PaaS-beágyazás elsajátításához tekintse meg a [Lapszámozott Power BI-jelentések beágyazása egy alkalmazásba az ügyfelek számára](../developer/embedded/embed-paginated-reports-customers.md) című oktatóanyagot.

### <a name="can-i-drill-through-from-a-power-bi-report-to-a-paginated-report"></a>Végezhetek részletezést egy Power BI-jelentésből egy lapszámozott jelentésbe?

Igen, ez úgy valósítható meg, hogy URL-paramétereket használ a többoldalas jelentésekhez.

### <a name="can-i-share-my-paginated-report-content-through-a-power-bi-app"></a>Megoszthatom a lapszámozott jelentésem tartalmát egy Power BI-alkalmazáson keresztül?

Igen, a lapszámozott jelentések alkalmazásokkal való üzembe helyezése v1 és v2 munkaterületekről is támogatott. 

### <a name="will-other-report-specific-features-in-power-bi-like-pinning-to-report-tiles-to-dashboards-work-with-paginated-reports"></a>A Power BI más jelentésspecifikus funkciói – például az irányítópultok jelentéscsempéin való rögzítés – is működnek a lapszámozott jelentésekkel?

Terveink szerint a jelentések ugyanazokat a főbb szolgáltatásbeli forgatókönyveket fogják támogatni.  Ideális esetben – ügyfélszempontból – ezeknek ugyanolyan jelentésként kell majd megjelenniük a portálon, még ha a szerkesztésükre szolgáló eszköz más is. Számukra nem fontos, hogyan jött létre a jelentés, amíg a feladatát ellátja.  Ezen funkcióparitás jó példája a megjegyzések támogatásának terve. Bár a funkció kissé eltérő módon működik minden jelentéstípus esetén, mindkettőhöz hozzáfűzhet megjegyzéseket.

### <a name="is-there-a-report-viewer-control-for-paginated-reports-in-the-power-bi-service"></a>Létezik jelentésmegjelenítő vezérlőelem a Power BI szolgáltatásban a lapszámozott jelentésekhez?

Nem, jelentésmegjelenítő vezérlőelem jelenleg nem érhető el.

### <a name="can-you-search-for-paginated-reports-from-the-new-home-experience-in-the-power-bi-service"></a>Kereshetek lapszámozott jelentéseket a Power BI szolgáltatás új kezdőlapján?

Igen, már kereshet lapszámozott jelentésekre a kezdőlapról.  Ezeket az új kezdőlap egyéb területein is láthatja.

## <a name="considerations-and-troubleshooting"></a>Megfontolandó szempontok és hibaelhárítás
A többoldalas jelentésekben használt DateTime mezőkkel végzett munka során figyelembe kell venni a következőt.

- A DateTime-paraméterekre jelenleg globalizációs korlátozások érvényesek. A Power BI szolgáltatásban minden DateTime-paraméter az USA-beli formátumban (HH/NN/ÉÉÉÉ) van betöltve, függetlenül attól, hogy hogyan tervezi meg a Power BI Jelentéskészítőben.

## <a name="next-steps"></a>Következő lépések

- [A Power BI Jelentéskészítő telepítése a Microsoft letöltőközpontból](https://go.microsoft.com/fwlink/?linkid=2086513)
- [Oktatóanyag: Lapszámozott jelentés létrehozása](paginated-reports-quickstart-aw.md)
