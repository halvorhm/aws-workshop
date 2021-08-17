# Oppgave 6

## Når alt kobles sammen

Vi har vært innom mye ting nå, men det henger liksom ikke skikkelig sammen. Det skal vi ordne nå!
Vi går trinnvis frem og kobler sammen de forskjellige elementene.

## 6.1
Nå skal vi dykke litt dypere ned i ting!
Hvis vi ser på lambda-koden vår så mottar vi et objekt som heter `event`. Denne inneholder ganske så mye morro nemlig.

### 6.2
La oss titte litt mer på dette `event` objektet. 
- Legg inn `console.log(event);` før du returnerer noe i lambda-funskjonen din.
- Gjør en `serverless deploy --stage dev` for å dytte koden ut. 
- Prøv å trigge funksjonen din en gang med en test-event, som i oppgave 3. 
- Prøv å trigge en event ved å gå inn på lenken til API gatewayen din. 

Nå skal vi se litt på de loggene. Først finner du din funksjon her: https://eu-west-1.console.aws.amazon.com/cloudwatch/home?region=eu-west-1#logsV2:log-groups.
Når du har funnet den, trykk på den oransje knappen oppe til høyre hvor det står "Search log group". 
Huk av den lille sjekkboksen for "View as text" for å gjøre livet litt enklere.
Her ser vi litt morsomme ting, blant annet query params!

Her er et eksempel på dette fra imdb.com, hvor genre og year er queryparametere:  
https://www.imdb.com/search/title/?genres=drama&year=2021

Hvis vi nå legger på litt query parameters når vi sender en melding til apiet vårt, 
f.eks. legg på `?mat=digg` så ser vi dette i loggen som `queryStringParameters: {
mat: "digg"}` i event-objektet!


### 6.3
Hittil har vi kalt /hytter for å hente hytteinformasjon med API-et vårt.
Nå skal vi utvide funksjonaliteten så vi også kan velge å kun hente hytter med spesifikke egenskaper ved hjelp av query params!
Bekk har hytter både på fjellet og ved havet. La oss prøve å kun hente de hyttene som ligger på fjellet. Denne informasjonen finner vi på feltet “lokasjon”.
- Legg til queryparameteret “lokasjon” etter /hytter i api-url-en din.
Vi må også redigere lambdafunksjonen vår, sånn at den tar hensyn til at vi kan ha sendt med et queryparameter, og at den i så fall bare returnerer de relevante hyttene.
- Gå inn i Functions -> Lambda og finn lambdafunksjonen din i aws-consollen.
- Trykk på den lille trekanten i den orange test-boksen. Trykk configure test event og lim inn dette:

```
{
  “queryStringParameters”: {
    “lokasjon”: “fjellet”
  }
}
```

Dette gjør at vi later som vi har sendt inn lokasjon som queryparameter når vi tester funksjonen vår i consollen.
Queryparameterne våre finner vi inni event i lambdafunksjonen under event.queryStringParameters

- Legg til en const som inneholder queryparameteret lokasjon mellom exports.handler.... og await, og send denne inn som parameter til lesHyttedataFraTabell. Du kan sniktitte på lambdafunksjonen som heter hentHyttedataMedQueryparams hvis du lurer på hvordan du skal gjøre det.

🤫  Du kan ta en sniktitt på lambdaen `hentHyttedataMedQueryparams` her 🤫.

- Ta en ny kikk på eksempelet med filmtabellen. Prøv å bruke FilterExpression og ExpressionAttributeValues for å sette “lokasjon” som et filter i søket. (det er lov å sniktitte her og).
  
```
var params = {
    TableName: “Movies”,
    ProjectionExpression: “#yr, title”,
    FilterExpression: “#yr between :start_yr and :end_yr”,
    ExpressionAttributeNames: {
        “#yr”: “year”,
    },
    ExpressionAttributeValues: {
         “:start_yr”: 1950,
         “:end_yr”: 1959
    }
}
```

Deploy dette og test funksjonen i consollen, og se om du nå får opp tre hytter, som alle har lokasjon: fjellet.


## 6.4
Helt til sist vil vi jo sende requesten fra nettsiden vår! Ta Api-gateway URLen din fra tidligere. Lim inn denne i `API_FUNCTION_URL` i index.html filen din (med `hytte` bak). 
Deretter laster du opp den nye index.html siden din i s3 bøtta. Da bør du være good to go!

## 6.5
Gratulerer! Du har nå satt opp en vaskeekte tjeneste! Du har nå:
- En nettside til brukeren
- En api gateway som kan ta imot spørringer og sende de til forskjellige steder. 
- En "backend" i lambda som tar imot requester og behandler de

Vi erklærer deg herved en fullstackutvikler 🙌

