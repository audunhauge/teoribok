# Ballspill

Poenget med dette spillet er å ta i bruk betingelser, løkker og array.  
Du skal også kunne lage en enkel funksjon som gir tilbake en verdi.  
For at spillet skal fungere må jeg ta med en del ting som ikke er pensum ennå - konsentrer deg om de temaene som er nevnt.

{% tabs %}
{% tab title="class Ball" %}
```javascript
/**
  Du skal kunne lage en enkel klasse med egenskaper.
  Funksjoner i klasser er ikke pensum ennå, men
  må være med for at spillet skal fungere.
*/

class Ball {
    x = 0;
    y = 0;
   
    // en del kode tatt bort
}

/**
 * ballTabell inneholder alle ballene i spillet
 */
const ballTabell = [];
let antall = 20;
```
{% endtab %}

{% tab title="flyttPaaBallen" %}
```javascript
/**
  Jeg vet at jeg har   antall   baller lagra i
  ballTabell. Jeg lager en for-løkke som 
  går gjennom alle elementene i arrayet.
  Merk at jeg først henter ut en ball fra
  lista med baller:   b=ballTabell[i]
  Deretter kan jeg oppdatere posisjonen til
  ballen:   b.x += b.v
  Så sjekker jeg at ballen er innenfor grensene
  if (b.x .... ) {  }
  Helt til slutt (inne i løkka) tegner jeg
  ballen på den nye posisjonen.
*/
function flyttPaaBallen() {
    for (let i = 0; i < antall; i += 1) {
        const b = ballTabell[i];
        b.x += b.vx;
        b.y += b.vy;
        if (b.x > 500 - b.w) {
            b.vx = -maxX;
            b.div.style.backgroundColor = rndColor();
        }
        if (b.x < 0) {
            b.vx = maxX;
            b.div.style.backgroundColor = rndColor();
        }
        if (b.y > 500 - b.h) {
            b.vy = -maxY;
            b.div.style.backgroundColor = rndColor();
        }
        if (b.y < 0) {
            b.vy = maxY;
            b.div.style.backgroundColor = rndColor();
        }
        b.tegnPaaSkjerm();
    }
}
```
{% endtab %}

{% tab title="rndColor" %}
```javascript
/**
 Skal kunne lage en funksjon som beregner og gir
 tilbake en verdi.
 Lager en tabell colors med en del fargenavn.
 Denne kan også skrives slik:
   const color = [ "red","green", ... ]
 men legg merke til at jeg da må skrive mange ""
 Med split() kan jeg klippe opp en tekst og få
 eksakt samme tabell/array.
 antall   er antall farger i tabellen
 indeks   er en tilfeldig posisjon i tabellen
 return   gir tilbake verdien på høyre side.
*/

function rndColor() {
    const colors = 
      "red,green,blue,yellow,pink,teal,aqua,orange"
      .split(",");
    const antall = colors.length;
    const indeks = Math.trunc(Math.random() * antall);
    return colors[indeks];
}
```
{% endtab %}
{% endtabs %}

