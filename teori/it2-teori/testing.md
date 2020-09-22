# Testing

### Beskrivelse av en testplan

* Ikke beskriv programmet
* Beskriv hvordan teste
* Beskriv hva du tester
* Beskriv akseptable resultat av testene

### Eksempel på en testplan

Testplan for eksamen vår 2019.  
Skal teste funksjonen pixelcalculator som beregner antall pixler  
gitt bredde og høyde.

1. Test at app godtar bare gyldige verdier på bredde/høyde Skal akseptere tall i område \(1..1920\) for begge. Tester med negative tall, 0, 1, 200, 500, 1920, 1921, store tall. Forventer aksept for alle tall 1..1920. Forventer feilmelding for alle andre. RESULTAT: godtar alle tall mellom 1..1920
2. Test at app beregner riktig. Tester med 1x1 1x100, 1000x1, 513x265, 1920x1920 Forventer 1x1 gir 1pixels 0.0000001Mpix RESULTAT riktige verdier



