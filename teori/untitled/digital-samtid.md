# Digital samtid

## Læreplanmålene

* beskrive ulike typer digitalt utstyr og forklare hovedtrekkene ved virkemåten 
* forklare hvordan de fysiske signalene i datautstyr kan tolkes som binære tall, tegnsett, grafiske framstillinger, billedpunkter og lyd 
* gjøre rede for standarder for kommunikasjon mellom ulike former for digitalt utstyr og mellom programmer 
* gjøre rede for hvilke utfordringer og muligheter den digitale verden kan skape for språklige og kulturelle minoriteter 
* gjøre rede for og argumentere for nødvendigheten av regelverk og etiske normer for bruk av informasjonsteknologi 
* beskrive og drøfte informasjonsteknologiens muligheter og konsekvenser 
* beskrive og foreslå tiltak mot trusler i den digitale verden

## Digitalt utstyr <a id="digitalt-utstyr"></a>

## Hovedkomponenter i datamaskinen

### **Hovedkort**

Datamaskinens hovedkort er et kretskort som binder sammen de andre komponentene i maskinen. På hovedkortet er det en databuss som kobler sammen de komponentene som må sende signaler til hverandre.

![Hovedkort for en pc](../../.gitbook/assets/image%20%286%29.png)

### **Ram**

RAM er datamaskinens arbeidsminne

### **CPU**

Central Prosessing Unit, Prosessor

![Skjematisk fremstilling av en CPU](../../.gitbook/assets/image%20%284%29.png)

I diagrammet over viser svarte piler dataflyt, røde er kontrollsignaler.  


### **Skjermkort**

Rendrer det som skal vises på skjermen.  
Moderne skjermkort innholder en egen GPU \(graphics processing unit\) som kan være like avanserte som hovedprosessoren. Den er spesialisert på å utføre beregninger som trengs for å vise 3D grafikk.

![Nvidia GeForce GTX 650 grafikk-kort](../../.gitbook/assets/image%20%288%29.png)

### **Nettverkskort/WiFi**

Sender signaler over kabel eller trådløst, mellom maskiner.

![En mikroprosessor med wifi - det svarte feltet &#xF8;verst er antennen.](../../.gitbook/assets/image%20%287%29.png)

### **Skjerm**

Viser bilder, oppløsning i dag er ofte 4k. 

### Operativsystem <a id="operativsystem"></a>

Alle maskiner trenger et operativsystem som styrer resurssbruken og hvilke programmer som skal kjøre. Operativsystemet gir også rettigheter til brukere slik at de har forskjellige begrensninger på hva de kan gjøre på maskinen \(lese filer, kjøre programmer\).

### Linux

Operativsystemet som driver alle top 500 \(i skrivende stund\) superdatamaskineri verden.  
Android er også en linux-variant.

### Windows

Brukes av noen \(ingen vet helt hvorfor\).

#### OSX <a id="osx"></a>

For de som synes design er det viktigste.

### Andre OS

Tidligere var OS2 en konkurrent til windows \(laga av IBM\).

Unix og AIX og SCO var konkurrenter til Linux

Eldre os er dos, amiga pdp-11 osv

### Nettverk <a id="nettverk"></a>

Datamaskiner kobles sammen i nettverk.

![](https://audunhauge.gitbooks.io/it1-informasjonsteknologi1/content/assets/network-topology-idea.PNG)

Tegningen viser et nettverk tilsvarende det vi har på skolen vår. Noen av disse maskinene står plassert i fylket \(SW og BWF\), resten er innstallert på skolen. Koblingen mellom switcher og PCer er tegna som kabler, men er nå stort sett trådløs.

POE switchene leverer strøm over internett-kablingen \(cat6\) slik at det er enkelt å montere kamera og levere strøm og nett samtidig.

## Binærtall, hex, bits og bytes <a id="bin&#xE6;rtall-hex-bits-og-bytes"></a>

Datamaskiner bruker binærtall internt \(CPU bruker binærtall\)

Et binærtall slik som 11011011 kan konverteres til desimal slik:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 0 | 1 | 1 | 0 | 1 | 1 |

Summer 128+64+16+8+2+1 \(der hvor binærtallet har siffer 1\).

Et binærtall kan konverteres til hex på denne måten:

Grupper binærtallet i grupper på 4 bits \(1 bit er et binært siffer, 0 eller 1\)  
Skriv over tallfølgen 8 4 2 1 \( som vi gjør for konvertering til desimal\)  
For hver gruppe på 4 bits får vi da et hexadesimalt siffer  
0-9 er uendra, 10=A,11=B, ... 15=F

Eksempel:

| 8 | 4 | 2 | 1 |
| :--- | :--- | :--- | :--- |
| 1 | 1 | 0 | 1 |

Tallverdien blir 8+4+1 = 13, 13 = D

Som nevnt kalles 1 binært siffer for en bit.  
8 bits kalles 1 byte.  
En byte kan inneholde tallverdier fra 0 til 255.  
En byte brukes ofte til å representere ett tegn fra et tegnsett.  
I starten brukte datamaskiner tegnsettet ASCII som var 7 bit \(128 forskjellige tegn\)  
Dette ble senere utvida til ANSI \(256 tegn\)  
Nå bruker vi UTF-8, hvor hvert tegn kan bruke fra 1 til 4 bytes.  
Noen programmer bruker fortsatt eldre tegnsett - slik at vi får problemer når vi publiserer,  
typisk blir ÆØÅøæå til &\#rølp;

På en nettside må vi bruker &lt;meta charset="UTF-8"&gt; for at vi skal kunne bruke øæå uten problemer.

Bildet under viser Microsoft Office 365 som sliter med øæå og hermetegn ...

![](https://audunhauge.gitbooks.io/it1-informasjonsteknologi1/content/assets/image.png)

### **Hexverdier**

Hexadesimale tall vil du vanligvis se som fargeverdier i css

* \#FF0000 = rød
* \#00FF00 = grønn
* \#0000FF = blå

Legg merke til rekkefølgen: rød,grønn,blå. Denne fargekodingen kalles RGB \(red,green,blue\).

Noen fargeverdier har med 2 ekstra hex-siffer slik som \#FF000080  
Dette er rgba - hvor siste verdi angir gjennomsiktighet \(00=transparent, FF=opaque\)

