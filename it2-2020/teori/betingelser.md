# Betingelser



## Betingelser <a id="betingelser"></a>

Alle betingelser er basert på å sammenligne verdier. Vi må da bruke sammenligningsoperatorer:

```text
>               større enn, er a > b ? sann dersom a er størst
≺               mindre enn
>=              større eller lik
≺=              mindre eller lik
!=              forskjellig fra, merk "" != 0 er false
!==             helt forskjellig fra, merk "" !== 0 er true
==              er veldig lik (sammenligning) , merk "" == 0
===                  er identisk lik, merk at "" er ulik 0
&&              og (binder sammen to tester - begge må være sann)
||              eller (binder sammen to tester - bare en trenger være sann)
```

Denne lista har du sett tidligere \(beregninger og uttrykk\), men her har vi bare de operatorene som sammenligner to verdier eller kobler sammen betingelser \( &&, \|\|\).

En sammenligning utføres slik: verdi1 op verdi2  
Her kan du bytte ut verdi1 og verdi2 med variable eller tall/tekst, op kan byttes ut med en av de 8 første fra lista over.

### Kombinasjon av flere betingelser <a id="kombinasjon-av-flere-betingelser"></a>

Du kan som nevnt koble sammen betingelser :

`betingelse1 && betingelse2`  
begge må være true for at resultatet skal bli true \(OG\)

`betingelse1 || betingelse2`  
resultate blir true dersom minst en er true \(ELLER\)

#### Eksempel <a id="eksempel"></a>

Du kan teste eksemplene under i consol:

```text
// følgende tester viser true
 12 > 10    
 "a" < "b"
 120 >= 120
 "" == 0
 "" !== 0
 12 == "12"
 "a" < "b" && 12 > 10
 // resten viser false
 12 === "12"
 12 === "12" || "" === 0
 NaN == NaN
 NaN === NaN   
 // NaN (Not a Number) er ikke lik noe som helst
```

### if - tester <a id="if---tester"></a>

Slike tester bruker vi til å styre handlingene et program skal utføre. For å få det til trenger vi beslutningsstrukturer:

```text
if (betingelse) {
  // kode som skal utføres
  // dersom betingelsen er TRUE
} else {
  // Kode som kjøres 
  // dersom betingelsen er FALSE
}
```

### Switch

Du kan også bruke en annen struktur, switch:

```text
var melding;
var alder = 13;    // endre denne verdien
switch(alder) {
   case 10:
     melding = "10 års jubileum";
     break;
   case 20:
     melding = "20 års jubileum";
     break;
   case 30:
     melding = "30 års jubileum";
     break;
   default:
     melding = "vanlig bursdag";
     break;
}
console.log("Du har ", melding)
```

Den kan gi litt finere struktur dersom du sammenligner innholdet av en variabel mot flere mulige verdier.  
Du kan lett skrive om en switch til if-setninger:

```text
var melding;
var alder = 13;    // endre denne verdien
if(alder === 10) {
     melding = "10 års jubileum";
} else if (alder === 20) {
     melding = "20 års jubileum";
} else if (alder === 30) {
     melding = "30 års jubileum";
} else {
     melding = "vanlig bursdag";
}
console.log("Du har ", melding)
```

