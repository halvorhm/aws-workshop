# Oppgave 2

## Vi kobler på et kult domene!

For at nettsiden vår skal være tilgjengelig på noe annet enn `xyzblabla-s3.aws.something.com` så lager vi oss en såkalt DNS record. Mer presist skal vi lage en alias-record for å peke mot nettsiden vår!

Til dette bruker vi [route 53](https://aws.amazon.com/route53/). Route53 er AWS sin DNS (Domain Name System) tjeneste. Her kan man bestille og håndtere domener og haugevis mer. Her skal vi sette opp en såkalt alias record. Alias er en egen greie i route 53 og bruker mye i AWS til å peke mot forskjellige interne AWS-tjenester. For å gjøre dette velger vi `A record` i menyen etterpå (som vanligvis brukes når man ønsker å peke en nettside som vg.no mot en ip-addresse), og så fikses resten under panseret.

En liten ting å merke seg når man jobber med DNS er at på grunn av måten DNS fungerer på kan oppdateringer noen ganger ta litt tid og det skjer normalt ikke på sekunder. 
Derfor er det fint å hente seg en kaffe hvis man gjør en DNS endring og det ikke funker med en eneste gang ☕.


## 2.1

Først, søk etter route53 i søkefeltet i toppen av aws-consolet, eller gå inn her: https://console.aws.amazon.com/route53/v2/home#Dashboard.

Det bør se noe slikt ut.
![](route53-dashboard.png)

## 2.2
Deretter navigerer vi oss inn i domenet vårt. Gå til `Hosted zones` og velg `bekk.cloud`. Her inne skal vi lage DNS-recorden vår.

## 2.3
Velg `Create Record`. Du kan enten fylle den ut etter eksempelet under, eller bruke `switch to wizard` og følge oppskriften under typen `simple routing`. Husk å sette TTL til 60 sekunder, så slipper man å vente så lenge seinere hvis man gjør endringer.

![](create-a-record.png)

## 2.4

Ferdig! Det burde ha gjort susen! Prøv å åpne domenet i nettleseren din, så ser du om det fungerer!