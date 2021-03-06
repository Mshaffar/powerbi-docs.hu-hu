---
title: Tippek és trükkök a színformázáshoz a jelentésekben
description: Tippek és trükkök a színformázáshoz a Power BI-jelentésekben
author: mihart
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-desktop
ms.topic: conceptual
ms.date: 03/29/2020
ms.author: mihart
LocalizationGroup: Visualizations
ms.openlocfilehash: c2800ab9d57732448db9e4fe647a0601a20a816c
ms.sourcegitcommit: 0e9e211082eca7fd939803e0cd9c6b114af2f90a
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83276605"
---
# <a name="tips-and-tricks-for-color-formatting-in-power-bi"></a>Tippek és trükkök a színformázáshoz a Power BI-ban

[!INCLUDE[consumer-appliesto-nyyn](../includes/consumer-appliesto-nyyn.md)]    

A Power BI sokféle lehetőséget kínál, amelyekkel egyedivé tehetők az irányítópultok és a jelentések. Ez a cikk néhány olyan ötletet fejt ki részletesen, amelyek segítségével meggyőzőbb, érdekesebb és az Ön igényeinek jobban megfelelő Power BI-vizualizációkat készíthet.

A következő tippeket kínáljuk Önnek. Van egy másik remek ötlete? Nagyszerű! Küldje el nekünk, és talán hozzáadjuk ehhez a listához.

* Téma alkalmazása a teljes jelentésre
* Egy adatpont színének módosítása
* Feltételes formázás
* Diagram színeinek meghatározása egy numerikus érték alapján
* Adatpontok színének meghatározása egy mező értéke alapján
* A színskála összeállításának testre szabása
* Széttartó színskálák használata
* Táblasorok kiszínezése
* Művelet visszavonása a Power BI-ban

Módosítások végrehajtásához szerkesztési engedélyekkel kell rendelkeznie a jelentéshez. A Power BI Desktopban nyissa meg a jelentést a **Jelentés** nézetben. A Power BI szolgáltatásban ez azt jelenti, hogy meg kell nyitnia a jelentést, és a **Szerkesztés** menüt kell választania a menüsávon, amint az a következő ábrán látható.

![a Szerkesztés menü helye](media/service-tips-and-tricks-for-color-formatting/power-bi-edit-report.png)

Amikor a jelentésvászon jobb oldalán megjelenik a **Szűrők** és **Vizualizációk** panel, megkezdheti a testre szabást. Ha a panelek nem láthatók, a jobb felső sarokban található nyíllal nyithatók meg.

![jelentésvászon szerkesztési nézetben](media/service-tips-and-tricks-for-color-formatting/power-bi-edit.png)

## <a name="apply-a-theme"></a>Téma alkalmazása
A jelentéstémák használatával olyan tervezési módosításokat hajthat végre az egész jelentésen, mint a vállalati színek, a változó ikonkészletek, vagy egy új alapértelmezett vizualizációs formázás. Jelentéstéma alkalmazásakor a jelentésben szereplő összes vizualizáció a kiválasztott téma színeit és formázását fogja használni. További információért olvassa el a [Jelentéstémák használata](../create-reports/desktop-report-themes.md) szakaszt

![Téma ikon módosítása a menüsávon](media/service-tips-and-tricks-for-color-formatting/power-bi-theme.png)

Itt az **Innováció** témát alkalmaztuk az értékesítési és marketingjelentésre.

![Az Innováció téma alkalmazva](media/service-tips-and-tricks-for-color-formatting/power-bi-theme-innovate.png)

## <a name="change-the-color-of-a-single-data-point"></a>Egy adatpont színének módosítása
Előfordul, hogy egy adott adatpontot szeretne kiemelni. Ez lehet egy újonnan bevezetett termék eladott mennyisége, vagy javuló minőségi mutató egy új program elindítása után. A Power BI-ban kiemelhet egy választott adatpontot a színe módosításával.

Az alábbi vizualizáció egységeket rangsorol a termékszegmens szerint. 

![Az adatszínek módosítása szürkére](media/service-tips-and-tricks-for-color-formatting/power-bi-data.png)

Tegyük fel, hogy a **Kényelem** szegmens színes kiemelésével meg szeretné mutatni, hogy milyen jól teljesít az új szegmens. A lépések a következők:

Bontsa ki az **Adatszínek** kártyát, és kapcsolja be a csúszkát **Az összes megjelenítése** lehetőséghez. Így a vizualizáció összes adatelemének színe megjelenik. Most már módosítsa bármelyik adatpontot.

