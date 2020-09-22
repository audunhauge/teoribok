---
description: Tegning - grafikk - bilder
---

# Canvas

## Canvas brukt fra javascript

For å bruke canvas må du lage et element:

```text
<canvas id="tegning"></canvas>
```

Du må deretter lage følgende kode for å kunne tegne på dette elementet:

```javascript
let ctx = document.getElementById("tegning").getContext('2d');
// kobling til tegnings-kontekst for canvas ctx = context
const π = Math.PI;   // kjekk å ha

ctx.beginPath();
ctx.fillStyle = 'rgb(200,0,0)';
ctx.arc(200,375,30,0,2*π);
ctx.stroke();
// tegner en sirkel
```

Sjekk ut [denne](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial) tutorial som ligger på mdn. 

Prøv å lage et tegneprogram hvor du kan tegne forskjellige figurer - firkanter, sirkler osv.

Du kan også sjekke ut et større eksempel som viser design av et Paint program - se [link](../../it2-2020/paint/).

