---
title: A Q&A használata élő kapcsolatokkal a Power BI-ban
description: Dokumentáció a Power BI Q&A természetes nyelvi lekérdezések Analysis Services-adatokkal és helyszíni adatátjáróval kialakított élő kapcsolatokkal történő használatához.
author: maggiesMSFT
ms.reviewer: mihart
ms.service: powerbi
ms.subservice: powerbi-service
ms.topic: conceptual
ms.date: 10/16/2018
ms.author: maggies
LocalizationGroup: Ask questions of your data
ms.openlocfilehash: 3544a5330a21036e0ddecb351fd67b424ca6ebc7
ms.sourcegitcommit: bfc2baf862aade6873501566f13c744efdd146f3
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83348873"
---
# <a name="enable-qa-for-live-connections-in-power-bi"></a>A Q&A engedélyezése élő kapcsolatokhoz a Power BI-ban
## <a name="what-is-the-on-premises-data-gateway--what-is-a-live-connection"></a>Mi az a helyszíni adatátjáró?  Mi az az élő kapcsolat?
A Power BI-ban az adatkészletek importálhatók, vagy létrehozhat hozzájuk élő kapcsolatot. Az élő kapcsolattal rendelkező adathalmazokra gyakran „helyszíni”-ként utalnak. Az élő kapcsolatok kezelése [átjáró](../connect-data/service-gateway-onprem.md) használatával történik, az adatok és kérdések oda vissza küldése pedig élő lekérdezésekkel.

## <a name="qa-for-on-premises-data-gateway-datasets"></a>Q&A helyszíni adatátjáró-adatkészletekhez
Ha olyan adatkészleteken szeretné használni a Q&A-t, amelyeket átjárón keresztül ér el, akkor azokat először engedélyeznie kell.

Engedélyezés után a Power BI indexet hoz létre az adatforrásról, és feltölti ezeknek az adatoknak egy részét a Power BI-ba a kérdésfeltevés engedélyezéséhez. Az elsődleges index létrehozása eltarthat néhány percig, aztán a Power BI automatikusan karbantartja és frissíti az indexet az adatok változásának megfelelően. A Q&A ezeken az adatkészleteken használva ugyanúgy viselkedik, mint a Power BI-ban közzétett adatokkal. A Q&A területén elérhető összes funkció támogatott mindkét esetben.

Miközben kérdéseket tesz fel a Power BI-ban, a Q&A az adatkészlet indexe alapján meghatározza, milyen vizualizáció létrehozása vagy jelentéslap használata lesz a legjobb a kérdés megválaszolására. A lehetséges legjobb válasz meghatározása után a Q&A a DirectQueryt használja az adatforrás élő adatainak az átjárón keresztül történő lekérésére a diagramok és grafikonok kitöltéséhez. Ennek eredményeképp a Power BI Q&A mindig a legnaprakészebb adatokat jeleníti meg közvetlenül az alapul szolgáló adatforrásból.

Mivel a Power BI Q&A az adatforrásból származó szöveg- és sémaértékeket használja az alapul szolgáló modell lekérdezésére, a meghatározott új vagy törölt szöveges értékek keresése (például egy újonnan hozzáadott szöveges bejegyzéshez kapcsolódó ügyfélnév lekérdezése) attól függ, hogy az index naprakész-e a legújabb értékekkel. A Power BI 60 percenként frissíti a szöveg- és a sémaindex módosításait.

További információ:

* Mi az a [helyszíni adatátjáró](../connect-data/service-gateway-onprem.md)?
* [A Power BI Q&A felhasználók számára](../consumer/end-user-q-and-a.md)

## <a name="enable-qa"></a>A Q&A engedélyezése
Miután beállította az adatátjárót, kapcsolódjon az adatokhoz a Power BI-ból.  Hozzon létre egy irányítópultot a helyszíni adatokkal, vagy töltsön fel egy .pbix-fájlt, amely helyszíni adatokat használ.  Rendelkezhet már helyszíni adatokkal olyan irányítópultokban, jelentésekben és adatkészletekben is, amelyeket megosztottak Önnel.

