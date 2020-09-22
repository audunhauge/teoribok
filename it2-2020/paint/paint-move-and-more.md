# Paint - move and more

## Operasjoner på valgte elementer

Nå har vi en versjon hvor det er mulig å velge ut en eller flere Shapes. Neste trinn blir da å utføre en handling med de valgte figurene. Starter med de enkleste: slette og flytte. Jeg stjeler litt fra Blender hvor du angir handling slik: g=Grab/flytt x=slett s=scale r=roter. Alle handlinger gjelder valgte elementer.  
For noen av disse spiller det ingen rolle om du har valgt ett eller flere element \(g,x\). For roter blir matten litt komplisert \(trur eg\). For scale ... litt usikker foreløpig.  
Vil også legge til Shift-D for å duplisere valgte shapes. Tror den er enkel.  
To ekstra actions er u \(up\) og d \(down\) som flytter ett valgt element opp/ned i tegnelista. Det elementet som ble lagt til sist - tegnes over tidligere elementer.  
Jeg starter derfor med kode for g \(move\) og x \(slett\).

### Move \(g for grab\)

Jeg har mye av koden som trengs ferdig i koden for select - den registrer start/end på en bevegelse og tegner en firkant på ghost. Move kan gjøre omtrent det samme - må endre posisjon på valgte elementer og tegne på Ghost, men de skal ikke flyttes før peker-knappen slippes. 

{% tabs %}
{% tab title="Pseudo" %}
```text
// Dette er eventhandler for mousemove
case "move":
  beregn vektor:delta fra start til dette punktet
  dersom delta.lengde > 1
    visk ut det som er på ghost
    for shape <- alle valgte shapes
      lagre egenskapene {x,y,bb,c} for shape
      shape.c (farge) = rød
      shape.move(dx)  // antar at .move finnes
      shape.render(gtx) // vis på ghost
      tilbakestill shape med originale {x,y,bb,c}
```
{% endtab %}

{% tab title="JS" %}
```javascript
case "move":
        // show move on ghost canvas
        const p1 = new Vector(AT.start);
        const p2 = new Vector(AT.end);
        const diff = p2.sub(p1);
        if (diff.length > 1) {
          cleanGhost();  // visker ut ghost canvas med clearRect
          for (const s of SelectedShapes.list) {
            const { x, y, c, f } = s;
            // must make a 1 level deeper copy of bb
            let bb;
            {
              const { x, y, w, h } = s.bb;
              bb = { x, y, w, h };
            }
            s.c = "red";
            s.f = "rgba(250,0,0,0.1)";
            s.move(diff);
            s.render(gtx);
            Object.assign(s, { x, y, bb, c, f });
          }
        }
        break;
```
{% endtab %}
{% endtabs %}

Her bomma jeg i første forsøk, jeg skrev `const  bb = s.bb`  som ikke er kopiering, men et alias.  
_Merk at    a = {x:1,y:2};   b = a;   b.x=2;     fører til at    a.x === 2_  
Dermed ble bounding-box endra ved avbrytt flytting \(Escape knappen skal avbryte\).  
I koden over plukker jeg ut tallverdiene \(basic values are not refs\) og da fungerer det.

### X delete \(x for xterminate ? \)

Veldig enkel kode. Jeg filterer drawings arrayet og fjerner alle som finnes i SelectedShapes.  
Deretter tegner jeg opp canvas på nytt \(renderAll\). Må også oppdatere SelectedList - som nå skal være tom og vise den tomme lista.

```javascript
if (Keys.has("x")) {
  drawings = drawings.filter(e => !SelectedShapes.list.includes(e));
  renderAll();
  SelectedShapes.list = [];
  SelectedShapes.show(divShapelist);
}
```

### Up og Down \(u og d\)

Denne handlingen krever at bare en shape er valgt, finner index og bytter plass med over/under.  
Jeg viser bare kode for Up - Down er nesten identisk. Disse trengs slik at en kan legge ett element over et annet som ble tegna senere.

```javascript
if (Keys.has("u") && SelectedShapes.list.length === 1) {
   // move selected shape UP in drawing stack
   // towards end of drawing array
   const shape = SelectedShapes.list[0];
   const index = drawings.indexOf(shape);
   if (index < drawings.length - 1) {
     // not last ie TOP element
     // swap with next higher element
     const temp = drawings[index + 1];
     drawings[index + 1] = shape;
     drawings[index] = temp;
     renderAll();
   }
 }
```

### Escape - avbryt

Legger til egenskapen **AT.abort** . Sjekker denne før en handling fullføres - foreløpig bare **move** som er påvirket.

### Velg farge

Dersom du har valgt en del shapes og klikker på strekfarge eller fyllfarge - så er det rimelig at de valgte får denne fargen. Enkel endring i funksjonene **chooseColor** og **chooseFill**.

```javascript
// Skifter strek-farge
AT.color = t.title;
SelectedShapes.update("c", AT.color);
if (SelectedShapes.list.length > 0) {
  renderAll();
}

// ny metode i SelectedShapes
static update(what, color) {
    for (const s of SelectedShapes.list) {
      s[what] = color;
    }
  }
```

Link til denne versjonen: [https://github.com/audunhauge/jspaint/tree/v1.7](https://github.com/audunhauge/jspaint/tree/v1.7)

