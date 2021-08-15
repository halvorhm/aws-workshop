# Oppgave 3

## Lambda

Vi har nå laget en nettside ved hjelp av to AWS-tjenester: S3 (lagring) og Route53 (DNS). Det neste vi skal kikke på er tjenesten Lambda, som brukes til å kjøre funksjoner.

Vi begynner med å lage en liten funksjon som returnerer en selvvalgt beskjed, og etter det skal vi lage en funksjon for å hente info om Bekk sine hytter. 


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
- Gå til prosjektmappa i terminalen og deploy ved hjelp av kommandoen `serverless deploy --stage dev`.

🙌 Bra jobba! 🙌

## 3.3

Nå skal vi sjekke ut det vi har gjort i aws-konsollen!
- Gå inn på https://console.aws.amazon.com/
- I menyen i toppen søk etter og velg "Lambda".
- Under "Functions" finn din funksjon (navnetditt-dev-hello) og trykk på denne.
- For å kjøre funksjonen din trykker du på den oransje "TEST"-knappen. Får du opp et vindu som spør om _configure test event_ så bare skriv noe på Event name, f.eks. "test" og trykk Create.
- BAM! Du har nå kjørt funksjonen din! Woop!


## 3.3
Her skal vi lese noe fra dynamodb og returnere det.

## 3.4