# Klasser

## Klasser <a id="klasser"></a>

Jeg velger å beskrive klasser ut fra siste versjon som er implementert i nettleseren Chrome \(mars 2016\).  
Den eldre løsningen for klasser vises i et tillegskapittel.

### Class <a id="class"></a>

```javascript
class Rektangel {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};

var r1 = new Rektangel(30,40);
```

Her har jeg definert en ny klasse med navnet Rektangel. Merk at jeg må definere klassen før jeg bruker den, klasser blir ikke _hoisted_ \(flyttet til toppen av scopet\) slik som funksjoner.

En klasse kan bare ha en funksjon med navnet **constructor**. Det er denne funksjonen som kjøres når du lager en ny instans \(en variabel av klassen, slik som r1 er en instans av klassen Rektangle\).

Dersom du tester koden over i consol \(ctrl+shift+j\) \(copy paste koden inn i consol, trykk deretter enter\) og så skriver **r1** og trykker enter, da viser chrome:

```javascript
Rektangel {height: 30, width: 40}
```

Dette sier oss at variabelen _r1_ er av typen _Rektangel_ og har innhold `{height: 30, width: 40}`.

### Eksempel - definisjon av en klasse for elev <a id="eksempel---definisjon-av-en-klasse-for-elev"></a>

```javascript
class Elev {
  constructor(id, fn, en, klasse) {
    this.fornavn = fn;
    this.etternavn = en;
    this.klasse = klasse;
  }
}

var elev = new Elev(123,"petter","olsen","3a");
elev.fornavn === "petter";  // true
elev.klasse === "3a";  // true

// Lagre data for mange elever
var elever = [ ];

elev = new Elev( ....);
elever.push(elev);
...  // repetert mange ganger
```

### Eksempel - definisjon av Sprite <a id="eksempel---definisjon-av-klassen-tank"></a>

For å plasser/flytte ting rundt på skjermen lager vi ofte en Sprite klasse.  
Den inneholder nok info til å kunne legge noe på skjermen på en bestemt plass \(x,y\) og med en bestemt størrelse \(w,h\). I eksemplet under bruker vi en div som det grafiske elementet - dette kunne selvsagt vært kode for å tegne på canvas eller svg.

```javascript
class Sprite {
  constructor({ div, x, y, w, h } ) {
    this.div = div;
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
  }
  render() {
    this.div.style.transform = 
      `translate(${x},${y})`;
  }
}
// antar at div-en finnes og har en css regel som gjør at den
// vises etter kravspek.
let div = document.getElementById('tre');
let spriteTre = new Sprite( {div, x:100, y:200, w:10, h:100} );
```

### Utviding av en enkel klasse \(slik som Sprite\)

Vi har flere ting på skjermen som er Sprite - de kan plasseres, men vi trenger ting som kan bevege seg med en gitt fart/retning. Vi lager en ny klasse som utvider Sprite:

```javascript
class Movable extends Sprite {
  constructor(spriteInfo, vx,vy) {
    super(spriteInfo);
    this.vx = vx;
    this.vy = vy;
  }
  move() {
    this.x += this.vx;
    this.y += this.vy;
  }
}
```







