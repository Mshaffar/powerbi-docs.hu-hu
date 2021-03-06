---
title: Power BI-engedélyek
description: Power BI-engedélyek
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-developer
ms.topic: conceptual
ms.date: 10/01/2018
ms.openlocfilehash: 51c43a19613381d39e0397864e55baed2022663c
ms.sourcegitcommit: 7aa0136f93f88516f97ddd8031ccac5d07863b92
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/05/2020
ms.locfileid: "79491364"
---
# <a name="power-bi-permissions"></a>Power BI-engedélyek

## <a name="permission-scopes"></a>Engedélyek hatókörei

A Power BI-engedélyek lehetővé teszik az alkalmazások számára, hogy bizonyos műveleteket végezzenek a felhasználók nevében. Minden engedélyt jóvá kell hagynia egy felhasználónak, hogy érvényesek legyenek.

| Megjelenített név | Description (Leírás) | Hatókör értéke |
| --- | --- | --- |
| Az összes adatkészlet megtekintése |Az alkalmazás megtekintheti a bejelentkezett felhasználó összes adatkészletét, illetve azokat az adatkészleteket, amelyekhez a felhasználónak hozzáférése van. |Dataset.Read.All |
| Az összes adatkészlet olvasása és írása |Az alkalmazás megtekintheti a bejelentkezett felhasználó összes adatkészletét, illetve azokat az adatkészleteket, amelyekhez a felhasználónak hozzáférése van, továbbá írhat ezekbe az adatkészletekbe. |Dataset.ReadWrite.All |
| Adatok hozzáadása egy felhasználó adatkészletéhez |Hozzáférést nyújt egy alkalmazásnak egy felhasználó adatkészletbeli sorainak hozzáadásához vagy törléséhez. Ez az engedély nem nyújt hozzáférést az alkalmazásnak a felhasználó adataihoz. |Data.Alter_Any |
| Tartalom létrehozása |Az alkalmazás automatikusan tud létrehozni tartalmat és adatkészleteket egy felhasználóhoz. |Content.Create |
| Felhasználói csoportok megtekintése |Az alkalmazás megtekintheti az összes olyan csoportot, amelyeknek a bejelentkezett felhasználó a tagja. |Group.Read |
| Az összes csoport megtekintése |Az alkalmazás megtekintheti az összes olyan csoportot, amelyeknek a bejelentkezett felhasználó a tagja. |Group.Read.All |
| Az összes csoport olvasása és írása |Az alkalmazás megtekintheti a bejelentkezett felhasználó összes csoportját, illetve azokat a csoportokat, amelyekhez a felhasználónak hozzáférése van, továbbá írhat is ezekbe a csoportokba. |Group.ReadWrite.All |
| Az összes irányítópult megtekintése |Az alkalmazás megtekintheti a bejelentkezett felhasználó összes irányítópultját, illetve azokat az irányítópultokat, amelyekhez a felhasználónak hozzáférése van. |Dashboard.Read.All |
| Az összes jelentés megtekintése |Az alkalmazás megtekintheti a bejelentkezett felhasználó összes jelentését, illetve azokat a jelentéseket, amelyekhez a felhasználónak hozzáférése van. Az alkalmazás továbbá megtekintheti a jelentések adatait és struktúráját is. |Report.Read.All |
| Az összes jelentés olvasása és írása |Az alkalmazás megtekintheti a bejelentkezett felhasználó összes jelentését, illetve azokat a jelentéseket, amelyekhez a felhasználónak hozzáférése van, továbbá írhat ezekbe a jelentésekbe. Ez nem nyújt jogosultságot új jelentés létrehozására. |Report.ReadWrite.All |
| Az összes kapacitás olvasása és írása |Az alkalmazás megtekintheti a bejelentkezett felhasználó összes kapacitását, illetve azokat a kapacitásokat, amelyekhez a felhasználónak hozzáférése van, továbbá írhat is ezekbe a kapacitásokba. Viszont nem biztosít engedélyt új kapacitás létrehozásához. |Capacities.ReadWrite.All |
| Az összes kapacitás olvasása |Az alkalmazás megtekintheti a bejelentkezett felhasználó összes kapacitását, illetve azokat a kapacitásokat, amelyekhez a felhasználónak hozzáférése van, továbbá írhat is ezekbe a kapacitásokba. Viszont nem biztosít engedélyt új kapacitás létrehozásához. |Capacities.Read.All |
| A bérlőben szereplő összes tartalom olvasása és írása |Az alkalmazás megtekintheti az összes összetevőt (pl.: csoportok, jelentések, irányítópultok és adatkészletek a Power BI-ban), továbbá írhat is ezekbe az összetevőkbe. Ennek feltétele, hogy a bejelentkezett felhasználó Power BI-szolgáltatásadminisztrátor legyen. |Tenant.ReadWrite.All |
| A bérlőben szereplő összes tartalom megtekintése |Az alkalmazás láthatja a Power BI minden összetevőjét, köztük a csoportokat, a jelentéseket, az irányítópultokat és az adatkészleteket is. Ennek feltétele, hogy a bejelentkezett felhasználó Power BI-szolgáltatásadminisztrátor legyen. |Tenant.Read.All |

