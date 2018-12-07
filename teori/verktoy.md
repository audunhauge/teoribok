---
description: Programmer og nettsider
---

# Verktøy

## Verktøy brukt i faget <a id="verkt&#xF8;y-brukt-i-faget"></a>

### Editor <a id="editor"></a>

Vi skal bruke Visual Studio Code som editor. Denne kan du installere for mac, windows eller linux ved å søke opp  
**visual studio code** og deretter velge nedlasning. Denne editoren er gratis og har god støtte for syntax for javascript, html og css - som er de teknologiene vi bruker til å bygge opp en nettside.

#### Starte et prosjekt i visual studio code.

Lag en mappe med passende navn for prosjektet ditt \(dette gjør du i filbehandleren, utforsker eller i terminal/console\).

Start VSCode og velg **Open folder**. Naviger fram til den nye mappa og klikk ok/enter.

VSCode viser nå den nye tomme mappa, du kan nå legge til en ny fil

![](https://audunhauge.gitbooks.io/it1-informasjonsteknologi1/content/assets/nyFil.png)

ved å klikke på ny-fil ikonet \(hvitt ark med grønn pluss\).

Sett navn på filen - skriv **eksempel.html** i tekstboksen som kom fram. Trykk **enter** og du får fram en ny blank side.

**Lag din første html side.**

I editoren kan du nå skrive ! \(skriv et utropstegn og trykk enter\).

Du vil nå få fram følgende kode:

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>

</body>
</html>
```

### Github - lagringsplass for alle sidene <a id="github---lagringsplass-for-alle-sidene"></a>

Github virker litt på samme måte som DropBox og andre skytjenester hvor du kan lagre dokumenter, men er spesielt beregna på kode \(html, javascript, css og andre programmerings-språk\).

I kurset skal dere opprette en egen konto på github hvor alle filer skal lagres.

#### **Opprett github-konto**

Gå til github.com i en nettleser, velg **sign up** og lag et brukernavn. Velg et brukernavn med tanke på at denne skal du bruke ofte, og du må sende det som en link til lærer, f.eks: du velger **mittNavn** som brukernavn, da vil linken lærer bruker være **mittNavn.github.io** . Denne linken gir lærer adgang til alle filene du lagrer på github. **NB!** github er **public** dvs alle kan se det du legger ut her.

#### **Lag en github.io**

Lag en github-bruker \(eks: janpedersen\)  
Lag en ny Repository med navnet `janpedersen.github.io` \(ditt brukernavn + github.io\)  
Merk at du må bruke nøyaktig denne navneformen - ellers virker ikke linken.

Klikk på Settings på Repositoriet og bla ned til du finner Github Pages - sjekk at det står

> Your site is published at [https://janpedersen.github.io/](https://janpedersen.github.io/)

Du kan gå inn på github på din konto og lage en ny fil **index.html** inne i det nye repositoriet \(det med navnet xxx.github.io\).  
Skriv inn den html koden du ønsker og lagre - denne vil nå bli sida som vises på adressen over.

#### Lokal kopi av filene

Etter å ha laget repositoriet \(oppskriften over\) kan du legge til en fil \(bruk knappen Create new file\). Gi filen navnet index.html og legg inn en enkel html  
slik som `<html><body><h1>hei</h1></body></html>` . Klikk på knappen commit nederst på sida.

Neste trinn er å lage en lokal kopi på datamaskinen. Klikk på repostoriet \(navnet er xxx.github.io -- xx er brukernavnet ditt\) og deretter på knappen Clone or download.  
Du skal nå velge clone with https og klikk på knappen for å kopiere linken.

Nå starter du terminal \(eller powershell\) og går inn i eller lager den mappen hvor du vil ha kopien.  
Skriv `git clone`  og trykk cmd+v \(eller ctrl+v\) for å lime inn linken du kopierte.  
Trykk _enter_ og du vil få en lokal kopi

### Oppdatering med git

Legg nye prosjekter inn i denne git-mappen og skriv:  
  `git add mappeNavn/` for at denne nye mappa skal bli med i repositoriet.

Hver gang du har redigert/sletta/lagt til filer i et prosjekt og ønsker å legge disse endringene ut - da skriver du kommandoene under:

```text
git commit -a -m "en beskrivelse av endringene"
git push
```

Nå må du oppgi brukernavn og passord \(du ser ikke passordet når du skriver\).  
Filene vil bli synkronisert opp til github.  
Dette skal vanligvis gjøres i slutten av timen slik at alle filer er lagra på github.

### Git i VS-code

Dersom du åpner git-mappa i VSCode vil du kunne gjøre det meste herfra.  
Rediger filer som vanlig - før timen er slutt klikker du på **Source Control** i venstre marg - se bildet.



![Source Control er nederst til venstre](https://audunhauge.gitbooks.io/it1-informasjonsteknologi1/content/assets/nyFil.png)

Her vil du se en liste over filer som er endra - klikk på **+** knappen over lista.  
Klikk nå på ok knappen \( ✓\)  \(se bildet under\) , skriv en liten melding om hva endringen går ut på \("redigerte noe"\). Klikk deretter på \(...\)  \(se bildet under\) knappen og velg **push**. Du må nå oppgi brukernavn og passord for din github.

![Knapper for GIT i vscode](../.gitbook/assets/image%20%281%29.png)

  


