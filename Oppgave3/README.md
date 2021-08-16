# Oppgave 3

## Lambda

Vi har nå laget en nettside ved hjelp av to AWS-tjenester: S3 (lagring) og Route53 (DNS). Det neste vi skal kikke på er tjenesten Lambda, som brukes til å kjøre funksjoner.

Vi begynner med å lage en liten funksjon som returnerer en selvvalgt beskjed, og så skal vi lage en funksjon for å hente info om Bekk sine hytter fra en database.


## 3.1

Hittil har vi bare jobbet direkte i AWS-konsollen (på nettsiden). I denne oppgaven skal vi derimot kode lokalt på maskina vår, men vi trenger en måte å få deployet koden vår til aws. Til det skal vi bruke et rammeverk som heter Serverless, så det første vi skal gjøre er å opprette et Serverless-prosjekt:

- Åpne terminalen på laptopen og gå til mappen du vil ha prosjektet ditt i.
- Kjør kommandoen `serverless` og svar ja på at du vil opprette et nytt prosjekt.
- Når den spør om hva du vil lage, velg AWS Node.js - Starter (evt. bare AWS Node.js hvis det ikke står noe mer)
- Bruk ditt eget navn som navn på prosjektet.   
- Spør den om du vil lage en serverless konto kan du svare `nei`. 
- Spør den om du vil deploye prosjektet ditt svarer du `nei`. 


## 3.2

Det skal nå være opprettet en mappe med prosjektnavnet ditt som inneholder to filer: `serverless.yml` og `handler.js`.

- I `serverless.yml` trenger vi ikke å gjøre noe bortsett fra å sette riktig region. Gjør dette ved å legge til `region: eu-west-1` under `provider`.

- `handler.js` inneholder javascript-koden vi skal kjøre, og er fylt ut med et ferdig eksempel. Endre `message` i denne fila til en personlig melding og lagre.

- For å kjøre en funksjon lokalt, går du inn i prosjektmappa i terminalen og skriver
  `serverless invoke local --function navnPåFunksjonen` 
  dvs `serverless invoke local --function hello` i dette tilfellet.
  Du skal da få opp statusCode 200 og meldinga du har skrevet.

🙌 Bra jobba! 🙌

## 3.3

Nå skal vi deploye funksjonen vår og sjekke ut det vi har gjort i aws-konsollen!

- Gå til prosjektmappa i terminalen og deploy ved hjelp av kommandoen `serverless deploy --stage dev`.
- Gå inn på https://console.aws.amazon.com/
- I menyen i toppen søk etter og velg "Lambda".
- Funksjonen din bør nå ha dukket opp under "Functions" (navnetditt-dev-hello). Trykk på denne.
- For å kjøre funksjonen din her, trykker du på den oransje "TEST"-knappen. Får du opp et vindu som spør om _configure test event_ så bare skriv noe på Event name, f.eks. "test" og trykk Create.
- BAM! Du har nå kjørt funksjonen din! Woop!

## 3.4

Nå som vi har prøvd oss på å kjøre og deploye en funksjon, skal vi lage en funksjon som gjør noe litt mer spennende, nemlig å hente hytteinfo fra en database. Databasetabellen er allerede utfylt, og til dette er det brukt en AWS-tjeneste som heter DynamoDB. Tabellen heter bekk_hytter, og finnes her:
https://eu-west-1.console.aws.amazon.com/dynamodb/home?region=eu-west-1#tables:selected=bekk_hytter;tab=items


Funksjonen skal hente hytte-informasjon om alle hyttene fra tabellen, og printe denne informasjonen med console.log

Vi lager funksjonen vår i handler.js-fila som ble opprettet da du lagde serverless-prosjekt. 

- Siden vi skal hente data fra en DynamoDB-database, må vi gjøre noe for at javascript-koden vår skal få tilgang til denne aws-tjenesten. Dette gjør vi ved hjelp av AWS SDK, ved å legge til disse to linjene på toppen av handler.js:

`const AWS = require('aws-sdk');`
`const database = new AWS.DynamoDB.DocumentClient({region: 'eu-west-1'});`

- Opprett en ny funksjon i `handler.js` som du kaller `hentHyttedata` e.l.. Hvis du vil, kan du ta utgangspunkt i hello-funksjonen som allerede ligger der ved å kopiere den, fjerne alt innhold og endre navn.


Info om hvordan man skriver funksjonen.

For å teste funksjonen din lokalt, kjører du samme kommando i terminalen som du gjorde med hello-funksjonen:
`serverless invoke local --function hentHyttedata`



- Deploye, men huske å legge til funksjonen i serverless.yml
- Kjøre funksjonen i konsollen. 

## 3.5