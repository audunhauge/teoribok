# Funksjoner

## Funksjoner <a id="funksjoner"></a>

En funksjon er en samling av kode inne i et større program som utfører en spesifikk oppgave og er relativt uavhengig av resten av koden.

En funksjon oppfører seg på mye av den samme måten som et vanlig program - men den er ofte kodet slik at den kan brukes flere ganger mens hovedprogrammet kjører. Funksjoner er viktige verktøy i programmering og kan bidra til å strukturere programmer på en god måte.

Objektorientert programmering går som regel ut på å binde sammen funksjoner og data på en logisk måte, et elev-objekt har funksjoner for å skrive ut elevdata osv.

Mange språk har samlinger av funksjoner i funksjonsbibliotek eller klasser \(tenk på Math i actionscript\).

Ofte er det nødvendig å sende verdier inn til funksjonene, disse verdiene kalles for parametre eller argumenter til funksjonen.

Et eksempel på dette er sinus funksjonen.

```javascript
var x = 1.2;
var y = sin(x);
```

Her er x en parameter som brukes av funksjonen sin til å beregne en verdi \(som lagres i variabelen y\).

Mange funksjoner sender tilbake resultatet av en beregning - det gjøres med kommandoen return. Se eksemplene under for bruk av return. Dersom du ikke angir noen return verdi, da vil funksjonen returnere verdien undefined. I javascript kan du bare returnere én verdi, men den kan være en av alle definerte typer/klasser.

### Definere funksjoner <a id="definere-funksjoner"></a>

Du definerer en funksjon på følgende måte:

```javascript
function navnPaaFunksjon(parameter1, p2) {
   // den neste linja er vanlig
   var r;  // verdien som skal returneres
   // programkode
   // en eller flere linjer, løkker, betingelser osv
   // som oftest gir funksjonen en verdi tilbake
   return r;
}
```

Som et eksempel viser vi definisjonen av sin\(\):

```javascript
function sin(x) {
   var y;  // verdien som skal returneres
   // vi bruker en Taylor approximasjon
   // dette er ikke den reelle definisjonen av Math.sin
   y = x - x*x*x/(3*2) + x*x*x*x*x/(5*4*3*2);
   return y;
}
```

Når funksjonen er definert, kan vi bruke den i kode:

```javascript
var x = 0.7657;
var y = sin(x);
console.log(y);
// skriver ut 0.693..
```

Merk at parantesene etter navnet på funksjonen beskriver hvilke data du skal sende til funksjonen.

Definisjonen:

```javascript
/**
 * @param {number} x
 * @returns {number} tilnærma verdi for sinus til x
 */
function sin(x) { … }
```

sier at sin skal ta imot et Number og beregner en ny verdi av typen Number som returneres.

