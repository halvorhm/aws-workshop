# Oppgave 3

## Lambda

Vi har nå laget en nettside ved hjelp av to AWS-tjenester: S3 (lagring) og Route53 (DNS). Det neste vi skal kikke på er tjenesten Lambda, som brukes til å kjøre funksjoner.

Vi begynner med å lage en liten funksjon som bare printer en beskjed, og etter det skal vi lage en funksjon for å hente info om Bekk sine hytter fra en database.


## 3.1

Hittil har vi bare jobbet direkte i AWS-konsollen (på nettsiden). I denne oppgaven skal vi derimot kode lokalt på maskina vår, men da trenger vi en måte å få deployet funksjonene vår til aws. Til det skal vi bruke et rammeverk som heter Serverless, så det første vi gjør er å opprette et Serverless-prosjekt:

- Åpne terminalen på laptopen og gå til mappen du vil ha prosjektet ditt i.
- Kjør kommandoen `serverless` og svar ja på at du vil opprette et nytt prosjekt.
- Når den spør om hva du vil lage, velg AWS Node.js - Starter (evt. bare AWS Node.js hvis det ikke står noe mer)
- Bruk ditt eget navn som navn på prosjektet.   
- Spør den om du vil lage en serverless account kan du svare `nei`. 
- Spør den om du vil deploye prosjektet ditt svarer du `nei`. 


## 3.2

Det skal nå være opprettet en mappe med prosjektnavnet ditt som inneholder to filer: `serverless.yml` og `handler.js`.

- I `serverless.yml` trenger vi ikke å gjøre noe bortsett fra å sette riktig region. Gjør dette ved å legge til `region: eu-west-1` under feltet `provider`.

- `handler.js` er den fila hvor vi skal ha funksjonene våre, og denne er allerede fylt ut med et ferdig eksempel. Endre `message` i denne fila til en personlig melding og lagre.

- For å kjøre en funksjon lokalt, går du inn i prosjektmappa i terminalen og skriver
  `serverless invoke local --function navnPåFunksjonen` 
  dvs `serverless invoke local --function hello` i dette tilfellet.
  Du skal da få opp statusCode 200 og meldinga du har skrevet.

🙌 Bra jobba! 🙌

## 3.3

Nå skal vi deploye funksjonen vår og sjekke ut det vi har gjort i aws-konsollen!

- Gå til prosjektmappa i terminalen og deploy ved hjelp av kommandoen `serverless deploy --stage dev` (dette kan ta litt tid).
- Gå inn på aws-consollen: https://console.aws.amazon.com/
- I menyen i toppen søk etter og velg "Lambda".
- Funksjonen din bør nå ha dukket opp under "Functions" (navnetditt-dev-hello). Trykk på denne.
- For å kjøre funksjonen din her, trykker du på den oransje "TEST"-knappen. Får du opp et vindu som spør om _configure test event_ så bare skriv noe på Event name, f.eks. "test" og trykk Create. Trykk så på test-knappen på nytt.
- BAM! Du har nå kjørt funksjonen din! Woop!
(Hvis du gjør endringer på funksjonen din her, må du trykke deploy før du kjører funksjonen din på nytt for at endringene skal ta effekt)

