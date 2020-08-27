# Tall

Vi lager et enkelt eksempel som skriver ut gangetabellen

```javascript
function setup() {
    let divListe = document.getElementById("liste");
    for (let i = 1; i < 11; i += 1) {
        for (let j = 1; j < 11; j += 1) {
            let div = document.createElement("div");
            div.innerHTML = String(i*j);
            divListe.append(div);
        }
    }
}
```

Legg merke til at vi her har en løkke inne i en løkke. Da vil den innerste løkken kjøre 10 ganger for hver gang den ytterste kjører 1 gang. Dermed utføres koden inne i den innerste løkka 100 ganger.

