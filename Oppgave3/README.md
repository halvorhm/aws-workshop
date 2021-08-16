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

Nå som vi har prøvd oss på å kjøre og deploye en funksjon, skal vi lage en funksjon som gjør noe litt mer spennende, nemlig å hente hytteinfo fra en database. Databasetabellen er laget med en AWS-tjeneste som heter DynamoDB, og finnes her:
https://eu-west-1.console.aws.amazon.com/dynamodb/home?region=eu-west-1#tables:selected=bekk_hytter;tab=items

Funksjonen vår skal hente hytte-informasjon om alle hyttene fra tabellen, og printe denne informasjonen med console.log

- Åpne handler.js-fila som ble opprettet da du opprettet serverless-prosjekt. Vi skal lage funksjonen vår her.
- Siden vi skal hente data fra en DynamoDB-tabell, må vi gjøre noe for at koden vår skal få tilgang til denne aws-tjenesten. Det gjør vi ved hjelp av AWS SDK, ved å legge til disse to linjene på toppen av handler.js:  
```
const AWS = require('aws-sdk');
const database = new AWS.DynamoDB.DocumentClient({region: 'eu-west-1'});
```
Da kan vi begynne på selve funksjonen! :)


## 3.5

- Kopier koden under inn i handler.js.

```
module.exports.hentHyttedata = async (event, context, callback) => {
    await lesHyttedataFraTabell().then(hyttedata => {
      // Kode for å printe det vi har hentet.

    }).catch((err) => {
      console.error(err);
    })  
};

function lesHyttedataFraTabell() {
   //kode for å hente data fra databasen 
}
```

function lesHyttedataFraTabell() {
   //kode for å hente data fra databasen 
}

Her mangler det kode for å både hente og printe data, så det skal vi fylle inn nå.

Vi begynner med å fylle ut funksjonen for å lese hyttedata fra tabellen.
Til dette skal vi bruke scan-funksjonen til DynamoDB. 

Under er et eksempel på bruk av scan for henting av data fra en filmtabell. 
I dette eksempelet ønsker de å hente filmer fra 1950-1959, og de ønsker kun å ha tilgang til år og tittel.
I vårt tilfelle skal vi hente alt som ligger i tabellen bekk_hytter, så det eneste parameteret vi trenger er TableName.
De andre parameterne kommer vi tilbake til i senere oppgaver.

- Ta utgangspunkt i eksempelet under og fyll ut funksjonen lesHyttedataFraTabell.

```
var params = {
    TableName: "Movies",
    ProjectionExpression: "#yr, title",
    FilterExpression: "#yr between :start_yr and :end_yr",
    ExpressionAttributeNames: {
        "#yr": "year",
    },
    ExpressionAttributeValues: {
         ":start_yr": 1950,
         ":end_yr": 1959 
    }
};
```


For å teste funksjonen din lokalt, kjører du samme kommando i terminalen som du gjorde med hello-funksjonen:
`serverless invoke local --function hentHyttedata`



- Deploye, men huske å legge til funksjonen i serverless.yml
- Kjøre funksjonen i konsollen. 

## 3.5