![](media/service-tips-and-tricks-for-color-formatting/power-bi-show.png)

Állítsa a **Kényelem** színét narancssárgára. 

![](media/service-tips-and-tricks-for-color-formatting/power-bi-one-color.png)

Miután választott, a **Kényelem** adatpont szép narancssárga, és kétségtelenül szembeszökő színt vesz fel.

A Power BI akkor is megjegyzi a választását és narancssárgán jeleníti meg a **Kényelmet**, ha Ön megváltoztatja, majd visszaváltoztatja a vizualizáció típusát.

Egynél több, sőt akár az összes adatelem adatpontjának színe is megváltoztatható. A vizualizáció például a sárga, zöld és kék vállalati színeket is tükrözheti. 

![sávdiagram zöld, sárga és kék színű sávokkal](media/service-tips-and-tricks-for-color-formatting/power-bi-corporate.png)

A színekkel sok mindent megtehet. A következő bekezdésben a feltételes formázással foglalkozunk.

## <a name="conditional-formatting-for-visualizations"></a>Vizualizációk feltételes formázása
A vizualizációknak gyakran előnyére válik a színek dinamikus meghatározása egy mező numerikus értéke alapján. Ezen a módon az oszlopok magasságát megadó érték mellett egy másikat is megjeleníthet, így két értéket szemléltethet egy diagramon. Használhatja a lehetőséget egy bizonyos érték feletti (vagy alatti) adatpontok kiemelésére – például alacsony jövedelmezőségű területek kimutatására.

A következő szakaszok különböző módszereket mutatnak be a színek numerikus érték alapján történő meghatározására.

### <a name="base-the-color-of-data-points-on-a-value"></a>Adatpontok színének meghatározása egy érték alapján
Ha egy érték alapján szeretné módosítani a színt, válasszon egy vizualizációt az aktiváláshoz. Nyissa meg a Formátum panelt a festőhenger ikon kiválasztásával, majd nyissa meg az **Adatszínek** kártyát. Vigye az egérmutatót a kártyára, és válassza a megjelenő három pontot, majd a **Feltételes formázás** lehetőséget.  

![a feltételes formázás lehetőség választása a három pontra történő kattintással](media/service-tips-and-tricks-for-color-formatting/power-bi-conditional-formatting.gif)

Az **Alapértelmezett színek** panel legördülő menüjében adja meg a feltételesen formázni kívánt mezőket. Ebben a példában a **Sales fact** > **Total Units** mezőt választottuk, amelyhez a **legalacsonyabb értéknek** a világoskéket, **legmagasabb értéknek** pedig a sötétkéket adtuk meg. 

![az adatszínnel történő feltételes formázás beállításai](media/service-tips-and-tricks-for-color-formatting/power-bi-conditional-formatting2-new.png)

![alapértelmezett színekkel ellátott oszlopdiagram](media/service-tips-and-tricks-for-color-formatting/power-bi-default-colors.png)

A vizualizáció színét egy vizualizáción kívüli mezővel is formázhatja. A következő ábrán a **%Market Share SPLY YTDP** (Piaci részesedés a tavalyi év azonos időszakában, az év elejétől számítva (%)) mező szolgál erre. 

![](media/service-tips-and-tricks-for-color-formatting/power-bi-conditional-colors.png)


Mint látja, bár mind a **Productivity**, mind az **Extreme** egységei több eladást eredményeztek (amit a magasabb oszlop jelez), a **Moderation** nagyobb **%Market Share SPLY YTD** értékkel rendelkezik (amit az oszlop színtelítettségéből láthatunk).

### <a name="customize-the-colors-used-in-the-color-scale"></a>A színskála összeállításának testre szabása
Az értékek és a színek egymáshoz rendelése is módosítható. A következő ábrán a **legkisebb** és a **legnagyobb** értékhez választott két szín a narancs, illetve a zöld.

Figyelje meg az első képen, hogy a diagram oszlopai a sávon ábrázolt színátmenetet tükrözik. A legmagasabb érték zöld, a legalacsonyabb narancsszínű, a közöttük lévők pedig a skála zöld és narancs közötti árnyalatait viselik.

![](media/service-tips-and-tricks-for-color-formatting/power-bi-conditional4.png)

