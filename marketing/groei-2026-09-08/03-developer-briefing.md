# Developerbriefing — eerste groeirelease

8 september 2026. Eigenaar productbesluiten: Farid. Marketingrichting bevestigd: brede website, eerste gerichte verkoop aan workshopbegeleiders. Doel: begrijpelijke instap en een werkende route naar eerste en herhaalde betaalde sessies.

**Status:** opdrachten en acceptatiecriteria; de applicatiemap is door de marketingaudit niet gewijzigd. Copy: `02-publieke-paginas-copy.md`. Helpcentrumwijzigingen staan al lokaal in de aparte marketingrepository. Er is niets gepubliceerd. Schat zelf de ontwikkeltijd; onderstaande volgorde is prioriteit, geen technische tijdsgarantie.

## Eerste release: doe alleen D01–D06

### D01 — Leg vast of een klant vandaag kan starten en betalen (P0)

**Aanleiding:** Farid bevestigt dat Host en Facilitator nu afrekenbaar zijn. De audit heeft de volledige klantreis niet zelf doorlopen; automatische requests naar / en /pricing gaven 403.

**Opdracht:** doorloop de site als uitgelogde normale bezoeker, op mobiel en desktop. Controleer /, /pricing, /register, /login en /wall. Controle van de helpwebsite ligt bij de marketingexpert. Stel vast of een eventuele blokkade gewone gebruikers treft; verander botbescherming alleen op basis van dit bewijs. Controleer registratie-instelling, eventuele daglimiet, verificatiemail en actieve Host/Facilitator-productconfiguratie zonder geheimen te delen.

**Acceptatie:** rapporteer datum, apparaat/browser, uitkomst en één screenshot per kritieke stap. Gratis account kan inloggen en een board gebruiken. Gekozen premium/pro-plan blijft behouden na registratie, login en e-mailverificatie, ook bij openen van de verificatielink in een andere browser. Controleer checkout, terugkeer, succesvolle betaling, fout/annulering en planactivatie in de bestaande testomgeving. Laat Farid een eventuele echte betaling zelf uitvoeren; rapporteer afzonderlijk wat testmodus versus productie bewijst.

**Bronnen:** AuthController, CreemService, PricingController, BaseController, bestaande betaal- en registratietemplates. Geen nieuwe proefperiode of kortingsrecht als onderdeel van deze taak.

### D02 — Maak de publicatielimiet ondubbelzinnig (P0)

**Bestanden:** `app/resources/views/pricing.html`, relevante upgrademeldingen, `app/Controllers/PricingController.php`, app-`llms.txt` en metadata waar nodig.

**Opdracht:** vervang “Post up to 2/12 sticky notes per day” door “Publish up to [limiet] notes per day on the worldwide wall”. Voeg aan alle relevante kaarten toe dat privéboardnotities deze limiet niet gebruiken. Zet eigen boards en samenwerking vóór publieke publicaties en kleuren.

**Acceptatie:** zowel prijskaart als vergelijkingstabel maken duidelijk dat een gratis gebruiker meer dan twee notities op het eigen board kan maken. Getallen komen uit RoleHelper, BoardService en configuratie; geen nieuwe hardcoded limieten. Vergelijk opnieuw met de helpgids. Workshopdeelnemerslimiet komt uit de werkelijke instelling, niet uit deze briefing.

### D03 — Brede homepage, concrete workshoproute (P1)

**Bestanden:** `app/resources/views/home.html`, `layout.html`, `app/Controllers/HomeController.php`, `BaseController.php`; schema-/Open Graph- en llms-presentatie waar geraakt.

**Opdracht:** gebruik de secties en copy uit document 02. Gratis privéboard in de hero; drie toepassingskaarten; aparte workshopsectie; wall als optionele openbare publicatie. Primaire algemene CTA /register, workshop-CTA met bestaande pro-afhandeling. Bestaand /#how-it-works behouden; /#workshops toevoegen. Workshopcampagnes kunnen naar dezelfde homepage met dit anker: geen nieuwe landingspagina nodig voor release 1.