Egy alkalmazás engedélyeket kérhet, amikor először kísérel meg bejelentkezni egy felhasználó oldalára a hívás hatókör-paraméterében a kért engedélyek megadásával. Ha megkapja az engedélyeket, a rendszer egy hozzáférési tokent ad vissza az alkalmazásnak, amely a későbbi API-hívások során használható. A hozzáférést csak adott alkalmazás használhatja.

> [!NOTE]
> A Power BI API-k továbbra is csoportokként hivatkoznak a munkaterületekre. Bármely csoportokra való utalás munkaterületek használatát jelöli.

## <a name="requesting-permissions"></a>Engedélyek kérése

Bár behívhatja az API-t felhasználónévvel és jelszóval való hitelesítéshez, ha másik felhasználó nevében szeretne műveleteket végezni, olyan engedélyeket kell kérnie, amelyeket a felhasználó jóváhagy, majd az eredményül kapott hozzáférési tokent el kell küldenie az összes későbbi hívással. Ehhez a folyamathoz a standard [OAuth 2.0](https://oauth.net/2/) protokollt követjük. Bár a tényleges megvalósítás változó lehet, a Power BI OAuth folyamata a következő elemekből áll:

* **Bejelentkezési felhasználói felület** – Ez az a felhasználói felület, amelyet a fejlesztő engedélyek kérésére hívhat meg. A felület a felhasználó bejelentkezését kéri, ha még nem tette meg. A felhasználónak az alkalmazás által kért engedélyeket is jóvá kell hagynia. A bejelentkezési ablak visszaküld egy hozzáférési kódot vagy egy hibaüzenetet a megadott átirányítási URL-címre.
  * A Power BI-nak egy standard átirányítási URL-címet kell megadnia a natív alkalmazásokhoz.
* **Engedélyezési kód** – A rendszer engedélyezési kódokat ad vissza a webalkalmazásoknak az átirányítási URL-címen szereplő URL-paraméterekkel való bejelentkezés után. Mivel ezek paraméterekben szerepelnek, ez bizonyos biztonsági kockázattal jár. A webalkalmazásoknak engedélyezési tokenre kell cserélniük az engedélyezési kódot
* **Engedélyezési token** – Az API-hívások másik felhasználó nevében való hitelesítésére szolgál. Adott alkalmazásra lesz érvényes. A tokenek adott élettartammal rendelkeznek, és amikor lejárnak, frissítést igényelnek.
* **Token frissítése** – Amikor a jogkivonatok lejárnak, frissítési folyamat használható hozzájuk.

Több kérdése van? [Kérdezze meg a Power BI-közösséget](https://community.powerbi.com/)