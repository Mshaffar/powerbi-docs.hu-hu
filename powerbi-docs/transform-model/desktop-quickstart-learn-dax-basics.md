---
title: A DAX alapszintű használata a Power BI Desktopban
description: A DAX alapszintű használata a Power BI Desktopban
author: davidiseminger
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-desktop
ms.topic: conceptual
ms.date: 10/21/2019
ms.author: davidi
LocalizationGroup: Model your data
ms.openlocfilehash: 783a9bdce34345afd87be379aff7e073ff8c548d
ms.sourcegitcommit: a72567f26c1653c25f7730fab6210cd011343707
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83565856"
---
# <a name="apply-dax-basics-in-power-bi-desktop"></a>A DAX alapszintű alkalmazása a Power BI Desktopban
Ez a cikk a Power BI Desktoppal még csak most ismerkedő felhasználóknak szól. Azt mutatja be röviden és egyszerűen, hogyan lehet a Data Analysis Expressions (DAX) nyelv segítségével néhány alapszintű számítási és adatelemzési problémát megoldani. Ismerteti az alapvető fogalmakat, továbbá tartalmaz néhány elvégezhető feladatot és egy tudáspróbát az elsajátított ismeretek felmérésére, így segít a DAX nyelvvel kapcsolatos legfontosabb alapvető tudnivalók elsajátításában.

## <a name="what-is-dax"></a>Mi az a DAX?
A DAX függvények, operátorok és konstansok gyűjteménye, amelyeket képletekbe vagy más néven kifejezésekbe rendezve a rendszer különféle értékeket számít ki és ad vissza. Egyszerűbben fogalmazva, a DAX segítségével a modellben található adatok alapján új információk hozhatók létre.

## <a name="why-is-dax-so-important"></a>Mi a DAX jelentősége?
Nem nehéz létrehozni olyan új Power BI Desktop-fájlokat, amelyekbe adatokat lehet importálni. Még az adatok értékes összefüggéseit kiemelő jelentések is létrehozhatók DAX-képletek nélkül. Mi a helyzet azonban akkor, ha különböző termékkategóriák növekedési arányait kell elemezni különböző időszakokra vetítve, vagy a piaci trendekhez viszonyított éves növekedési rátákat kell kiszámítani? Az ilyen feladatok elvégzését és sok egyéb hasznos funkció használatát a DAX-képletek teszik lehetővé. Ha tisztában van vele, hogyan hozhat létre hatékony DAX-képleteket, a legtöbbet hozhatja ki adataiból. Miután kinyerte adataiból a szükséges információkat, nekiláthat megoldani a tényleges üzleti problémákat, amelyek kihatással vannak a vállalkozás eredményességére. Itt mutatkozik meg a Power BI igazi ereje, amely igazán a DAX segítségével aknázható ki.

## <a name="prerequisites"></a>Előfeltételek
Előfordulhat, hogy már rendelkezik gyakorlattal a Microsoft Excel-képletek létrehozásában. Az ilyen ismeretek hasznosak a DAX megértéséhez, de még ha nem is ismeri az Excel-képleteket, az itt ismertetett alapfogalmak mentén rögtön nekiláthat saját DAX-képletekkel valós BI-problémákat megoldani.

Szeretnénk a számításokban, különösen a mértékekben és a számított oszlopokban használt DAX-képletek bemutatására helyezni a hangsúlyt. Ehhez elengedhetetlen, hogy már tudja, hogyan kell használni a Power BI Desktopot, adatokat importálni, és mezőket hozzáadni egy jelentéshez, valamint ismeri a [Mértékek](desktop-measures.md) és a [Számított oszlopok](desktop-calculated-columns.md) alapvető fogalmait.

### <a name="example-workbook"></a>Példamunkafüzet

