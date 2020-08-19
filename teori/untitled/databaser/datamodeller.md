---
description: Hvordan designe databaser
---

# Datamodeller

## Bruk av dbDiagram

Du kan tegne diagrammer med programmet [dbdiagram](https://dbdiagram.io).

Det er enklest å importere **create table { ... }** som vi lager i vs-code.  
Definer tabellene, lag nøkkelfelt og fremmednøkler. Importer sql til dbdiagram.

Deretter kan du lage koblinger mellom tabellen ved å dra nøkkelfelt bort til fremmednøkler.  
Da kan du lett lage et diagram som vist under:

![er-diagram for bibliotek](../../../.gitbook/assets/dbdiagram%20%281%29.png)

### Tolkning av et er-diagram

I erdiagram vises koblingene mellom tabeller, typisk vi du ha en-til-mange koblinger mellom to tabeller slik som mellom laaner og utlaan i erd-modellen over.  
Den tabellen som har fremmednøkkelen \(kopi av nøkkelfelt fra en annen tabell\) er på mange-siden.  
Dermed leser vi koblingen i modellen over slik:  
   en laaner har mange utlaan  
   et eksemplar har mange utlaan  
   en bok har mange eksemplar  
   en forfatter har mange bok \(bøker\)

