# Oppgave 1

## Lage en nettside og en S3-bucket

Amazon S3 står for Simple Storage Service, og er en tjeneste for lagring og henting av data. Tenk litt på det som en fancy delt disk! 

I dag skal vi bruke det å hoste en statisk nettside. 
Dette gjør vi ved å lagre html-en og css-en vår i en såkalt S3-bucket. La oss sette igang! 

Start med å gå inn på s3, enten via "Services"-menyen oppe til venstre, søkefeltet på toppem midt i, eller via denne lenken: https://s3.console.aws.amazon.com/s3/home?region=eu-west-1#.

## 1.1 Din S3-bucket
Da skal vi lage bøtta vår! Når man skal bruke en bøtte til en statisk nettside er det litt rare regler fra Amazon sin side. En av disse er at en bøtte må hete det samme som domenet som brukes. De må også være unike. 
Her lager vi en bøtte som heter `<fornavn><etternavn>.bekk.cloud` for å sørge for at det fungerer senere. For eksempel `karinordmann.bekk.cloud`. 

Trykk på den oransje "Create bucket" knappen og velg følgende:
- Bucket name: `<fornavn><etternavn>.bekk.cloud`
- AWS Region: EU (Ireland) eu-west-1.
- Skru **AV** Block all public access og bekreft dette.
 
Trykk "Create Bucket" på bunnen. Tadaa! Da har du en bøtte!

## 1.2 Statisk nettside

Til sist må vi jo få opp netsiden.
Søk opp bøtten din og åpne den opp. Nå skal vi gjøre den om til en statisk nettside. 
Velg `Properties` og finn `Static website hosting`. Trykk "Edit" på denne og fyll inn:
- Static website hosting: enable
- Hosting type: Host a static website
- Index document: `index.html`
- Error document: blank
- Redirection rules: blank

Trykk på "Save changes". Deretter velger du `objects` i fanebladene.
Drag-n-dropp filen som heter `index.html` fra denne mappen over til S3. Under "Permissions" pass på å sette `Predefined ACLs` til `Grand public-read access` og bekreft dette. Hvis ikke får ingen lov til å åpne nettsiden din 🤷‍♂️.
Trykk "Upload". Nettsiden din bør nå være tilgjengelig på `http://<bucket-name>.s3-website.eu-west-1.amazonaws.com/`. Bra jobba!