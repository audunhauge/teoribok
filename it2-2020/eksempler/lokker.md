# Løkker

For løkka er den vi bruker mest i js. Eksemplet under viser forskjellige løkker som teller opp/ned med steg på +1 -1 eller +- 2. Den første løkka kjører bare 10 ganger - og det er derfor problemfritt å bruke en tidkrevende kommando som div.innerHTML = ...  inne i løkka.  
De andre løkkene bygger opp teksten som skal vises i en variabel og kjører div.innerHTML helt til slutt.  
Dette er en mye bedre måte å gjøre det på dersom antall repetisjoner er stort.

```javascript
        for (let i=1; i<11; i += 1 ) {
            divTier.innerHTML += " " + String(i);
        }
        let s = "<hr>";

        for (let i=20; i<51; i += 1 ) {
            s += " " + String(i);
        }
        s += "<hr>";
        for (let i=70; i>59; i -= 1 ) {
            s += " " + String(i);
        }
        s += "<p>";
        for (let i=2; i<101; i += 2 ) {
            s += " " + String(i);
        }
        s += "<hr>";
        for (let i=1; i<100; i += 2 ) {
            s += " " + String(i);
        }
        s += "<p>";
        for (let i=100; i<10001; i += 100 ) {
            s += " " + String(i);
        }
        divTusen.innerHTML = s;
```

