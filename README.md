# aws-workshop

Velkommen til AWS workshop!
I denne workshopen skal vi kjenne litt på hvordan man bruker sky i praksis!
Sky er litt ullent og uangripelig til tider. Samtidig er det noe man ofte møter på prosjekt, 
da veldig mange bruker sky nå om dagen til å kjøre løsningene sine. 
Derfor tenkte vi at det kan være fint å prøve det littegrann, så vi ser hvordan det egentlig funker. 

## Hvordan gjøre denne workshopen. 
Start med å laste ned pre-reqs (se under) så maskinen er klargjort. 
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

Installer [serverless](https://www.serverless.com/framework/docs/getting-started/).

Installer aws-sdk: `npm install aws-sdk`
