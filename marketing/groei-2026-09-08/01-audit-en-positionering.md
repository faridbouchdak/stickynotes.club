# Audit en positionering — StickyNotes.club

Datum: 8 september 2026. Opdracht: publieke pagina’s, Help Centre en marketing verbeteren; €1.000 terugkerende maandelijkse omzet uiterlijk 8 januari 2027.

## Feiten, zekerheid en grenzen

**Door Farid bevestigd:** nul externe gebruikers; geen bereikcijfers, aanmeldingen of klantgesprekken beschikbaar; één uur per dag; marketingbudget nog niet vastgesteld; doel betreft terugkerende omzet. Host en Facilitator zijn volgens Farid nu afrekenbaar. Farid heeft de brede website, gerichte eerste verkoop aan workshopbegeleiders en ondergeschikte plaatsing van Chosen Few bevestigd.

**Geverifieerd in lokale applicatiecode:** gratis eigen privéboard; standaard boardlimieten 1/5/15; Club Host €4,99 en Club Facilitator €14,99 per maand exclusief btw; Chosen Few €999.999,99 eenmalig bovenop Host bij aanschaf. De runtime-instellingen en checkout zijn niet zelfstandig gecontroleerd; Farid bevestigt wel dat beide maandplannen afrekenbaar zijn. Bronnen: `app/Helpers/Plans.php`, `RoleHelper.php`, `Controllers/PricingController.php` in de applicatiemap.

**Live geverifieerd:** Help Centre-homepage, startgids en abonnementengids retourneerden HTTP 200 op 8 september. De live abonnementengids noemt 1/5/15 boards en maximaal 50 workshopdeelnemers. Bron: https://docs.stickynotes.club/plans-and-subscriptions/.

**Niet geverifieerd:** visuele weergave van productie op desktop en mobiel, checkout, daadwerkelijke aanmelding, mailbezorging, productie-instellingen en conversies. De hoofdwebsite en /pricing gaven mijn automatische leesverzoeken HTTP 403; dit bewijst niet dat gewone bezoekers worden geblokkeerd. Het browserhulpmiddel kon door een lokale omgevingsfout niet starten. De pagina-audit hieronder betreft daarom de lokale applicatietemplates en leesbare live helpteksten. Aanvullend is de gewijzigde helpwebsite door de marketingexpert lokaal gebouwd en in Chrome op desktop en mobiel gecontroleerd; zie 06.

**Aannames:** geen veronderstelde bezoekersaantallen, conversiepercentages, klantbehoefte of beschikbare advertentie-uitgaven. Rekenscenario’s in het groeiplan zijn expliciet hypothetisch.

## Wat nu aandacht verdient

| Prioriteit | Waarneming | Mogelijk gevolg, nog niet gemeten | Aanbevolen ingreep |
| --- | --- | --- | --- |
| P0 | Pricingkaart: “Post up to 2 sticky notes per day”; code beperkt alleen Public-publicaties | Persoonlijk gebruik lijkt beperkt tot twee notities | “Publish up to 2 notes per day on the worldwide wall”; daarnaast “Private-board notes do not use this allowance” |
| P0 | Homepage opent met “Run a focused workshop in minutes” en workshop-CTA | Bezoeker die alleen ideeën wil ordenen herkent zichzelf niet | Brede, concrete productbelofte; gratis privéboard direct zichtbaar; workshoproute behouden |
| P0 | Geen nulmeting beschikbaar | Niet te onderscheiden: geen verkeer, onduidelijke boodschap, aanmeldprobleem of ontbrekende betaalbehoefte | Live instap en betaling doorlopen; bestaande tellingen opvragen; eerste vijf begripstests |
| P1 | Vier prijskaarten; Chosen Few is bovendien geen maandabonnement | Cognitieve last en mogelijke twijfel aan ernst | Drie maandplannen als hoofdvergelijking; Chosen Few als ondergeschikte, duidelijk beschreven verwijzing |
| P1 | Host-kaart opent met meer publieke publicaties en kleuren | De echte koopreden — eigen boards delen — raakt ondergesneeuwd | Eigen boards, uitnodigen en toegangslinks bovenaan |
| P1 | Help-home en navigatie zijn vooral workshopgericht | Gratis persoonlijke gebruiker vindt weinig directe begeleiding | Persoonlijke startkaart, concreet weekplannerrecept en zichtbaarheidsgids |
| P1 | Oud marketingplan activeert negen kanalen | Eén uur per dag gaat op aan productie en distributie | Eén primair kanaal, gesprekken en één wekelijkse groepsdemo |
| P1 | Event-tabel telt gebeurtenissen, geen identieke personen door de funnel | Verhouding tussen events kan ten onrechte “conversie” heten | Tellingen als tellingen tonen; echte verkoopcohorten voorlopig handmatig bijhouden |

