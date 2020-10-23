# World map

Det er et stort sprang siden sist - jeg har lagt til kode som lager et verdenskart.  
Foreløpig er verden 80x80 ruter - den består av ca 10 øyer som kan vokse sammen \(tilfeldig variasjon\). Du kan få separate øyer - eller sammenhengende landmasser.  
Jeg har lagt til en Stifinner-modul som finner veien fra et punkt til et annet på kartet - der det er mulig å gå \(bruker Astar algoritmen\).

Disse relativt store modulene kan vi betrakte som ferdig kode som bare skal kunne brukes - trenger ikke å forstå koden i detalj. Jeg har også fjerna en del moduler jeg testa ut for å lage kart - de var ofte basert på nodejs og medførte mange ekstra moduler. Går nå for en enkel hjemmesnekra modul som lager brukbare øyer som kart.

Så denne versjonen plasserer avataren på den første øyen og strør et antall goblins rundt på kartet. Den lager også en vei \(eget canvas overlay\) som lar deg gå fra øy til øy. Der hvor veien krysser havet er terrenget endra til å være "tidal mudflats" som kan passeres ved lavvann \(foreløpig er det alltid lavvann\). Dersom det er stor avstand mellom to øyer legges en liten holme mellom slik at det blir _litt_ mer troverdig.

Her er koden som brukes til å styre avataren - ser bort fra bevegelse:

```javascript
 switch (last) {
    case "a":  // attack
        const inrange = touchingMonsters(monsters,{x,y});
        for (let m of inrange) {
            m.alive = false;
            m.div.classList.add("dead");
            const {x,y} = m;
            map.clear(x, y)
        }
        break;
}
```

**inrange** vil være en liste over monster som berører avataren.   
Slik koden virker nå kan spilleren drepe alle monster med et one-hit attack.  
Vi ønsker å bruke standard løsning på kamp i d&d, spiller og monster må ha hitpoints, de må ha våpen som gir bonus til angrep og rustning som gir bonus til forsvar.  
Anta at spiller \(22hp\) har en attack på +2, et sverd som er 2d6 \(trill to 6er terninger\).  
Anta at monster \(15hp\) har defence på +1, en rustning på 1d3 \(trill en 3er terning\).  
For hvert angrep må vi da regne ut attack : +2 + 2d6 = 2+7 \(eksempel\) = 9  
Forsvar:  +1 +1d3 = 1 +1 = 2,    =&gt; attack blir da 9-2 = 7  
Monster taper da 7 hp og har 8hp igjen.  
Monster bør da ha sin tur til å angripe \(må legges i monster-klassen\).

Hvilke endringer og hvor må vi lage for å få dette til?

