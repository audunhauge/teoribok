---
description: Teori for it3
---

# Variable og funksjoner

## Variable

En variabel i javascriptEn variabel er en navngitt beholder som kan inneholde en verdi. Denne verdien kan hentes ut \(brukes i en beregning\) eller endres/oppdateres.

 I javascript må variabelnavn begynne med en bokstav. De kan inneholde bokstaver, tall \_ og $. Du kan ikke bruke punktum eller mellomrom. 

Vanligvis skal en variabel begynne med liten bokstav \(stor førstebokstav brukes ofte for klasser\). Bruk deskriptive navn, men de bør ikke være for lange \(da kan koden bli vanskelig å lese\). 

En del variabelnavn er standard slik som i, j og k for løkketellere, x,y,z for posisjon i rommet. Utenom disse bør du helst ha deskriptive navn, men du kan godt bruke i istedenfor løkketeller. 

Du bør unngå å havne i java-land hvor de lager variabel/funksjonsnavn som dette:

```java
int numberOfSimilarElementsInTheMainList;
int applicativeResourceAllocatorFactoryFactory() { ... };
void SimpleBeanFactoryAwareAspectInstanceFactory() { ... };
boolean InternalFrameInternalFrameTitlePaneInternalFrameTitlePaneMaximizeButtonWindowNotFocusedState = false;
```

### Variabeldeklarasjon

Øverst i alle js filene dine bør du skrive :

```javascript
// @ts-check
```

Dette er en melding til vs-code om at du ønsker feilmeldinger dersom du bruker en variabel uten først å ha deklarert den.

Test ut koden under i consol \(høyre-klikk + inspiser i chrome\)

```javascript
let antall = 0;   
    // en variabel som inneholder tall
    // javascript vil automatisk gi variabelen typen Number

antall += 1;   // øk verdien i antall med 1

let i;   
    // en ny variabel med navnet i - den er udefinert
    // dvs den har ikke noen verdi (undefined)

i = 5;  
    // nå gir vi verdi til variabelen, den har nå typen Number

i = i + 2;
    // verdien lagra i i er nå 7

i = i + antall;
    // dersom en variabel står på venstre side av likhetstegnet
    // - da får den ny verdi (verdien av høyresida)
    // dersom en variabel brukes på høyresida da erstattes 
    // variabelen med verdien den har
    // i får verdien 7 + 1, dvs i er nå 8
```

## Funksjoner

En funksjon er en samling av kode inne i et større program som utfører en spesifikk oppgave og er relativt uavhengig av resten av koden. 

En funksjon oppfører seg på mye av den samme måten som et vanlig program - men den er ofte kodet slik at den kan brukes flere ganger mens hovedprogrammet kjører. Funksjoner er viktige verktøy i programmering og kan bidra til å strukturere programmer på en god måte. 

Objektorientert programmering går som regel ut på å binde sammen funksjoner og data på en logisk måte, et elev-objekt har funksjoner for å skrive ut elevdata osv. 

Mange språk har samlinger av funksjoner i funksjonsbibliotek eller klasser \(tenk på Math i actionscript\). 

Ofte er det nødvendig å sende verdier inn til funksjonene, disse verdiene kalles for parametre eller argumenter til funksjonen. Et eksempel på dette er sinus funksjonen.

```javascript
let x = 1.2;
let y = sin(x);
```

Her er x en parameter som brukes av funksjonen sin til å beregne en verdi \(som lagres i variabelen y\). 

Mange funksjoner sender tilbake resultatet av en beregning - det gjøres med kommandoen return. Se eksemplene under for bruk av return. Dersom du ikke angir noen return verdi, da vil funksjonen returnere verdien undefined. I javascript kan du bare returnere én verdi, men den kan være en av alle definerte typer/klasser.

### Definere funksjoner

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

{% tabs %}
{% tab title="sin.js" %}
```javascript
function sin(x) {
   var y;  // verdien som skal returneres
   // vi bruker en Taylor approximasjon
   // dette er ikke den reelle definisjonen av Math.sin
   y = x - x*x*x/(3*2) + x*x*x*x*x/(5*4*3*2);
   return y;
}

```
{% endtab %}

{% tab title="cos.js" %}
```javascript
function cos(x) {
   var y;  // verdien som skal returneres
   // vi bruker en Taylor approximasjon
   // dette er ikke den reelle definisjonen av Math.cos
   y = 1 - x*x/(1*2) + x*x*x*x/(4*3*2);
   return y;
}


```
{% endtab %}

{% tab title="atan.js" %}
```javascript
function atan(x) {
   var y;  // verdien som skal returneres
   // vi bruker en Taylor approximasjon
   // dette er ikke den reelle definisjonen av Math.atan
   // best presisjon for små verdier av x
   y = x - x*x*x/3 + x*x*x*x*x/5 - x*x*x*x*x*x*x/7;
   return y;
}

```
{% endtab %}
{% endtabs %}



