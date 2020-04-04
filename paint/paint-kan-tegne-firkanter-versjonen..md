# Paint - "kan tegne firkanter" versjonen.

Nå legger jeg til de endringene som må til for å kunne plassere pixler på arket.  
Jeg lager en klasse som lagrer info om aktivt verktøy.

{% tabs %}
{% tab title="ActiveTool" %}
```javascript
// AT Active Tool
// denne klassen blir ikke instansiert - den oppfører seg mye som 
// den innebygde Math klassen. Trenger ikke const b = New AT()
// Kan skrive AT.tool = "square"
class AT {
  static tool = "pointer";
  static points = [];
  static start = null;
  static end = null;
  static color = "blue";
  static fill = "transparent";
}

// Fordelen med denne framfor 
// const BAT = { tool:"pointer", .. }
// er at    AT.finnesIkke = 12  vil gi feilmelding i VScode.
// AT godtar bare de egenskapene som er nevnt i klassen, 
// et obj har ingen slike begrensninger.
// Merk at dette ikke gjelder i console - bare i editoren.

// Klassen har navnet AT og ikke ActiveTool da den blir mye brukt i koden.
// Det er en balanse mellom kompakt kode (lett å "se" som ett bilde)
// og beskrivende variabelnavn. Ofte brukte navn - som ActiveTool vil være 
// - kan da (etter min mening) godt forkortes.

// alternativ navnegivning som gir kode som er vanskelig å fange i ett "blikk"
// Ekte kode tatt fra Java-prosjekt på github - i stigende skrekkelighet.
int numberOfSimilarElementsInTheMainList;
int applicativeResourceAllocatorFactoryFactory() { ... };
void SimpleBeanFactoryAwareAspectInstanceFactory() { ... };
boolean InternalFrameInternalFrameTitlePaneInternalFrameTitle 
  PaneMaximizeButtonWindowNotFocusedState = false;
// siste to linjer skal være en sammenhengende linje
```
{% endtab %}

{% tab title="Drawings" %}
```javascript
// For å kunne "Angre" på en operasjon må vi lagre alle figurer i et array

let drawings = [ ];

// denne er ikke const da vi sletter alle tegninger ved å
// skrive    drawings = [ ]
```
{% endtab %}

{% tab title="Ghost css" %}
```css
/* samme regler som for canvas - men med disse i tillegg */
#ghost {
  pointer-events: none;
  position: absolute;
  background-color: transparent;
}
```
{% endtab %}
{% endtabs %}

Ved start er "pointer" det aktive verktøyet, kantfarge blå, fyll gjennomsiktig.  
**drawings**  er array variabelen som skal lagre alle figurene som blir lagt til.  
Jeg legger også til et nytt canvas i html - med id= **ghost** . Denne brukes til forhåndsvisning av tegningen etter hvert som bruker flytter på markøren. Den viskes ut mellom hver tegneoperasjon.  
Den er gjennomsiktig, ligger over canvas og reagerer ikke på pointer-events \(se Ghost css over\).  
**const B**  lagrer \(x,y\) for øvre venstre hjørne på canvas - brukes til å beregne \(x,y\) for pointer.

{% hint style="info" %}
Dersom jeg fikk klager på det korte navnet **B** i en "code review"   
ville jeg kalt den **canvasBoundingRect**.  
Min personlige preferanse er å bruke korte navn på variable som   
forekommer i beregninger slik som  
 **const x = e.clientX - B.x;**   --- det er vanligvis viktigere å forstå   
beregningen/uttrykket enn at variablene har veldig beskrivende navn.   
I dette tilfellet er uttrykket veldig enkelt, men jeg bikker mot kortnavn her.  
Tenk på formler i matte:  
       lengdenTilDenMotståendeSidenTilEnVinkeliEnTrekant ^ 2 =  
       lengdenTilDenOverLiggendeSidenTilVinkelen ^ 2  
       + lengdenTilDenUnderLiggendeSidenTilVinkelen ^ 2   
       - 2 \* lengdenTilDenOverLiggendeSidenTilVinkelen  
             \*  lengdenTilDenUnderLiggendeSidenTilVinkelen  
       \* cos\(vinkelenMellomDenOverliggendeOgDenUnderliggende\).  
Denne finner jeg vanskeligere å "se" enn **a²=b²+c²-2bc\*cos\(A\)** - den siste trenger forklaringer på hva variablene betyr, men det kan godt være kommentarer. Nå er det alltid en spenning mellom disse to syn. Du må selv finne en løsning som fungerer for deg og teamet ditt. Tenk også på framtidige folk som skal vedlikeholde koden din.
{% endhint %}

Nå legger jeg til funksjoner som reagerer på hendelser - click på verktøy - mouse-events på canvas.  
Disse er relativt enkle nå i starten - regner med at de får vorter etter hvert.

