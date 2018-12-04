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

### Eksempel - definisjon av klassen Tank <a id="eksempel---definisjon-av-klassen-tank"></a>

Denne klassen skal vi bruke i spillet vi lager.

Merk at klassen har en construktor funksjon. Det er denne funksjonen som kjøres når du lager en ny instans av klassen.

```javascript
let t34 = new Tank("t"+tankcount, "active");
```

Merk også måten du lager funksjoner som er knytta til en klasse

```javascript
  hit(klass) {
    return 5;
  }
```

Dette betyr at du kan skrive t32.hit\(\) for å kjøre denne funksjonen. I alle slike funksjoner definert inne i klassen vil **this** referere til instansen \(t34 i vårt eksempel\).

Dermed kan vi skrive en klassefunksjon som dette

```javascript
  move(delta) {
    if (this.alive) {
      this.body.move(delta);
      this.setpos();
    }
  }
```

**this** er her tanksen som vi kjører koden på, f.eks t34.move\(5\)

```javascript

const THW = 16;

class Tank {
  constructor(id, klass) {
    this.div = document.createElement("div");
    this.div.className = "tanks " + klass;
    this.div.id = id;
    this.speed = 1;
    this.a = 0.035;
    this.body = new RigidBody(0,0,THW,THW,0);
    this.delay = 0;
    this.turnrate = 2;
    this.alive = true;
    this.owner = null;
    this.is = 'Tank';
    this.idnum = 0;
    this.hitpoints = 100;
  }

  hit(klass) {
    return 5;
  }

  takeDamage(amount) {
    this.hitpoints -= amount;
    if (this.hitpoints < 50) {
      this.div.classList.add("damaged");  
    }
  }

  move(delta) {
    if (this.alive) {
      this.body.move(delta);
      this.setpos();
    }
  }

  setpos() {
    this.div.style.left = this.body.x + "px";
    this.div.style.top = this.body.y + "px";
  }

  turn(delta) {
    if (this.alive) {
      if (this.body.v < 0) delta *= 2.5;        //turn fast when reversing
      let d = (this.body.rot + delta) % 360;
      this.body.rot = d;
    }
  }

  direction(angle) {
    this.div.style.transform = 'rotate(' + angle + 'deg)';
  }
}
```