Most próbáljon meg numerikus értéket adni a **Minimum** és **Maximum** mezőknek. Válassza az **Egyéni** lehetőséget a legördülő menükből a **Minimum** és a **Maximum** értékeinek megadásához, és adja meg a **Minimum** értékeként, hogy 3500 a **Maximum** értékeként, hogy 6000.

![Feltételes formázás számok alapján](media/service-tips-and-tricks-for-color-formatting/power-bi-conditional-formatting-numbers.png)

Ezekkel az értékekkel a színátmenet már nem alkalmazható a diagramnak a **Minimum** alatti vagy **Maximum** feletti értékeire. A **Maximum** értéknél magasabb oszlopok színe zöld, a **Minimum** alattiaké piros.

![a feltételes formázás számok alapján művelet eredménye](media/service-tips-and-tricks-for-color-formatting/power-bi-conditional3.png)

### <a name="use-diverging-color-scales"></a>Széttartó színskálák használata
Előfordul, hogy az adatok természetes módon széttartó jellegűek. Egy hőmérsékleti skálának például természetes középpontja a fagypont, egy jövedelmezőségi érték természetes középpontja a nulla.

Széttartó színskálák használatához jelölje be a **Széttartó** jelölőnégyzetet. A **Széttartó** beállítással újabb paletta jelenik meg **Középérték** néven, ahogyan az alábbi képen látható.

![Alapértelmezett szín párbeszédpanel kiválasztott színskálával](media/service-tips-and-tricks-for-color-formatting/power-bi-diverging-colors.png)

Amíg a **Széttartó** beállítás be van kapcsolva, a **Minimumhoz**, a **Maximumhoz** és a **Középértékhez** tartozó szín külön módosítható. A következő képen a **% Market Share SPLY YTD** **Középértékeként** 0,2 van megadva, ezért a 0,2-nél nagyobb értékek a zöld, az egynél kisebbek a piros árnyalataiban jelennek meg.

![oszlopdiagram piros és zöld oszlopokkal](media/service-tips-and-tricks-for-color-formatting/power-bi-diverging.png)

## <a name="add-color-to-table-rows"></a>Táblasorok kiszínezése
A táblák és a mátrixok számos lehetőséget kínálnak a színformázásra. 

![alapértelmezett tábla](media/service-tips-and-tricks-for-color-formatting/power-bi-table.png)

Egy szín táblára vagy mátrixra alkalmazásának az egyik leggyorsabb módja a Formázás lap megnyitása és a **Stílus** kiválasztása.  Az alábbi ábrán a **Félkövér fejléc, feltűnő sorok** beállítást választottuk.

![alapértelmezett tábla](media/service-tips-and-tricks-for-color-formatting/power-bi-table-style.png)

Más színformázási beállításokkal is kísérletezhet. Ezen az ábrán megváltoztattuk a háttérszínt az **Oszlopfejlécek** alatt, valamint a **Háttérszín** és az **Alternatív háttérszín** értékét az **Értékek** (sorok) mezőhöz.

![alapértelmezett tábla](media/service-tips-and-tricks-for-color-formatting/power-bi-table-rows.png)

## <a name="how-to-undo-in-power-bi"></a>Művelet visszavonása a Power BI-ban
Sok más Microsoft-szolgáltatáshoz és -szoftverhez hasonlóan a Power BI is egyszerű módot kínál az utolsó parancs visszavonására. Képzelje el például, hogy megváltoztatta egy adatpont vagy adatpont-sorozat színét és a vizualizáción megjelenő szín nem teszik Önnek. Majd pedig az eredeti színt szeretné visszaállítani, csakhogy már nem emlékszik rá!

A legutóbbi művelet vagy néhány nemrégiben végzett művelet **visszavonásához** csak a CTRL+Z billentyűkombinációt kell megnyomnia.

Ha el szeretné vetni a Formázás kártyán végzett összes módosítást, válassza a **Visszaállítás alapértelmezettre** beállítást.

![Formázás kártya az alján a Visszaállítás alapértelmezettre beállítás megjelenítésével](media/service-tips-and-tricks-for-color-formatting/power-bi-revert.png)

## <a name="feedback"></a>Visszajelzés
Van egy tippje, amelyet szívesen megosztana másokkal? Kérjük, küldje el nekünk, és megvizsgáljuk, hozzáadhatjuk-e ehhez a listához.

## <a name="next-steps"></a>Következő lépések
[Bevezetés a színformázás és tengelytulajdonságok használatába](service-getting-started-with-color-formatting-and-axis-properties.md)

[Jelentések megosztása](../collaborate-share/service-share-reports.md).