Dit zijn aantoonbare communicatieproblemen en werkhypothesen over hun effect. Nul gebruikers bewijst geen specifieke oorzaak en bevestigt ook geen product-market fit.

## Aanbevolen positionering

Productbelofte: **Online sticky notes for your ideas, plans and shared work.**

Uitleg: **Start with a private board of your own. Invite others when you want to work together, or guide a workshop with a link or QR code. Publishing on the worldwide wall is optional.**

De bestaande merklijn “A place where ideas can grow together” kan in de footer of het merkverhaal blijven. De eerste schermtekst moet zonder interpretatie uitleggen wat iemand ermee kan doen.

Breed bruikbaar zijn betekent niet dat we nu “geschikt voor iedereen” kunnen bewijzen. Voorbeelden als weekplanning, ideeën verzamelen en samen prioriteren maken de breedte concreet. Offline gebruik, native desktopbriefjes, algemene tekstzoekfunctie en export van gewone boards mogen niet worden gesuggereerd.

**Door Farid gekozen:** brede website, eerste gerichte verkoop aan workshopbegeleiders.

**Aanbeveling voor acquisitie:** begin bij zelfstandige trainers, coaches en facilitators die de komende 30 dagen een echte sessie hebben én dit vaker doen. Zij kunnen zelf besluiten en hebben een concreet evaluatiemoment. Dit is een te toetsen segmentkeuze, geen bewezen ideale doelgroep. Vraag daarnaast drie mensen die dagelijks sticky notes gebruiken om de persoonlijke route te proberen; die route hoeft de betaalde acquisitie niet te domineren.

**Tweede-orde-effect:** een bredere homepage kan meer gratis gebruikers aantrekken en het aandeel directe workshopaankopen verlagen. Beoordeel daarom persoonlijk gebruik en betaald workshopgebruik apart. **Derde-orde-effect:** extra gratis gebruik kan support vragen zonder omzet; geef zelfhulp voorrang en houd begeleiding begrensd.

## Drie gebruikssituaties, twee inhoudscontexten

1. **Eigen privéboard:** persoonlijk werken; gratis instap.
2. **Privéboard met anderen:** samenwerking via uitnodiging of toegangslink; eigenaar heeft passende betaalde rechten.
3. **Workshop op een privéboard:** de eigenaar begeleidt een sessie; gasten kunnen zonder account deelnemen.

De **publieke wall** is een afzonderlijke, optionele publicatiefunctie met losse Public-notities. Er bestaan geen publieke boards en geen ingebouwde verplaatsing van een wall-notitie naar een privéboard. Een workshop is geen derde boardtype.

Privé betekent toegangscontrole. Een actieve link kan worden doorgestuurd; bevoegde medewerkers kunnen zo nodig toegang hebben. Vermijd “alleen jij kunt dit ooit zien”, “volledig anoniem” en “alle informatie blijft voor altijd privé”. Houd de materiële publicatievoorwaarden zichtbaar bij publiceren; de juridische formulering zelf valt buiten deze marketingbewerking.

## Pakketten eenvoudig uitleggen