Denne måten å dokumentere en funksjon på er basert på [jsdoc](http://usejsdoc.org/about-getting-started.html).

### Anonyme funksjoner og arrow funksjoner <a id="anonyme-funksjoner-og-arrow-funksjoner"></a>

Du kan også lage funksjoner som ikke blir tildelt et navn.

```javascript
btnBeregn.addEventListener("click", function(e) {
  // utfør beregning
})
```

Denne typen kalles anonyme funksjoner og kan også brukes til å kjøre kode med en gang uten å ta vare på funksjonen. Den kan dermed ikke kjøres omigjen ved et uhell \(da den ikke lenger finnes\).

```javascript
function() {
  let a = 12;  // denne forsvinner etter funksjonen er ferdig 
  // mer kode som kjøres ved oppstart

}();
```

**Merk** de to parantesene til slutt **\(\)** . De vil aktivere den anonyme funksjonen og kjører koden, deretter er funksjonen borte. Dette kan være nyttig ved oppstart av et spill/app.

### Arrow funksjoner <a id="arrow-funksjoner"></a>

En arrow funksjon defineres slik:

```javascript
let  f = e => e + 1;
// f(2) === 3
let skalar = (u,v) => u.x * v.x * + u.y * v.y + u.z * v.z;
let kryss = (u,v) => [u.y * v.z - u.z * v.y  ,  u.z * v.x - u.x * v.z  ,  u.x * v.y - u.y * v.x];
let sin = x => { return x - x²/2 + x³/6;}
let cos = (x) => { return Math.cos(x); }
```

Merk at du trenger paranteser rundt parameterlista dersom den er tom eller har fler enn 1 parameter. Dersom funksjonskroppen bare er et uttrykk - da slipper du skrive **return** eksplisitt. Dersom du bruker { } rundt kroppen - da må du skrive return for å gi tilbake en verdi.

```javascript
  ( )  =>  12;            // en arrow func uten parameter, returnerer 12 som verdi
   x   =>  x * x;         // bare en parameter, slipper parantes
  (x)  =>  x*x+2;         // du kan bruke parantes dersom du ønsker det selv med 1 parameter
 (x,y) =>  x*x + y*y;     // her må du ha paranteser
 (a,b) => { return a+b;}  // når du bruker { } rundt kroppen MÅ du skrive return
```

Den er en forenkla skrivemåte for anonyme funksjoner \(med en del endra egenskaper\).

```javascript
btnBeregn.addEventListener("click", e => { /* kode */  } );
// tillsvarer den anonyme funksjonen for btnBeregn vist tidligere

tall.sort( (x,y) => x - y );
// merk at du ikke trenger return dersom du ikke bruker {} rundt funksjoneskroppen
// tillsvarer tall.sort(function(x,y) { return x - y;})
```

Arrow funksjoner binder ikke **this**. Dermed vil **this** være definert av scopet hvor arrow funksjonen defineres. Dette er ofte ønskelig for eksempler som under:

```javascript
class Person {
  constructor(age) {
    this.age = age;
    setInterval( () => this.age++,1000);
    // i arrow funksjonen vil this være Person sin this
  }
}

var p = new Person(0);
p.age;  // 12
p.age;  // 16  -- alder øker med 1 for hvert sekund
```

Uten arrow funksjon er dette ikke så rett fram

```javascript
this.age = 100;   // den globale this får egenskapen age
class Menneske {
  constructor(age) {
    this.age = age;
    setInterval( function() {this.age++;},1000);
    // den globale this.age øker for hvert sekund
  }
}

var m = new menneske(40);
m.age;  // 40
m.age;  // 40 .. m.age endrer seg ikke
this.age; // 156   ... this.age øker for hvert sekund
```

Her vil funksjonen i setIntervall bruke en this som er kobla til det globale skopet Dermed vil m.age ikke endres.

### Bruke funksjoner <a id="bruke-funksjoner"></a>

Dersom du har definert en funksjon selv eller ønsker å bruke en som er ferdig definert i javascript, så er metoden den samme:

```javascript
navnetPaaFunksjonen();
```

Du kjører koden som funksjonen representerer \(kroppen til funksjonen\) ved å nevne den ved navn - etterfulgt av \(\).

Dersom funksjonen tar parametre sendes disse i parentesene etter funksjonsnavnet - slik som sinus-funksjonen:

```javascript
var y = sin(1.23);
```

Verdien du sender kan være et tall \(slik som over\) eller en variabel. Dersom du bruker en variabel, da hentes verdien ut og sendes til funksjonen - som om du hadde skrevet det tallet som er lagra i variabelen.

```javascript
var x = 1.23;
var y = sin(x);  // tilsvarer sin(1.23)
```

Dette har samme effekt som om du skrev `y = sin(1.23)` siden x inneholder tallet 1.23.

### Avanserte funksjoner <a id="avanserte-funksjoner"></a>

Funksjoner av høyere orden er vanligvis betegnelsen på funksjoner som tar funksjoner som parameter, eller gir tilbake funksjoner som return-verdi.

Vi skal ikke dykke dypt her, men gi en liten innføring.  
Dette temaet kan du lese mer om på nett dersom du søker på _functional programming javascript_.

#### Gjennomgang av alle elementer i en array. <a id="gjennomgang-av-alle-elementer-i-en-array"></a>

Ofte lager vi kode som under for å gå gjennom elementene i en tabell \(array\).

```javascript
// anta var elever er en array
for (var i = 0; i < elever.length; i++) {
  // vi gjør noe med elementet elever[i]
  // f.eks vi kjører en funksjon på elementet
  sendBrev(elever[i]);  // sender email til valgt elev
}
```

Det hadde vært nyttig om vi kunne si

```javascript
  ta denne funksjonen (sendBrev) og bruk den på
  alle elementer i elever
```

Vi kan lage en slik funksjon:

```javascript
function forAlle(arr, handling) {
  for (var i = 0; i < arr.length; i++) {
     handling( arr[i] );
  }
}

// eksempel på bruk
forAlle( elever, sendBrev );
```

#### Alle elementer i en tabell skal endres <a id="alle-elementer-i-en-tabell-skal-endres"></a>

Tenk deg at du har en tabell som inneholder priser for en webshop. Nå har det blitt nødvendig å skru opp prisene med 5%.

```javascript
// anta var priser er en array
for (var i = 0; i < priser.length; i++) {
  priser[i] *= 1.05;   // legger til 5%
}
```

Vi lager en funksjon som kan endre verdiene i en tabell:

```javascript
function endreAlle(arr, endring) {
  for (var i = 0; i < arr.length; i++) {
     arr[i]  = endring( arr[i] );
  }
}

// eksempel på bruk
function prisVekst(pris) { return pris*1.05; }

endreAlle(priser, prisVekst);
```

### Innebygde array-funksjoner <a id="innebygde-array-funksjoner"></a>

De to eksemplene vi har vist er allerede ferdiglaga for array i javascript.

```javascript

elever.forEach(sendBrev);
var nyePriser = priser.map(prisVekst);  
// merk at map lager en ny array
// endreAlle funksjonen vi laga over endrer originalen
```

I tillegg finnes

```javascript
.reduce .reduceRight .each .filter .every .some
```

som er mer avanserte høyere ordens funksjoner. Sjekk dem ut på google ...

