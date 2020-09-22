# Praktiske eksempler



## Variabeldeklarasjoner

```text
let tall = 12;
let navn = "ole";
let elev = { fornavn:"ole", etternavn:"olsen" };
let ferdig = false;
let tabell = [ 1,2,3 ];
```

### Const <a id="const"></a>

```text
const BREDDE = 12;
const NAVN = "ole";
const ELEV = { fornavn:"ole", etternavn:"olsen" };
const FERDIG = false;
const TABELL = [ 1,2,3 ];
```

Merk at enkle const slik som BREDDE,NAVN,FERDIG ikke kan modifiseres.

* Denne koden er gyldig: ELEV.fornavn = "ole hetland" // eleven har fått ett nytt mellomnavn
* Denne er ugyldig: ELEV = { fornavn:"ole hetland, etternavn:"olsen" } // lager ny elev
* Denne koden er gyldig: TABELL.push\(4\); // endrer innholdet i TABELL
* Denne er ugyldig: TABELL = \[1,2,3,4\]; // Lager ny tabell

## Interaksjon med skjema/html

```text
// hent verdi fra tekstfelt
let inpNavn = document.getElementById("navn");
let navn = inpNavn.value;

// hent inn en tallverdi
let inpAlder = document.getElementById("alder");
let alder = inpNavn.valueAsNumber;

// vis tekst i en div
let divTekst = document.getElementById("tekst");
divTekst.innerHTML = " tekst som skal vises";

// funksjon aktivert av en knapp
let btnBeregn = document.getElementById("beregn");
btnBeregn.addEventListener("click", beregning);

function beregning(event) {
    // kode ...
    // typisk linjene over som henter data fra skjema/viser data
}
```

## Legge html elementer til en div

```text
let divMain = document.getElementById("main");
let btnKlikkMeg = document.createElement("button");
btnKlikkMeg.id = "klikkmeg";
btnKlikkMeg.innerHTML = "Klikk Meg";
btnKlikkMeg.addEventListener("click",duKlikkaMeg);
divMain.appendChild(btnKlikkMeg);
// du må også lage funksjonen duKlikkaMeg
```

## Beregninger

```text
let verdi = (12 + 3) / 4;
let vinkel = Math.asin(3/4);
let minst = Math.min(verdi, vinkel);
```

## Betingelser og valg

**enkel if**

```text
// enkel if
if ( betingelse ) {
    // handling dersom sann
} else {
    // handling dersom usann
}
```

**if else if**

```text
if ( betingelse1 ) {
    // handling dersom betingelse1
} else if ( betingelse2 ) {
    // handling dersom betingelse2
}
// kan gjentas med så mange betingelser som nødvendig
```

## Switch

Kan brukes for både tall og tekst

{% tabs %}
{% tab title="Tekst" %}
```javascript
switch(key) {
  case "en":
    // kode for dette tilfellet
    break;
  case "to":
    // kode
    break;
  case "tre":
  case "fire":
    // kode for 3 og 4
    break;
  default:
    // alle andre
}
```
{% endtab %}

{% tab title="Tall" %}
```javascript
switch(key) {
  case 12:
    // kode for dette tilfellet
    break;
  case 13:
    // kode
    break;
  case 14:
  case 15:
    // kode for 14 og 15
    break;
  default:
    // alle andre
}
```
{% endtab %}
{% endtabs %}

## Løkker

**for løkke**

```javascript
for (let i=0; i < 10; i++) {
    // kode som gjentas 10 ganger
}
```

**while løkke**

```javascript
let i = 0;
while (i<10) {
    // kode som gjentas 10 ganger
    i++;
}
```

**travasering av array**

```javascript
// vi antar at tabell er en array
let antall = tabell.length;
for (let i=0; i < antall; i++) {
    let verdi = tabell[i];
    // kode som gjør noe med hver verdi
}
```

En moderne variant \(es6\)

```javascript
// vi antar at tabell er en array
for (let verdi of tabell) {
    // kode som gjør noe med hver verdi
}
```

**finn minste / største verdi i en array**

```javascript
// vi antar at tabell er en array av tall
// f.eks tabell = [1,2,3-5,8,0,1222]
let minst = Math.min( ... tabell);
let storst = Math.max( ... tabell);
// ... er spread operatoren
```

## Lese en fil

{% hint style="info" %}
#### NB! Denne metoden virker bare dersom du laster sida fra en webserver.
{% endhint %}

I eksemplene under antar vi at funksjonen **behandle** tar seg av bearbeiding av motatt data.

Koden under bruker fetch metoden som støttes av moderne nettlesere slik som Chrome og Firefox.

```javascript
let url = "elevliste.json";
fetch(url).then(r => r.json())
  .then(data => behandle(data))
  .catch(e => console.log("Dette virka ikke."))
```

## Kjøre kode etter en delay \(forsinkelse\)

```javascript
setTimeout(() => {
    // denne koden kjøres etter 400ms
}, 400);
```

## Summere opp verdier fra et array

```javascript
// for et array med rene tallverdier kan du bruke denne
let a = [ 1,2,3,4,5,6,7,8,9,10 ];
let sum = a.reduce( (sum, verdi) => sum+verdi, 0);

// for en array av objekter
let a = [ { navn:"ole", poeng:12 } , {..}, ... ];
let sum = a.reduce( (s,e) => s + e.poeng, 0 );

// array av objekter, men med antall og pris
let a = [ { vare:"spiker", antall:1000, pris:0.3 },
          { vare:"hammmer", antall:2, pris:217 }, .... ]
let sum = a.reduce( (s,e) => s + e.antall * e.pris, 0 );
```

## Finne verdier/plassering i en array

```javascript
// sjekk om et tall finnes i et array
let a = [ 1,2,3,4,5 ];
if (a.includes(3) { /* kjøres dersom 3 finnes i a */ }
// det samme for tekst
let s = "det er en fin dag"
if (s.includes("fin") { .... }

// finn POSISJON til en verdi
let p = a.findIndex( e => e === 3 ) // p = 2
let q = a.findIndex( e => e > 3 )  // q = 3
// q finner posisjon til første verdi som er større enn 3
let nope = a.findIndex(e => e > 100) // nope = -1, ikke funnet

// finn en VERDI som oppfyller et krav
let odd = a.find( e => e > 3 && e % 2 === 0) // finner 5
let kvad = a.find( e => Number.isInteger(Math.sqrt(e)) ) // finner 4

// Finn alle verdier som oppfyller et krav
// Merk at nå er resultatet et array
let partall = a.filter(e => e%2 === 0) // [2,4]
let odde = a.filter(e => e%2 === 1) // [1,3,5]
```

## Endre alle verdier i et array

```javascript
// øke alle verdier med 20%
// elementene { } kan inneholde flere egenskaper
let vareListe = [ { pris:200 }, { pris:300 } ]
vareListe.forEach( e => e.pris *= 1.2 );

// plukk ut prisene (bare tallverdiene)
let priser = vareListe.map(e => e.pris)
// priser = [ 200,300 ]

// endre alle ord til uppercase
let ord = "mange ord som skal bli uppercase".split(" ")
let storeOrd = ord.map(e => e.upperCase() );
// storeOrd = [ "MANGE","ORD", ... ]
```

