# Last inn bilde

Versjonen vi starter med er [https://github.com/audunhauge/jspaint/tree/v1.12](https://github.com/audunhauge/jspaint/tree/v1.12)

Jeg har lagt til en ny klasse under Shapes - den har navnet Picture.  
Tredje ikon fra toppen i verktøylinja lar deg tegne en firkant som er bilderammen.  
Etter at du har tegna den kan du trykke "liten L" mens peker er på denne rammen. Da vil du få fram et   
"last inn bilde skjema". Dette skjema kommer midt på skjermen og har fast størrelse.  
Dagens oppdrag er å få dette skjemaet til å ligge over bilderammen.

{% tabs %}
{% tab title="Actionkeys.js" %}
```javascript
// ca linje 80 -100 fra denne filen
static l(obj) {
    if (SelectedShapes.list.length === 0) {
      // select shape under pointer
      const p = AT.mouse;
      const inside = drawings.filter((e) => e.contains(p));
      if (inside.length > 0) {
        const target = inside[inside.length - 1];
        if (target.isa("Picture")) {
          const np = g("newpage");

          // plasserer venstre kant omtrent på rammen
          np.style.left = target.x + "px";
          // må gjøre det samme for top,width,height

          
          makeForm(
            np,
            "loadpic",
            () => {
              const loader = g("imgloader");
              loader.addEventListener("change", e => {
                var output = document.createElement("img");
                output.src = URL.createObjectURL(event.target.files[0]);
                output.onload = function () {
                  const {width:tw, height:th} = target;
                  const {width,height} = output;
                  URL.revokeObjectURL(output.src); // free memory
                  const ctx = target.offscreenCanvas.getContext("2d");
                  ctx.drawImage(output, 0, 0,width,height,0,0,tw,th);
                  np.classList.add("hidden");
                  renderCanvas();
                };
              })
            },
            null
          );
        }
      }
    }
  }
```
{% endtab %}
{% endtabs %}