| Plan | Eerste reden om te kiezen | Niet als hoofdargument gebruiken |
| --- | --- | --- |
| Club Member — Free | Een eigen privéboard en gratis deelnemen aan uitnodigingen | Twee publieke publicaties |
| Club Host — Shared boards | Meer eigen boards en anderen uitnodigen | Zes keer meer publieke publicaties, pastelkleuren |
| Club Facilitator — Workshops | Een groep begeleiden en resultaat meenemen | Algemene “aanbevolen” badge voor iedere bezoeker |

Behoud de bestaande namen voorlopig en voeg functionele ondertitels toe. Dat geeft duidelijkheid zonder betalingen, rollen en bestaande helpverwijzingen onnodig te veranderen. Facilitator mag “For guided workshops” dragen; “Most popular” is zonder betalende gebruikers onjuist.

**Chosen Few:** advies is uit de hoofdkaarten en hoofdvergelijking halen. Een compacte verwijzing onder de vergelijking houdt het speelse verhaal toegankelijk. Bestaande rechten, betalingsregels en ondersteuning blijven bestaan. Verwijdering van rechten of technisch stopzetten van verkoop is niet opgedragen. Het afschrikeffect is onbewezen; test wat mensen denken dat het betekent.

## Concurrentie: wat wel en niet verdedigbaar is

Miro documenteert bezoekers zonder account en zonder betaalde seat; Mural documenteert eveneens gratis bezoekers en op Team+ bewerkrechten voor bezoekers. “Bij anderen betaalt elke deelnemer” is dus geen houdbare claim. Bronnen gecontroleerd 8 september 2026: [Miro pricing](https://miro.com/pricing/) en [Mural pricing](https://www.mural.co/pricing).

Verdedigbaar voorstel: een overzichtelijke toepassing rondom sticky notes en begeleide sessies, met een zichtbaar resultaat. Nog te bewijzen: dat de bedoelde gebruiker daarmee sneller start of prettiger werkt. Test dezelfde kleine opdracht en laat mensen zelf beschrijven waar ze vastlopen. Start geen brede featurewedloop en claim geen algemeen prijsvoordeel zonder dezelfde rechten, facturatieperiode en valuta te vergelijken.

## Open vragen

- Segmentkeuze is bevestigd: brede website, gerichte eerste verkoop aan workshopbegeleiders.
- Zelfstandige verificatie van de complete nieuwe klantreis resteert; afrekenbaarheid is door Farid bevestigd.
- Chosen Few wordt met Farids instemming ondergeschikt geplaatst; zie het concrete component in 02.
- Wie in Farids netwerk kan een echte sessie binnen 30 dagen plannen? Dit netwerk is nog niet geïnventariseerd.
- Welk eventueel marketingbudget komt later beschikbaar? Tot die beslissing schrijft dit plan geen betaalde campagne voor.

## Onderzoeksbronnen

Applicatiemap `stickynotes-club`: `app/resources/views/home.html`, `pricing.html`, `wall.html`, `layout.html`, `auth/register.html`, `boards/index.html`; `app/resources/pages/about.md`; `app/Helpers/Plans.php`, `RoleHelper.php`; `app/Controllers/AuthController.php`, `HomeController.php`, `PricingController.php`, `BaseController.php`; `app/Models/Event.php`.

Marketingmap `stickynotes.club`: `README.md`; `marketing/01_MARKETINGPLAN.md`, `00_README.md`, `Nieuwe positionering StickyNotes.club.md`; relevante helpgidsen; `design/01_Product_Model.md`; PDF `marketing/conversatie_workshop_facilitatie_natraject.pdf` (zes pagina’s, tekst gelezen als historisch advies, niet als nieuwe opdracht of geverifieerd bewijs voor externe claims).

De oude stukken bevatten ontwerpbesluiten en eerdere aanbevelingen. Die zijn context; dit nieuwe verzoek geeft de opdracht. Juridische documenten zijn niet gewijzigd.
