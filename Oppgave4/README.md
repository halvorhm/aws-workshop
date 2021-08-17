# Oppgave 4

## Lese fra DynamoDB


Nå som vi har prøvd oss på å kjøre og deploye en funksjon, skal vi lage en funksjon som gjør noe litt mer spennende, nemlig å hente data fra en database. Database-tjenesten vi bruker heter DynamoDB, og tabellen kan dere se [her](https://eu-west-1.console.aws.amazon.com/dynamodb/home?region=eu-west-1#tables:selected=bekk_hytter;tab=items).  
Funksjonen vår skal hente informasjon om hyttene til Bekk fra tabellen, og printe denne informasjonen.

## 4.1

- Åpne handler.js-fila som ble laget da du opprettet serverless-prosjektet. Vi skal lage funksjonen vår her.
- Det første vi skal gjøre er å legge til disse to linjene på toppen av handler.js:

```
const AWS = require('aws-sdk');
const ddb = new AWS.DynamoDB.DocumentClient({region: 'eu-west-1'});
```

[AWS.DynamoDB.DocumentClient](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/DynamoDB/DocumentClient.html) inneholder nyttige metoder for å gjøre ting med databasen (get, put, query, delete osv.).


- Vi må også gjøre en liten endring i serverless.yml-fila for å få tilgang til å lese fra databasen. Legg til iamRoleStatements under provider, så det ser sånn ut:

```
provider:
  name: aws
  runtime: nodejs12.x
  lambdaHashingVersion: 20201221
  region: eu-west-1
  iamRoleStatements:
    - Effect: 'Allow'
      Action:
        - 'dynamodb:*'
      Resource:
        - '*'
```
  
  
Nå er vi klare til å begynne på selve funksjonen! :) 


## 4.2
Siden vi ikke har kjempemye tid i dag, har vi gjort klart noe av koden på forhånd.

- Kopier dette inn i handler.js:

```
module.exports.hentHyttedata = async (event, context, callback) => {
    return await lesHyttedataFraTabell().then(hyttedata => {
        return hyttedata;
    }).catch((err) => {
      console.error(err);
    })  
};

function lesHyttedataFraTabell() {
   //kode for å hente data fra tabellen 
}  
```
  
I funksjonen du nettopp kopierte mangler koden som trengs for å hente data fra tabellen, så det skal vi fylle inn nå! For å hente data fra tabellen vår skal vi bruke en metode som heter scan. Denne henter all data fra en tabell, og man kan velge å filtrere dataene når de er hentet.

Under er et eksempel på bruk av scan for henting av data fra en filmtabell. 
I dette eksempelet hentes alle data som ligger i tabellen Movies, og så filtreres dette så man kun blir sittende igjen med feltene "yr" og "title", og bare filmer fra 1950-1959.

I vårt tilfelle vil vi foreløpig ha tak i alt som ligger i tabellen bekk_hytter, så det eneste parameteret vi trenger å ha med er TableName. De andre parameterne trenger dere ikke å tenke på her. Vi kommer tilbake til det i senere oppgaver :) 

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
}

ddb.scan(params).promise();

```

- For å teste funksjonen din lokalt, kjører du samme kommando i terminalen som du gjorde med hello-funksjonen:  
`serverless invoke local --function hentHyttedata`. 



Hvis du står fast kan du ta en kikk på den ferdige funksjonen "hent-hyttedata" som ligger under Lambda -> Functions i aws-consollen (nettsiden).

## 4.3

- Prøv å deploye den nye funksjonen slik du gjorde med hello-funksjonen med `serverless deploy --stage dev`   
  I terminalen vil du se at den nye funksjonen ikke dukker opp under `functions` når du kjører kommandoen, og du vil heller ikke finne den under Lambda -> Functions i aws-consollen.
  Grunnen til dette er at vi ikke har lagt til funksjonen i serverless.yml.

- Åpne serverless.yml. Et stykke ned i fila står dette under functions:
```
  functions:
    hello:
      handler: handler.hello
```
- legg til dette nedenfor hello:
```
  hentHyttedata:
    handler: handler.hentHyttedata
```

- Prøv å deploye på nytt. Funksjonen bør nå være å finne i aws-consollen under Lambda -> Functions med navnet dittnavn-dev-hentHyttedata

- Kjør funksjonen ved å trykke på den oransje test-knappen sånn som du gjorde sist.


## 4.4

Vi har ikke bruk for hello-funksjonen lenger, så denne kan vi slette.

- Fjern hellofunksjonen fra handler.js og fra serverless.yml og lagre.
- deploy med `serverless deploy --stage dev`
- `dittnavn-dev-hello` skal nå ikke finnes under Lambda -> Functions lenger.
