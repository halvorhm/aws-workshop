# aws-workshop

Velkommen til AWS workshop!
I denne workshopen skal vi kjenne litt på hvordan man bruker sky i praksis!
Sky er litt ullent og uangripelig til tider. Samtidig er det noe man ofte møter på prosjekt, 
da veldig mange bruker sky nå om dagen til å kjøre løsningene sine. 
Derfor tenkte vi at det kan være fint å prøve det littegrann, så vi ser hvordan det egentlig funker. 

## Hvordan gjøre denne workshopen. 
Start med å laste ned pre-reqs så maskinen er klargjort. 
Deretter går dere en for en oppgave. Dere kan starte på neste så snart dere vil. 

NB! Les oppgavene nøye.

Målet er ikke å komme gjennom alle oppgavene, men bare å prøve ting i skyen, så ikke stress.

## Prereqs
Installer aws cli (MacOS: brew install awscli). Kjør kommandoen aws configure. Legg inn verdiene:

Access Key (fra epost)
Secret (fra epost)
Default region name: eu-west-1
Default output format: json
Hvis du ønsker å gjøre endringer på dette seinere så finner du filen under ~/.aws/credentials.

Installer serverless.




## TODO workshop
Jeg bare plotter ned litt småting. Dette er bare et forslag til struktur, bare å endre som dere vil. 

Jeg tenker vi prepper en ferdig DynamoDB table? Eller skal det også være en del av oppgavene? Jeg mistenker det kanskje blir litt mye jobb med den tiden vi har.

- [ ] Script for å lage brukere
- [ ] Oppgave 0: Sett opp miljø på maskinen din
- [ ] Oppgave 1: Lag en s3-bøtte og en nettside
- [ ] Oppgave 2: Vi slenger på en DNS record på bøtta så nettsiden vår har fancy nettside.
- [x] Oppgave 3: Lambda! Først en enkel hello-world som trigger.
- [x] Oppgave 4: Next up: Les fra databasen. enkel boto3 query.
- [ ] Oppgave 5: API gateway in da house. Først endepunkt som sender alt til lambdaen. Så bare printer vi input og returner statisk element
- [ ] Oppgave 6: Plukk ut det som kommer fra requesten. Print og returner tilbake.
- [ ] Oppgave 7: Bruk parameter fra request til å søke i DBen. 
- [ ] Oppgave 8: Ferdig?

