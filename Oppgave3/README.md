# Oppgave 3

## Lambda

Intro


## 3.1

### Oppgave 1
- Kjør kommandoen `serverless` i repoet. Dette burde initiere et nytt serverless prosjekt. 
  Når den spør om type repo, velg `starter` og Node.
  Bruk ditt eget navn i navn på prosjektet.   
  Spør den om du vil lage en serverless konto kan du svare `nei`. 
  Spør den om du vil deploye prosjektet ditt svarer du `nei`. 
- I `serverless.yml` legg inn `region: eu-west-1` under `provider`.
- Endre `handler.js` til å ha en personlig melding.
- Deploy ved hjelp av kommandoen `serverless deploy --stage dev`.

🙌 Bra jobba! 🙌

## 3.2
Nå skal vi ta å sjekke ut UIen og se hvordan koden kjører!
- Logg inn på https://console.aws.amazon.com/
- I menyen i toppen søk etter og velg "lambda". Under "Functions" finn din funksjon!
- Trykk på den oransje "TEST"-knappen. Får du opp et vindu som spør om _configure test event_ så bare skriv et navn, f.eks. "test" og trykk save.
- BAM! Du har nå kjørt funksjonen din! Woop!


## 3.3
Her skal vi lese noe fra dynamodb og returnere det.

## 3.4