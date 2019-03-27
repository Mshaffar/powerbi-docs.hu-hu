---
title: Útmutató Power BI-vizualizációkhoz
description: Megtudhatja, hogyan teheti közzé egyéni vizualizációit az AppSource-ban, amelyeket aztán mások is felfedezhetnek és használhatnak vásárlással.
author: sranins
ms.author: rasala
manager: kfile
ms.reviewer: maghan
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: conceptual
ms.date: 03/10/2019
ms.openlocfilehash: cf9a613e82b4f5b7ce9cc67f5b920760d01ccbf7
ms.sourcegitcommit: 39bc75597b99bc9e8d0a444c38eb02452520e22b
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/25/2019
ms.locfileid: "58430300"
---
# <a name="guidelines-for-power-bi-visuals"></a>Útmutató Power BI-vizualizációkhoz

## <a name="guidelines-for-power-bi-visuals-with-additional-purchases"></a>Útmutató további vásárlásos Power BI-vizualizációkhoz

Mostanáig a piactér (AppSource) csak ingyenes Power BI-vizualizációkat fogadott el. Ez a szabályzat megváltozott (2018. decemberben), így az AppSource-ra már a „További vásárlásra lehet szükség” címkéjű vizualizációk is beküldhetők. 

A „További vásárlásra lehet szükség” típusú vizualizációk az Office áruházában található, alkalmazáson belüli vásárlást (IAP-t) lehetővé tevő bővítményekhez hasonlóak. Ilyen vizualizációkat a fejlesztők is beküldhetnek minősítésre, miután az AppSource csapata jóváhagyta azokat, illetve meggyőződtek arról, hogy megfelelnek a minősítési feltételeknek. A követelményekről a [Minősített egyéni vizualizációk](../power-bi-custom-visuals-certified.md) című cikkben talál további információt.

> [!NOTE]
> A vizualizáció minősítéséhez az nem kapcsolódhat külső szolgáltatásokhoz és erőforrásokhoz.

>[!IMPORTANT]  
> Ha a vizualizációt az ingyenesről „További vásárlásra lehet szükség” szintűre frissíti, a felhasználók ugyanazon szintű funkciókkal fognak rendelkezni, mint a frissítés előtt. A meglévő ingyenes funkciók mellett felvehet választható, speciális fizetett funkciókat. Javasoljuk, hogy a speciális funkciókkal rendelkező IAP-vizualizációkat új vizualizációkként vegye fel, és ne a meglévő ingyeneseket frissítse.

## <a name="what-changed-in-the-submission-process"></a>Mi változott a beküldési folyamatban?

A fejlesztők az Értékesítői információ-központról tölthetik fel az IAP-vizualizációikat az AppSource-ba, ahogyan az ingyenes vizualizációkkal is tették. A fejlesztőknek az alábbi jegyzetet kell feltüntetniük az irányítópult értékesítői megjegyzései között, így jelezve, hogy a vizualizáció IAP-funkciókkal rendelkezik: „Alkalmazáson belüli vásárlást tartalmazó vizualizáció”. A fejlesztőknek emellett licenckulcsot vagy tokent kell szolgáltatniuk, amellyel az ellenőrző csapat ellenőrizheti az IAP-funkciókat. A vizualizáció ellenőrzése és jóváhagyása után az AppSource jelzi az IAP-vizualizáció díjszabási beállításainál, hogy ahhoz további vásárlásra lehet szükség.

## <a name="what-is-a-power-bi-visual-with-iap-features"></a>Mik az IAP-funkciókkal rendelkező Power BI-vizualizációk?

Az IAP-vizualizációk **ingyenes funkciókat** kínáló, **ingyenes** vizualizációk. Ezen kívül speciális funkciókkal is rendelkeznek, amelyek használatához további díjat kell fizetni. A fejlesztőknek a vizualizáció leírásában értesíteniük kell a felhasználókat arról, hogy mely funkciók használatához van szükség további vásárlásra. A Microsoft jelenleg nem nyújt natív API-kat az alkalmazások és bővítmények vásárlásának támogatásához.

A fejlesztők bármilyen külső fizetési rendszert használhatnak az ilyen vásárlásokhoz. További információt [üzletszabályzatunkban](https://docs.microsoft.com/office/dev/store/validation-policies#2-apps-or-add-ins-can-display-certain-ads) talál.

> [!NOTE]
> Az ingyenes funkciókkal vagy vizualizációkkal a vízjelek nem használhatóak. A vízjelek csak az érvényes licenc nélkül használt, fizetős funkciókkal használhatók. Azt javasoljuk, hogy egy előugró ablakot jelenítsen meg, amely a licenccel kapcsolatos adatokat tartalmazza, ha a speciális, fizetős funkciókat érvényes licenc nélkül használják.  

## <a name="logo-guidelines"></a>Embléma-irányelvek

Ez a szakasz az emblémák és logotipiák vizualizációkhoz való hozzáadásának részleteit ismerteti.

> [!IMPORTANT]
> Az emblémák **csak Szerkesztési módban** használhatók. Az emblémák **nem** jelennek meg Megtekintési módban.

![Definíciók](media/guidelines-powerbi-visuals/definitions.png)

![Ügyeljen az alábbiakra](media/guidelines-powerbi-visuals/things-to-keep-in-mind.png)

![Fontos megfontolások](media/guidelines-powerbi-visuals/things-to-avoid.png)

![Méret és a formátum](media/guidelines-powerbi-visuals/size-and-format.png)

![Margók és méretezés](media/guidelines-powerbi-visuals/margins-and-sizes.png)

![Szerkesztési mód](media/guidelines-powerbi-visuals/logos-in-edit-mode.png)

## <a name="best-practices"></a>Ajánlott eljárások

### <a name="visual-landing-page"></a>Vizualizáció kezdőlapja

A kezdőlapon tudathatja a felhasználókkal, hogy hogyan használhatják a vizualizációt, és hol vásárolhatnak licencet. Ne használjon automatikusan induló videókat. Csak olyan anyagot adjon hozzá, amely hozzájárul a felhasználói élményhez, például licencvásárlással vagy az IAP-funkció használatával kapcsolatos információk vagy hivatkozások.

### <a name="license-key-and-token"></a>Licenckulcs és token

Az egyszerűbb használat érdekében a licenckulccsal vagy tokenekkel kapcsolatos mezőket a formázási panel tetején helyezze el.

## <a name="faq"></a>Gyakori kérdések

A vizualizációkkal kapcsolatban a [Gyakori kérdések a vizualizációkon belüli további vásárlásokról](https://docs.microsoft.com/power-bi/power-bi-custom-visuals-faq#visuals-with-additional-purchases) weblapon talál további információt.

## <a name="next-steps"></a>Következő lépések

Megtudhatja, hogyan teheti közzé egyéni vizualizációit az [AppSource-ban](office-store.md), amelyeket aztán mások is felfedezhetnek és használhatnak.