---
description: Hvordan designe databaser
---

# Datamodeller

## Bruk av ERDPlus

Du kan tegne diagrammer med programmet [erdPluss](https://erdpluss.com).

Klikk på New knappen og lag først et ER Diagram.  
Lag en ny tabell ved å bruke verktøyet **Entity** \(knapperad\).  
Legg til felt i tabellen med Add Attribute **knappen** \(til høyre\).

Lag alle tabeller og deretter kobling mellom dem \(Connect\).

Husk at alle tabeller skal ha et ID felt - tabellen bok skal ha **bokID**, tabellen forfatter skal ha **forfatterID** .

Når denne modellen er ferdig skal du konvertere den til et relasjonsdiagram \(Convert to relational schema\). Dette gjør du ved å klikke på tannhjulet for ER-modellen i oversikten over diagram \(**Diagrams**\).

Rediger tabellene: sjekk at nøkkelfelt er satt, set typer på alle felt \(de er alle INT som default\). Sjekk også at koblingene er i orden - lag dem på nytt i dette vinduet dersom de mangler. Husk at kråkefoten skal vises på mange-sida.

