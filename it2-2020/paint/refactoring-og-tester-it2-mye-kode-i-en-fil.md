# Refactoring og tester \(it2\) - mye kode i en fil

## Grunn til å bryte opp

Nå har paint.js vokst ubegrenset siden starten på prosjektet. I de første versjonene var det rimelig greit å finne fram og få oversikt over hva som skjer i koden. Nå har filen blitt 650 linjer - noen funksjoner er på over 100 linjer \(ser bort fra setup som fungerer som et slags skall rundt de indre funksjonene\).  
Filen inneholder oppstartkode \(setup\), klasser, gui-events og mye mer. Det er på tide å splitte opp i mer logiske enheter. 

Dette er selvsagt ikke noe du gjør på eksamen eller heldag, men du kan skrive en kommentar om at det kan bli nødvendig. Det er alltid en risk for at fungerende kode slutter å fungere dersom du bryter koden opp i flere filer.

Derfor ville jeg før jeg brøt opp koden \(refactoring\) sørge for at jeg hadde tester på plass slik at det er enkelt å teste om systemet virker etter hver endring. Da kan jeg lage en ny fil, flytte kode og teste om systemet fortsatt virker \(uten å gå gjennom appen som en bruker - testene finner feil automatisk\).

### Automatiske tester

I et større system bør disse testen kjøres automatisk \(på hver kommit f.eks\).  
Jeg går ikke inn på hvordan du kan sette opp for slike tester, men det finnes mange løsninger for dette \(chai , mocha osv\). Jeg legger til et enkelt lite testbibliotek som jeg har laga selv \(for å vise at det ikke er magi\). Denne kjøres fra **setup** slik at vi slipper å gjøre andre grep.

### Hvordan teste et tegneprogram

Anta at vi har en versjon som virker. Vi lager en tegning og lagrer **drawings** \(arrayet\) som tekst. Vi lagrer canvas som en png og tar en crc-checksum på dette bildet. Vi kan lage flere slike oppskrifter \(serie med shapes lagra i drawings\) sammen med checksum for bildet som skal lages.  
For å teste en ny versjon av Paint sender vi inn listen med tegnekommandoer - lagrer bilde - beregner crc og sammenligner. Den nye versjonen er ok dersom alle crc er like.

Dersom vi gjør endringer slik at en ikke kan forvente samme bilde med samme drawings array - \(f.eks default linjetykkelse er endra\) - da må settet med crc genereres på nytt - eller drawings må endres slik at vi setter linjetykkelse til det den var som default før.

I vårt eksempel hopper vi over testing foreløpig og begynner med =&gt;

### Refactoring

**Refactoring** - bryte koden opp i mindre biter.

Jeg skiller først ut alle klassene i en fil - Shapes.js. En kunne godt ha en klasse pr fil, men da de er relativt korte/enkle samler jeg dem i en. Merk at browsere har støtte for å laste modules - tester ikke dette ut nå.

Lag en ny fil **Shapes.js** . Flytt alle klassene over til denne filen. Sørg for at denne filen blir lasta før paint.js i  paint.html \(se linje 10\). Rekkefølgen er viktig - da Shapes må være definert før bruk i paint.js

Test at programmet fortsatt virker ...

### Endre funksjoner slik at de er "pure" dersom det er mulig.

En _**pure**_ function er bare avhengig av input-parametre og påvirker/endrer ikke verden - bortsett fra at de kan gi tilbake en verdi/verdier.  
Ser at jeg egentlig bare har en slik funksjon: g som jeg legger inn i Shapes.js  
Dersom jeg hadde flere ville jeg hatt en egen fil for dem.  
De andre endrer canvas og ghost - kan ikke lett gjøres pure.

### Splitte opp lange funksjoner

Jeg har tre lange funksjoner - **keyAction, activateTool** og **makeShape**.  
Disse vil sannsynligvis vokse seg enda større når nye kommandoer/figurer legges til.  
I denne versjonen bruker begge en switch til å velge hvilken handling som skal utføres. Jeg tror kanskje det blir enklere kode med en function-dispatcher - dvs en tabell hvor en slår opp og finner funksjonen som skal kjøres. Jeg flytter også en god del funksjoner ut av **setup** slik at de ikke er lokale funksjoner.  
De må da få tilsendt parametre slik som **ctx** og **gtx**. Fordelen med å ha dem utenfor setup er at de da blir enklere å teste. Ulempen er at variable definert i **setup** må sendes som parametre.

