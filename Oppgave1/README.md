# Oppgave 1

## Lage en nettside og en S3-bucket

Amazon S3 står for Simple Storage Service, og er en tjeneste for lagring og henting av data.
Vi skal bruke dette til å hoste nettsiden vår. Dette gjør vi ved å lagre html-en og css-en vår i en såkalt S3-bucket. Filene vi legger i bucketen blir tilgjengelige på en url på dette formatet:

https://s3.amazonaws.com/bucketnavn/filnavn