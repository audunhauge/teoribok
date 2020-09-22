# Eksamensoppgaver

## Eksamen høst 2018

### Tema: ferie og fritid

Snøfjell alpinsenter har fire utleiehytter som de leier ut i tre av skolens ferieuker vinteren 2018/2019 - juleferie, vinterferie og påskeferie.  
Du skal utvikle tre apper som de skal bruke i presentasjonen av utleiehyttene.

### Oppgave 1  - Beregne pris for heiskort i alpinanlegget.

Du skal lage en app som beregner prisen på et heiskort for inntil en uke, basert på alder og antall dager man ønsker å bruke anlegget.

#### Krav til beregning:

1. Heiskort har standardpris på 200kr for voksne og 100 for barn \(0 til og med 12 år\) per dag.
2. Dersom prisen blir over 1000kr for en voksen - skal appen gi avslag slik at prisen blir 1000. Samme for barn med grense på 500.
3. Dersom bruker får avslag, skal det gis melding om hvor stort avslaget er.
4. Du skal ikke kunne bestille for mer enn en uke.

#### Oppgave

a\) Lag et flytdiagram som beskriver appen  
b\) Lag appen som beregner prisen basert på alder og antall dager

### Oppgave 2 - Presentasjon av hyttene

Du skal planlegge og lage en app som presenterer hyttene. Utgangspunktet er et menybilde der hyttene er markert \(menybilde.jpg\). i denne oppgaven holder det at ferdigstiller presentasjon for Granbo og Granstua.

#### Krav til app

1. Bruker skal kunne klikke på markerte hytter \(Granbo/Granstua\).
2. Ved klikk på en hytte, skal et brukerstyrt bildegalleri bli tilgjengelig for hyttas som er valgt. bruker skal da kunne bla i bildene som presenter den valgte hytta. Endre dimensjon på granstua03.jpg slik at det får samme dim som de andre bildenen, forhold skal bevares.
3. Informasjon om hytta \(valgt\) skal vise: **navn, antall sengeplasser, standard**.
4. På samme side som menyen skal en redigert versjon av filmen hyttefelt.mp4 vises dersom bruker ønsker det.
5. Redigering av filmen: - dimensjon 320 x 180 piksler - skal ende med å vise hyttefelt \(ca 44s inn i orginalen\) - skal vare i 20s
6. Presentasjonen kan vises som et skjermbilde. Hvis det brukes flere skjermbilder, skal navigeringen mellom sidene være enkel og intuitiv.

#### Oppgave

a\) Lag en skisse som viser brukergrensesnittet for app, det kan være en wireframe eller lignende.  
b\) Lag app

### Oppgave 3 - Booking av ledige hytter

Det begynner å bli fyllt for bestillinger for 18/19 på hyttene. Tabellen viser hvilke bestillinger som allerede er klare, tabell 2 viser beskrivelse av hyttene.

| **Hytte** | **Jul** | **Vinterferie** | **Påske** |
| :--- | :--- | :--- | :--- |
| Granstua | utleid | utleid | ledig |
| Granbo | ledig | ledig | utleid |
| Grantoppen | utleid | ledig | utleid |
| Granhaug | utleid | ledig | utleid |

| Hytte | Sengeplasser | Standard | Badstue | Ukepris | Bilde |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Granstua | 4 | Høy | ja | 12000 | granstua.jpg |
| Granbo | 6 | Middels | Nei | 15000 | granbo.jpg |
| Grantoppen | 8 | Lav | Nei | 16000 | grantoppen.jpg |
| Granhuag | 10 | Høy | Ja | 30000 | granhaug.jpg |

#### Krav til app

1. Brukeren skal velge/angi ferie \(jul,vinterferie,påske\) og få opp bare de ledige hyttene i den valgte ferien med beskrivelse og bilde.
2. Det skal være mulig å booke en av de ledige hyttene.
3. Når bruker booker en hytte, skal utleiestatus på valgt hytte endres til "utleid".
4. En god løsning tar høyde for at app lett kan utvides med flere hytter.