**Acceptatie:** op 375px en desktop zijn belofte, gratis instap en workshoproute leesbaar; geen horizontale pagina-overloop. CTA’s hebben concrete labels en werken met toetsenbord. Gebruik bestaande stijlen en echte voorbeeldscreenshots met alt-tekst. Behoud accountnavigatie voor ingelogde gebruikers en controleer ook 404/403-layout: de bestaande layoutdefaults mogen niet breken. Metadata en deelvoorbeeld passen bij de brede pagina. Geen onbewezen tijdwinst of populariteitsclaims.

### D04 — Drie maandplannen en Chosen Few als apart verhaal (P1)

**Bestanden:** `pricing.html`, PricingController; alleen presentatie van bestaande bedragen en rechten.

**Opdracht:** Free/Your own sticky notes, Shared boards en Workshops als ondertitels onder bestaande namen. Host: boards en uitnodigen centraal. Facilitator: sessieregie en resultaten centraal. Geen algemene “Most popular”. Farid heeft ingestemd: verplaats Chosen Few naar het ondergeschikte uitklapblok uit document 02. Verwijder het uit de drie hoofdkaarten en hun vergelijkingstabel; bestaande rechten blijven behouden.

**Acceptatie:** drie maandplannen zijn zonder eenmalige upgrade te begrijpen. De aparte Chosen Few-vermelding noemt de echte eenmalige prijs, Host-voorwaarde en de bestaande rechten na opzegging. Rollen, flags, Creem-producten en bestaande klantrechten veranderen niet. Controleer /checkout/premium, /checkout/pro en /checkout/chosen_few plus bijbehorende /register?plan= parameters. Een niet-afrekenbaar plan krijgt geen actieve koopbelofte. Controleer prijs/btw/verlenging tegen werkelijke checkout; geen nieuwe facturatietekst op basis van aannames.

**Nevenbevinding:** `boards/index.html` verwijst bij een betaalde boardlimiet naar Chosen Few of verwijderen. Laat een Host de bestaande Facilitator-optie zien wanneer die meer boardruimte biedt. Bij Facilitator: leg de huidige limiet uit en bied contact; presenteer een miljoenenaankoop niet als standaard oplossing. Geen nieuw archief of rechtensysteem bouwen. Geen suggestie om inhoud te wissen zonder bestaande gevolgenmelding.

### D05 — Houd de belofte vast bij aanmelden en het eerste board (P1)

**Bestanden:** `auth/register.html`, `boards/index.html`; AuthController uitsluitend waar aantoonbaar nodig.

**Opdracht:** gebruik de gratis en betaalde copy uit 02. Maak het lege boardoverzicht uitnodigend met Week planner/Blank/Kanban als bestaande startpunten. De gratis route moet persoonlijk gebruik uitleggen; de betaalde route moet betaling en e-mailbevestiging correct aankondigen.

**Acceptatie:** geen verplichte publieke notitie, profielverrijking of extra onboardingvragen. Geen tekst die gratis workshops belooft. Controleer een nieuwe gewone gebruiker, nieuwe pro-gebruiker, bestaande gebruiker en verlopen/bestaande sessie. Gebruik geen adminaccount als bewijs dat gratis of betaalde klantrechten werken. Start geen nieuwe automatische-loginontwikkeling tenzij de waargenomen aanmeldfrictie dit later rechtvaardigt.

### D06 — Verbind applicatiepagina’s met de helpgidsen (P1)

**Scope developer:** uitsluitend de verwijzingen vanuit de applicatie. De bestaande helpwebsite in `stickynotes.club/docs` is volledig in beheer bij de marketingexpert: inhoud, navigatie, bouwcontrole, zoekindex, visuele controle en afstemming van publicatie.

**Opdracht:** gebruik vanuit de app de volgende help-URL’s zodra de marketingexpert bevestigt dat ze gepubliceerd zijn:

