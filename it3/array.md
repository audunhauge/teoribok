# Array

Tabeller \(array\) og strenger \(string\) kan lagre samlinger av data. En tabell brukes ofte til å lagre lister med like data. Anta at vi lager en tabell i javascript slik:

```javascript
let elevTabell = [ "Ole","Per","Kari", "Lise","Lars","Oda" ];
```

Da kan du se for deg at tabellen ser slik ut:

| Indeks | Elev |
| :--- | :--- |
| 0 | Ole |
| 1 | Per |
| 2 | Kari |
| 3 | Lise |
| 4 | Lars |
| 5 | Oda |

Som du ser har hvert element sitt nummer \(fra 0\). Dette nummeret tilsvarer adressen til verdien.

Med dette bildet i hodet er det lett å forstå hvordan man henter ut en verdi fra en tabell:

```javascript
NavnPåTabell[indeks]
```

Dette betyr: Hent ut verdien fra NavnPåTabell på plass gitt av indeks.

```text
console.log(elevTabell[3]);
// Skriver ut "Lise"
```

Oppdatering/endring av en verdi skjer på samme måte:

```text
elevTabell[4] = "Lars Even";
```

Legg merke til at all tekst må ha hermetegn rundt seg. Dersom jeg skrev

```text
elevTabell[4] = Lars;
```

da vil js prøve å hente verdien fra en variabel med navnet Lars. Dette vil som oftest gi en feilmelding \(fordi variabelen Lars ikke er definert\).

## Arbeide med tabeller

Vi har tabellen elevTabell som vi nå ønsker å skrive ut

| Indeks | Elev |
| :--- | :--- |
| 0 | Ole |
| 1 | Per |
| 2 | Kari |
| 3 | Lise |
| 4 | Lars |
| 5 | Oda |

For å skrive ut alle elementene i tabellen bruker vi en løkke:

```javascript
let elevTabell = [ "Ole","Per","Kari","Lise","Lars","Oda" ];
let it;  // løkketelleren
let ant = elevTabell.length;  // antall elementer
for (i = 0; i < ant; i++) {
   console.log(elevTabell[i]);
}

// du kan også bruke denne metoden (es2016)
for (let elev of elevTabell) {
  console.log(elev);
}
// i denne løkka tilsvarer elev elevTabell[i]
```

Her ser vi at alle Tabeller \(arrays\) har en innebygd egenskap med navnet length som gir deg antall elementer i tabellen.

Denne er viktig å kjenne til slik at du kan finne lengden på tabellen \(antall elementer\).

## Array funksjoner

| Funksjon | Formål |
| :--- | :--- |
| push\(element\) | Legger til ny verdi bakerst i tabellen. Tabellen vokser. |
| pop\(\) | Henter ut den bakerste verdien, tabellen krymper. |
| shift\(\) | Henter ut den første verdien fra tabellen. De andre verdiene flyttes ned ett hakk. Tabellen krymper. |
| unshift\(element\) | Dytter en ny verdi inn forran i tabellen. De andre verdiene forskyves ett hakk. Tabellen vokser. |
| sort\(\) | Sorterer tabellen |
| indexOf\(element\) | Søker etter verdien i tabellen. Dersom den finnes får du indeksen \[0..\], ellers får du -1. |
| join\(sep\) | Lager en tekst-streng \(string\) av tabellen. Alle elementene i tabellen blir limt sammen med sep i mellom. |
| slice\(start,lengde\) | \[1,2,3\].slice\(0,2\) === \[1,2\] |
| reverse\(\) | \[1,2,3\].reverse\(\) === \[3,2,1\] |
| Sjekk Array funksjoner på nett for flere | Gjør dette dersom du ønsker toppkarakter.Se på map, slice, each |

## Flere dimensjoner

Flerdimensjonale tabeller. Tenk deg at du skal lage et sudoku brett. Brettet er 9 x 9 ruter. Du ønsker å bruke en array til å lagre brettet.

```javascript
let Brett = [
  [ 0,0,0,0,0,0,0,0,0 ],
  [ 0,0,0,0,0,0,0,0,0 ],
  [ 0,0,0,0,0,0,0,0,0 ],
  [ 0,0,0,0,0,0,0,0,0 ],
  [ 0,0,0,0,0,0,0,0,0 ],
  [ 0,0,0,0,0,0,0,0,0 ],
  [ 0,0,0,0,0,0,0,0,0 ],
  [ 0,0,0,0,0,0,0,0,0 ],
  [ 0,0,0,0,0,0,0,0,0 ],
];
```

