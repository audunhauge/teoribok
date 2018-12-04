# Beregninger

## Beregninger og uttrykk <a id="beregninger-og-uttrykk"></a>

I js kan du skrive beregninger og uttrykk på nesten samme måte som du er vant til fra matematikken eller symbolkalkulatoren. x = 2\*a + 4/\(1-b\)

I beregningen over brukes operatorene \* + - / som du sikkert kjenner fra før. I tillegg har js en god del andre operatorer som vist i denne lista:

```text
+               addisjon, legger sammen to verdier (limer også sammen tekst)
-               subtraksjon
*               multiplikasjon
/               divisjon
>               større enn, er a > b ? sann dersom a er størst
≺               mindre enn
>=              større eller lik
≺=              mindre eller lik
!=              forskjellig fra
!==             helt forskjellig fra
==              er lik (sammenligning) , merk "" == 0
===             er identisk lik, "" er ulik 0
&&              og (binder sammen to tester - begge må være sann)
||              eller (binder sammen to tester - bare en trenger være sann)
++              øker verdien i en variabel med en
--              minker med en
+=              a += 3, verdien lagra i a økes med 3
-=              a -= 5, verdien i a minker med 5
=               a = 5, lagre ny verdi i a
```

Ofte vil du ha bruk for matematiske formler, da kan du bruke **Math** biblioteket som er innebygd i javascript.

| Funksjon | Virkemåte | Eksempel |
| :--- | :--- | :--- |
| Math.random\(\) | Gir et tillfeldig tall mellom 0 og 1 | 0.234342263 |
| Math.floor\(number\) | Runder av nedover | Math.round\(2.34\) === 2 |
| Math.PI | Tallverdien til pi | Math.PI == 3.1415926536... |
| Math.sin\(number\) | Beregner sinus til vinkel i radianer | Math.sin\(Math.PI\) === 0 |
| Math.cos\(number\) | Beregner sinus til vinkel i radianer | Math.cos\(Math.PI\) === 1 |
| Math.tan\(number\) | Beregner sinus til vinkel i radianer | Math.tan\(Math.PI\) === 0 |
| Math.abs\(number\) | Gjør tallet positivt | Maths.abs\(-3\) === Math.abs\(3\) === 3 |
| Math.min\(a,b\) | Minste av a,b | Maths.min\(2,3\) === 2 |
| Math.max\(a,b\) | Størst av a,b | Maths.max\(2,3\) === 3 |

Du kan finne ut mer om Math biblioteket ved å åpne consol \(ctrl+shift+j\) og skrive  
Math. \(legg merke til punktum til slutt\)  
Du vil da se en liste med mulige funksjoner - forklaring på virkemåte finner du lett ved å søke på Math.xxx hvor xxx er den funksjonen du lurer på.

