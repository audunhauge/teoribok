# Uke 43

## Animasjon med css

Vi lager et spill med en start-animasjon.

```css
#snake {
    position: absolute;
    left: 0px;
    top: 0px;
    background-image: url("snake.png");
    background-position: center;
    background-size: 200px 200px;
    height: 200px;
    width: 200px;
    background-repeat: no-repeat;
    transform: scaleX(-1);
    animation: crawl 10s linear infinite;
}

@keyframes crawl {
    0% { left: 0px; top: 0px;  transform: scaleX(-1);}
    29.9% { left: 500px; top: 0px;  transform: scaleX(-1);}
    30% { left: 500px; top: 0px;  transform: scaleX(1);}
    50% { left: 500px; top: 400px; transform: scaleX(1);}
    80% { left: 0px; top: 400px; transform: scaleX(1);}
   100%  { left: 0px; top: 0px; transform: scaleX(1);}
}
```

Merk knepet med å lage to keyframes på omtrent samme tidspunkt : 29.9% og 30%.  
Dette brukes dersom vi har en egenskap som skal ha en brå endring.  
Denne typen animasjoner er typisk for den første oppgaven i eksamens-sett.

I tillegg bør dere kunne redigere bilder: endre størrelse, beskjære og sette på gjennomsiktig bakgrunn.

Husk at det også kan være oppgaver som går ut på redigering av lyd eller video.

## Switch i javascript

Dersom en skal teste en variabel mot flere mulige verdier - da kan det passe å bruke **switch** .

I spillet vi lager \(snake.js\) skal vi reagere på fire forskjellige tastetrykk. Dette gjør vi med en event-listener som sjekker verdien på keyCode.

{% tabs %}
{% tab title="switch.js" %}
```javascript
function tastTrykkes(e) {   // merk at vi MÅ ta imot e her
  switch(e.keyCode) {
    case 37:
      // kode for å kjøre til venstre
      break;
    case 38:
      // kode for å kjøre til opp
      break;    
    case 39:
      // kode for å kjøre til høyre
      break;    
    case 40:
      // kode for å kjøre til ned
      break;
    default:
      // alle andre tastetrykk
      break;
  }
}
```
{% endtab %}

{% tab title="if\_else.js" %}
```javascript
function tastTrykkes(e) {   // merk at vi MÅ ta imot e her
  if (e.keyCode === 37 ) {
      // kode for å kjøre til venstre
  } 
  else 
  if (e.keyCode === 38) {
      // kode for å kjøre til opp
  } 
  else 
  if (e.keyCode === 39) {
      // kode for å kjøre til høyre
  } 
  else 
  if (e.keyCode === 40) {
      // kode for å kjøre til ned
  }
  else {
      // kode for alle andre tastetrykk
  }
}
  
```
{% endtab %}
{% endtabs %}

Typisk bruk for en switch er der hvor en variabel testes mot mange forskjellige muligheter.  
Sammenlign løsningene over som bruker switch eller if-else.

