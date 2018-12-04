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