A legjobban úgy sajátíthatja el a DAX használatát, ha létrehoz néhány alapvető képletet, azokat tényleges adatokkal használja, és megvizsgálja a kapott eredményeket. Az itt található példák és feladatok a Power BI Desktop előzetes verziójához készült [Contoso értékesítési mintára](https://download.microsoft.com/download/4/6/A/46AB5E74-50F6-4761-8EDB-5AE077FD603C/Contoso%20Sales%20for%20Power%20BI%20Designer.zip) épülnek. Ez a mintafájl megegyezik a következőben alkalmazottal: [Oktatóanyag: Saját mértékek létrehozása a Power BI Desktopban](desktop-tutorial-create-measures.md). 

## <a name="lets-begin"></a>Lássunk is hozzá!
A DAX nyelvvel kapcsolatos ismeretek három alapvető fogalom köré fűzhetőek fel: *Szintaxis*, *Függvények* és *Környezet*. Léteznek egyéb fontos fogalmak is a DAX-ban, de ennek a három fogalomnak az elsajátítása adja a lehető legjobb alapot, amelyre DAX-ismereteit építheti.

### <a name="syntax"></a>Szintaxis
Mielőtt elkezdene saját képleteket létrehozni, tekintsük át a DAX-képletek szintaxisát. A szintaxis a képletet alkotó elemeket vagy egyszerűbben a képlet írásmódját foglalja magában. Itt van például egy mérték egyszerű DAX-képlete:

![DAX-képlet szintaxisa](media/desktop-quickstart-learn-dax-basics/qsdax_1_syntax.png)

A szintaxis képletet alkotó elemei a következők:

**A.** A mérték neve, **Total Sales** (Értékesítések teljes összege).

**B.** Az egyenlőségjel operátor ( **=** ), amely a képlet kezdetét jelöli. A kiszámításakor a képlet egy eredményt ad vissza.

**C.** A **SUM** DAX-függvény, amely összegzi a **Sales[SalesAmount]** (Értékesítések[ÉrtékesítésekÖsszege]) oszlopban lévő összes számot. A függvényekre a későbbiekben térünk vissza.

**D.** Zárójelek **()** , melyek az egy vagy több argumentumot tartalmazó kifejezéseket zárják közre. Mindegyik függvényhez legalább egy argumentumot meg kell adni. Az argumentumokkal értékek adhatók a függvényekbe.

**E.** A hivatkozott tábla, a **Sales** (Értékesítések) tábla.

**F.** A hivatkozott oszlop, a Sales (Értékesítések) tábla **[SalesAmount]** ([ÉrtékesítésekÖsszege]) oszlopa. Ebből az argumentumból tudja a SUM függvény, hogy melyik oszlop értékeit kell összegezni.

A DAX-képletek megértéséhez érdemes lehet az egyes elemeket lebontani a mindennapokban használt és beszélt nyelvre. Ez a képlet például a következőképp olvasható ki:

> *A Total Sales nevű mértékhez számítsuk ki (=) a Sales tábla [SalesAmount] oszlopában lévő értékek összegét (SUM).*
> 
> 

Ha ezt a mértéket egy jelentéshez adjuk, kiszámítja az összes többi szerepeltetett mező (például: Mobiltelefonok az Egyesült Államok területén) értékesítési értékeinek összegét.

Most talán azt gondolja, hogy „Nem ugyanazt csinálja ez a mérték, mintha hozzáadnám a SalesAmount mezőt a jelentéshez?” Voltaképpen igen. Megvan azonban az oka, hogy miért hozunk létre egy külön saját mértéket, amely összegzi a SalesAmount mező értékeit: Ezt a mértéket ugyanis használhatjuk argumentumként más képletekben. Lehet, hogy ez elsőre nem egyértelmű, ahogy azonban jobban megismeri a DAX-képleteket, ezzel a mértékkel sokkal hatékonyabbá teheti a képleteket és a modelleket. A későbbiekben viszont is fogja látni a Total Sales mértéket más képletek argumentumaként.

Lássunk még néhány dolgot ezzel a képlettel kapcsolatban. Kiemelendő, hogy a részeként egy függvényt is bemutattunk, a [SUM](/dax/sum-function-dax) függvényt. A függvények előre megírt képletek, amelyek használatával bonyolultabb számításokat és átalakításokat végezhet többek között számokkal, dátum- és időértékekkel, valamint szövegekkel. A függvényekkel a későbbiekben foglalkozunk részletesebben.

Azt is láttuk, hogy a [SalesAmount] ([ÉrtékesítésekÖsszege]) oszlopnév előtt szerepelt a Sales (Értékesítések) tábla is, amelyhez az oszlop tartozik. Ezt a nevet teljesen minősített oszlopnévnek nevezik, mivel az oszlop neve előtt a tábla neve is szerepel benne. Az ugyanabban a táblában található hivatkozott oszlopok esetében nem szükséges megadni a tábla nevét a képletben; így könnyebben olvashatók lehetnek a hosszú képletek, amelyek sok oszlopra hivatkoznak. A mértékképletek esetében azonban hasznos a tábla nevét is szerepeltetni, még ha a saját táblájukon belül hivatkozunk is rájuk.

> [!NOTE]
> Ha valamely tábla neve szóközt, fenntartott kulcsszavakat vagy tiltott karaktereket tartalmaz, aposztrófok közé kell foglalni. Ugyanígy idézőjelek közé kell foglalni azokat a táblaneveket, amelyek az ANSI alfanumerikus karakterskálán kívül eső karaktereket tartalmaznak, függetlenül attól, hogy a területi beállítások támogatják-e az adott karakterkészletet.
> 
> 

Fontos, hogy a képletekben a megfelelő szintaxist alkalmazza. Hibás szintaxis esetén a rendszer legtöbb esetben egy szintaxishibát ad vissza. Az is előfordulhat, hogy a szintaxis helyes ugyan, a visszaadott értékek mégsem felelnek meg az elvárásoknak. A Power BI Desktop DAX-szerkesztője tartalmaz egy javaslatokat nyújtó funkciót is, mely segít a megfelelő elemek kiválasztásával szintaktikailag helyes képleteket előállítani.

Hozzunk létre egy egyszerű képletet. Ez a feladat segít jobban megérteni a képletek szintaxisát és a képletsáv javaslatokat nyújtó funkciójának működését.

### <a name="task-create-a-measure-formula"></a>Feladat: Mértékképlet létrehozása

1. [Töltse le](https://download.microsoft.com/download/4/6/A/46AB5E74-50F6-4761-8EDB-5AE077FD603C/Contoso%20Sales%20for%20Power%20BI%20Designer.zip) és nyissa meg a Contoso értékesítési mint Power BI Desktop-fájlját. 
    
2. A Jelentés nézet mezőlistájában kattintson a jobb gombbal a **Sales** (Értékesítések) táblára, majd válassza az **Új mérték** gombot.
    
3. A szerkesztőlécben írja a **Mérték** helyőrző helyére az új mérték nevét: *Previous Quarter Sales* (Előző negyedévi értékesítések).
    
4. Az egyenlőségjel után írja be az első néhány betűt (*CAL*), majd kattintson duplán a használni kívánt függvényre. Ebben a képletben használja a **CALCULATE** függvényt.

   A CALCULATE függvénnyel a függvénynek átadott argumentum alapján szűrheti az összegezni kívánt összegeket. Ezt nevezzük a függvények beágyazásának. A CALCULATE függvény legalább két argumentumot vesz fel. Az első a kiértékelendő kifejezés, a második pedig egy szűrő.
   
5. A **CALCULATE** függvény nyitó zárójele *(* után írja be a *SUM* függvényt, majd nyisson még egy zárójelet *(* . 

   Ezután átadunk egy argumentumot a SUM függvénynek.

6. Kezdje el begépelni a *Sal* kifejezést, majd válassza ki a **Sales[SalesAmount]** argumentumot, és zárja be a zárójelet *)* . 

   Ez a CALCULATE függvény első kifejezésargumentuma.
    
7. Írjon be egy vesszőt ( *,* ), aztán egy szóközt az első szűrő megadásához, majd írja be a *PREVIOUSQUARTER* kifejezést. 
    
   A PREVIOUSQUARTER időintelligencia-függvény segítségével szűrhetjük a SUM eredményeit az előző negyedévre.
    
8. A PREVIOUSQUARTER függvény nyitó zárójele *(* után írja be a *Calendar[DateKey]* argumentumot.
    
   A PREVIOUSQUARTER függvénynek egy argumentuma van, egy egybefüggő dátumtartományt tartalmazó oszlop. Ebben az esetben ez a Calendar (Naptár) táblázat DateKey oszlopa.
    
9. A PREVIOUSQUARTER függvénynek átadott mindkét argumentumot és a CALCULATE függvényt is zárja le két zárójel *))* beírásával.
    
   A képletnek most így kell kinéznie:
    
   **Previous Quarter Sales = CALCULATE(SUM(Sales[SalesAmount]), PREVIOUSQUARTER(Calendar[DateKey]))**
    
10. Válassza a pipa jelet ![Pipa ikon](media/desktop-quickstart-learn-dax-basics/qsdax_syntax_taskcheckmark.png) a szerkesztőlécen vagy nyomja le az Enter billentyűt a képlet érvényesítéséhez és a modellhez való hozzáadásához.

És kész is! Épp most hozott létre egy összetett mértéket a DAX használatával, amely egyáltalán nem könnyű. Ez a képlet az előző negyedévi teljes értékesítést számítja ki a jelentésben alkalmazott szűrők alapján. Például ha felvesszük a SalesAmount mezőt és az új Previous Quarter Sales mértéket egy diagramra, majd hozzáadjuk a Year és a QuarterOfYear mezőt szeletelőként, valami ilyesmit kapunk:

![A Previous Quarter Sales és a SalesAmount diagramja](media/desktop-quickstart-learn-dax-basics/qsdax_3_chart.png)

Most több fontos dolgot is megtanult a DAX-képletekkel kapcsolatban: 

- Ez a képlet két függvényt tartalmazott. A [PREVIOUSQUARTER](/dax/previousquarter-function-dax) időintelligencia-függvény a [CALCULATE](/dax/calculate-function-dax) szűrőfüggvénynek átadott argumentumként van beágyazva. 

   A DAX-képletek legfeljebb 64 beágyazott függvényt tartalmazhatnak. Valószínűtlen, hogy bármelyik képlet valaha is tartalmazna ennyi beágyazott függvényt. Egyébként is nehéz egy ilyen képletet létrehozni és abban hibákat keresni, és valószínűleg nem is lenne valami gyors.

- Ebben a képletben szűrőket is alkalmaztunk. A szűrők leszűkítik a kiszámítandó értékek halmazát. Esetünkben egy szűrőt választottunk argumentumként, amely egy másik függvény eredménye. A szűrőkre a későbbiekben térünk vissza.

- Használtuk a CALCULATE függvényt. Ez az egyik leghasznosabb DAX-függvény. A modellek készítése és a bonyolultabb képletek összeállítása során valószínűleg igen sokszor fogja majd alkalmazni ezt a függvényt. Bár a CALCULATE függvény további ismertetése nem képezi a jelen cikk részét, a DAX-ismeretei növelése során érdemes külön figyelmet szentelnie neki.

### <a name="syntax-quickquiz"></a>Szintaxis-gyorsteszt
1. Mire jó ez a gomb itt, a szerkesztőlécen?
   
   > ![Gomb kiválasztása](media/desktop-quickstart-learn-dax-basics/qsdax_2_syntaxquiz.png)
   > 
   > 
2. Mit kell mindig az oszlopok neve köré írni a DAX-képletekben?

A válaszokat a cikk végén találja.

### <a name="functions"></a>Függvények
A függvények előre definiált képletek, amelyek adott sorrendben vagy struktúrában megadott értékek, az úgynevezett argumentumok alapján végeznek számításokat. Az argumentumok lehetnek más függvények, egy másik képlet vagy kifejezés, oszlophivatkozások, számok, szövegek, logikai értékek (IGAZ vagy HAMIS) vagy konstansok.

A DAX a következő függvénykategóriákat tartalmazza: [Dátum és idő](/dax/date-and-time-functions-dax), [Időintelligencia](/dax/time-intelligence-functions-dax), [Információs](/dax/information-functions-dax), [Logikai](/dax/logical-functions-dax), [Matematikai](/dax/math-and-trig-functions-dax), [Statisztikai](/dax/statistical-functions-dax), [Szöveg](/dax/text-functions-dax), [Szülő/gyermek](/dax/parent-and-child-functions-dax) és [Egyéb](/dax/other-functions-dax) függvények. Ha már ismeri az Excel-képletekben használt függvényeket, a DAX-függvények nagy része ismerősnek fog hatni, azonban a DAX-függvények a következő szempontokból egyedinek tekinthetők:

* A DAX-függvény minden esetben egy oszlopra vagy táblára hivatkozik. Ha csak bizonyos értékeket szeretne egy táblából vagy oszlopból használni, kiegészítheti szűrőkkel a képletet.
* Ha a számításokat soronként testre szeretné szabni, a DAX-ben léteznek olyan függvények, amelyeknek az aktuális sor értékét vagy egy kapcsolódó értéket átadhat argumentumként, így környezetfüggő számításokat végezhet. A környezetekre a későbbiekben térünk vissza.
* A DAX számos függvénye nem értéket, hanem egy táblát ad vissza. A tábla nem jelenik meg, hanem értékeket biztosít más függvényeknek. Például le lehet kérni egy táblát, és megszámolni benne az eltérő értékeket, vagy szűrt táblák és oszlopok dinamikus összegeit kiszámítani.
* A DAX különböző időintelligencia-függvényeket is tartalmaz. Ezekkel a függvényekkel megadhat vagy kiválaszthat dátumtartományokat, és azokon dinamikus számításokat hajthat végre. Például összehasonlíthat párhuzamos időszakokra vonatkozó összegeket.
* Az Excel egyik népszerű függvénye a HKERES. Ellentétben az Excel HKERES függvényével, a DAX-függvényeknek nem adható át hivatkozásként cella vagy cellatartomány. A DAX-függvényeknek oszlopok vagy táblák adhatók át hivatkozásként. Mindig tartsa szem előtt, hogy a Power BI Desktopban relációs adatmodellekkel dolgozik. Könnyedén megkereshet egy értéket egy másik táblában, és ehhez legtöbbször még csak képlet sem kell.
  
  Amint látható, a DAX függvényeivel hatékony képletek hozhatóak létre. Eddig még csak alapszinten tekintettük át a képleteket. Ahogy egyre jobban elsajátítja a DAX használatát, számos különböző függvényt alkalmaz majd a képletekben. A DAX-függvényekkel kapcsolatos információkért leginkább a [DAX-függvények referencia-útmutatóját](/dax/) érdemes tanulmányoznia.

### <a name="functions-quickquiz"></a>Függvények-gyorsteszt
1. Mire hivatkoznak minden esetben a függvények?
2. Tartalmazhat egy képlet egynél több függvényt is?
3. Melyik kategória valamelyik függvényét alkalmazná két szöveges sztring egybefűzésére?

A válaszokat a cikk végén találja.

### <a name="context"></a>Környezet
A környezet a DAX egyik legfontosabb alapfogalma. A DAX-ben kétféle környezet létezik: a sorkörnyezet és a szűrőkörnyezet. Először a sorkörnyezettel foglalkozunk.

**Sorkörnyezet**

A sorkörnyezetet a legegyszerűbb úgy elképzelni, mint az adott sort. Akkor van jelentősége, ha egy képlet valamelyik függvénye olyan szűrőket alkalmaz, amelyek egy tábla egyetlen sorát azonosítják. A függvény automatikusan sorkörnyezetet alkalmaz a szűrt tábla minden egyes sorára. Az ilyen típusú sorkörnyezet leggyakrabban a mértékek esetén merül fel.

**Szűrőkörnyezet**

A szűrőkörnyezet már egy kicsit összetettebb, mint a sorkörnyezet. A szűrőkörnyezetet legegyszerűbben a következőképp foghatja fel: Egy adott számításban alkalmazott egy vagy több szűrő, amely egy eredményt vagy értéket határoz meg.

A szűrőkörnyezet nem a sorkörnyezetet váltja ki, hanem amellett érvényes. Például egy számításba belefoglalt értékek további szűkítéséhez alkalmazhat egy szűrőkörnyezetet, amely nem csupán a sorkörnyezetet határozza meg, hanem azon belül egy adott értéket (szűrőt) is.

A szűrőkörnyezet könnyen megfigyelhető a jelentésekben. Például ha felveszi a TotalCost mezőt egy vizualizációra, majd hozzáadja Year és a Region mezőt, egy szűrőkörnyezetet határoz meg, amely az adatok egy részhalmazát adja meg egy adott év és régió alapján.

Miért olyan fontos a szűrőkörnyezet a DAX esetén? Bár a legkönnyebben a mezők a vizualizációkhoz adásával alkalmazhatóak, a szűrőkörnyezeteket a DAX-képletekben is használhatja, ha az ALL, RELATED, FILTER, CALCULATE függvények, kapcsolatok vagy más mértékek és oszlopok segítségével meghatároz egy szűrőt. Tekintsük például a következő képletet a Store Sales elnevezésű mértékben:

![A Store Sales (Áruházi értékesítés) mérték](media/desktop-quickstart-learn-dax-basics/qsdax_4_context.png)

Hogy jobban megértsük, a képletet más képletekhez hasonlóan részekre bonthatjuk.

A szintaxis képletet alkotó elemei a következők:

**A.** A mérték neve, **Store Sales** (Áruházi értékesítés).

**B.** Az egyenlőségjel operátor ( **=** ), amely a képlet kezdetét jelöli.

**C.** A **CALCULATE** függvény, amely a megadott szűrők által módosított környezetben értékel ki egy argumentumként megadott kifejezést.

**D.** Zárójelek **()** , melyek egy olyan kifejezést zárnak közre, amely egy vagy több argumentumot tartalmaz.

**E.** A **[Total Sales]** mérték ugyanabban a táblázatban kifejezésként. A Total Sales mérték képlete: =SUM(Sales[SalesAmount]).

**F.** Pontosvessző ( **;** ), amely elválasztja az első kifejezés argumentumát a szűrőargumentumtól.

**G.** A hivatkozott oszlop teljes neve: **Channel[ChannelName]** . Ez a sorkörnyezetünk. Ebben az oszlopban minden sor egy olyan értékesítési csatornát ad meg, mint például a Store (Áruház) vagy az Online.

**H.** Az adott érték, **Store** (Áruház), mint szűrő. Ez a szűrőkörnyezetünk.

Ez a képlet garantálja, hogy a rendszer csak a Total Sales (Értékesítések teljes összege) mérték által megadott értékesítési mennyiségeket veszi számításba, csak a Channel[ChannelName] (Csatorna[CsatornaNeve]) oszlop azon sorai esetében, amelyekben a szűrőként használt *Store* (Áruház) érték szerepel.

Ha belegondolunk, láthatjuk, hogy a szűrőkörnyezetek képletekben való megadásával milyen hatalmas és sokoldalú lehetőségek nyílnak meg előttünk. Csak egy ezek közül, hogy lehetséges egy kapcsolódó táblának csak egy adott értékére hivatkozni. Ne aggódjon, ha egyelőre még nem teljesen látja át a környezeteket. Ahogy majd elkezd saját képleteket létrehozni, jobban megérti a környezet fogalmát, és hogy miért olyan fontos a szerepe a DAX-ben.

### <a name="context-quickquiz"></a>Környezet-gyorsteszt
1. Milyen két típusa van a környezetnek?
2. Mi a szűrőkörnyezet?
3. Mi a sorkörnyezet?

A válaszokat a cikk végén találja.

## <a name="summary"></a>Összefoglalás
Most, hogy valamelyest megismerte a DAX legfontosabb alapfogalmait, elkezdhet kísérletezgetni mértékek DAX-képleteinek létrehozásával. A DAX elsajátítása talán nem a legegyszerűbb dolog, de rengeteg forrásanyag áll rendelkezésre. A cikk átolvasása után, és miután már kísérletezgetett saját képletek összeállításával is, a DAX más fogalmaival és képleteivel is megismerkedhet, amelyek segíthetnek megoldást találni üzleti problémáira. A számos elérhető DAX-forrásanyag közül a legfontosabb a [Data Analysis Expressions (DAX) referencia-útmutatója](/dax/).

Mivel a DAX néhány éve már jelen van a Microsoft más üzletiintelligencia-eszközeiben, például a Power Pivot és az Analysis Services táblázatos modelljeiben, rengeteg további nagyszerű forrásanyag is elérhető. További információkat találhat még a mind a Microsoft, mind a vezető üzletiintelligencia-szakemberek tollából született könyvekben, tanulmányokban és blogokon. [A TechNeten a DAX-forrásanyagközpont wikije](https://social.technet.microsoft.com/wiki/contents/articles/dax-resource-center.aspx) szintén nagyszerű kiindulópontot jelenthet.

### <a name="quickquiz-answers"></a>A gyorstesztek válaszai
Szintaxis:

1. Ellenőrzi a mértéket, és átadja a modellnek.
2. Szögletes zárójeleket [].

Függvények:

1. Egy táblára és egy oszlopra.
2. Igen. Az egyes képletek akár 64 beágyazott függvényt is tartalmazhatnak.
3. A [szöveges függvények](/dax/text-functions-dax) kategóriájáét.

Környezet:

1. A sorkörnyezet és a szűrőkörnyezet.
2. Egy adott számításban alkalmazott egy vagy több szűrő, amely egy értéket határoz meg.
3. Az aktuális sor.