- https://docs.stickynotes.club/use-sticky-notes-for-yourself/
- https://docs.stickynotes.club/public-wall-private-board-workshop/
- https://docs.stickynotes.club/plans-and-subscriptions/#chosen-few-a-separate-one-time-upgrade

Geef nieuwe helpgidsen zo nodig een sleutel in de bestaande applicatiehelper DocsHelper. Bestaande help-URL’s blijven behouden. Bouw of wijzig geen helpwebsite als onderdeel van deze opdracht.

**Acceptatie:** de links vanuit de applicatie gaan naar de juiste gepubliceerde gids en het bedoelde anker. Bij een productwijziging die de uitleg raakt: meld concreet de gewijzigde functie, knop, limiet of toegangsregel aan de marketingexpert, zodat die de helptekst zelf bijwerkt.

**Informatievragen:** momenteel is geen aanvullende informatie van de developer nodig voor de klaargezette helpteksten. Mocht productiegedrag afwijken van de onderzochte bron of bestaande live gidsen, dan volgt één concrete vraag over die afwijking; geen algemene overdracht van helpwerk.

## Daarna: D07 alleen zo klein als nodig

### D07 — Maak tellingen en omzet bruikbaar voor besluiten (P1/P2)

**Wat al bestaat:** Event.php bevat homepage/pricing, registratie, account, checkout, planactivatie en workshop-events, plus gast-instap en workshopresultaatstatistieken. `campaigns()` telt UTM’s op homepagebezoeken. Dit niet opnieuw bouwen.

**Probleem:** eventverhoudingen zijn geen cohortconversies. Iemand kan pricing overslaan, herladen of meerdere workshops doen. Campagnebron reist niet mee naar een individuele aankoop. “Geen persoonsgegevens” uit oude adviezen is geen juridische conclusie van deze audit; een board_id kan via andere data verband houden met een persoon.

**Essentieel:** dashboard benoemt “gebeurtenissen” en “paginabezoeken”; toon onbekend/niet beschikbaar waar data ontbreekt. Leg nulmeting vast. Controleer dat herhaalde betaalwebhooks geen meerdere nieuwe-klantmeldingen veroorzaken. Actieve abonnementen en MRR baseren op actuele betaalstatus en werkelijk terugkerend tarief, niet het aantal plan_activated-events. Sluit Farid/testaccounts, gratis accounts, gasten, btw en eenmalige Chosen Few-bedragen uit.

**Voorlopig voldoende:** Farid houdt de eerste prospects, betaalde klanten en herhaalafspraken handmatig bij. Weekrapport: actieve Host/Facilitator-klanten, nieuwe en verloren MRR, voltooide echte sessies, tweede sessie gepland/gehouden. Handmatige bronvraag geeft indicatie, geen volledige attributie.

**Pas later:** extra persoonlijke activeringsmeting of bronkoppeling als de concrete beslissing zonder die data niet kan. Definieer doel, minimale velden en bewaartermijn vóór implementatie. Geen trackers, extra cookies, database-toegang of marketingmails aanzetten als impliciet onderdeel van de copywijziging.

## Afbakening en oplevering

Geen wijziging van prijzen, abonnementenrechten, database-rollen, eigendomsvoorwaarden, verificatievereisten, gratis proefperiodes of limieten. Geen nieuwe templates, native apps, integraties of advertentieplatforms nodig voor de eerste release.

Lever één reviewbare wijzigingsset met: pagina-screenshots mobiel/desktop, gecontroleerde links, samenvatting van D01, gecontroleerde app-naar-helpverwijzingen, gebruikte bedragen/limieten en resterende onzekerheden. Bestaande tests alleen gericht uitvoeren waar gedrag verandert; voor copy en layout volstaan relevante render- en routechecks. Volg het gebruikelijke releaseproces van Farid; deze briefing is geen bewering dat iets al is gebouwd of gepubliceerd.
