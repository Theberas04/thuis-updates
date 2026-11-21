# Thuis — updatekanaal

Hier staan alleen de **ondertekende APK's** van de app Thuis (pakket `nl.werdens.thuis`).
De app zelf wordt in een besloten repo ontwikkeld; dit repo bestaat zodat een toestel zonder
account kan zien welke versie er is.

## Hoe de app het gebruikt

Bij "Controleer op updates" in de app (en één keer per dag automatisch, als dat aanstaat) vraagt
de Android-schil:

```
GET https://api.github.com/repos/Theberas04/thuis-updates/releases/latest
```

Uit dat antwoord leest de app de tag (`v1.0.52`) en de eerste APK in de uitgave, vergelijkt de
tag met de versie op het toestel, en biedt "Bijwerken" aan. De APK wordt gedownload en aan de
installateur van het toestel gegeven — Android vraagt daarbij één keer om bevestiging.

Er gaan geen huishoudgegevens over de lijn: het verzoek is dezelfde vraag die een browser stelt
aan een openbare pagina, en de app werkt volledig zonder verbinding. Alleen bijwerken heeft
internet nodig.

## Een nieuwe versie publiceren

De APK moet met dezelfde sleutel ondertekend zijn als de vorige (`C=NL, O=Werdens, CN=Thuis`),
anders weigert Android de update. Daarna:

```
gh release create v1.0.53 --repo Theberas04/thuis-updates \
  --title "Thuis 1.0.53" --notes "Ondertekende APK van Thuis 1.0.53." \
  Thuis-1.0.53.apk
```

De workflow van de app doet dit automatisch wanneer het geheim `KANAAL_TOKEN` in de app-repo
staat (een token met schrijfrecht op dit repo).

## Wat hier niet staat

De broncode, de recepten en de winkelbestanden. Die staan in de app-repo en in de bundel voor de
winkels.
