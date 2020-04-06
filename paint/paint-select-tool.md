# Paint - select tool

Vi må kunne velge/selektere shapes slik at vi kan modifisere dem. Typisk flytte/skalere/rotere/farge.  
Metoden jeg velger er at bruker drar opp en firkant over elementer som hun ønsker å endre.  
Da må koden finne alle elementer som har overlapp med denne firkanten. Denne metoden virker også ved klikk på canvas \(en firkant på \(x,y\) med w=h=0\) - en slik firkant vil overlappe alle figurer som den ligger inni. Jeg utvider derfor **Shape** klassen slik at vi har en metode **overlap** som gir true dersom to shapes ligger over hverandre.

{% tabs %}
{% tab title="Overlap" %}
```text
TEORI bak overlap
antar at alle shapes nå har en bb (bounding box) = {x,y,w,h}
de som ikke har de egenskapene w,h må beregne disse.
f.eks Circle kan lage en bb = { x:x-r,y:y+r,w:2r,h2r }
Dette er litt av samme teknikk som brukes i spill - der vil kompliserte
geometrier ha en forenkla versjon (sylinder, box) som brukes til å
sjekke kollisjon.

To firkanter overlapper dersom:

 (a.x,a.y)  ___          
           | a |   <--- a.h
           |___|_____
               |  b  |
               |_____|
                  ^
                  | b.w

 a.x > b.x - a.w OG 
 a.x < b.x + b.w OG
 a.y > b.y - a.h OG
 a.y < by. + b.h
 
Sjekker altså om punktet (a.x,a.y) ligger innenfor den store firkanten
som dannes av a og b, her er (b.x,b.y) utgangspunktet for den store.
```
{% endtab %}

{% tab title="Shape" %}
```javascript
class Shape extends Point {
 
  constructor({ x, y, c, f }) {
    // viser bare ny kode
    this.bb = {x,y,w:0,h:0};  // adjust in subclass
  }
 
  //   render og drawme uendra
   
  // bb skal være {x,y,w,h}
  // dette er beskrevet med jsdoc kommentarer
  overlap(b) {
    const a = this.bb;  // just for shortform
    return (
      a.x > b.x - a.w &&
      a.x < b.x + b.w &&
      a.y > b.y - a.h &&
      a.y < b.y + b.h
      );
  }
}
```
{% endtab %}
{% endtabs %}

Klassene **Square** og **Circle** utvides slik at de setter this.bb. For Circle blir dette   
`this.bb = {x: x-r,y:y-r,w:r+r,h:r+r};`  
Ved bruk av **select** verktøyet tegner vi nå en grå firkant på skjermen på ghost-canvas. Når bruker slipper pekerknappen lager vi en BoundingBox fra AT.start og AT.end. Så finner vi alle Shapes som overlapper denne boksen.

{% tabs %}
{% tab title="Pseudocode" %}
```javascript
// pseudo
  bb er en BoundingBox for AT.start,AT.end
  inside er alle drawings som oppfyller testen
     e.overlap(bb)
  Lagre alle valgte i en liste
  Vis listen på skjermen

DETALJER

Lager en egen static class for å lagre og vise lista
Må da lage kode slik at følgende virker:
  SelectedShapes.list = inside;
  SelectedShapes.show(divShapelist);
  
class SelectedShapes {
  static list = [];
  static show(elm) {
    const s = SelectedShapes.list.map(e => e.info).join("");
    elm.innerHTML = s;
  }
}

Ser da at Shape må få en get info metode:
// viser type shape (Circle|Square) (x,y) og farge/fyll
get info() {
  const { x, y, c, f } = this;
  return `<div>${this.constructor.name} {x:${x} y:${y}} 
          <span style="color:${this.c};background:${this.f}">⬜</span>
          </div>`;
}

Må også lage en divShapelist i html.
```
{% endtab %}

{% tab title="JS" %}
```javascript
case "pointer": {
    const { x, y } = AT.start;
    const { x: a, y: b } = AT.end;
    const bb = { x, y, w: a - x, h: b - y }; // bounding box
    const inside = drawings.filter(e => e.overlap(bb));
    SelectedShapes.list = inside;
    SelectedShapes.show(divShapelist);
    break;
}
```
{% endtab %}
{% endtabs %}