Jeg prøver først å flytte **activateTool**. Ser da at en mengde andre må også flyttes:  
**activateTool** krever **cleanGhost**, **cleanCanvas**, **renderAll** og **divShapelist**.   
**cleanGhost** og **cleanCanvas** endres til let, defineres før **setup**, tildeles funksjonskropp i **setup**. De kan da brukes utenfor **setup**.  
**renderAll** får nå **ctx** som parameter - det gjør også **activateTool** - den får i tillegg **divShapelist**.  
For å få dette til må jeg endre måten jeg setter opp eventlistener for click på canvas  
før :      `divTools.addEventListener("click", activateTool)`  
etter:    `divTools.addEventListener("click", e => activateTool(e,ctx,divShapelist));`  
Du kan ikke sette parameter for en eventlistener - den tar automatisk en parameter - en event.  
For å løse problemet lager jeg en anonym eventlistener som kaller activateTool med ctx og divShapelist.

Etter disse endringene ser jeg gjennom koden får å sjekke om ts-check finner noen opplagte feil. Ingen røde streker gjør at jeg saver og sjekker for hånd. Ser at **renderAll** ikke har jsdoc - skriver inn denne.  
Får da plutselig mange feilmeldinger for feil bruk av **renderAll**\(\) andre plasser i koden.  
Fikser **renderAll**\(\) til **renderAll**\(**ctx**\) der hvor vs-code markerer feil.

En annen fordel med å flytte ut funksjoner fra setup er at de nå blir dokumentert av jsdoc. Jsdoc dokumenterer ikke indre-funksjoner \(uklart hvorfor ikke\).

Etter disse endringene tester jeg programmet \(her hadde vært kjekt med automatiske tester\). Det ser ut til å virke. Nå kan jeg prøve meg med en function-tabell og oppslag i stedenfor en switch.

Den nye koden er slik:

{% tabs %}
{% tab title="JavaScript" %}
```javascript
function activateTool(e,ctx,divShapelist) {
  const t = /** @type {HTMLElement}*/ (e.target);
  if (t.title) {
    AT.type = "shape"; // assume a shape
    const toolName = t.title;
    if (Tools[toolName]) {
      Tools[toolName]({t,ctx,divShapelist});
    } else { 
      Tools.default(t)
    }
  }
}
```
{% endtab %}
{% endtabs %}

Den forrige versjonen var på ca 50 linjer \(en stor switch\) og ville vokse når nye verktøy blir lagt til.  
Nå er hver case i den switchen splitta ut som en egen funksjon - en static func i klassen Tools - denne har samme formål som klassen Math - samler funksjoner som har et felles tema.

{% hint style="info" %}
Klassene AT, Tools, MakeShapes o.l. er litt spesielle.  
For å dokumentere disse klassene bruker jeg @namespace i jsdoc. Det gir en kompakt og fin doc på alle de statiske funksjonene i en slik klasse - klassen fungerer egentlig som en slags innpakning for funksjoner med et felles formål.
{% endhint %}

### One for all and all for Al  \(Al Capones valgspråk\).

Samme framgangsmåte som vist over kjøres på de tre andre store switch-funksjonene.  
Resultatet er en ny versjon - link: [https://github.com/audunhauge/jspaint/tree/v1.8](https://github.com/audunhauge/jspaint/tree/v1.8)

**makeShapes** kan også skrives som under med den nye **?.** operatoren.  
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional\_chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

```javascript
function makeShape(ctx, gtx, start, end) {
  // using the new Optional chaining operator ?.
  // IF makeshapes has this tool THEN run the function
  // ELSE return undefined
  return MakeShapes[AT.tool]?.({ gtx, ctx, start, end });
}
```

Det går fordi vi ikke trenger noen default kode som for **activateTool** .  
**Dersom** MakeShapes har dette verktøyet **Da** aktiveres det, ellers skjer ingenting.

