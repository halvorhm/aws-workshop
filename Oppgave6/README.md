# Oppgave 6

## Når alt kobles sammen

Vi har vært innom mye ting nå, men det henger liksom ikke skikkelig sammen. Det skal vi ordne nå!
Vi går trinnvis frem og kobler sammen de forskjellige elementene. 

## 6.1 Nettsiden vår

Her trengs det ikke så mye magi for å få ting til å fungere. Det eneste vi trenger å endre hvor vi sender API-kallet vårt i index.html
Last så opp den nye versjonen i S3-bøtten vi laget i oppgave 1 og vi bør være good to go!

## 6.1 Lambdaen og API gatewayen vår
Nå skal vi dykke litt dypere ned i ting!
Hvis vi ser på lambda-koden vår så mottar vi et objekt som heter `event`. Denne inneholder ganske så mye morro nemlig.

### 6.2.1
Først av alt skal vi prøve å returnere en hytte i stedet for å printe den.
Legg på en `return` foran `await`-en i din hentHytteData-funksjon. Deretter plukker du ut det første elementet i hyttedata.Items og returnerer det.

🤫 Hvis du står litt fast så kan du ta en sniktitt på lambdaen `hent-og-returner-en-hytte-dev-hentHyttedata` i disse oppgavene 🤫.

Voila, vi har nå en lambda-funksjon som returnerer ting til hva enn som har kalt på den.

### 6.1.1
La oss titte litt mer på dette `event` objektet. 
- Legg inn `console.log(event);` før du returnerer noe i lambda-funskjonen din.
- Gjør en `serverless deploy --stage dev` for å dytte koden ut. 
- Prøv å trigge funksjonen din en gang med en test-event, som i oppgave 3. 
- Prøv å trigge en event ved å gå inn på lenken til API gatewayen din. 

Nå skal vi se litt på de loggene. Først finner du din funksjon her: https://eu-west-1.console.aws.amazon.com/cloudwatch/home?region=eu-west-1#logsV2:log-groups.
Når du har funnet den, trykk på den oransje knappen oppe til høyre hvor det står "Search log group". 
Huk av den lille sjekkboksen for "View as text" for å gjøre livet litt enklere.
Her ser vi litt morsomme ting!

### 6.1.2
Hvis vi nå legger på litt query parameters når vi sender en melding til apiet vårt, 
f.eks. legg på `?mat=digg` så ser vi at dette blir gjort tilgjengelig som `queryStringParameters: {
mat: "digg"}` i event-objektet!

Oppgaven: Hvis `event.queryStringParameters.sted` eksisterer, velg den riktige hytta og returner den. 

🤫 Igjen kan du ta en sniktitt på lambdaen `hent-og-returner-en-hytte-dev-hentHyttedata` her 🤫.

## 6.3
Gratulerer! Du har nå satt opp en vaskeekte tjeneste! Du har nå:
- En nettside til brukeren
- En api gateway som kan ta imot spørringer og sende de til forskjellige steder. 
- En "backend" i lambda som tar imot requester og behandler de

Vi erklærer deg herved en fullstackutvikler 🙌

