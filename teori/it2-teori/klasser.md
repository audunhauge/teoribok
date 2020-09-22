# Klasser

## Klasser <a id="klasser"></a>

Jeg velger å beskrive klasser ut fra siste versjon som er implementert i nettleseren Chrome \(mars 2016\).  
Merk at klasser i js egentlig er objects med pene klær.

[Denne linken](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model) gir en dypere innføring i javascript klasser - sammenligna med java.

### Class <a id="class"></a>

{% hint style="info" %}
I språk som Java,C++,D,C\# osv er det et klart skille mellom klasser og instanse.  
Klassen er definisjonen - instansen er objektet du bruker.  
  
I javascript er Klassen egentlig et Object \(prototype object\) og instansen er en kopi av dette objectet. Funksjonaliteten blir den samme ved at kopien har en link til prototypen \(som igjen kan ha en videre link\). Dette er måten arv implementeres på i js.
{% endhint %}

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

En klasse kan bare ha én funksjon med navnet **constructor**. Det er denne funksjonen som kjøres når du lager en ny instans \(en variabel av klassen, slik som r1 er en instans av klassen Rektangle\).

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
      `translate(${this.x}px,${this.y}px)`;
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
      `translate(${this.x}px,${this.y}px) rotate(${this.angle}rad)`;
  }
}
```

### Bruk av klassene Sprite, Movable og Turnable

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
let r = new Turnable( { div:div3, x,y,w,h }, 0.3, 10 );

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

### En liten kjørbar demo med Sprite, Movable og Turnable

Lag et nytt prosjekt i vs-code og legg inn koden under. Koble css og js som vanlig

{% tabs %}
{% tab title="HTML" %}
```
<div id="game">
</div>
<script>
  setup();
</script>
```
{% endtab %}

{% tab title="CSS" %}
```css
#game {
  position: relative;
  width: 600px;
  height: 600px;
  border: solid 1px gray;
  background-color: whitesmoke;
}

.tree {
  width: 5px;
  height: 25px;
  background-color: teal;
}

.bird {
  width: 20px;
  height: 20px;
  background-color: green;
  border-radius: 50%;
}

.dog {
  width: 30px;
  height: 15px;
  background-color: red;
}
```
{% endtab %}

{% tab title="JS" %}
```javascript
class Sprite {
  constructor({ div, x, y, w, h }) {
    this.div = div;
    this.x = x || 0;
    this.y = y || 0;
    this.w = w || 10;
    this.h = h || 10;
  }
  render() {
    this.div.style.transform = `translate(${this.x}px,${this.y}px)`
  }
}

class Movable extends Sprite {
  constructor(spriteInfo, vx, vy) {
    super(spriteInfo);
    this.vx = vx;
    this.vy = vy;
  }
  move() {
    this.x += this.vx;
    this.y += this.vy;
  }
}

class Turnable extends Movable {
  constructor(spriteInfo, angle, speed) {
    let vx = Math.cos(angle) * speed;
    let vy = Math.sin(angle) * speed;
    super(spriteInfo, vx, vy);
    this.angle = angle;
    this.speed = speed;
  }
  turn(delta) {
    this.angle = (this.angle + delta) % (Math.PI * 2);
    this.vx = Math.cos(this.angle) * this.speed;
    this.vy = Math.sin(this.angle) * this.speed;
  }

  // må lage egen render da Sprite sin render ikke har med rotasjon
  render() {
    this.div.style.transform = `translate(${this.x}px,${this.y}px) 
    rotate(${this.angle}rad)`;
  }
}

const g = id => document.getElementById(id);
const getdiv = () => document.createElement("div");

function setup() {
  let divGame = g("game");
  let x = 100,
    y = 100,
    w = 10,
    h = 10;
  let s = new Sprite({ div: getdiv(), x, y, w: 5, h: 25 });
  let m = new Movable({ div: getdiv(), x, y, w: 20, h: 20 }, 2, 3);
  let r = new Turnable({ div: getdiv(), x, y, w: 30, h: 15 }, 0.3, 3);
  s.div.className = "tree";
  m.div.className = "bird";
  r.div.className = "dog";
  divGame.appendChild(s.div);
  divGame.appendChild(m.div);
  divGame.appendChild(r.div);
  const itemList = [s,m,r];

  setInterval(() => {
      for (let item of itemList) {
          item.render();
          if (item instanceof Movable) item.move();
          if (item instanceof Turnable) item.turn(0.05);
      }
  }, 40);
}
```
{% endtab %}
{% endtabs %}