1. Kattintson a fogaskerék ikonra ![fogaskerék ikon](media/service-q-and-a-direct-query/power-bi-cog.png) a Power BI jobb felső sarkában, majd a **Beállítások** gombra.
   
   ![Beállítások menü](media/service-q-and-a-direct-query/powerbi-settings.png)
2. Válassza az **adatkészletek** lapfület, majd válassza ki azokat az adatkészleteket, amelyeket engedélyezni szeretne a Q&A-hez.
   
   ![A Beállítások menü Adatkészletek képernyője](media/service-q-and-a-direct-query/power-bi-q-and-a-settings.png)
3. Bontsa ki a **Q&A** területet, jelölje be a **Q&A bekapcsolása ehhez az adathalmazhoz** jelölőnégyzetet, majd válassza az **Alkalmaz** elemet.
   
    ![A Q&A kibontva](media/service-q-and-a-direct-query/power-bi-qna-dataset-direct-query.png)

## <a name="what-data-is-cached-and-how-is-privacy-protected"></a>Milyen adatok gyorsítótárazása történik, és hogyan valósul meg az adatvédelem?
Amikor engedélyezi a Q&A-t a helyszíni adataihoz, az adatok egy részét a szolgáltatás gyorsítótárazza. Ez a gyorsítótárazás biztosítja, hogy a Q&A ésszerű teljesítménnyel működjön. A 24 karakternél hosszabb értékeket a Power BI kizárja a gyorsítótárazásból. Az adatkészlet néhány órán belül törlődik, miután letiltotta a Q&A-t a **Q&A bekapcsolása ehhez az adatkészlethez** jelölőnégyzet törésével, vagy miután törli az adatkészletet.

## <a name="considerations-and-troubleshooting"></a>Szempontok és hibaelhárítás
A funkcióra bizonyos korlátozások érvényesek:

* Eredetileg a funkció csak az SQL Server 2016 Analysis Services táblázatos adatforrásaihoz áll rendelkezésre. A funkció táblázatos adatokkal való munkavégzésre van optimalizálva. A Q&A használata többdimenziós adatforrások esetén még nem támogatott. A helyszíni adatátjáró által támogatott további adatforrások bevezetése a későbbiekben fog történni.
* Az SQL Server Analysis Servicesben meghatározott sorszintű biztonság teljes támogatása kezdetben nem áll rendelkezésre. Miközben a felhasználó kérdéseket tesz fel a Q&A-ben, a kérdések beírása közben használt „automatikus kitöltés” miatt megjelenhetnek olyan sztringértékek, amelyekhez a felhasználó nem rendelkezik hozzáféréssel. A modellben meghatározott RLS-t azonban tiszteletben tartja a rendszer a jelentés- és a diagramvizualizációknál, ezért nem fed fel alapul szolgáló számadatokat. Az ezt a viselkedést vezérlő beállítások az elkövetkező frissítésekben fognak szerepelni.
* Az objektumszintű biztonság (OLS) nem támogatott. A Q&A figyelmen kívül hagyja az objektumszintű biztonságot, és megjeleníti a táblázatok és oszlopok neveit azon felhasználóknak, akik nem férnek hozzájuk. Célszerű engedélyezni a sorszintű biztonságot, így meggyőződhet arról, hogy az adatértékeket is megfelelő biztonságban tartja. 
* Az élő kapcsolatok csak a helyszíni adatátjárónál támogatottak. Ezért ez a funkció nem használható a személyes átjáróval.

## <a name="next-steps"></a>További lépések

- [Helyszíni adatátjáró](../connect-data/service-gateway-onprem.md)  
- [Adatforrások kezelése – Analysis Services](../connect-data/service-gateway-enterprise-manage-ssas.md)  
- [A Power BI szolgáltatás alapfogalmai tervezők számára](../fundamentals/service-basic-concepts.md)  
- [A Power BI Q&A áttekintése](../consumer/end-user-q-and-a.md)  

Több kérdése van? [Kérdezze meg a Power BI-közösséget](https://community.powerbi.com/)
