# Eksempel - Demografi

### Klasse for å lagre data om land

```javascript
class Land {
  constructor(navn,befolkning,hovedstad,bnp,areal,hbef) {
    this.navn = navn;
    this.befolkning = befolkning;
    this.hovedstad = hovedstad;
    this.bnp = bnp;
    this.areal = areal;
    this.hbef = hbef;
  }
}
```

### Skjema for å registrere et land

```markup
<div id="registrer">
  <form id="reg">
    <label for="navn">Navn<input type="text" id="navn"></label>
    <label for="befolkning">Befolkning<input type="number" id="befolkning"></label>
    <label for="hovedstad">Hovedstad<input type="text" id="hovedstad"></label>
    <!--  flere linjer -->
    <label for="lagre"><button type="button" id="lagre">Lagre</button></label>
    </form>
</div>
```

### Kode for å lagre

{% code-tabs %}
{% code-tabs-item title="function setup\(\)" %}
```javascript
let personListe = [ ];

    let inpNavn = document.getElementById("navn");
    let inpAlder = document.getElementById("alder");
    let inpAdresse = document.getElementById("adresse");
    let btnLagre = document.getElementById("lagre");
    let divOversikt = document.getElementById("oversikt");
    btnLagre.addEventListener("click", lagreData);

    function lagreData() {
        let navn = inpNavn.value;
        let alder = inpAlder.value;
        let adresse = inpAdresse.value;
        let person = new Person(navn,alder,adresse);
        personListe[0] = person;
        visListe();
    }

    function visListe() {
        let innhold = "";
        for (let p of personListe) {
           innhold += `Navn:${p.navn}  Alder:${p.alder} Adresse:${p.adresse}`;
        }
        innhold += "";
        divOversikt.innerHTML = innhold;
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

