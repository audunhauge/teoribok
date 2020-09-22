# Øvingsoppgaver

## Arrow functions

{% tabs %}
{% tab title="spill.js" %}
```javascript
function spillOgStop(lyd, tid) {
  lyd.load();  // spiller fra start
  lyd.play();
  setTimeout( () => lyd.pause(), tid);
}
```
{% endtab %}
{% endtabs %}

En arrow function har formen : `(x) => x+2` . Eksemplet viser en funksjon som tar en parameter \(x\) og gir tilbake verdien x+2. Merk at funksjonen ikke har navn og at du ikke trenger å skrive **return**.  
I funksjonen **spillOgStopp** over bruker vi en arrow function på denne måten - den trenger ikke navn da setTimeout tar en funksjon som parameter \(og setter navn på den selv\).  
Dersom funksjonskroppen består av flere linjer - da må en arrow function skrives slik:

{% code title="abc-formel.js" %}
```javascript
const abc = (a,b,c) => {
   let dd = b*b-4*a*c;
   if (dd >=0 && a !== 0) {
     let d = Math.sqrt(dd);
     return ({x1:(-b+d)/(2*a), x2:(-b-d)/(2*a) });
   } else {
     return ({x1:NaN, x2:NaN});
}
```
{% endcode %}

Dersom vi trenger navn på funksjonen bruker vi en av følgende:  
`let dobbel = (x) => 2 * x;`  
`const trippel = (x) => 3 * x;`

### Øvinger

Lag arrow funksjoner :

{% tabs %}
{% tab title="Oppgaver" %}
```javascript
bigName  ("ole") => "OLE"
niceName ("ole") => "Ole"
niceNames ("ole olsen") => "Ole Olsen"
lastNiceName ("ole petter olsen") => "Olsen, Ole Petter"
initialsNiceName ("ole petter olsen") => "O.P. Olsen"
```
{% endtab %}

{% tab title="Løsningsforslag" %}
```javascript
// bigName  ("ole") => "OLE"
const bigName = (n) => n.toUpperCase();

// niceName ("ole") => "Ole"
const niceName = (n) => n.charAt(0).toUpperCase() + n.substr(1).toLowerCase();

//niceNames ("ole olsen") => "Ole Olsen"
// Løsning med arrow functions og Array.map
const niceNames = (n) => n.split(" ").map(e => niceName(e)).join(" ");
// Vanlig function og for-løkke
function niceNames(n) {
  let parts = n.split(" ");
  let nuname = [];
  for (let i=0; i < parts.length; i++) {
     let p = parts[i];   // henter parts på plass [i]
     let np = niceName(p);
     nuname.push(np);
  }
  return nuname.join(" ");
}

//lastNiceName ("ole petter olsen") => "Olsen, Ole Petter"
const lastNiceName = (n) => {
  let parts = n.split(" ");
  let last = parts.pop();
  parts.unshift(last + ",");
  return parts.map(e => niceName(e)).join(" ");
}

//initialsNiceName ("ole petter olsen") => "O.P. Olsen"
const initialsNiceName = (n) {
  let parts = n.split(" ");
  let last = parts.pop();
  let initials = parts.map(e => e.charAt(0).toUpperCase() + ".").join("");
  return initials + " " + niceName(last);
}
```
{% endtab %}
{% endtabs %}

### Oversett disse fuksjonen til arrow notasjon

{% tabs %}
{% tab title="Function" %}
```javascript
function add(a,b) {
  return a+b;
}

function summer(arr) {
  let sum = 0;
  for (let v of arr) {
    sum += v;
  }
  return sum;
}

function finnPersonMedNavn(arr,n) {
  // antar person har .navn
  for (let p of arr) {
    if (p.navn === n) {
      return p;
    }
  }
  return {}  // fant ikke noen
}

function lagNyListeMedFolkFraBy(arr,by) {
  // antar folk.adresse = "Haugesund" osv
  let ny = [ ];  
  for (let p of arr) {
    if (p.adresse === by) {
      ny.push(p);
    }
  }
  return ny;
}
  
```
{% endtab %}

{% tab title="Arrow" %}
```javascript
// her kommer løsningsforslag
const add = (a,b) => a+b;

const summer = (arr) => arr.reduce( (s,v) => s+v, 0 );

const find = (arr, n) => arr.find( p => p.navn === n);

const fraBy = (arr, by) => arr.filter( p => p.adresse === by);
```
{% endtab %}
{% endtabs %}

