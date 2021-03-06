---
title: Indítási URL-cím létrehozása
description: Ez a cikk bemutatja, hogyan nyithat meg egy URL-címet egy új lapon Power BI-vizualizációkkal.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 06/18/2019
ms.openlocfilehash: 7e398354ab069bb02554c94312909c0ed835d027
ms.sourcegitcommit: 7aa0136f93f88516f97ddd8031ccac5d07863b92
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/05/2020
ms.locfileid: "79379776"
---
# <a name="create-a-launch-url"></a>Indítási URL-cím létrehozása

Indítási URL-cím létrehozásával új böngészőlapot (vagy -ablakot) nyithat meg a tényleges munka a Power BI-nak való delegálásával.

> [!IMPORTANT]
> A `host.launchUrl()` a Vizualizációk API 1.9.0 verziójában lett bevezetve.

## <a name="sample"></a>Minta

Importálja az `IVisualHost` interfészt és mentse a `host` objektumra mutató hivatkozást a vizualizáció konstruktorában.

```typescript
import powerbi from "powerbi-visuals-api";
import IVisualHost = powerbi.extensibility.visual.IVisualHost;

export class Visual implements IVisual {
    private host: IVisualHost;
    // ...
    constructor(options: VisualConstructorOptions) {
        // ...
        this.host = options.host;
        // ...
    }

    // ...
}
```

## <a name="usage"></a>Használat

A `host.launchUrl()` API-hívással sztringargumentumként adhatja meg a cél URL-címet:

```typescript
this.host.launchUrl('https://some.link.net');
```

## <a name="restrictions"></a>Korlátozások

* Csak abszolút elérési utakat használjon, relatívokat ne. Példa egy abszolút elérési útra: `https://some.link.net/subfolder/page.html`. A `/page.html` relatív elérési út nem nyílik meg.

* Jelenleg csak a *HTTP* és *HTTPS* protokollok támogatottak. Ne használjon *FTP*, *MAILTO* és hasonló protokollokat.

## <a name="best-practices"></a>Ajánlott eljárások

* A legtöbb esetben célszerű csak egy felhasználó explicit műveletére reagálva megnyitni egy hivatkozást. Tegye könnyen érthetővé a felhasználó számára, hogy a hivatkozásra vagy gombra kattintva új lap nyílik meg. Egy `launchUrl()` hívás aktiválása felhasználói művelet nélkül vagy egy másik művelet mellékhatásaként zavaró és bosszantó lehet a felhasználónak.

* Ha a hivatkozás nem elengedhetetlen a vizualizáció megfelelő működéséhez, érdemes lehetővé tenni a jelentés szerzőjének, hogy letilthassa és elrejtse a hivatkozást. Ez különösen fontos különleges Power BI-forgatókönyvekben, például egy jelentés külső alkalmazásba való beágyazásakor vagy a weben való közzétételekor.

* Ne indítson `launchUrl()` hívást hurkon belül, a vizualizáció `update` függvényén belül, vagy egyéb gyakran ismétlődő kódban.

## <a name="a-step-by-step-example"></a>Részletes példa

### <a name="add-a-link-launching-element"></a>Hivatkozásindítási elem hozzáadása

A vizualizáció `constructor` függvényéhez a következő sorok lettek hozzáadva:

```typescript
    this.helpLinkElement = this.createHelpLinkElement();
    options.element.appendChild(this.helpLinkElement);
```

Bővült egy privát függvénnyel, amely a horgonyelemet hozza létre és csatolja:

```typescript
private createHelpLinkElement(): Element {
    let linkElement = document.createElement("a");
    linkElement.textContent = "?";
    linkElement.setAttribute("title", "Open documentation");
    linkElement.setAttribute("class", "helpLink");
    linkElement.addEventListener("click", () => {
        this.host.launchUrl("https://docs.microsoft.com/power-bi/developer/visuals/custom-visual-develop-tutorial");
    });
    return linkElement;
};
```

Végül a *visual.less* fájl egyik bejegyzése definiálja a hivatkozási elem stílusát:

```less
.helpLink {
    position: absolute;
    top: 0px;
    right: 12px;
    display: block;
    width: 20px;
    height: 20px;
    border: 2px solid #80B0E0;
    border-radius: 20px;
    color: #80B0E0;
    text-align: center;
    font-size: 16px;
    line-height: 20px;
    background-color: #FFFFFF;
    transition: all 900ms ease;

    &:hover {
        background-color: #DDEEFF;
        color: #5080B0;
        border-color: #5080B0;
        transition: all 250ms ease;
    }

    &.hidden {
        display: none;
    }
}
```

### <a name="add-a-toggling-mechanism"></a>Váltómechanizmus hozzáadása

Váltómechanizmus hozzáadásához egy statikus objektumot kell hozzáadnia, hogy a jelentés szerzője váltani tudjon a hivatkozáselem láthatósági beállításai között. (Az alapértelmezett beállítás a *rejtett* állapot.) További információért tekintse meg a [statikus objektumok oktatóanyagát](https://microsoft.github.io/PowerBI-visuals/docs/concepts/objects-and-properties).

A *capabilities.json* fájl objektumainak bejegyzése egy `showHelpLink` logikai statikus objektummal bővült, ahogyan az a következő kódban látható:

```typescript
"objects": {
    "generalView": {
            "displayName": "General View",
            "properties":
                "showHelpLink": {
                    "displayName": "Show Help Button",
                    "type": {
                        "bool": true
                    }
                }
            }
        }
    }
```

![Indítási URL-cím kapcsolója](media/launch-url/launchurl-toggle.png)

A vizualizáció `update` függvényéhez a következő sorok lettek hozzáadva:

```typescript
if (settings.generalView.showHelpLink) {
    this.helpLinkElement.classList.remove("hidden");
} else {
    this.helpLinkElement.classList.add("hidden");
}
```

A *rejtett* osztály a *visual.less* fájlban van definiálva, és az elem megjelenítését vezérli.