# Map og Set



## Set <a id="set"></a>

Set er en nær slektning \(nokså fersk\) av Array. I Set vil alle elementer være unike.

Dermed er det enklere å sjekke om en verdi finnes i et sett, også fjerning av element er en billigere operasjon.

Merk at elementene i ett Set kan itereres i samme rekkefølge som de ble satt inn.

#### Eksempel <a id="eksempel"></a>

```javascript
let skoler = new Set();  // nytt tomt sett
skoler.add("skeisvang");
skoler.add("vardafjell");
skoler.add("haugaland");
skoler.add("skeisvang-vgs");
skoler.delete("skeisvang-vgs");  // fjerner element
if (skoler.has("skeisvang")) { ... }  // dersom skeisvang er i settet

// skoler.size gir antall elementer

skoler.forEach( function(s) { console.log(s); });
// skriver ut alle skolene i skoler
// rekkefølgen blir: skeisvang,vardafjell,haugaland
```

### Konvertere mellom set og Array <a id="konvertere-mellom-set-og-array"></a>

```javascript
// konvertering fra Array til Set
let arrSkoler1 = "Skeisvang,Vardafjell,Haugaland".split(",");
// arrSkoler1 er nå en Array
let setSkoler = new Set(arrSkoler1);

// konvertering fra Set til Array
let arrSkoler2 = Array.from(setSkoler)
```

## Map <a id="map"></a>

Map er en nær slektning av Object.

Forskjellene er:

* An Object has a prototype, so there are default keys in the map that could collide with your keys if you're not careful.
* The keys of an Object are Strings and Symbols, whereas they can be any value for a Map, including functions, objects, and any primitive.
* You can get the size of a Map easily with the size property, while the size of an Object must be determined manually.

På norsk blir dette omtrent:

* Object har prototyper, så det finnes nøkler fra før som kan kollidere med dine nøkler.
* For Object er nøklene String eller Symbol, mens for Map kan de være alle mulige verdier. En kan dermed bruke functions som nøkler \(kan være nyttig\)
* Enkelt å finne ut hvor mange elementer det er i en map \(map.size\), og du kan bruke map.forEach til å traversere alle elementer.

### Utvidelser for Map utover Set <a id="utvidelser-for-map-utover-set"></a>

Map har nesten de samme funksjonene som set, men har noen i tillegg

| Funksjon | Forklaring |
| :--- | :--- |
| map.get\(key\) | Henter ut verdien som er lagra på plass \[key\], eller undefined |
| map.set\(key,val\) | Setter verdien på adresse \[key\] til val, mymap.set\("name","ole"\) |
| map.entries\(\) | Gir tilbake en liste over \[key, value\] |
| map.keys\(\) | Returnerer en liste over alle nøkkler i mapen |
| \* map.size\(\) | Returnerer antall elementer i map/set |
| \* map.clear\(\) | Fjerner alle registreringer - map/set tømmes |
| \* map.delete\(key\) | Fjerner verdien som er lagra på plass \[key\] fra set/map |
| \* map.values\(\) | Gir tilbake en liste over verdiene som er lagra i map/set |
| \* map.has\(key\) | Sann dersom map/set har en verdi på plass \[key\], ellers usann |
| \* map.forEach\(cb\) | Kjører funksjonen cb\(value,set\) / cb\(value,key,map\) for alle elementer lagra i set/map |

De funksjonen markert med stjerne kan også brukes på Set.

Set har i tillegg funksjonen **set.add\(verdi\)** som legger en verdi inn i settet.

## Array funksjoner på Set og Map <a id="array-funksjoner-p&#xE5;-set-og-map"></a>

Array har mange nyttige innebygde funksjoner slik som

map, filter, sort, reverse

Disse kan ikke brukes direkte på map og set, men metodene under viser mulige løsninger:

**NB** merk at Array har en funksjon Array.map, dette er ikke en **Map**

```javascript
// Mapping:

const set = new Set([1, 2, 3]);
set = new Set([...set].map(x => x * 2));
// Resulting Set: {2, 4, 6}

// Filtering:
const set = new Set([1, 2, 3, 4, 5]);
set = new Set([...set].filter(x => (x % 2) == 0));
// Resulting Set: {2, 4}
// Du kan gjøre akkurat det samme med map


// Lag en ny map fra map1 og map2
let nymap = new Map([... map1, ... map2]);

// Dette kan du gjøre med Set også, men du får unionen
let set1 = new Set([1,2]);
let set2 = new Set([2,3]);
let union = new Set([... set1, ... set2]);
// union === {1,2,3}

// snitt mellom to set  (a ∩ b) ( elemeneter fra a som også finnes i b)
const a = new Set([1,2,3]);
const b = new Set([4,3,2]);
const snitt = new Set([...a].filter(x => b.has(x)));
// {2,3}

// differanse mellom to set ( bare de elementene i a som ikke finnes i b)
const a = new Set([1,2,3]);
const b = new Set([4,3,2]);
const difference = new Set([...a].filter(x => !b.has(x)));
// {1}
```