{% tabs %}
{% tab title="EventListeners" %}
```javascript
divTools.addEventListener("click", activateTool);
divColors.addEventListener("click", chooseColor);
divFill.addEventListener("click", chooseFill);

/* tool-use activated by mouse-down */
canCanvas.addEventListener("mousedown", startAction);
canCanvas.addEventListener("mouseup", endAction);
```
{% endtab %}

{% tab title="activateTool" %}
```javascript
function activateTool(e) {
    const t = e.target;
    if (t.title) {
      AT.tool = t.title;
      // some tools have a simple action
      // some have no submenues
      switch (t.title) {
        case "erase":
          ctx.clearRect(0, 0, 1024, 800);
          AT.fill = "transparent";
          AT.color = "blue";
          AT.tool = "pointer";
          break;
        case "polygon":
        case "polyline":
          // just so they dont reach default
          break;
        default:
          // all others are subtools
          // so we set parent radio to checked
          {
            if (t.dataset && t.dataset.parent) {
              const p = document.getElementById(t.dataset.parent);
              /**  @type {HTMLInputElement} */
              (p).checked = true;
            }
          }
          break;
      }
    }
  }
```
{% endtab %}

{% tab title="startAction" %}
```javascript
function startAction(e) {
    const x = e.clientX - B.x;
    const y = e.clientY - B.y;
    AT.start = { x, y };
    canCanvas.addEventListener("mousemove", showGhost);
  }
```
{% endtab %}

{% tab title="endAction" %}
```javascript
function endAction(e) {
    if (AT.start) {
      // must have valid start
      {
        const x = e.clientX - B.x;
        const y = e.clientY - B.y;
        AT.end = { x, y };
      }
      {
        const shape = makeShape(ctx, AT.start, AT.end);
        if (shape) {
          drawings.push(shape);
        }
      }
    }
    canCanvas.removeEventListener("mousemove", showGhost);
    if (AT.tool !== "pgon") {
      gtx.clearRect(0, 0, 1024, 800);
      AT.start = null;
    }
  }
```
{% endtab %}

{% tab title="showGhost" %}
```javascript
function showGhost(e) {
    if (AT.start) {
      // must have valid start
      {
        const x = e.clientX - B.x;
        const y = e.clientY - B.y;
        AT.end = { x, y };
      }
      const P = new Vector(AT.start);
      const Q = new Vector(AT.end);
      const delta = P.sub(Q).length;
      if (delta > 2) {
        gtx.clearRect(0, 0, 1024, 800);
        makeShape(gtx, AT.start, AT.end);
      }
    }
  }
```
{% endtab %}

{% tab title="makeShape" %}
```javascript
function makeShape(ctx, start, end) {
    let shape;
    const c = AT.color;
    const f = AT.fill;
    switch (AT.tool) {
      case "square":
        {
          const { x, y } = start;
          const P = new Vector(start);
          const Q = new Vector(end);
          const wh = P.sub(Q);
          const w = Math.abs(wh.x);
          const h = Math.abs(wh.y);
          if (h > 0 && w > 0) {
            shape = new Square({ x, y, w, h, c, f });
            shape.render(ctx);
          }
        }
        break;
      case "circle":
        {
          const { x, y } = start;
          const P = new Vector(start);
          const Q = new Vector(end);
          const wh = P.sub(Q);
          const r = Math.round(wh.length * 10) / 10;
          if (r > 1) {
            shape = new Circle({ x, y, r, c, f });
            shape.render(ctx);
          }
        }
        break;
      default:
        break;
    }
    return shape;
  }
```
{% endtab %}
{% endtabs %}

**chooseColor** og **chooseFill** er fra tidligere versjoner.  
**activateTool** skal hovedsaklig sette **At.tool** til **title** på verktøyet som ble klikka.  
   default i switch fixer et problem med verktøy-menyen som jeg ikke klarte å løse i CSS.  
**startAction** blir trigga ved **mousedown** på canvas. Setter **AT.start** til \(x,y\) for pointer.  
   starter også en eventlistener på **mousemove** som kjører **showGhost** .  
**endAction** blir trigga ved **mouseup** på canvas. Lagrer \(x,y\) i AT.end. Kjører **makeShape** som gir tilbake  
   en gyldig shape dersom det går. Denne shapen blir dytta inn i **drawings** arrayet.  
   Fjerner event-handler for **mousemove** og tømmer ghost for innhold.  
**showGhost** tegner opp figuren slik den vil bli dersom du slipper pekerknappen nå.  
  Den tester om du har flytta markøren mer enn 2px og tegner da shapen på ghost.  
**makeShape** tegner en figur på et gitt canvas, bruker Vector klassen til å finne avstand mellom to punkt.  
  

