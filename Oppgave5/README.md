# Oppgave 5

Da er det er på tide å sette opp API gateway! Hva er det sier du? Jo det er mellomlaget mellom logikken (lambda) og konsumenten av .....

## 5.1 Å Finne frem

Føst må vi finne frem til riktig sted i denne amason jungelen. Søk opp "API gateway" og velg tjenesten for å komme inn på riktig side.

![](gateway-service.png)

## 5.2 Skapelsen

Du vil nå se en liste med eksisterende API-gateways, men vi ignorer de for nå. Start med å trykke på den store oransje `Create API` knappen.

![](create-new.png)

Du kommer så videre til en side som ber deg API type. Siden vi skal lage en veldig enkel gateway, velger vi `HTTP API`.

![](gateway-type.png)

Så følger vi bare stegene slik de kommer.

![](configure-1.png)

Trykk på `Add Integration` og velg `Lambda`. 

![](configure-2.png)

Skriv deretter inn navnet du ga lambdaen din i tidligere oppgave. Pass også på at du har valgt riktig region. Versjon kan du la stå på standarinstillingen, `2.0`.

![](configure-3.png)

Velg ut et navn for gatewayen din og trykk `next`.

![](configure-4.png)

På `Configure routes` skjermen vil vi sette metoden til `GET` og definere en path som er litt lettere å huske, `/hytter` funker fint.

![](configure-5.png)

"Stages" her er litt som forskjellige miljøer. Her kunne man definert en gateway for prod, dev og test separat. Siden dette er en workshop, trenger vi ikke å gjøre noe fancy her. Trykk deg videre med `Next`-knappen.

![](stages.png)

Se over at ting ser riktig ut, hvis de ikke gjør det kan du gå tilbake og fikse ting nå. Er alt OK kan du trykke `Create`.

![](review.png)


## 5.3 Prøvelsen

## 5.x: test med CURL
`curl -x GET "<din URL>"`