#### Oppgave

Lag app

## Eksamen høst 2019

{% file src="../../.gitbook/assets/it2\_h19.pdf" caption="IT2 heldag høst 2019.pdf" %}

### Oppgave 1.   animasjon - redigering - eventlistener

Ting du må kunne

* [ ] Redigere en gif - endre størrelse til 607 x 700 px
* [ ] Redigere en mp3 - ta vekk område med støy \(klippe filen\)
* [ ] Lage evenlisteners slik at du kan klikke på områder av et bilde. En enkel løsning er å lage en div som du plasserer oppå bildet. Denne kan da ha en eventlistener. Du kan bruke css - clip-path `clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0 23%);` til å matche div med muskel på bildet. Div-en er transparent og fungerer bare som click target. Bruk inspect til å redigere verdiene slik at de treffer godt.
* [ ] Spille av lyd styrt av en evenlistener Legg inn `<audio id="lyd1" src="lyd.mp3"></audio>` Lag en kobling i html :  `let audioLyd1 = document.getElementById("lyd1")` I eventlistener for klikk på muskel kan du skrive `audioLyd1.play()`



### Oppgave 2.  Enkel app med combo, input, radio, knapp og resultat

Ting du må kunne

* [ ] Lage en kombo med value og visning : &lt;option value="814"&gt;Aerobics&lt;/option&gt;
* [ ] Lage en input type="radio" med verdier:  \(alle tre har samme name="intensitet" \) &lt;label&gt; &lt;input name="intensitet" type="radio" value="1.2"&gt; Middels &lt;/label&gt;
* [ ] Lese valgte verdier
* [ ] Beregne forbruk og vise i en html
* [ ] Lage flytdiagram

Dette er en klassisk oppgave 1, enkelt skjema med en enkel beregning. Se eksempler.

### Oppgave 3.  combo som styrer en combo

Ting du må kunne \(del 1\)

* [ ] Lage en combo med gitte valg og en eventlistener på change
* [ ] Lage en ny \(eller sette options for\) en kombo med valg styrt av forrige combo
* [ ] Enkel løsning er: object: { armer: "Bicepscurl med stang,Fransk press".split\(\),  ... } Den første comboen velger f.eks "armer" som value, bruker denne til å slå opp i obj. henter ut alternativene \(en  array\). Trenger da en funksjon som kan lage select+options fra en array med alternativer Jeg søkte på 'option' i min github og fant denne:

```javascript
// en funksjon som lager en nedtrekksliste
/**
 * @param {Object}  tabell      Inneholder verdier som skal brukes i nedtrekk
 * @param {string} valgtNokkel  Nøkkel fra første nedtrekk 
 *                              - fyller ut den andre med verdier fra tabell
 * @returns {string}            Innhold til en select, 
 *                              bruk sel.innerHTML = lagNedTrekk(..)
 */

function lagNedtrekk(valgtNokkel, tabell) {
    let s = '';
    if (tabell[valgtNokkel]) {
        let verdier = tabell[valgtNokkel];
        for (let v of verdier) {
            s += `<option>${v}</option>`;
        }
    }
    return s;
}
```

Ting du må kunne \(del 2\)

* [ ] Dette er egenlig et registrerings-skjema slik som for person.
* [ ] Lag en class Trening {  navn, reps,motstand }  // viser bare navnene på egenskaper i klassen.
* [ ] NB! merk at både **set** og **Set** allerede er brukt av javascript, **set** er et keyword, bør unngå variable eller klasser med disse navnene, derfor class Trening og ikke class Sett \(som er forvirrende likt Set\).
* [ ] Registrer nye sett \(bør også trigge/kjøre funksjon som viser alle registrerte, neste punkter\).
* [ ] Vis deltakerliste \(alle sett\) og en oppsummering
* [ ] For å beregne totalvolum må vi travasere lista med sett `let sum = 0; for (let s of setListe) {   sum += s.reps * s. motstand; }`



