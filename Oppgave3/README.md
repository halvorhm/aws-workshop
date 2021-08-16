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
- Gå inn på https://console.aws.amazon.com/
- I menyen i toppen søk etter og velg "Lambda".
- Funksjonen din bør nå ha dukket opp under "Functions" (navnetditt-dev-hello). Trykk på denne.
- For å kjøre funksjonen din her, trykker du på den oransje "TEST"-knappen. Får du opp et vindu som spør om _configure test event_ så bare skriv noe på Event name, f.eks. "test" og trykk Create. Trykk så på test-knappen på nytt.
- BAM! Du har nå kjørt funksjonen din! Woop!
(Hvis du gjør endringer på funksjonen din her, må du trykke deploy før du kjører funksjonen din på nytt for at endringene skal ta effekt)

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
Da kan vi begynne på selve funksjonen! :) Siden vi ikke har kjempemye tid i dag, har vi gjort klart noe av koden på forhånd.

- Kopier dette inn i handler.js:

```
module.exports.hentHyttedata = async (event, context, callback) => {
    await lesHyttedataFraTabell().then(hyttedata => {
      hyttedata.Items.forEach(function(hytte){
        console.log(hytte)
      })

    }).catch((err) => {
      console.error(err);
    })  
};

function lesHyttedataFraTabell() {
   //kode for å hente data fra tabellen 
}
```


## 3.5

I funksjonen du nettopp kopierte mangler koden som trengs for å hente data fra tabellen, så det skal vi fylle inn nå! For å hente data fra tabellen vår kan vi bruke en dynamoDB-funksjon som heter scan. Denne henter all data fra en tabell, og man kan velge å filtrere dataene når de er hentet.

Under er et eksempel på bruk av scan for henting av data fra en filmtabell. 
I dette eksempelet hentes alle data som ligger i tabellen Movies, og så filtreres dette så man kun blir sittende igjen med feltene "år" og "tittel", og bare filmer fra 1950-1959.

I vårt tilfelle vil vi foreløpig ha tak i alt som ligger i tabellen bekk_hytter, så det eneste parameteret vi trenger å ha med er TableName. De andre parameterne trenger dere ikke å tenke på nå. Vi kommer tilbake til det i senere oppgaver :) 

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

database.scan(params).promise();

```

For å teste funksjonen din lokalt, kjører du samme kommando i terminalen som du gjorde med hello-funksjonen:  
`serverless invoke local --function hentHyttedata`

Hvis du står fast kan du ta en kikk på den ferdige funksjonen "hent-hyttedata" som ligger under Lambda -> Functions i aws-consollen (nettsiden).


## 3.6

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


## 3.7

Vi har ikke bruk for hello-funksjonen lenger, så denne kan vi slette.

- Fjern hellofunksjonen fra handler.js og fra serverless.yml og lagre.
- deploy med `serverless deploy --stage dev`
- `dittnavn-dev-hello` skal nå ikke finnes under Lambda -> Functions lenger.