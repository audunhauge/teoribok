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
      `translate(${this.x},${this.y})`;
  }
}
// antar at vi har en css regel som gjør at div.tree
// vises etter kravspek.
// lager 20 trær og plasserer dem i divMain
for (let i=0; i<20; i++) {
  let div = document.createElement('div');
  div.className = 'tree';
  divMain.appendChild(div)
  let spriteTree = new Sprite( {div, x:100, y:200, w:10, h:100} );
  spriteTree.render();
  // merk at alle trærne ligger oppå hverandre
  // da de har samme (x,y)
  // linjene under lager tilfeldig x,y for hvert tre
  // merk hvordan bruk av samme navn (x,y) som i 
  // constructor gjør det lett å pakke {div,x,y .. }
  /*
  let x = Math.random()*500;
  let y = Math.random()*300;
  let spriteTree = new Sprite( {div, x, y, w:10, h:100} );
  */
}
```

I eksemplet med spriteTree over kan vi selvsagt også bruke div.innerHTML til å vise tekst.  
spriteTree.div.innerHTML = "noe text". Denne kunne være med i render\(\) dersom klassen har noen tekstegenskaper som skal vises.

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

Denne klassen \(Movable\) virker greit for ting som skal bevege seg rett fram, men dersom vi har krav om at noen ting på skjermen skal kunne snu seg \(rotere\) slik at det ser ut som de peker den veien de går - da lager vi en ny klasse:

```javascript
class Turnable extends Movable {
  constructor(spriteInfo, angle, speed) {
    let vx = Math.cos(angle) * speed;
    let vy = Math.sin(angle) * speed;
    super(spriteInfo,vx,vy);
    this.angle = angle;
    this.speed = speed;
  }
  turn(delta) {
    this.angle = (this.angle + delta) % (Math.PI*2);
    this.vx = Math.cos(this.angle) * this.speed;
    this.vy = Math.sin(this.angle) * this.speed;
  }
  
  // må lage egen render da Sprite sin render ikke
  // har med rotasjon
  render() {
    this.div.style.transform = 
      `translate(${x},${y}) rotate(${this.angle}rad)`;
  }
}
```

### Bruk av klassene Sprite, Movable og Rotatable

```javascript
// jeg lager en instans av hver klasse
// antar at jeg har tre div´s div1 div2 og div3
// som allerede er på stagen (inne i divMain)
let x = 100;
let y = 200;
let w = 40;
let h = 30;
let s = new Sprite( { div:div1, x,y,w,h } );
let m = new Movable( { div:div2, x,y,w,h }, 2, 3 );
let r = new Rotatable( { div:div3, x,y,w,h }, 0.3, 10 );

s.render()      // div1 plasseres på (x,y) = (100,200) 
                // og blir værende der
m.render()      // som s
m.move()        // men nå flytter m seg til (102,203)
// dette kan vi gjøre med setInterval slik at m flytter
// seg med gitt interval

r.render()      // som s og m
                // men div3 vil være rotert 0.3 radianer
r.move()        // som m
r.turn(0.01)    // r snur seg litt
r.move()        // beveger seg i den nye retningen
```



