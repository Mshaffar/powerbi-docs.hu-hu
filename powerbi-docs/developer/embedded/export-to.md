---
title: API Power BI-jelentések exportálásához
description: Útmutató beágyazott Power BI-jelentés exportálásához
author: KesemSharabi
ms.author: kesharab
ms.topic: conceptual
ms.service: powerbi
ms.subservice: powerbi-developer
ms.date: 03/24/2020
ms.openlocfilehash: 1d51c16502d3217e0158add2126d0b5726d87ff1
ms.sourcegitcommit: bfc2baf862aade6873501566f13c744efdd146f3
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83144708"
---
# <a name="export-power-bi-report-to-file-preview"></a>Power BI-jelentés exportálása fájlba (előzetes verzió)

Az `exportToFile` API lehetővé tesz a Power BI-jelentések exportálását REST-hívással. A támogatott fájlformátumok a következők:
* **.pptx** (PowerPoint)
* **.pdf**
* **.png**
    * .png-be való exportáláskor a többoldalas jelentések egy .zip-fájlba lesznek tömörítve
    * A tömörített fájlban minden fájl egy jelentésoldalnak felel meg
    * Az oldalnevek a [Get Pages](https://docs.microsoft.com/rest/api/power-bi/reports/getpages) vagy a [Get Pages in Group](https://docs.microsoft.com/rest/api/power-bi/reports/getpagesingroup) API visszatérési értékeivel egyeznek meg

## <a name="usage-examples"></a>Használati példák

Az exportálási funkció többféleképpen is felhasználható. Bemutatunk néhány példát:

* **Küldés nyomtatóra gomb** – Létrehozhat egy gombot az alkalmazásban, amely kattintásra elindít egy exportálási feladatot. A feladat .pdf vagy .pptx formátumban exportálhatja a megtekintett jelentést, és amikor az elkészül, a felhasználó letöltheti a fájlt. Könyvjelzők használatával egy meghatározott állapotban exportálhatja a jelentést, a konfigurált szűrőkkel, szeletelőkkel és más beállításokkal. Mivel az API aszinkron, a fájlok esetleg csak valamivel később lesznek elérhetők.

* **E-mail-melléklet** – Automatikusan e-mailt küldhet a beállított időközökkel, egy ahhoz mellékelt .pdf-jelentéssel. Ez a megoldás hasznos például akkor, ha automatizálni szeretné a vezetőknek küldött heti jelentést.

## <a name="using-the-api"></a>Az API használata

Az API használatba vétele előtt ellenőrizze, hogy engedélyezve vannak az alábbi [rendszergazdai bérlő-beállítások](../../admin/service-admin-portal.md#tenant-settings):
* **Jelentések exportálása PowerPoint-bemutatóként vagy PDF-dokumentumként** – Alapértelmezés szerint engedélyezett.
* **Jelentések exportálása képfájlokként** – Csak a *.png* formátumhoz szükséges, és alapértelmezés szerint le van tiltva.

Az API aszinkron. Az [exportToFile](https://docs.microsoft.com/rest/api/power-bi/reports/exporttofile) API a meghívásakor egy exportálási feladatot indít el. Az exportálási feladat elindítása után [ciklikus lekérdezéssel](https://docs.microsoft.com/rest/api/power-bi/reports/getexporttofilestatus) követi nyomon a feladatot annak befejezéséig.

A ciklikus lekérdezés során az API egy számot ad vissza, amely az elvégzett munka mennyiségét tükrözi. Az egyes exportálási feladatok munkája a jelentés oldalainak száma alapján vagy kiszámítva. Minden oldal azonos súllyal van figyelembe véve. Ha például egy 10 oldalas jelentést exportál, és a ciklikus lekérdezés a 70 értéket adja vissza, az azt jelenti, hogy az API a 10 oldalból hetet dolgozott fel az exportálási feladatban.

Amikor az exportálás befejeződik, a ciklikus lekérdezést végző API egy [Power BI URL-címet](https://docs.microsoft.com/rest/api/power-bi/reports/getfileofexporttofile) ad vissza a fájl eléréséhez. Az URL-cím 24 órán át érhető el.

## <a name="supported-features"></a>Támogatott funkciók

### <a name="selecting-which-pages-to-print"></a>A nyomtatandó oldalak kijelölése

Megadhatja a [Get Pages](https://docs.microsoft.com/rest/api/power-bi/reports/getpages) vagy a [Get Pages in Group](https://docs.microsoft.com/rest/api/power-bi/reports/getpagesingroup) visszatérési érték alapján kinyomtatni kívánt oldalakat. Az exportált oldalak sorrendje is megadható.

### <a name="bookmarks"></a>Könyvjelzők

 Az `exportToFile` API használatával programozottan is exportálhat jelentést egy megadott állapotban, a szűrő alkalmazása után. Ez a [Könyvjelzők](../../consumer/end-user-bookmarks.md) képesség használatával oldható meg. Egy jelentés könyvjelzők használatával történő exportálásához használja a [Bookmarks JavaScript-API-t](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Bookmarks).

 A könyvjelző `capturedBookmark.state` metódusával például a jelentés egy adott felhasználó által végrehajtott módosításait rögzítheti, majd exportálhatja azt az aktuális állapotában.

A [személyes könyvjelzők](../../consumer/end-user-bookmarks.md#personal-bookmarks) és az [állandó szűrők](https://powerbi.microsoft.com/blog/announcing-persistent-filters-in-the-service/) nem támogatottak.

### <a name="authentication"></a>Hitelesítés

A hitelesítést felhasználó (vagy fő felhasználó) vagy egy [egyszerű szolgáltatásnév](embed-service-principal.md) használatával is elvégezheti.

### <a name="row-level-security-rls"></a>Sorszintű biztonság (RLS)

[Sorszintű biztonság (RLS)](embedded-row-level-security.md) használatával úgy exportálhat jelentést, hogy az csak a bizonyos felhasználók számára látható adatokat jelenítse meg. Ha például regionális szerepkörökkel definiált jelentést exportál, programozottan szűrheti a jelentést úgy, hogy csak egy adott régiót jelenítsen meg.

Az RLS használatával végzett exportálsához rendelkeznie kell az alábbi engedélyekkel:
* Írási és újramegosztási engedély az adathalmazra, amelyhez a jelentés csatlakozik
* Ha a jelentés 1. verziójú munkaterületen van, a munkaterület rendszergazdájának kell lennie
* Ha a jelentés 2. verziójú munkaterületen van, a munkaterület tagjának vagy rendszergazdájának kell lennie

### <a name="data-protection"></a>Adatvédelem

A .pdf és a .pptx formátum támogatja a [bizalmassági címkék](../../admin/service-security-data-protection-overview.md#sensitivity-labels-in-power-bi) használatát. Ha bizalmassági címkével ellátott jelentést exportál .pdf vagy .pptx formátumba, az exportált fájl a bizalmassági címkével jeleníti meg a jelentést.

A bizalmassági címkével rendelkező jelentések nem exportálhatók .pdf- vagy .pptx-fájlba [egyszerű szolgáltatásnév](embed-service-principal.md) használatával.

### <a name="localization"></a>Honosítás

Az `exportToFile` API használatakor átadhatja a kívánt területi beállításokat. A területi beállítások befolyásolják a jelentés megjelenítésének módját, például a formátumoknak a választott helynek megfelelő módosításával.

## <a name="concurrent-requests"></a>Egyidejű kérések

Az `exportToFile` támogatja az exportálási feladatokra vonatkozó egyidejű kéréseket. Az alábbi táblázat mutatja be, hogy hány feladat futtatható egyszerre attól a termékváltozattól (SKU) függően, amelyben a jelentés megtalálható. Az egyidejű kérések a jelentésoldalakra vonatkoznak. Például egy 20 oldalas jelentésre vonatkozó kérés az A6 termékváltozatban egyidejűleg lesz feldolgozva. Ez nagyjából ugyanannyi ideig tart, mintha 20, egyenként egyoldalas exportálási kérést küldött volna el.

Az egyidejű kérések számát meghaladó feladatok sem lesznek megszakítva. Ha például három oldalt exportál az A1 termékváltozatban, az első feladat fog futni, a másik kettő pedig várakozik a következő két végrehajtási ciklusig.

|Azure SKU  |Office SKU  |Egyidejű jelentésoldalak maximális száma  |
|-----------|------------|-----------|
|A1         |EM1         |1          |
|A2         |EM2         |2          |
|A3         |EM3         |3          |
|A4         |P1          |6          |
|A5         |P2          |12         |
|A6         |P3          |24         |

## <a name="limitations"></a>Korlátozások

* Az exportálni kívánt jelentésnek Premium vagy Embedded kapacitásban kell lennie.
* Az exportálni kívánt jelentés adathalmazának Premium vagy Embedded kapacitásban kell lennie.
* Nyilvános előzetes verzió esetében az óránként exportált Power BI-jelentésoldalak száma kapacitásonként 50-re van korlátozva.
* Az exportált jelentések fájlmérete nem haladhatja meg a 250 MB-ot.
* .png-be exportálás esetén a bizalmassági címkék nem támogatottak.
* A bizalmassági címkével rendelkező jelentések nem exportálhatók .pdf- vagy .pptx-fájlba [egyszerű szolgáltatásnév](embed-service-principal.md) használatával.
* Az egy exportált jelentésbe foglalható oldalak száma legfeljebb 30. Ha a jelentés több oldalból áll, az API hibát jelez, és az exportálási feladat megszakad.
* A [személyes könyvjelzők](../../consumer/end-user-bookmarks.md#personal-bookmarks) és az [állandó szűrők](https://powerbi.microsoft.com/blog/announcing-persistent-filters-in-the-service/) nem támogatottak.
* A szuverén felhők nem támogatottak.
* Az alábbiakban felsorolt Power BI-vizualizációk nem támogatottak. Ilyen vizualizációt tartalmazó jelentés exportálásakor a jelentésnek az ezen vizualizációkat tartalmazó része helyett hibajelzés lesz megjelenítve.
    * Nem minősített Power BI-vizualizációk
    * R vizualizációk
    * PowerApps
    * Python-vizualizációk
    * Visio

## <a name="code-examples"></a>Kódpéldák

Exportálási feladat létrehozásakor három lépést kell végrehajtania:

1. Exportálási kérés küldése.
2. Ciklikus lekérdezés.
3. A fájl lekérése.

Ez a szakasz erre a három lépésre mutat be példát.

### <a name="step-1---sending-an-export-request"></a>1\. lépés – exportálási kérés küldése

Az első lépés egy exportálási kérés elküldése. Ebben a példában egy adott oldalra vonatkozó exportálási kérés van elküldve.

```csharp
/////// Export sample ///////
private async Task<string> PostExportRequest(
    Guid reportId,
    Guid groupId,
    FileFormat format,
    IList<string> pageNames = null /* Get the page names from the GetPages API */)
{
    var powerBIReportExportConfiguration = new PowerBIReportExportConfiguration
    {
        Settings = new ExportReportSettings
        {
            Locale = "en-us",
        },
        // Note that page names differ from the page display names.
        // To get the page names use the GetPages API.
        Pages = pageNames?.Select(pn => new ExportReportPage(Name = pn)).ToList(),
    };
    var exportRequest = new ExportReportRequest
    {
        Format = format,
        PowerBIReportConfiguration = powerBIReportExportConfiguration,
    };
    var export = await Client.Reports.ExportToFileInGroupAsync(groupId, reportId, exportRequest);
    // Save the export ID, you'll need it for polling and getting the exported file
    return export.Id;
}
```

### <a name="step-2---polling"></a>2\. lépés – ciklikus lekérdezés

Egy exportálási kérés elküldése után ciklikus lekérdezéssel állapíthatja meg, hogy elkészült-e a várt exportált fájl.

```csharp
private async Task<Export> PollExportRequest(
    Guid reportId,
    Guid groupId,
    string exportId /* Get from the ExportToAsync response */,
    int timeOutInMinutes,
    CancellationToken token)
{
    Export exportStatus = null;
    DateTime startTime = DateTime.UtcNow;
    const int c_secToMillisec = 1000;
    do
    {
        if (DateTime.UtcNow.Subtract(startTime).TotalMinutes > timeOutInMinutes || token.IsCancellationRequested)
        {
            // Error handling for timeout and cancellations 
            return null;
        }
        var httpMessage = await Client.Reports.GetExportToFileStatusInGroupWithHttpMessagesAsync(groupId, reportId, exportId);
        exportStatus = httpMessage.Body;
        // You can track the export progress using the PercentComplete that's part of the response
        SomeTextBox.Text = string.Format("{0} (Percent Complete : {1}%)", exportStatus.Status.ToString(), exportStatus.PercentComplete);
        if (exportStatus.Status == ExportState.Running || exportStatus.Status == ExportState.NotStarted)
        {
            // The recommended waiting time between polling requests can be found in the RetryAfter header
            // Note that this header is only populated when the status is either Running or NotStarted
            var retryAfter = httpMessage.Response.Headers.RetryAfter;
            var retryAfterInSec = retryAfter.Delta.Value.Seconds;
            await Task.Delay(retryAfterInSec * c_secToMillisec);
        }
    }
    // While not in a terminal state, keep polling
    while (exportStatus.Status != ExportState.Succeeded && exportStatus.Status != ExportState.Failed);
    return exportStatus;
}
```

### <a name="step-3---getting-the-file"></a>3\. lépés – a fájl lekérése

Ha a ciklikus lekérdezés egy URL-címet ad vissza, a kapott fájlt az alábbi példa alapján kérheti le.

```csharp
private async Task<ExportedFile> GetExportedFile(
    Guid reportId,
    Guid groupId,
    Export export /* Get from the GetExportStatusAsync response */)
{
    if (export.Status == ExportState.Succeeded)
    {
        var fileStream = await Client.Reports.GetFileOfExportToFileAsync(groupId, reportId, export.Id);
        return new ExportedFile
        {
            FileStream = fileStream,
            FileSuffix = export.ResourceFileExtension,
        };
    }
    return null;
}
public class ExportedFile
{
    public Stream FileStream;
    public string FileSuffix;
}
```

### <a name="end-to-end-example"></a>Teljes példa

Ez a példa egy jelentés exportálásának teljes folyamatát mutatja be. A példa tartalmazza a következő szakaszokat:
1. [Az exportálási kérés elküldése](#step-1---sending-an-export-request).
2. [Ciklikus lekérdezés](#step-2---polling).
3. [A fájl lekérése](#step-3---getting-the-file).

```csharp
private async Task<ExportedFile> ExportPowerBIReport(
    Guid reportId,
    Guid groupId,
    FileFormat format,
    int pollingtimeOutInMinutes,
    CancellationToken token,
    IList<string> pageNames = null /* Get the page names from the GetPages API */)
{
    try
    {
        var exportId = await PostExportRequest(reportId, groupId, format, pageNames);
        var export = await PollExportRequest(reportId, groupId, exportId, pollingtimeOutInMinutes, token);
        if (export == null || export.Status != ExportState.Succeeded)
        {
            // Error, failure in exporting the report
            return null;
        }
        return await GetExportedFile(reportId, groupId, export);
    }
    catch
    {
        // Error handling
        throw;
    }
}
```

## <a name="next-steps"></a>Következő lépések

Tekintse át, hogyan ágyazhat be tartalmat ügyfelei és vállalata számára:

> [!div class="nextstepaction"]
>[Többoldalas jelentés fájlba exportálása](export-paginated-report.md)

> [!div class="nextstepaction"]
>[Beágyazás az ügyfelek számára](embed-sample-for-customers.md)

> [!div class="nextstepaction"]
>[Beágyazás a cég számára](embed-sample-for-your-organization.md)
