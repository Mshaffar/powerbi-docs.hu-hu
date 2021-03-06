---
title: Paraméterek létrehozása lapszámozott jelentésekhez a Power BI szolgáltatásban
description: Ebből a cikkből megismerheti, hogyan hozhat létre paramétereket lapszámozott jelentésekhez a Power BI szolgáltatásban.
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.service: powerbi
ms.subservice: report-builder
ms.topic: conceptual
ms.date: 12/03/2019
ms.openlocfilehash: 42b9057ccfaa918593e1be8a182c7b0ee57f9760
ms.sourcegitcommit: 7aa0136f93f88516f97ddd8031ccac5d07863b92
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/05/2020
ms.locfileid: "78920987"
---
# <a name="create-parameters-for-paginated-reports-in-the-power-bi-service"></a>Paraméterek létrehozása lapszámozott jelentésekhez a Power BI szolgáltatásban

Ebből a cikkből megismerheti, hogyan hozhat létre paramétereket lapszámozott jelentésekhez a Power BI szolgáltatásban.  A jelentésparaméter módot kínál a jelentés adatainak kiválasztására és a megjelenésének módosítására. Megadhat egy alapértelmezett értéket és a rendelkezésre álló értékek listáját, és a jelentés olvasói kiválaszthatják a nekik tetszőeket.  

Az alábbi ábrán a Tervező nézet látható a Power BI Jelentéskészítőben egy jelentéshez a következő paraméterekkel: @BuyingGroup, @Customer, @FromDate és @ToDate. 
  
![Paraméterek a Jelentéskészítőben](media/paginated-reports-parameters/power-bi-paginated-parameters-report-builder.png)
  
1.  A jelentés paraméterei a Jelentésadatok panelen.  
  
2.  Tábla az adatkészlet egyik paraméterével.  
  
3.  A Paraméterek panel. A paraméterek elrendezését a Paraméterek panelen szabhatja testre. 
  
4.  A @FromDate és @ToDate paraméterek adattípusa **DateTime**. A jelentés megtekintésekor beírhatja a szövegmezőbe a dátumot, vagy választhat egy dátumot a naptár vezérlőelemeivel. 

5.  Az **Adatkészlet tulajdonságai** párbeszédpanel egyik paramétere.  

  
## <a name="create-or-edit-a-report-parameter"></a>Jelentésparaméter létrehozása vagy szerkesztése  
  
1.  Nyissa meg a lapszámozott jelentést a Power BI Jelentéskészítőben.

1. A **Jelentésadatok** panelen kattintson a jobb gombbal a **Paraméterek** csomópontra, majd kattintson a **Paraméter hozzáadása** elemre. Megnyílik a **Jelentésparaméter tulajdonságai** párbeszédpanel.  
  
2.  A **Név** mezőbe írjon be egy nevet a paraméterhez, vagy fogadja el az alapértelmezett nevet.  
  
3.  A **Rákérdezés** mezőbe írja be azt a szöveget, amely a paraméter szövegmező mellett fog megjelenni, amikor a felhasználó futtatja a jelentést.  
  
4.  Az **Adattípus** mezőben válassza ki az adattípust a paraméterértékhez.  
  
5.  Ha a paraméter tartalmazhat üres értéket, válassza ki az **Üres érték engedélyezése** lehetőséget.  
  
6.  Ha a paraméter tartalmazhat null értéket, válassza ki a **Null érték engedélyezése** lehetőséget.  
  
7.  Ha szeretné engedélyezni a felhasználó számára, hogy egynél több értéket is kiválaszthasson a paraméterhez, válassza ki a **Több érték engedélyezése** lehetőséget.  
  
8.  Állítsa be a láthatóságot.  
  
    -   A paraméternek a jelentés tetején lévő eszköztáron való megjelenítéséhez válassza a **Látható** lehetőséget.  
  
    -   A paraméter elrejtéséhez, hogy ne legyen látható az eszköztáron, válassza a **Rejtett** lehetőséget.  
  
    -   A paraméter elrejtéséhez és a jelentés közzététele után a jelentéskészítő kiszolgálón a módosítás elleni védelméhez válassza a **Belső** lehetőséget. A jelentésparaméter ekkor csak a jelentésdefinícióban lesz megtekinthető. Ehhez a lehetőséghez be kell állítania egy alapértelmezett értéket, vagy engedélyeznie kell a paraméter számára a null érték elfogadását.  
  
9. Kattintson az **OK** gombra. 

## <a name="considerations-and-troubleshooting"></a>Szempontok és hibaelhárítás

- Ha adatforrásként egy Power BI-adathalmazt vagy egy Analysis Services-modellt használ, akkor a DAX korlátozásai miatt egy adott kérelemben legfeljebb 1 000 paramétert adhat át. 

 
## <a name="next-steps"></a>További lépések

Ha látni szeretné, hogyan jelennek meg a paraméterek a Power BI szolgáltatásban, olvassa el a [Paraméterek megtekintése lapszámozott jelentésekhez](../consumer/paginated-reports-view-parameters.md) szakaszt.

További információ a lapszámozott jelentések paramétereiről: [Jelentésparaméterek a Power BI Jelentéskészítőben](report-builder-parameters.md).
