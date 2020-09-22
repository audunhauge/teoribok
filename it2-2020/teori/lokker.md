# Løkker



Ofte vil vi oppdage at vi lager flere kodelinjer som er nesten identiske.

```javascript
  // kode som skriver ut tallene 1..10 i console
  console.log(1);
  console.log(2);
  console.log(3);
  console.log(4);
  console.log(5);
  console.log(6);
  console.log(7);
  console.log(8);
  console.log(9);
  console.log(10);
```

Dette er tungvint å skrive og vanskelig å vedlikeholde.  
Heldigvis har javascript en struktur som tar seg av gjentagelser.  
Vi skal se på det samme eksempelet laget med en **for** løkke.

```javascript
for (let i=1; i<11; i+=1) {
  console.log(i);
}
```

### for-løkke <a id="for-l&#xF8;kke"></a>

Denne løkkestrukturen er den vi bruker mest.  
Strukturen er slik:

```javascript
for (≺startverdi≻; ≺betingelse≻; ≺endring≻) {
  ≺kode som skal gjentas≻;
}
```

For-løkker trenger vanligvis en løkketeller:

```javascript
let i;   // løkketelleren
for (i=1; i<11; i+=1) {
  console.log(i);
}
```

Det er verdiene i denne variabelen som styrer løkka.  
≺startverdi≻ : `i=1` gir startverdi til løkketelleren  
≺betingelse≻ : `i≺11` så lenge som denne betingelsen er sann skal løkka fortsette.  
≺endring≻ : `i+=1` for hver gang løkka kjøres skal verdien i **i** økes med 1.

#### break <a id="break"></a>

Du kan avslutte en løkke før den er ferdig med **break**.

```javascript
const finnEtternavn = inpEtternavn.value;   // henter søkeordet fra skjema
const antallElever = elev.length;  // lengden på arrayet == antall elever
let funnet = false;
for (let i=0; i<antallElever; i+=1) {
  if (elev[i].etternavn === finnEtternav) {
    funnet = true;
    break;   // vi har funnet en elev med riktig etternavn
    // og trenger ikke lete lenger
  } 
}
```

Her brukes _break_ til å bryte ut av en løkke som leter gjennom en tabell.

## **while løkke**

```javascript
let i = 0;
while (i<10) {
    // kode som gjentas 10 ganger
    i++;
}

// eksempel som venter på en betingelse
let betingelse = true;
while(betingelse) {
   // forskjellig kode
   betingelse = testOmNoeHarSkjedd();
}
// Denne passer best som while
```

Merk at en while løkke kan skrives om til en for løkke slik:

```javascript
let i = 0;
while (i<10) {
    // kode som gjentas 10 ganger
    i++;
}

// blir til
for (let i=0; i<10; i++) {
  // kode som gjentas
}
```

Under et eksempel hvor while passer best. Vi vet ikke hvor mange bokstaver vi må bla forbi før første siffer. Vi vet heller ikke hvor mange siffer vi finner i en klynge. Med en for-løkke vil vi helst vite hvor mange ganger vi skal iterere før vi starter løkka.

```javascript
//  finnTall("ole er 12 og per er 16 år") => [12,16]
function finnTall(tekst) {
  const numbers = [];
  const isDigit = ch => "0123456789".includes(ch);
  let i=0; const lengde = tekst.length;
  while (i < lengde) {
    const ch = tekst[i]; 
    i++;
    if (isDigit(ch) ) {
       // fant et siffer
       let strNum = ch;
       // neste løkke suger opp alle påfølgende siffer
       while(i < lengde && isDigit(tekst[i]) ) {
          strNum += tekst[i];  // limer på neste siffer
          i++;
       }
       numbers.push(Number(strNum));
    }
  }
  return numbers;
}
```

