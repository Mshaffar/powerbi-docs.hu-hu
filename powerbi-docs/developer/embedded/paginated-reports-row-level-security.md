---
title: Sorszintű biztonság használata beágyazott Power BI tartalommal
description: Megismerheti Power BI-tartalmak az alkalmazásba való beágyazásának lépéseit.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: nishalit
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: conceptual
ms.date: 11/04/2019
ms.openlocfilehash: 8d3068453ea2d166b0b55fbba45d8452431de319
ms.sourcegitcommit: 7aa0136f93f88516f97ddd8031ccac5d07863b92
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/05/2020
ms.locfileid: "79491732"
---
# <a name="implementing-row-level-security-in-embedded-paginated-reports-preview"></a>Sorszintű biztonság implementálása beágyazott lapszámozott jelentésekben (előzetes verzió)

Lapszámozott jelentés beágyazásakor megadhatja, hogy mely adatok legyenek megjelenítve. Ezáltal a megjelenő adatok felhasználónként testre szabhatók. Például egy globális értékesítési eredményeket tartalmazó, lapszámozott Power BI-jelentés beágyazható úgy, hogy csak egy adott régióra vonatkozó értékesítési eredmények legyenek elérhetők.

Ezzel a funkcióval biztonságos módon megjeleníthető az adatok egy része úgy, hogy a többi adat nem kerül veszélybe. Ez a megoldás hasonlít a [sorszintű biztonság (RLS)](embedded-row-level-security.md) funkcióhoz, amely biztonságos lehetőséget biztosít a (nem lapszámozott) Power BI-jelentésekben, irányítópultokon, csempéken és adatkészletekben található adatok megjelenítésére.  

> [!NOTE]
> Ez a funkció lapszámozott jelentések beágyazásához használható az ügyfelek számára.

## <a name="configuring-a-parameter-to-filter-the-dataset"></a>Egy paraméter konfigurálása az adatkészlet szűréséhez

Amikor sorszintű biztonságot alkalmazunk egy lapszámozott Power BI-jelentésnél, hozzá kell rendelni egy [paramétert](../../paginated-reports/report-builder-parameters.md) a **UserID** attribútumhoz. Ez a paraméter korlátozza az adatkészletből lekért adatok körét a jelentés beágyazását megelőzően.

Miután hozzárendelte a paramétert a **UserID** attribútumhoz, a [Reports GenerateTokenForCreateInGroup](https://docs.microsoft.com/rest/api/power-bi/embedtoken/reports_generatetokenforcreateingroup) API segítségével kérheti le a beágyazási tokent.

## <a name="use-userid-as-a-filter-at-report-or-query-level"></a>A UserID attribútum használata szűrőként a jelentés vagy a lekérdezés szintjén

A **UserID** attribútum használható *szűrőként* vagy egy, az adatforrás felé irányuló *lekérdezésben* a [Power BI Jelentéskészítőben](../../paginated-reports/report-builder-power-bi.md).

### <a name="using-the-filter"></a>A szűrő használata

1. A bal oldali panelen, az **Adatkészlet tulajdonságai** ablakban válassza a **Szűrő** lehetőséget.

    ![Power BI-jelentéskészítő – szűrő](media/paginated-reports-row-level-security/filter.png)

2. A **Kifejezés** legördülő menüben válassza ki az adatok szűréséhez használni kívánt paramétert.

     ![Power BI-jelentéskészítő – kifejezés](media/paginated-reports-row-level-security/expression.png)

3. Kattintson az **Érték** funkciógombra. 

    ![Power BI-jelentéskészítő – érték](media/paginated-reports-row-level-security/function.png)

4. A **Kifejezés** ablakban a **Kategória** listából válassza a **Beépített mezők** lehetőséget.

    ![Power BI-jelentéskészítő – kifejezés](media/paginated-reports-row-level-security/built-in-fields.png)

5. Az **Elem** listában válassza a **UserID** attribútumot, majd kattintson az **OK** gombra.

    ![Power BI-jelentéskészítő – UserID](media/paginated-reports-row-level-security/userid.png)

6. Az **Adatkészlet tulajdonságai** ablakban ellenőrizze, hogy a *kiválasztott paraméter = UserID* kifejezés szerepel-e ott, majd kattintson az **OK** gombra.

    ![Power BI-jelentéskészítő – adatkészlet tulajdonságai](media/paginated-reports-row-level-security/verify.png)

### <a name="using-a-query"></a>Lekérdezés használata

1. A bal oldali panelen, az **Adatkészlet tulajdonságai** ablakban válassza a **Paraméterek** lehetőséget, majd kattintson a **Hozzáadás** gombra.

    ![Power BI-jelentéskészítő – paraméterek](media/paginated-reports-row-level-security/parameters.png)

2. A **Paraméter neve** mezőbe írja be a **\@UserID** kifejezést, a **Paraméter értéke** mezőben pedig adja hozzá a **[&UserID]** értéket.

    ![Power BI-jelentéskészítő – paraméter neve](media/paginated-reports-row-level-security/parameter-name.png) 

3. A bal oldali panelen válassza a **Lekérdezés** lehetőséget, a lekérdezéshez adja hozzá a **UserID** paramétert a lekérdezés részeként, majd kattintson az **OK** gombra.
    > [!NOTE]
    > Az alábbi képernyőképen a Color (Szín) paramétert használjuk példaként (whereFinalTable.Color = @UserID). Szükség esetén összetettebb lekérdezések is létrehozhatók.

    ![Power BI-jelentéskészítő – lekérdezések szerkesztése](media/paginated-reports-row-level-security/query-edit.png)

## <a name="passing-the-configured-parameter-using-the-embed-token"></a>A konfigurált paraméter átadása a beágyazási token használatával

Amikor beágyazunk egy lapszámozott jelentést az ügyfelek számára, a [Reports GenerateTokenForCreateInGroup](https://docs.microsoft.com/rest/api/power-bi/embedtoken/reports_generatetokenforcreateingroup) API segítségével kérhetjük le a beágyazási tokent. Ez a token a lapszámozott jelentésből lekért adatok egy részének szűrésére is használható.

Ha csak az adatok egy részét szeretné megjeleníteni, rendelje hozzá a `username` mezőhöz a megjeleníteni kívánt információkat. Ha például egy Color (Szín) paraméterrel rendelkező, lapszámozott jelentésben beírjuk a *green* (zöld) értéket a `username` mezőbe, a beágyazási token úgy korlátozza a beágyazott adatokat, hogy csak az olyan adatok jelenjenek meg, amelyeknél a Color (Szín) oszlopban a *green* (zöld) érték szerepel.

```JSON
{
    "accessLevel": "View",
    "reportId": "cfafbeb1-8037-4d0c-896e-a46fb27ff229",
    "identities": [
            {
                    // Replace the 'username' with a paginated report parameter
                    "username":     "...",
                    "reports: [
                        "cfafbeb1-8037-4d0c-896e-a46fb27ff229"
                    ]
            }
    ]
}
```
