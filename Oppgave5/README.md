# Oppgave 5

## Når alt kobles sammen

Vi har vært innom mye ting nå, men det henger liksom ikke skikkelig sammen. Det skal vi ordne nå!
Vi går trinnvis frem og kobler sammen de forskjellige elementene. 

## 5.1 Nettsiden vår

Her trengs det ikke så mye magi for å få ting til å fungere. Det eneste vi trenger å endre hvor vi sender API-kallet vårt i index.html
Last så opp den nye versjonen i S3-bøtten vi laget i oppgave 1 og vi bør være good to go!

## 5.2 Lambdaen og API gatewayen vår
Nå skal vi dykke litt dypere ned i ting!
Hvis vi ser på lambda-koden vår så mottar vi et objekt som heter `event`. Denne inneholder ganske så mye morro nemlig.

### 5.2.1
La oss starte med å titte litt på dette objektet. 
- Legg inn `console.log(event);` før du returnerer noe i lambda-funskjonen din.
- Gjør en `serverless deploy --stage dev` for å dytte koden ut. 
- Prøv å trigge funksjonen din en gang med en test-event, som i oppgave 3. 
- Prøv å trigge en event ved å gå inn på lenken til API gatewayen din. 

Nå skal vi se litt på de loggene. Først finner du din funksjon her: https://eu-west-1.console.aws.amazon.com/cloudwatch/home?region=eu-west-1#logsV2:log-groups.
Når du har funnet den, trykk på den oransje knappen oppe til høyre hvor det står "Search log group". 
Huk av den lille sjekkboksen for "View as text" for å gjøre livet litt enklere.
Her ser vi litt morsomme ting!

### 5.2.2
Hvis vi nå legger på litt query parameters når vi sender en melding til apiet vårt, 
f.eks. legg på `?mat=digg` så ser vi at dette blir gjort tilgjengelig som `queryStringParameters: {
mat: "digg"}` i event-objektet!

Oppgaven: Bytt ut den hardkodete lokasjonen i lambda-koden med et query parameter via api-gatewayen. Du velger selv hva den skal hete ☺️.

## 5.3
Gratulerer! Du har nå satt opp en vaskeekte tjeneste! Du har nå:
- En nettside til brukeren
- En api gateway som kan ta imot spørringer og sende de til forskjellige steder. 
- En "backend" i lambda som tar imot requester og behandler de