Du kan nå legge inn tallene dine slik:

```javascript
Brett[0][1] = 4;
Brett[0][2] = 5;
```

Dette kalles en todimensjonal tabell, du må oppgi to verdier for å spesifisere en celle i tabellen \(tilsvarer \(x,y\) i koordinatsystemet\). Du kan selvsagt lage tabeller med flere nivåer \(en tabell inne i en tabell inne i en tabell … …\).  
En mye brukt teknikk er å lage en tabell som inneholder objekter . Et objekt kan for eksempel være informasjon om en elev. Vi kan da lage en tabell med info om elever slik:

```javascript
let arrElever = [
  { fornavn:"Ole", etternavn:"Olsen", klasse:"3A", poeng:20 },
  { fornavn:"Lise", etternavn:"Larsen", klasse:"3A", poeng:22 },
  { fornavn:"Lars", etternavn:"Nilsen", klasse:"3B", poeng:21 }
];
```

## Mer om Array funksjoner

### Funksjoner som endrer verdiene i arrayet <a id="funksjoner-som-endrer-verdiene-i-arrayet"></a>

```javascript
let a = [1,12,4,5,612,44,55,121212];

// sorter a alfabetisk ('1' > '12')
a.sort();  // a === [ 1,12,,121212,4,44,5,55,612]

// sorter a numerisk
a.sort( (x,y) => x - y ); // a === [1, 4, 5, 12, 44, 55, 612, 121212]

// sorter a numerisk synkende
a.sort( (x,y) => y - x ); // a === [121212, 612, 55, 44, 12, 5, 4, 1]

// reverser a 
a.reverse();  // a === [121212, 55, 44, 612, 5, 4, 12, 1]
```

### Funksjoner som gir en ny array som resultat <a id="funksjoner-som-gir-en-ny-array-som-resultat"></a>

```javascript

// største tall i a 
let maksimum = Math.max(...a);  // 121212
// minste tall i a 
let minimum = Math.min(...a);  // 1

// summen av tallene i a 
let total = a.reduce( (sum,v) => sum + v, 0);  // den siste nullen er startverdien for sum
// v vil få verdien til tallene i a i sekvens

// endre tallene i a med et uttrykk/funksjon 
let b = a.map( e => 2 *  e + 4);
// b === [6, 28, 12, 14, 1228, 92, 114, 242428]

// filtrer tallene i a 
let c = a.filter( e => e % 2 === 0);
// c === [12, 4, 612, 44, 121212]

// test om alle tallene i a oppfyller en betingelse
let barePositive = a.every( e => e > 0);
// barePositive === true , fordi alle tall i a er > 0
```

### En innebygd travasering av array-elementer <a id="en-innebygd-travasering-av-array-elementer"></a>

```javascript

// utfør en funksjon for hver verdi i a 
a.forEach(doit);

function doit(verdi, index) {
  // verdi vil være tallene fra a i sekvens
  // index vil være posisjonen verdi har i a (tilsvarer løkkeindeks).
}
```

### Sortere elementer med egenskaper <a id="sortere-elementer-med-egenskaper"></a>

Du kan også sortere array som inneholder objekter.

```javascript
class Elev {
  constructor(fornavn,etternavn,klasse) {
    this.fornavn = fornavn;
    this.etternavn = etternavn;
    this.klasse = klasse;
  }
}

let elever = [];
elever.push(new Elev("ole","olsen","3a") );
elever.push(new Elev("kar","olsen","3a") );
elever.push(new Elev("lasse","olsen","3a") );
elever.push(new Elev("lise","olsen","3a") );

elever.sort( (x,y) => +(x.fornavn > y.fornavn) 
              || +(x.fornavn === y.fornavn) - 1 );
// her sortereres det på fornavn a..z

// denne gjør det samme, men det er litt lettere å se hva som skjer
elever.sort( (x,y) => {
  if (x.fornavn > y.fornavn) return 1;
  if (x.fornavn === y.fornavn) return 0;
  return -1;
} );

// merk at alle funksjoner gitt til sort skal returnere 1,0,-1
// henholdsvis dersom større,lik,mindre
// for sammeligningen mellom x og y
```

