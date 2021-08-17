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

Installer [serverless](https://www.serverless.com/framework/docs/getting-started/). Dette skal vi bruke med lambda.

Installer aws-sdk: `npm install aws-sdk`

### Logg inn i AWS
Vi starter med å aller først åpne opp AWS consolen, altså nettsiden til aws. Logg inn på https://console.aws.amazon.com/. 
Brukernavnet er privatmailen din vi fikk i bekk før du startet. Passordet står på tavlen.

Velg `IAM User` og skriv inn account ID: `bekk-skyskolen`.

I samme slengen setter vi også opp så du kan bruke kommandolinjen.
Dette gjør vi ved å legge inn en aws Access Key og Access Secret på maskinen din. 
- Gå [hit](https://console.aws.amazon.com/iam/home?region=eu-west-1#/security_credentials): og trykk på "Create New Access Key".
- skriv kommandoen `aws configure`. Legg inn Access Key og Access secret her når den spør.
- Velg `default region name`: `eu-west-1`.
- Velg `default format`: `json`.

Sånn! Da skal du ha aws oppe og kjøre. Du kan teste det ved f.eks. å skrive `aws s3 ls` og se om den lister opp flere ting eller om den gir en feilmelding.
