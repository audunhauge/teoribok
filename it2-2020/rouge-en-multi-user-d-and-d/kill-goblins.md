# Kill goblins

I denne versjonen har jeg lagt til goblins som beveger seg tilfeldig rundt - men dersom avstand fra avatar  
 &lt; 5 ruter - da går de til angrep. Da hverken goblins eller avatar har hitpoints - lar jeg effekten av angrep fra en goblin være en blink av rødfarge på kartet \(damage received\).  
Avatar kan drepe alle goblins i nærkontakt med "a" for attack.  
Actors har fått egenskapen alive som har en opplagt funksjon.

{% tabs %}
{% tab title="Basis-klassen Actor" %}
```javascript
// denne klassen tegner seg selv med render()
// den har (x,y) og alive som egenskaper + en div.
// den kan også beregne avstand (kvadrert) til en annen Actor
// canSee bør nok være avhengig av hvilken type monster
//    må dermed flyttes senere
// En død Actor vil også håndteres forskjellig for diverse monster
//   så testen på alive i render skal nok fjernes
class Actor {
    x = 2;
    y = 2;
    alive = true;
    /** @type {HTMLElement} */
    div;
    render() {
        this.div.style.left = (this.x * 32) + "px";
        this.div.style.top = (this.y * 32) + "px";
        if (!this.alive) {
            this.div.style.opacity = "0.3";
            this.div.style.backgroundColor = "rgba(255,0,0,0.5)";
        }
    }
    /**
     * @param {Actor} other
     * @returns {number} distance squared
     */
    distance(other) {
        const dx = this.x - other.x;
        const dy = this.y - other.y;
        return (dx ** 2 + dy ** 2);
    }
    /**
     * @param {Actor} other
     * @returns {boolean} true if close
     */
    canSee(other) {
        return this.distance(other) < 25;
    }
}
```
{% endtab %}

{% tab title="Monster klassen" %}
```javascript
// Monster utvider Actor - et monster har forskjellige handlinger det
// kan utføre:  attack, move og towards
// foreløpig angriper monster bare avatar

class Monster extends Actor {
    constructor() {
        super();
    }

    action() {
        if (!this.alive) return;
        if (this.canSee(avatar)) {
            if (this.distance(avatar) < 3) {
                this.attack(avatar);
            } else {
                this.towards(avatar);
            }
        } else {
            this.move();
        }
    }
    /**
     * @param {Actor} other
     */
    towards(other) {
        const dx = other.x - this.x;
        const dy = other.y - this.y;
        this.x += clamp(dx, -1, 1);
        this.y += clamp(dy, -1, 1);
    }

    /**
     * @param {Actor} other
     */
    attack(other) {
        if (this.alive && other.alive) {
            divActors.classList.add("attack");
            setTimeout(() => divActors.classList.remove("attack"), 300);
        }
    }
    move() {
        if (!this.alive) return;
        this.x += Math.round(Math.random() * 2 - 1);
        this.y += Math.round(Math.random() * 2 - 1);
        this.x = clamp(this.x, 0, 11);
        this.y = clamp(this.y, 0, 11);
    }
}
```
{% endtab %}

{% tab title="Avatar klassen" %}
```javascript
// nesten identisk med Actor - bare en litt annen startposisjon
// en del kode kan kanskje flyttes inn her senere

class Avatar extends Actor {
    constructor() {
        super();
        this.x = 5;
        this.y = 5;
    }
}
```
{% endtab %}
{% endtabs %}

Neste trinn blir å utstyre Actors med hitpoints slik at vi må angripe flere ganger for å drepe et monster. Avataren får også hitpoints siden den også er en Actor. En Actor trenger også en mengde med stats som en karakter i et d&d rollespill.

### Stats

* hitpoints
* speed/movepoints
* attack damage
* defence
* mana
* wisdom
* intelligence
* luck
* race \(dwarf,elf,human,orc,troll\)
* ??? \(wizard,warrior,rouge,ranger ... \)

### Skills

* bow
* shield
* armor
* sword
* knife

Dette er bare en foreløpig liste over egenskaper vi kanskje kan gi en actor.

Denne versjonen er [v0.002](https://github.com/audunhauge/rouge/tree/v0.02)

