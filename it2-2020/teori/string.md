# String

## String-funksjoner

| Funksjon | Eksempel |
| :--- | :--- |
| s.length | "abc".length === 3 |
| s.includes | "ole petter".includes\("pe"\) === true |
| s.charAt | "abcde".charAt\(2\) === "c" |
| s.charCodeAt | "abcde".charCodeAt\(2\) === 99 |
| s.endsWith | "abcdef".endsWith\("def"\) === true |
| s.indexOf | "abcde".indexOf\("c"\) === 2    // -1 if not found |
| s.match | "abcdefgh".match\(/\[aeiouy\]/gi\) =&gt; \["a", "e"\] |
| s.padEnd | "1.0".padEnd\(6,"0"\) === "1.0000" |
| s.padStart | "1".padStart\(4,"0"\) === "0001" |
| s.repeat | "12".repeat\(4\) === "12121212" |
| s.replace | "søvnløs".replace\(/ø/g, "o"\) === "sovnlos" |
|  | "søvnløs".replace\("ø", "o"\) === "sovnløs" |
| s.search | "og dermed".search\(/er/\) === 4  // -1 dersom ikke funnet |
| s.slice | "abcdefg".slice\(1\) === "bcdefg" |
|  | "abcdefg".slice\(2,4\) === "cd"  // slutter rett før pos 4 |
| s.split | "a b c d".split\(" "\) =&gt; \[ "a" , "b" , "c" \]  |
|  | "a b c d".split\(" ", 2\) =&gt; \[ "a" , "b" \]  |
| s.startsWith | "abcde".startsWith\("ab"\) === true |
| s.substr | "abcde".substr\(1\) === "bcde" |
|  | "abcde".substr\(-2\) === "de" |
|  | "abcdefghij".substr\(2,3\) === "cde" |
| s.toLowerCase | "ABC".toLowerCase\(\) === "abc" |
| s.toUpperCase | "abc".toUpperCase\(\) === "ABC" |
| s.trim | " abc ".trim\(\) === "abc" |
| s.trimStart | " abc ".trimStar\(\) === "abc " |
| s.trimEnd | " abc ".timEnd\(\) === " abc" |

## Metoder for å lage strenger med bestemt tekst

### Lime sammen tekstbiter

Du kan lime sammen tekstbiter slik: `let a="fire"; let b = "en" + a + "to"` .  
Her vil du få teksten "enfireto" som resultat. Dersom du trenger mellomrom må du ta det med eksplisitt i strengen: "fire ".

### Variabler i teksten

Med det nye \`backtick\` hermetegnet kan du få verdier fra variable inn i tekst slik:

```javascript
let navn = "ole";
let alder = 22;
let msg = `Velkommen ${ole}, du er ${alder} år gammel.`;
```

### Erstatte markører i tekst

```javascript
let data = {  plass:"Oslo", antall:4, pris:5600 };
let pattern = `Velkommen til #plass#, du har bestillt
  #antall# netter med overnatting. Prisen blir #pris#`;
let msg = pattern.replace(/#(\w+)#/g, (m,s) => data[s] || m );
```

Merk at du kan velge markører helt fritt, /\#\(\w+\)/g vil matche \#plass - trenger ikke \# både før og etter. \(\w+\) vil matche en eller flere vanlige bosktaver a..zA..Z.  
Poenget med   **\|\| m**  er at dersom data\[s\] === undefined -  da endres ikke teksten.  
Du ser da lett feil fordi msg vil inneholde \#navn\# \(navn finnes ikke i data\).

## Eksempler

### Erstatte tekst

```javascript
// erstatte alle små tall (1,2..9) med tallord
let rawMsg = "Du har 1 bil og kan ta 4 passasjerer"
let tall2tale = { 1:" en ", 2:" to ", 4:" fire " };  
// ikke komplett ...
let niceMsg = rawMsg.replace(/ (\d) /g, (m,s) => tall2tale[s] || m);
// niceMsg === "Du har en bil ..."
```

Merk at vi bare erstatter tall med space rundt.

### Plukke ut siste bit av en tekst

```javascript
let s = "finn siste tre bokstaver";
let siste = s.substr(-3);  // siste === "ver"
```

