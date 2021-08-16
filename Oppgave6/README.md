# Oppgave 6

## Når alt kobles sammen

Vi har vært innom mye ting nå, men det henger liksom ikke skikkelig sammen. Det skal vi ordne nå!
Vi går trinnvis frem og kobler sammen de forskjellige elementene.

## 6.1
Nå skal vi dykke litt dypere ned i ting!
Hvis vi ser på lambda-koden vår så mottar vi et objekt som heter `event`. Denne inneholder ganske så mye morro nemlig.

### 6.2
Først av alt skal vi prøve å returnere en hytte i stedet for å printe den.
Legg på en `return` foran `await`-en i din hentHytteData-funksjon. Deretter plukker du ut det første elementet i hyttedata.Items og returnerer det.

🤫 Hvis du står litt fast så kan du ta en sniktitt på lambdaen `hent-og-returner-en-hytte-dev-hentHyttedata` i disse oppgavene 🤫.

Voila, vi har nå en lambda-funksjon som returnerer ting til hva enn som har kalt på den.

### 6.3
La oss titte litt mer på dette `event` objektet. 
- Legg inn `console.log(event);` før du returnerer noe i lambda-funskjonen din.
- Gjør en `serverless deploy --stage dev` for å dytte koden ut. 
- Prøv å trigge funksjonen din en gang med en test-event, som i oppgave 3. 
- Prøv å trigge en event ved å gå inn på lenken til API gatewayen din. 

Nå skal vi se litt på de loggene. Først finner du din funksjon her: https://eu-west-1.console.aws.amazon.com/cloudwatch/home?region=eu-west-1#logsV2:log-groups.
Når du har funnet den, trykk på den oransje knappen oppe til høyre hvor det står "Search log group". 
Huk av den lille sjekkboksen for "View as text" for å gjøre livet litt enklere.
Her ser vi litt morsomme ting!

### 6.4
Hvis vi nå legger på litt query parameters når vi sender en melding til apiet vårt, 
f.eks. legg på `?mat=digg` så ser vi at dette blir gjort tilgjengelig som `queryStringParameters: {
mat: "digg"}` i event-objektet!

Oppgaven: Hvis `event.queryStringParameters.location` eksisterer, velg den riktige hytta og returner den. 

Vi skal også gjøre en liten ting for å unngå 

🤫 Igjen kan du ta en sniktitt på lambdaen `hent-og-returner-en-hytte-dev-hentHyttedata` her 🤫.

## 6.5
Helt til sist vil vi jo sende requesten fra nettsiden vår! Ta Api-gateway URLen din fra tidligere. Lim inn denne i `API_FUNCTION_URL` i index.html filen din (med `hytte` bak). 
Deretter laster du opp den nye index.html siden din i s3 bøtta. Da bør du være good to go!

## 6.6
Gratulerer! Du har nå satt opp en vaskeekte tjeneste! Du har nå:
- En nettside til brukeren
- En api gateway som kan ta imot spørringer og sende de til forskjellige steder. 
- En "backend" i lambda som tar imot requester og behandler de

Vi erklærer deg herved en fullstackutvikler 🙌

