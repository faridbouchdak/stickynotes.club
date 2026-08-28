# Audit en actieplan — marketing, content en UX-flow

> Status: v1, concept voor besluitvorming
> Datum: 21 augustus 2026
> Scope: publieke pagina's, in-app microcopy, UX-flow, prijs- en checkoutflow, vindbaarheid en vertrouwen
> Toetssteen: `00_Product_Constitution` (v1.5, incl. D-30), `02_Product_Playbook`, `06_Public_Communication_Specification`, `07_frontpage-voorstel`
> Taal: analyse in het Nederlands, alle voorgestelde interfaceteksten in Brits Engels

---

## 0. Hoe je dit document leest

Elke bevinding heeft een code (`A1`, `B7`, …). Het actieplan in **§7** verwijst alleen naar die codes, zodat je de bevinding en het werk apart kunt lezen.

Ik scheid vier soorten uitspraken, en markeer ze overal expliciet:

| Markering | Betekenis |
|---|---|
| **FEIT** | Nagelopen in de code of op de live site. Bestandsnaam en regelnummer staan erbij. |
| **AANNAME** | Redenering die ik niet heb kunnen meten (bijvoorbeeld over gedrag van bezoekers). |
| **ADVIES** | Mijn voorstel. Vervangbaar. |
| **BESLUIT NODIG** | Een keuze die van jou is, niet van mij. Verzameld in §8. |

**Wat ik heb bekeken.** De live pagina's `/`, `/wall`, `/pricing`, `/privacy/`, `/robots.txt`, `/sitemap.xml`, en in de repository de templates en controllers van de publieke pagina's, de authenticatieflow, de bordpagina, de facilitatorbalk, de wachtkamer, de gedeelde deelnemersweergave, de resultatenpagina, de checkoutbevestiging en de foutteksten in `boardApi.js`.

**Wat ik niet heb bekeken.** De ingelogde app in een echte browser (dus geen oordeel over gerenderde visuele hiërarchie of werkelijke mobiele weergave — waar ik daarover iets zeg, staat er **AANNAME**), de negen transactionele e-mailtemplates, de adminsectie, het Help Centre zelf, en laadtijden/Core Web Vitals gemeten met echte data.

---

## 0b. Stand van zaken — bijgewerkt 24 augustus 2026

Alle drie de sprints zijn gebouwd, gecontroleerd en gedeployd. Van de 45 bevindingen zijn er 44 afgehandeld en één geschrapt op bewijs (B5, zie het verificatielogboek in §11).

| Sprint | Status | Op productie |
|---|---|---|
| Sprint 0 — 12 items | Afgerond | 22 augustus |
| Sprint 1 — 12 items, waarvan 11 gebouwd en 1 geschrapt | Afgerond | 22 augustus |
| Sprint 2 — 12 items | Afgerond | 23 augustus |
| D-24 fase 1 — plak A en B | Afgerond, handmatig geverifieerd | 24 augustus |
| L1 t/m L3 | Afgerond | 24 augustus |
| L4 t/m L6 | Open, wacht op de eerste meetweek | — |

**De handmatige controlelijst is afgerond op 24 augustus** — zie het einde van deze paragraaf. Besluit 1 en 2 uit §10 zijn diezelfde dag genomen; van de zeven besluiten staat alleen nummer 4 nog open, en dat wacht op de juristenronde. **De eerstvolgende bouwklussen zijn daarmee de twee ingrepen die uit besluit 1 en 2 volgen**, met de juristenronde uit §9 van `spec-D-24-rapportage-en-moderatie.md` parallel daaraan.

| Werk | Uit | Stand |
|---|---|---|
| Eén gratis-instapregel onder het prijsblok op `/` | Besluit 1 | **Gebouwd 24-08** |
| Login open voor ongeverifieerd, banner, plus drie gates | Besluit 2 | **Gebouwd 24-08** |
| `check-render.php` uitbreiden naar de layout en de auth-schermen | Zie hieronder | **Gebouwd 24-08** |
| Nieuwe homepagescreenshots met de actuele knoplabels | Los signaal | Open, 30 m |
| URL-inspectie op `/sitemap.xml` in Search Console | Verificatielogboek | **Gedaan 24-08** — oorzaak was een gecachete 404, zie §11 |
| Sitemaprapportage nog eens bekijken (verwerking duurt uren tot een dag) | Idem | Open, morgen |
| Juristenronde §9 van de D-24-spec — deblokkeert besluit 4 | D-24 | Extern |

Alles hierboven dat als gebouwd staat, is op 24 augustus gecommit en gepusht — drie commits: besluit 1, besluit 2 (met de `$db`-reparatie erin) en de uitbreiding van de smoke.

### Besluiten uit §10: waar staan ze

| # | Onderwerp | Stand |
|---|---|---|
| 1 | Risicoloze ingang naar workshops | **Genomen op 24 augustus: zichtbaar maken wat al waar is.** Geen proef en geen gratis workshop; wel één regel op `/` die zegt dat je gratis kunt beginnen. Zie hieronder. |
| 2 | `/boards` in vóór e-mailverificatie | **Genomen op 24 augustus: ja, met banner — behalve voor de twee naar buiten gerichte handelingen.** Zie hieronder. |
| 3 | Club Facilitator als visueel hoofdplan | **Genomen.** Bevestigd op 23 augustus; badge *Recommended*, uitgelichte kolom in de vergelijkingstabel. |
| 4 | Opzeg- en terugbetalingsregel bij de knop | **Open, wacht op de juridische ronde.** Bij de betaalknoppen staat nu alleen wat verifieerbaar is: betaalritme en btw. |
| 5 | Uitnodiging aan deelnemers na afloop | **Genomen, terughoudende variant.** Alleen ná `workshopFinished`, alleen uitgelogd, één blok; tijdens de sessie blijft er één grijze regel. Geen facilitator-schakelaar gebouwd. Uitzetten is één `<check>`-blok verwijderen in `shared.html`. |
| 6 | De twaalf willekeurige walltitels | **Genomen.** Vervangen door één vaste kop met de speelse variant als ondertitel. |
| 7 | Indexeren vóór de Report-knop bestaat | **Genomen op 23 augustus: laten staan.** Zie hieronder — dit besluit verhoogt de prioriteit van D-24. |

### Besluit 1 — de risicoloze ingang wordt zichtbaarheid, geen nieuw product

> **Genomen op 24 augustus 2026.** Er komt geen proefperiode en geen gratis eerste workshop. Wat er komt is één regel op de homepage die zegt wat al waar is: je kunt gratis beginnen als Club Member.

**Waarom dit en niet meer.** A1 constateert dat `/` precies één prijs toont en dat het woord *free* er alleen voorkomt in het FAQ-antwoord over deelnemers. Dat is een zichtbaarheidsprobleem, geen productprobleem: `/pricing` heeft de Club Member-kaart al staan, en `RoleHelper::privateBoardLimit()` geeft de gratis laag standaard één eigen bord. De goedkoopste ingreep is dus de kaart die je al hebt, ook noemen op de pagina waar de bezoeker begint.

**Wat de duurdere variant werkelijk had gekost.** Een gratis eerste workshop raakt laag 1 op twee plaatsen, niet één: `BoardService::canFacilitateWorkshops()` kijkt naar de huidige bezoeker, en `ownerCanFacilitate()` doet daarnaast een eigen `SELECT role, has_chosen_few FROM users` om te bepalen of gásten binnen mogen. Een teller die alleen in de eerste zit, levert een facilitator op die zijn sessie kan starten terwijl zijn deelnemers buiten blijven staan — het slechtst denkbare moment voor een storing. Daarbovenop komt de vraag wat er met het bord en de resultatenpagina gebeurt als iemand niet upgradet. Dat is geen twee uur werk, en het hoort na de meetweek thuis.

**De regel zelf.** Onder het prijsblok op `/`, en niet als losse claim maar als instap:

> Start free as a Club Member with one private board of your own. Running a guided session with participants is part of Club Facilitator.

Twee zinnen, allebei verifieerbaar, en de tweede voorkomt dat je de bezoeker naar een plan stuurt dat niet kan wat de pagina hierboven verkoopt — de fout die A2 in spiegelbeeld beschrijft.

**Wat open blijft.** Of dit genoeg is, weet je pas na de eerste meetweek. Blijkt de drempel dan nog steeds de duurste stap, dan ligt de gratis eerste workshop klaar als volgende zet, en dan is hij onderbouwd in plaats van gegokt.

---

### Besluit 2 — `/boards` mag open vóór verificatie, de wall en de gastlink niet

> **Genomen op 24 augustus 2026.** Een ongeverifieerd account mag inloggen en `/boards` gebruiken, met een banner die om verificatie vraagt. Twee handelingen blijven achter verificatie: publiceren op de worldwide wall, en het activeren van een gast- of post-sharelink.

**Drie feiten uit de code die §10 nog niet had.**

- **Verificatie wordt op precies één plek afgedwongen:** `User::login()` gooit een exception als `email_verified_at` leeg is. Er is geen tweede poortje. Wie die exception weghaalt, zet dus in één keer *alles* open — inclusief publiceren op de wall, en dat gaat sinds besluit 7 de zoekindex in.
- **De opruimtaak bestaat al.** `app/scripts/cleanup_unverified_users.php` draait dagelijks via supercronic, verwijdert ongeverifieerde accounts na zeven dagen, spaart admins en ruimt via `ON DELETE CASCADE` ook notes, hearts en instant photo-bestanden op. De kostenpost die §10 bij *"Ja, met banner"* noemde, is dus al betaald.
- **De limiet bestaat ook al.** De gratis laag mag standaard één privébord (`max_private_boards_free`), instelbaar zonder deploy. Een ongeverifieerd account kan dus niet in bulk borden aanmaken.

**Waarom de twee uitzonderingen.** De opruimtaak werkt op zeven dagen. Een spam-note die op dag één wordt geplaatst, staat dan een week in de index voordat het account wordt opgeruimd — en Google laat de pagina daarna niet meteen vallen. De gastlink is dezelfde redenering met een ander gezicht: die nodigt mensen zonder account uit naar inhoud die door een niet-geverifieerd account is gemaakt. Alles wat binnen het account blijft, is onschadelijk; alles wat naar buiten wijst, wacht op de bevestigde mail.

**Wat dit oplevert.** De uitstap naar het mailprogramma verdwijnt tussen intentie en betaling — volgens A8 de duurste stap van de funnel. De bezoeker ziet `/boards` en dus het product vóórdat hij afrekent, en verificatie verschuift van blokkade naar herinnering.

**Wat het kost, eerlijk.** Dit is echt bouwwerk, geen configuratie: er staan nu nul poortjes op verificatie na de login, en er komen er twee. Reken op de exception uit `User::login()`, een bannerregel in de layout voor `email_verified_at IS NULL`, en twee gates met bijbehorende uitlegtekst. De rechtencontrole hoort op de server, niet in de template — een verborgen knop is geen gate.

**Wat dit níet verandert.** De blootstelling die besluit 7 heeft gecreëerd blijft exact zoals hij is. D-24 fase 1 blijft daarmee toereikend, en de juristenronde uit §9 van de spec hoeft niet opnieuw.

---

### Besluit 1 en 2 — gebouwd en handmatig geverifieerd op 24 augustus

Tien bestanden. Besluit 1 is één alinea op `/`; besluit 2 is de verplaatsing van verificatie van de voordeur naar de deuren die naar buiten leiden.

- **De gratis-instapregel** staat onder het prijsblok, met het bordaantal uit `configuredFreeLimit()`. De tweede zin noemt Club Facilitator, zodat de regel een instap wordt en geen afslag.
- **`User::login()` weigert niet meer.** Erboven staat waarom die ene regel gevaarlijk was om zomaar te schrappen: hij was de énige verificatiecontrole in de hele applicatie.
- **`BaseController::requireVerifiedEmail($wat, $terug)`** is het nieuwe poortje en `emailUnverified()` de vraag erachter. Die gelooft een datum in de sessie zonder query — een bevestigd adres wordt nooit meer onbevestigd — maar gaat naar de database zodra de sessie "nog niet" zegt, want mensen bevestigen in een ander venster.
- **Drie gates in plaats van twee.** Naast de wall en de post-/gastsharelink hangt ook `BoardController::invite()` eraan. Dat is een afwijking van het besluit, en met opzet: bij een uitnodiging verstuurt het product zélf een e-mail naar een zelf ingetypt adres, namens een account dat nog niemand is. Dat is geen blootstelling maar een verzendkanaal, en zo komt een domein op een blocklist. Een view-link blijft open — lezen is de blokkade niet waard.
- **De banner** staat in `layout.html` boven de flashmeldingen, met `emailUnverified` als `false` in `setLayoutDefaults()` — anders breekt de 404-pagina precies zoals na S1.10.
- **Wat de bezoeker leest, klopt nu overal:** de registratieflash, de tekst na het klikken op de verificatielink (die weet nu dat je al ingelogd kunt zijn en stuurt door via `destinationAfterLogin()` in plaats van naar `/login`), en de verificatiemail zelf, die niet langer beweert dat je pas ná bevestiging kunt beginnen.

De regel staat in `CLAUDE.md`, zodat een vierde naar-buiten-gerichte route hem niet vergeet: **een handeling die mensen buiten het account bereikt, wacht op het bevestigde adres; alles daarbinnen niet.**

**Wat dit onbedoeld blootlegde: een bestaande 500 in het wachtwoordherstelpad.** `isEmailVerified()` gebruikte `$this->db`, en die property bestond niet — `App\Models\User` is het enige model dat noch van `BaseModel` erft, noch zoals `Board`, `BoardNote`, `UserSession` en `BoardShareLink` zijn eigen `$db` declareert. Drie andere methodes in datzelfde bestand maakten die aanname **al**, en één ervan is `findByResetToken()`, zonder `try/catch`: wie op een wachtwoordherstellink klikte, kreeg daar een 500. Die fout stond er vóór dit besluit en heeft er niets mee te maken; hij kwam alleen aan het licht doordat een nieuwe regel dezelfde vanzelfsprekende aanname maakte.

Gerepareerd door de property toe te voegen in plaats van vier aanroepen te verbouwen — dan klopt de aanname die de rest van de map ook maakt, en is de val weg in plaats van vier keer omzeild.

**De les, en hij is dezelfde als die van B5.** `php -l` was groen: een niet-bestaande property is geldige syntaxis.

`check-render.php` is diezelfde dag uitgebreid met vier layout-gevallen (uitgelogd, ingelogd bevestigd, ingelogd met de banner, en de foutpagina-variant die alleen `setLayoutDefaults()` heeft) en beide takken van de registratiepagina. Dat dekt de banner en het inlaadpad van de layout — het pad dat na S1.10 brak.

**Maar het dekt deze fout niet, en dat staat nu ook in de kop van dat script.** De `$db`-fout zat in een model dat door een controller wordt aangeroepen; een render-smoke rendert views. Wat hem wél had gevonden is een controle die de klasse instantieert en de methode aanroept. Die bestaat niet, en zolang dat zo is betekent "alle checks groen" niet dat deze klasse fouten gedekt is. Dat is geen reden om er nu een te bouwen — het is een reden om het op te schrijven in plaats van het te vergeten.

---

### Besluit 7 en wat het betekent voor D-24

> **Genomen op 23 augustus 2026.** De aanpassing in `robots.txt` blijft staan; publieke sticky notes worden vanaf nu geïndexeerd. Dit besluit is expliciet genomen ná de constatering dat het in sprint 0 was meegelopen zonder dat het gevolg was afgewogen.

**Wat er nu waar is.** Elke publieke sticky note en elke landenpagina kan door zoekmachines worden opgehaald, gecached en getoond. De Constitution belooft dat ook aan gebruikers, en de interface waarschuwt ervoor vóór publicatie — het product doet dus eindelijk wat het zegt. Wat er niet is, is de knop waarmee iemand een note kan melden. Het Help Centre wijst daarvoor sinds 21 augustus naar een e-mailroute, met de mededeling dat de knop nog gebouwd wordt. Dat is een geldig meldmechanisme in de zin van artikel 16 DSA, maar het is de minimale variant.

**Wat dit besluit verandert aan de volgorde.** De rekening voor indexeren is dat de blootstelling groter wordt vóórdat het instrumentarium er is: inhoud die eerst alleen op de wall stond, staat nu ook in zoekresultaten, en een verzoek tot verwijdering kan van buiten komen in plaats van alleen van een ingelogde gebruiker. **Fase 1 van `spec-D-24-rapportage-en-moderatie.md` schuift daarmee naar boven op de lijst** — hij stond al als launchpoort genoteerd, maar hij is nu ook de eerstvolgende inhoudelijke bouwklus, vóór de resterende Later-punten uit dit document.

Fase 1 is volgens de spec twee tot drie dagen: melden, zaaknummer, wachtrij, besluit met motivering, auditregel bij inzage.

**Wat dit besluit níet verandert.** Het is omkeerbaar. Eén regel uit `robots.txt` halen sluit de deur weer, en de al geïndexeerde pagina's verdwijnen dan binnen enkele weken. Zolang de meldroute per e-mail werkt en in het Help Centre staat, is er geen acute onrechtmatigheid — alleen minder marge dan met de knop.

### D-24 fase 1, plak A — gebouwd op 24 augustus

De eerstvolgende bouwklus uit dit document is begonnen. Plak A van fase 1 staat in de repo (nog niet gecommit, nog niet gedeployd): de `reports`-tabel, een Report-link op elke publieke sticky note, een zaak met zaaknummer `SN-2026-000123`, een ontvangstbevestiging aan de melder en een meldingsmail aan de beheerder.

Drie keuzes die van de spec afwijken, alle drie in de code toegelicht:

- **Een pagina in plaats van een dialoog.** `/notes/@id/report` werkt zonder JavaScript en kost één template in plaats van een Alpine-component per view waar gemeld kan worden.
- **Alleen publieke sticky notes in deze ronde.** Dat is de inhoud die besluit 7 aan zoekmachines heeft blootgesteld. Bordnotes, comments en borden houden voorlopig de e-mailroute; de tabel kent hun `target_type` al, dus uitbreiden kost geen migratie.
- **De rem op melden telt in de sessie, niet via `RateLimiter`.** Die helper escaleert na twintig pogingen naar een permanente blokkade, en een permanent geblokkeerd meldformulier is het tegenovergestelde van het *easy to access* uit artikel 16. Artikel 23 geldt bovendien niet voor micro en klein.

**Wat er nog niet was:** de wachtrij, het besluit en de documentatie. Dat is plak B geworden, dezelfde dag.

### D-24 fase 1, plak B — gebouwd op 24 augustus

Fase 1 is daarmee compleet. Erbij gekomen:

- **De Report-link is een vlaggetje.** Zelfde maat, stroke en hover-schaal als de deel- en hartknop; alleen de hover-kleur blijft grijs. Melden is geen handeling die je wilt uitnodigen, alleen een die vindbaar moet zijn. Zonder zichtbaar woord hoort er een `aria-label` bij, en die staat er.
- **`/admin/reports` — de wachtrij.** De volgorde zit in de query en niet in het oordeel van de beheerder: open vóór afgehandeld, kindveiligheid bovenaan, daarbinnen oudste eerst. Dat laatste is artikel 16 lid 6; nieuwste-eerst is precies hoe een melding onderop blijft liggen.
- **`/admin/reports/<id>` — het zaakdetail, met een auditregel bij élke inzage.** Dit was het ontbrekende stuk uit §6 van de spec: verwijderen werd gelogd, kíjken niet. De regel wordt geschreven vóórdat de zaak in beeld komt, want loggen achteraf betekent dat een afgebroken request wel inzage geeft en geen spoor.
- **Het besluit voert de maatregel uit.** *Content removed* verwijdert de note via dezelfde route als `/admin/notes` — `deleteNote()` is daarvoor opgesplitst, zodat er geen tweede verwijderpad ontstaat dat op termijn iets anders gaat doen. *Content hidden* zet de vlag, en zet hem, in plaats van te togglen: een besluit is een uitkomst, geen schakelaar.
- **Twee mails per besluit.** De melder krijgt de uitkomst (artikel 16 lid 5), de auteur de motivering met alle zes onderdelen (artikel 17). Bij *no action* is er niets beperkt en krijgt alleen de melder bericht. De volgorde is maatregel → zaak → mail: wie andersom werkt, verstuurt een brief over een verwijdering die niet gelukt is.
- **De looptijd en de grond worden afgeleid, niet gevraagd.** Een extra vrij veld in het besluitformulier is een veld dat op een drukke dag slordig wordt ingevuld, en dan staat er iets onjuists in een brief met juridisch gewicht. De grond citeert de gepubliceerde regel uit de community guidelines woordelijk — artikel 17 vraagt om de regel, niet om een samenvatting.
- **Bewaartermijn.** Zes maanden standaard, twaalf zodra een besluit iets beperkt.
- **Help Centre en Terms bij.** `community-guidelines.md` en `privacy-and-safety.md` beschrijven nu het vlaggetje in plaats van te zeggen dat het niet bestaat, en de Terms hebben een moderatieparagraaf 15.1 t/m 15.3 gekregen (artikel 14).

### C7, het lookalike-teken in het e-mailadres — GEEN bevinding maar een besluit

> **Vastgelegd op 24 augustus 2026.** Het adres blijft overal op de site staan als `farid﹫stickynotes.club`, met een SMALL COMMERCIAL AT (U+FE6B) in plaats van een gewone `@`. Er komen geen `mailto:`-links.

Dit onderdeel van C7 is op 24 augustus eerst "opgelost" — het teken werd in zes bestanden een gewone `@` met een aanklikbare link — en dezelfde dag op verzoek van Farid teruggedraaid. **De reden is spambestrijding, en dat is een keuze van de eigenaar, geen fout van het product.**

Dat het als fout gelezen wordt is niet gek: het adres is niet te kopiëren, niet aanklikbaar, en een schermlezer maakt er iets onbegrijpelijks van. Om die ronde niet elk half jaar opnieuw te draaien staat de afweging nu op één plek in de code, in `App\Helpers\ContactHelper`, met de prijs erbij opgeschreven. Die klasse kent twee vormen en het verschil is niet cosmetisch:

- `address()` — het échte adres, voor de `To:`-header van een e-mail. Nooit tonen.
- `forDisplay()` — hetzelfde adres met het lookalike-teken, voor het scherm. Nooit versturen.

**Wat er open blijft.** Artikel 11 en 12 DSA vragen om een contactpunt dat gebruikers én autoriteiten werkelijk kunnen gebruiken. Of een lookalike-teken daaraan voldoet is vraag 4 voor de jurist in `spec-D-24-rapportage-en-moderatie.md` §9. Komt daar een nee uit, dan is het één regel in `ContactHelper` en verder niets — dat is precies waarom die klasse er is.

Het overige deel van C7 (de About-pagina die het product van vóór D-30 beschreef) is in sprint 2 afgehandeld en blijft afgehandeld.

**Nog te doen aan D-24:** de juristenronde uit §9 van de spec. De teksten in de motiveringsmail, de gronden per categorie en de nieuwe Terms-paragraaf zijn geschreven op artikel 16 en 17, maar niet getoetst. Een correctie daarvandaan is een tekstwijziging, geen herbouw. Fase 2 (opruimscript, herhaling zichtbaar, tijdelijke maatregelen, cijfers per categorie) blijft staan waar hij stond: na de launch, als het volume erom vraagt.

### Wat er sindsdien is bijgekomen

Twee dingen die niet uit de audit kwamen maar uit het gebruik:

- **De sitemap is opgeschoond** (23 augustus): `/login` en `/register` eruit, `changefreq` en `priority` weg, `/c` erbij. Een sitemap hoort de URL's te bevatten die je geïndexeerd wilt hebben.
- **Een regressie uit S1.10 hersteld.** `facilitatorCta` werd alleen in `BaseController::render()` gezet, niet in de ONERROR-handler die de 401-, 403-, 404- en 500-pagina's rendert. Gevolg: de 404-pagina brak midden in de navigatiebalk af. De lijst met layoutvariabelen stond op twee plekken; hij staat nu op één, in `BaseController::setLayoutDefaults()`.

### 24 augustus, later op de dag — één defect vóór de Later-lijst, en L1 t/m L3

**Het defect: `is_flagged` verborg niets.** Gevonden bij het openen van de Later-lijst, en het gaat er in prioriteit ruim overheen. Het moderatiebesluit *Content hidden from the worldwide wall* zette de vlag netjes — `AdminController::hideNote()`, met auditregel — maar **geen enkele publieke query las hem**. Niet `getPublicNotes()`, niet `getPublicNotesByCountry()`, niet de tellers, en niet `NoteController::show()`. Een verborgen note bleef dus op de wall staan, op de landenpagina, op zijn eigen detailpagina, en sinds besluit 7 ook in de zoekindex — terwijl de auteur een artikel-17-brief kreeg die zei dat zijn inhoud was beperkt.

Dat is precies het geval waar `Report::DECISIONS` in zijn eigen commentaar voor waarschuwt: *"een besluit dat zegt dat inhoud is verwijderd terwijl de inhoud er nog staat, is erger dan geen besluit"*. Alleen ging die waarschuwing over verwijderen, en verwijderen wérkte.

**Waarom de bestaande test het niet vond.** `test-report-flow.php` controleerde `Report::decisionEffect('content_hidden') === 'flag'`. Dat is een test op de *intentie*, en die klopte. Er was geen test op het *gevolg*. Sectie 15 van dat script doet dat nu wel: hij zet twee echte notes in een echte database, vraagt de echte modelklasse wat een bezoeker ziet, en controleert ook de omgekeerde weg — de vlag weghalen brengt de note terug.

**De fix, in drie delen.** (1) Elke publieke leesquery op `notes` draagt nu `is_flagged = 0`, precies zoals `deleted_at IS NULL` op `board_notes`; die regel staat als zodanig in `CLAUDE.md`, want een vijfde query die het vergeet is een verborgen note die weer meetelt. (2) `/notes/@id` geeft **404** — geen 403: de pagina staat in de index, en alleen een 404 laat een zoekresultaat vervallen. (3) De auteur en de beheerder houden toegang, met een gele balk die zegt wat de brief zegt. Dat laatste is geen beleefdheid maar consistentie: de brief zegt *hidden — until we decide otherwise*, en de community guidelines beloven dat een beperking bijdragen niet wist.

**L1 — de sitemap wordt gegenereerd.** Nieuwe `SitemapController` op `GET /sitemap.xml`: statische pagina's, `/c`, elke landenpagina en elke publieke, niet-verborgen sticky note, met `lastmod` uit de database. Drie keuzes die afwijken van de kladversie in D2: statische pagina's krijgen **geen** `lastmod` (de enige afleidbare datum is de bestandsdatum, en die is in een Docker-image de builddatum — een `lastmod` die bij elke deploy verspringt leert Google dat je datums niet deugen); notes komen uit een eigen, kale query in plaats van uit `getPublicNotes()`, die per note nog drie extra queries doet; en er zit een plafond van 40.000 URL's op, want daarboven hoort een sitemap-index en geen hoger getal. **`www/sitemap.xml` moest daarvoor weg** — Caddy serveert een bestaand bestand vóór `index.php`, en dat gebeurt stil.

Erbij, want besluit 7 maakte het relevant: `robots.txt` sluit nu `/notes/*/report` uit. `Allow: /notes/` had het meldformulier per ongeluk opengezet, en dat is een handeling, geen inhoud.

**L2 — `srcset` op de homepagebeelden.** Elk van de vijf beelden heeft een halve variant gekregen. Een telefoon haalde tot nu toe ruim 550 kB aan beelden op voor een scherm van 360 pixels breed; dat is nu ongeveer 140 kB. De `sizes`-waarden beschrijven de CSS-breedte van de plek waar het beeld staat; verandert de lay-out van een sectie, dan hoort `sizes` mee te veranderen. De meting met PageSpeed Insights die D6 vraagt, kan pas ná deze deploy en staat in de handmatige lijst hieronder.

**L3 — `og:image` per pagina.** `layout.html` gebruikt nu `@ogImage` met het merkbeeld als standaard in `BaseController::setLayoutDefaults()`. De resultatenpagina zet zijn eigen beeld — dat is de enige pagina van dit product die stelselmatig door iemand anders wordt rondgestuurd, en dus de enige plek waar een eigen preview iets uithaalt. Bewust één vast beeld en geen per sessie gegenereerde kaart: die zou de inhoud van een privébord in een afbeelding zetten die elke chat- en mailprovider ophaalt en cachet.

**L4, L5 en L6: niet gedaan, met reden.** L4 (landingspagina's per situatie) wacht op de eerste meetweek — drie pagina's bouwen op een gok betekent ze daarna herschrijven, en dan is de opgebouwde zoekwaarde weg. L5 (testimonials) kan niet: er zijn er geen echte, en de regel is "geen dag eerder". L6 (A/B-test op de hero-copy) kan technisch pas iets opleveren met verkeer, en dat is er vóór de lancering niet.

**Met de hand nagelopen — afgerond op 24 augustus.** Farid heeft de hele lijst zelf doorlopen; alle bevindingen kwamen overeen met wat hierboven staat beschreven. De lijst blijft staan als vastlegging van wát er is gecontroleerd:

- `composer install` en dan `php scripts/check-templates.php`, `php scripts/check-render.php`, `php scripts/test-board-rights.php` en `php scripts/test-report-flow.php` — alle vier draaiden groen op een schone kopie van deze commit, en inmiddels ook op de machine van Farid.
- Meld een eigen note, kies *Content hidden*, en controleer met een tweede browser: weg van `/wall`, weg van de landenpagina, 404 op `/notes/<id>`, en als ingelogde auteur de gele balk. **Gedaan, gedrag zoals beschreven.**
- `/sitemap.xml` opvragen op de server en controleren dat het gegenereerde bestand komt en niet het oude statische — dat oude bestand staat als verwijderd in git, maar controleer dat het na de deploy ook echt niet meer in de image zit. **Gedaan, het gegenereerde bestand komt.**
- Eén PageSpeed-meting op `/` en `/pricing` (D6) — **ná de deploy**, en pas daarna beslissen of er meer nodig is. Op 24 augustus zijn beide pagina's gemeten terwijl de srcset-wijziging nog niet live stond; die twee runs zijn dus een nulmeting en geen controle. **De meting ná de deploy staat hieronder.**
- Sitemap opnieuw indienen in Search Console, nu er landenpagina's en notes in staan. **Gedaan.**

**Wat hiermee níet is beantwoord.** Het opnieuw indienen lost de openstaande vraag uit het verificatielogboek van 23 augustus niet op: of Google de sitemap eerder niet kon lezen door een tijdelijke verwerkingsfout aan hun kant, of doordat Cloudflare Googlebot op dat pad blokkeert. Alleen URL-inspectie op `/sitemap.xml` in Search Console onderscheidt die twee. Zolang dat niet is gedaan, is een uitblijvende verwerking niet te lezen als "het duurt gewoon even".

**Nagekomen op 24 augustus:** het meldvlaggetje stond op `w-6` omdat de maat van de deelknop was overgenomen, en was daardoor optisch het grootste icoon in de rij — de tekening loopt van y=3 tot y=21 omdat de stok doorloopt, terwijl het deelicoon rond y=4 begint en ophoudt bij y=20 en het hart al op `w-5` stond. Nu `w-5`. De les staat in de template: kijk naar wat de tekening vult, niet naar de klasse.

### De PageSpeed-meting van 24 augustus, ná de deploy

Mobiel, Moto G Power, trage 4G. Veldgegevens ontbreken nog (CrUX heeft te weinig verkeer), dus dit is labdata.

| | `/` | `/pricing` |
|---|---|---|
| Prestaties | **99** | **100** |
| Toegankelijkheid | 96 | 96 |
| Praktische tips | 100 | 100 |
| SEO | 92 | 92 |
| FCP / LCP | 1,2 s / 1,7 s | 0,9 s / 1,3 s |
| TBT / CLS | 0 ms / 0 | 0 ms / 0 |

**De srcset-wijziging heeft gedaan wat hij moest doen.** Wat er van L2 overblijft is één beeld van 12 kB te zwaar: `workshop-participant-mobile-640.webp` wordt op 560×1589 getoond terwijl er 640×1816 wordt geladen. Mijn `sizes="320px"` is net iets ruimer dan de werkelijke 280 CSS-pixels. Twaalf kilobyte is geen reden om die waarde te gaan finetunen.

**Wat de meting wél vond, en wat de audit nooit had kunnen vinden: één megabyte aan iconen.** `www/img/celestial/moon.png` was 775 kB bij 936×936 en `mars.png` 290 kB bij 517×517 — allebei getoond op **25×25 pixels**, want `CelestialHelper::icon()` rendert ze op `1em`. Ze staan niet alleen op `/pricing`: `countryHtml()` zet ze onder elke sticky note van de Maan of Mars, dus ook op de wall, de landenpagina's, de eigen-notes-lijst en de profielpagina. Beide zijn teruggebracht naar 64×64 — samen van 1,04 MB naar 16 kB, en op het scherm ziet niemand verschil. Dat de prestatiescore van `/pricing` toch 100 was, komt doordat de beelden `loading="lazy"` zijn en onder de vouw staan; de score zag ze niet, een bezoeker met een databundel wel.

**SEO 92 op beide pagina's, om dezelfde reden:** de mobiele CTA naast de hamburger heet `Start`, en Lighthouse rekent dat als niet-beschrijvende linktekst. Het zichtbare woord blijft — daar is geen ruimte voor meer en `07` schrijft het zo voor — maar de link heeft nu `aria-label="Start a workshop"`. Dat is ook los van de score de juiste zet: een schermlezer die de links van een pagina opsomt, las hier alleen een werkwoord zonder object.

**Toegankelijkheid 96 op beide:** één contrastfout, de regel *"Guest links expire, and the facilitator can replace or revoke them at any time"* in `text-gray-500` op de pastelroze body. Nu `text-gray-600`.

**Bewust niet aangepakt.** Twee dingen die Lighthouse noemt en die ik zou laten liggen tot er een reden is:

- **42 kB ongebruikte JavaScript** van de 52 kB in `app.js`. Dat is Alpine met de bordcomponenten, op een marketingpagina die er vrijwel niets van gebruikt. Een aparte bundel voor de publieke pagina's is een echte ingreep in de buildketen, en TBT staat op 0 ms — het kost nu niets aan snelheid, alleen aan bytes.
- **Renderblokkerende CSS**, 11,5 kB `app.css` met een geschatte besparing van 450 ms op `/`. Critical CSS inlinen betekent een tweede plek waar stijl vandaan komt, en dat is precies het soort tweede waarheid dat dit product elders zorgvuldig vermijdt. Bij een prestatiescore van 99 is dat de investering niet waard.

### De cache voor de app — bevestigd op 24 augustus

`robots.txt` bleef na de deploy zijn oude inhoud tonen terwijl de sitemap en de srcset uit dezelfde image wél nieuw waren. De headers wijzen het aan:

```
server: cloudflare
cf-cache-status: HIT
age: 2636
cache-control: max-age=2592000
```

**Dertig dagen**, en die waarde komt niet uit de app: de Caddyfile zette tot vandaag geen enkele `Cache-Control`, dus alles zonder eigen header kreeg de standaardwaarde van Cloudflare. Voor `/css/app.css?v=...` en `/js/app.js?v=...` is dat precies goed — die dragen hun eigen versie in de URL. Voor twee bestanden is het schadelijk:

- **`robots.txt`** — een crawlregel die je vandaag corrigeert, komt een maand niet aan. Dit is wat er gebeurde.
- **`/sitemap.xml`** — en dit is de stille: hij wordt sinds vandaag *gegenereerd* zodat hij altijd klopt, en zou vervolgens een maand lang de versie van vanmiddag blijven serveren. De hele winst van L1 verdampt dan zonder dat iemand het merkt, want het bestand ziet er goed uit — alleen een maand oud.

Beide zijn nu bij de bron geregeld: `SitemapController::send()` stuurt `Cache-Control: public, max-age=3600` mee, en de Caddyfile zet `max-age=300` op `robots.txt`. De origin zegt het, en niet het CDN bij gebrek aan beter.

**Afgehandeld op 24 augustus:** de cache voor `robots.txt` is met de hand geleegd (Cloudflare, Purge by URL) en de nieuwe versie is live. Vanaf nu is dat geen handmatige stap meer: met `max-age=300` uit de Caddyfile veroudert een verkeerde kopie binnen vijf minuten in plaats van binnen dertig dagen.

**Afgemaakt op 24 augustus.** Browser Cache TTL in Cloudflare staat nu op *Respect existing headers*, en de Caddyfile vult in wat er dan gezegd moet worden. Die twee horen bij elkaar: zonder de tweede stap krijgen `/css`, `/js`, `/fonts`, `/img` en `/uploads` helemaal géén bewaarinstructie meer, waar Cloudflare eerst nog dertig dagen invulde — dat zou de dag erna hebben gevoeld als een site die plotseling traag werd voor terugkerende bezoekers.

De regel waarop is gesplitst: **verandert de URL als de inhoud verandert?**

| Pad | TTL | Waarom |
|---|---|---|
| `/css/*`, `/js/*` | 1 jaar, `immutable` | `layout.html` hangt `?v=<filemtime>` eraan; een deploy is een nieuwe URL |
| `/fonts/*` | 1 jaar, `immutable` | gewicht en subset staan in de bestandsnaam; worden nooit ter plekke vervangen |
| `/img/*`, `/uploads/*` | 1 week | een afbeelding houdt zijn naam bij nieuwe inhoud — `moon.png` is vandaag onder dezelfde naam vervangen |
| `/robots.txt` | 5 minuten | een crawlregel die je vandaag corrigeert, moet vandaag aankomen |
| `/sitemap.xml` | 1 uur | gegenereerd; een crawler mist hooguit het laatste uur, en de origin wordt niet bij elke crawl aan het scannen gezet |

Op productie geverifieerd: alle vijf geven de bedoelde header terug.

**`immutable` verdient één zin uitleg**, want het is sterker dan het lijkt: een browser slaat daarmee zelfs de revalidatie bij een harde refresh over. Dat mag alleen omdat die URL's versiegestempeld zijn. Zet nooit `immutable` op een pad waar een bestand zijn naam kan houden — dan is een fout die je publiceert onherroepelijk tot de cache verloopt.

**Los signaal, geen bevinding:** de screenshots op de homepage tonen nog de oude statusknoppen (*Workshop running*, *Not a workshop*). Die labels bestaan sinds S0.1 niet meer. Nieuwe schermafdrukken zijn een klusje van een half uur, maar het is wel de eerste pagina die een bezoeker ziet.


---

## 1. Samenvatting in één pagina

Het product is in ongewoon goede staat. De positioneringsdocumenten zijn scherper dan wat ik bij de meeste SaaS-bedrijven zie, de homepage volgt het frontpagevoorstel bijna letterlijk, de foutteksten in `boardApi.js` zijn beter geschreven dan de meeste betaalde producten, en de facilitatorbalk is doordacht tot in de randgevallen.

De problemen zitten daarom niet in de kwaliteit van de teksten. Ze zitten op **vier naden**: plekken waar twee stukken van het product elkaar raken en niet hetzelfde zeggen.

**Naad 1 — tussen de belofte en de eerste stap.** De homepage verkoopt "Run a focused workshop in minutes". De knop leidt naar een registratiepagina met de kop *Create your free account* en de regel *Free forever · No credit card needed*, en eindigt na e-mailverificatie op een afrekenpagina van €14,99. Drie schermen, drie verschillende verhalen. (A1, A3, A8)

**Naad 2 — tussen betalen en doen.** Wie Club Facilitator koopt, leest op de bevestigingspagina dat workshopmodus wordt vrijgeschakeld — en krijgt als primaire knop **Create a note**, die naar het publiceren van een sticky note op de wereldwijde wall gaat. Klikt hij in plaats daarvan door naar `/boards`, dan komt hij op een pagina waar het woord *workshop* niet voorkomt. (B2, B3)

**Naad 3 — tussen de knop en zijn betekenis.** De belangrijkste knoppen van de facilitator dragen de naam van een *toestand*, niet van een *actie*. De knop waarmee je de sessie start heet **Workshop running**. De knop waarmee je hem afsluit heet **Finished**. De knop waarmee je workshopmodus uitzet heet **Not a workshop**. Dit is precies de vraag die je stelde — begrijpen mensen meteen wat de knop gaat doen — en het antwoord is hier aantoonbaar nee. (B1)

**Naad 4 — tussen de deelnemer en het merk.** Vijftig mensen per sessie zien dit product werken zonder ooit een account te maken. Dat is de sterkste groeimotor die je hebt. Hij wordt op dit moment uitgeoefend door één grijze regel onderaan de gedeelde weergave, en de resultatenpagina — het document dat ná afloop wordt rondgestuurd naar mensen die er níet bij waren — bevat geen enkele verwijzing naar wat dit is of hoe je het zelf doet. (B14, B15)

Daarnaast is er één technische bevinding met directe commerciële gevolgen: **`robots.txt` sluit elke publieke sticky note uit van indexering** (`Disallow: /notes` dekt ook `/notes/@id`), terwijl de Constitution het indexeren van publieke notes juist expliciet als productbelofte formuleert. (D1)

En één meetprobleem: **er zit geen enkele vorm van analytics in de applicatie.** Het frontpagevoorstel definieert vijf events en een funnel; geen daarvan bestaat. Zonder dat kun je geen enkele wijziging uit dit document beoordelen. (D7)

---

## 2. De rode draad: één regel die alles verklaart

De Constitution noemt onder *Signs that we are drifting* letterlijk: **"several names exist for the same concept"**. Dat is niet één bevinding in dit rapport — het is het patroon waar het merendeel van de contentbevindingen onder valt.

Tel mee. Voor "maak een account" bestaan in het product vijf labels: *Create Account*, *Get started today*, *Get started — it's free*, *Sign up for free*, *Create free account*. Voor "inloggen" bestaan er drie: *Log in*, *Login*, *Sign in*. Voor "uitloggen" twee: *Sign out*, *Log out*. Voor de voorwaardenpagina drie: *Terms*, *Terms and Conditions*, *Terms of Service*. Voor de wereldwijde wall twaalf, willekeurig door JavaScript gewisseld bij elke pageview.

Dit kost geen conversie doordat één label slecht is. Het kost conversie doordat de bezoeker steeds opnieuw moet vaststellen dat hij nog bij hetzelfde product is. **AANNAME**, maar wel de best onderbouwde aanname in dit document, want de Constitution zelf noemt het als drift-signaal.

De goedkoopste ingreep in dit hele rapport is daarom een **labelregister**: één tabel met het canonieke label per actie, en één zoek-en-vervangronde. Zie §7, sprint 0.

---

## 3. Bevindingen — A. Funnel en conversie (publieke pagina's)

### A1 — Er is geen risicoloze ingang naar het hoofdproduct

**FEIT.** De homepage toont precies één prijs: Club Facilitator, € 14,99 per maand exclusief btw. Het woord *free* komt op de hele pagina alleen voor in het FAQ-antwoord *"Participants take part for free"* — dat gaat over de deelnemers, niet over de bezoeker. Dat er een gratis Club Member-account bestaat, is op `/` nergens zichtbaar. Er is geen proefperiode; dat is in `07` bewust vastgelegd (*"Er is geen gratis trial; daarom wordt die niet beloofd"*).

**AANNAME.** Voor een onbekend product van een onbekende maker, zonder testimonials, zonder logo's en zonder proefperiode, is een maandabonnement van €14,99 als enige zichtbare optie de grootste enkele drempel in de funnel. De bezoeker die twijfelt heeft geen tussenstap: alleen kopen of weggaan.

**BESLUIT NODIG.** Zie §8, besluit 1. Ik schrijf hier geen prijsstrategie voor, maar de pagina moet minstens *ergens* zeggen dat je gratis kunt beginnen — dat is nu al waar en kost geen productwerk.

---

### A2 — De prijspagina stuurt actief weg van het plan waar de funnel heen leidt

**FEIT.** `app/resources/views/pricing.html`, regel 68: het badge **Best value** staat op **Club Host** (€ 4,99). Op Club Facilitator (€ 14,99) staat het badge *For workshops*. De volgorde van de vier kaarten is Member → Host → Facilitator → Chosen Few; het hoofdplan is dus de derde van vier, en op een tabletbreedte (twee kolommen) valt het onder de vouw.

**FEIT.** De secundaire CTA in het prijsblok op de homepage heet *Compare all plans →* en gaat naar precies deze pagina.

**Tweede-orde-effect.** De bezoeker die op de homepage is overtuigd van workshops, klikt door om te vergelijken, ziet dat een ander plan "de beste waarde" is, en koopt Club Host. Club Host kan geen workshops draaien: `canFacilitate()` vereist `canFacilitateWorkshops()`, dus de **Workshop**-knop verschijnt niet eens op zijn bord (zie B4). Hij vindt de functie waarvoor hij kwam niet terug, en er staat nergens in de app uitgelegd waarom. Dat eindigt in een supportmail of een terugbetaling, en in beide gevallen in wantrouwen.

**ADVIES.** Verplaats het badge. Club Facilitator krijgt **Most popular for workshops** of eenvoudig **Recommended**; Club Host verliest *Best value* (een claim die je bovendien niet kunt onderbouwen — Public Communication Specification §12). Zet Club Facilitator op positie twee, direct na Club Member, of geef hem visueel meer gewicht dan de andere drie.

---

### A3 — De registratiepagina belooft gratis aan iemand die naar een afrekenpagina gaat

**FEIT.** `app/resources/views/auth/register.html`, regels 3–4:

```
Create your free account
Free forever · No credit card needed
```

**FEIT.** De route ernaartoe is `/register?plan=pro` (`layout.html` nav en `home.html` via `@facilitatorCta`). `AuthController::rememberRequestedPlan()` bewaart `pro` in de sessie en `destinationAfterLogin()` stuurt na het inloggen door naar `/checkout/pro`. De eerste pagina ná registratie is dus een betaalpagina van €14,99.

**Tweede-orde-effect.** Twee kanten, allebei slecht. Wie de regel gelooft, voelt zich bij de checkout misleid — en dit is een product waarvan de Constitution zegt dat vertrouwen boven conversie gaat (*Decision hierarchy*, punt 1 en 2 boven punt 5). Wie de regel niet gelooft, denkt dat hij op de verkeerde pagina is beland en haakt af.

**ADVIES.** Maak de registratiepagina planbewust. Als `SESSION.pending_plan` gevuld is, toon dan een korte contextregel in plaats van de gratis-claim:

> **You are signing up for Club Facilitator**
> € 14.99 per month, excluding VAT. We will ask for payment after you confirm your email address. You can cancel at any time.

Zonder plan blijft de huidige kop staan, maar zonder superlatief:

> **Create your free account**
> No credit card needed. Upgrade whenever you want to run a workshop.

**Implementatie.** `AuthController::registerForm()` zet `pendingPlan` en `pendingPlanLabel` als templatevariabelen; `register.html` kiest daarop. De waarde bestaat al in de sessie, er is geen nieuwe logica nodig.

---

### A4 — Vijf labels voor één actie

**FEIT.** Voor "maak een account" bestaan deze knoppen:

| Label | Bestand |
|---|---|
| `Create Account` | `auth/register.html`:71 |
| `Get started today` | `pricing.html`:59 |
| `Get started — it's free` | `wall.html`:11 |
| `Sign up for free` | `wall.html`:102 |
| `Create free account` | `boards/shared.html`:77 |

En voor inloggen: `Log in` (`layout.html`, nav), `Login` (`boards/shared.html`:74), `Sign in` (`auth/register.html`:80). Voor uitloggen: `Sign out` (desktopmenu) en `Log out` (mobiel menu). Voor het profiel: `Profile` (desktop) en `My Profile` (mobiel). Voor het Help Centre: `Help` (desktopnavigatie, uitgelogd) en `Help Centre` (overal elders).

**ADVIES.** Eén labelregister, zie §7 sprint 0 en de tabel in §9.

---

### A5 — De primaire CTA is nergens primair

**FEIT.** In `layout.html` staat de knop *Start a workshop* in de uitgelogde desktopnavigatie als `class="nav-link shadow-lg"` — dezelfde klasse als *How it works*, *Worldwide wall*, *Pricing*, *Help* en *Log in*, met alleen een schaduw als verschil. Het frontpagevoorstel (`07`, sectie 1) schrijft voor: *"Gebruik één primaire knop."*

**FEIT.** In het mobiele menu staat *Start a workshop* als **laatste** van acht items, in exact dezelfde stijl als de rest. Buiten het hamburgermenu is er op mobiel geen enkele zichtbare CTA in de navigatie. Het voorstel schrijft voor: *"Primaire knop `Start` zichtbaar."*

**ADVIES.** Desktop: geef de knop een echte knopstijl (gevulde achtergrond, afwijkend van `nav-link`). Mobiel: haal hem uit het menu en zet hem naast de hamburger als korte knop **Start** — precies zoals `07` het beschrijft.

---

### A6 — De homepage bewijst de belofte niet met herkenbare situaties

**FEIT.** Het Playbook schrijft onder *Marketing and positioning*: *"Support claims with recognisable situations such as a team retrospective, a class collecting answers, a training group ranking priorities or a neighbourhood initiative organising suggestions."*

**FEIT.** Op de homepage komt geen enkele van die situaties voor. De enige plek waar een retrospective wordt genoemd is de placeholder in de facilitatorbalk (*"What slowed us down this sprint?"*) — zichtbaar voor wie al klant is.

**Tweede-orde-effect.** Zonder situatie moet de bezoeker zelf bedenken of dit voor hem is. Voor de doelgroepen uit `07` (scrum masters, docenten, trainers) is dat een extra denkstap precies op het punt waar hij beslist of hij doorleest. Het raakt bovendien de vindbaarheid: "retrospective tool", "workshop zonder account" en "brainstorm met QR-code" zijn de zoekopdrachten waarop deze pagina zou moeten scoren, en die woorden staan er niet.

**ADVIES.** Eén rustige strook tussen sectie 3 en sectie 4 (*From QR code to shared decision*), zonder beeld:

> ### Built for the sessions you already run
>
> **Sprint retrospective** — collect what helped and what slowed the team down, then vote on the one thing to change.
> **Classroom or training** — ask a question, let everyone answer at the same time, and discuss what comes back.
> **Planning or kick-off** — gather options from the whole room before the loudest voice sets the direction.
> **Community or team meeting** — give people who do not speak up in a room a way to be heard.

Vier korte blokken, geen extra screenshots, en elke regel beschrijft gedrag dat het product werkelijk doet.

---

### A7 — Geen enkel vertrouwenselement op de commerciële pagina's

**FEIT.** Op `/` en `/pricing` staat: geen maker, geen locatie, geen hostinginformatie, geen opzegregel, geen terugbetaalregel, geen contactadres, geen verwijzing naar Terms of Privacy (behalve in de laatste sectie van de homepage, als kleine tekstregel tussen zes andere links). De prijspagina heeft überhaupt geen footer.

**FEIT.** Die informatie *bestaat* wel — in `about.md` staat dat het product door Farid Bouchdak in Nederland wordt gemaakt en bij Fly.io in Amsterdam draait. Dat is precies wat een koper wil weten en het staat op de pagina die hij niet bezoekt.

**ADVIES.** Zie D3 (echte footer). Voeg daarnaast direct onder de betaalknop op `/pricing` en in het prijsblok van de homepage één regel toe:

> Monthly, cancel at any time. VAT is added at checkout where it applies. Built and run in the Netherlands.

**BESLUIT NODIG.** Zie §8, besluit 4 — er staat nu geen terugbetalingsbeleid in de Terms dat ik kan citeren.

---

### A8 — E-mailverificatie staat tussen de intentie en de betaling

**FEIT.** De volledige route van "Start a workshop" tot betalen:

1. `/` → knop → `/register?plan=pro`
2. Formulier invullen (vier velden) → flash *"Registration successful! Please check your email to verify your account."*
3. Naar de mail, verificatielink openen → flash *"Email verified successfully! You can now log in."*
4. Inloggen → flash *"Welcome back!"*
5. → `/checkout/pro` → betaalpagina van Creem

**FEIT.** `destinationAfterLogin()` leest `SESSION.pending_plan`. De docblock zegt het zelf: *"Wie de verificatiemail in een andere browser opent, verliest zijn plankeuze en komt gewoon op /boards uit."* Registreren op de laptop en de mail openen op de telefoon is het normale geval, niet de uitzondering.

**FEIT.** De flash bij stap 4 is *"Welcome back!"* voor iemand die er nog nooit is geweest.

**AANNAME.** Vijf stappen met een verplichte uitstap naar een mailprogramma tussen intentie en betaling is de duurste stap van de funnel. Wie in stap 3 afhaakt, komt zelden terug.

**ADVIES, drie ingrepen van oplopende omvang.**

*Klein, nu.* Sla het plan óók op in de verificatietoken, niet alleen in de sessie. Dan overleeft de keuze een browserwissel. Eén kolom of één queryparameter op de verificatielink.

*Klein, nu.* Maak de flash bij de eerste login planbewust:

> Your account is ready. One more step: choose how you pay for Club Facilitator.

En vervang *"Welcome back!"* voor een eerste login door *"Welcome to StickyNotes.club."*

*Middelgroot.* **BESLUIT NODIG** (§8, besluit 2): mag iemand `/boards` in vóórdat hij zijn e-mailadres verifieert, met een banner erboven? Dan verschuift verificatie van *blokkade* naar *herinnering*, en zie je het product voordat je betaalt.

---

### A9 — Nav-CTA en hero-CTA kunnen uit elkaar lopen

**FEIT.** `home.html` gebruikt `@facilitatorCta`, die in `HomeController` terugvalt op `/pricing` zodra `CREEM_PRODUCT_PRO` leeg is. `layout.html` heeft `/register?plan=pro` hardcoded, op twee plaatsen (desktop en mobiel).

**FEIT.** Op dit moment is Club Facilitator koopbaar (de kaart staat live op `/pricing`), dus dit is nu niet zichtbaar. Maar zodra het plan uit de verkoop gaat, leidt de navigatieknop naar een registratie die de plankeuze stil weggooit en op `/boards` eindigt — terwijl de prijspagina de kaart dan óók verbergt.

**ADVIES.** Zet `facilitatorCta` in `BaseController` zodat elke pagina hem heeft, en gebruik hem in `layout.html`. Kosten: drie regels.

---

## 4. Bevindingen — B. Activatie en UX-flow in de applicatie

### B1 — De knoppen van de facilitator dragen toestandsnamen, geen acties ★

Dit is de belangrijkste bevinding van het rapport.

**FEIT.** `WorkshopService::LABELS` bevat de omschrijvingen per status:

```php
STATUS_OFF      => 'Not a workshop',
STATUS_DRAFT    => 'Preparing',
STATUS_LOBBY    => 'Lobby open',
STATUS_RUNNING  => 'Workshop running',
STATUS_CLOSED   => 'Finished',
STATUS_ARCHIVED => 'Archived',
```

**FEIT.** `BoardController::nextStatusOptions()` (rond regel 771) bouwt de knoppen als `['status' => $target, 'label' => WorkshopService::label($target)]` — dus met **de label van de doelstatus**. Die array voedt zowel `x-text="ns.label"` in `_workshop_bar.html` als de server-gerenderde formulieren in stap 3 van het Workshop-paneel.

**Gevolg — wat de facilitator werkelijk ziet:**

| Status nu | Knoppen die hij ziet |
|---|---|
| Preparing (draft) | `Lobby open` · `Workshop running` · `Not a workshop` |
| Lobby open | `Workshop running` · `Preparing` |
| Workshop running | `Lobby open` · `Finished` |
| Finished | `Workshop running` · `Archived` · `Not a workshop` |
| Archived | `Finished` · `Not a workshop` |

De knop waarmee je een sessie start, heet *Workshop running*. Midden in een zaal, met vijftien mensen die op je scherm kijken, moet de facilitator raden of dat een status is die hij leest of een knop die hij indrukt. En de flash erna bevestigt de verwarring: *"Workshop is now: Workshop running"*.

Het Playbook zegt het letterlijk: *"Button labels describe the action: **Create board**, **Send invitation**, **Delete note**."*

**ADVIES.** Voeg een tweede tabel toe naast `LABELS`, gesleuteld op het **paar** `van → naar`. Dat is nodig: `closed → running` is *Reopen*, `draft → running` is *Start*. Eén map op de doelstatus alleen zou de tweede fout maken.

```php
/** Wat de knop DOET, per overgang. LABELS zegt wat een status IS. */
private const ACTIONS = [
    'off'      => ['draft'    => 'Set up a workshop'],
    'draft'    => ['lobby'    => 'Open the waiting room',
                   'running'  => 'Start the workshop',
                   'off'      => 'Turn off workshop mode'],
    'lobby'    => ['running'  => 'Start the workshop',
                   'draft'    => 'Back to preparing'],
    'running'  => ['lobby'    => 'Pause and send people to the waiting room',
                   'closed'   => 'Finish the workshop'],
    'closed'   => ['running'  => 'Reopen the workshop',
                   'archived' => 'Archive this session',
                   'off'      => 'Turn off workshop mode'],
    'archived' => ['closed'   => 'Restore this session',
                   'off'      => 'Turn off workshop mode'],
];

public static function actionLabel(string $from, string $to): string
{
    return self::ACTIONS[$from][$to] ?? self::label($to);
}
```

`nextStatusOptions()` wordt dan:

```php
$next[] = ['status' => $target, 'label' => WorkshopService::actionLabel($from, $target)];
```

De statuschip bovenin de balk blijft `LABELS` gebruiken — die zegt terecht wat de toestand *is*. Zo staat er straks *Workshop running* in de chip en *Finish the workshop* op de knop, en die twee spreken elkaar niet meer tegen.

**Nog twee dingen die hierbij horen.**

De bevestigingsflash na een overgang (`BoardController`, rond regel 757) wordt beter als hij de uitkomst benoemt in plaats van de statusnaam te herhalen:

| Naar | Flash |
|---|---|
| `running` | `The workshop is running — participants can add notes now.` |
| `lobby` | `The waiting room is open. Participants see the house rules until you start.` |
| `closed` | `The workshop is finished. The board is read-only and the results page is available.` |
| `draft` | `Back to preparing. Participants see the waiting room.` |
| `archived` | `Session archived. The results page stays available.` |
| `off` | `Workshop mode is off. This is a normal private board again.` |

En `Finish the workshop` is onomkeerbaar-genoeg om een bevestiging te verdienen, want hij bevriest bijdragen voor iedereen en sluit een lopende stemronde (`transitionEffects()`):

> **Finish this workshop?** Nobody can add, edit or vote after this — including you. An open voting round is closed and its results become visible. You can reopen the session afterwards, but a closed round stays closed.

---

### B2 — De betaalbevestiging voor Club Facilitator leidt naar de verkeerde plek

**FEIT.** `app/resources/views/billing/success.html`, regels 21–28 en 57–64. De tekst voor Club Facilitator luidt: *"Workshop mode is being unlocked for your account right now — invite participants with a QR code, run the timer and guide a session from start to finish."* De twee knoppen eronder zijn **Create a note** (`/notes/create`, het publiceren van een sticky note op de wereldwijde wall) en **Manage subscription** (`/settings`).

De pagina belooft workshops en biedt als hoofdactie iets uit een heel ander productcontext aan. Dat geldt overigens ook voor Club Host, waar de tekst over private boards gaat en de knop naar de publieke wall wijst.

**ADVIES.** Maak de vervolgactie planafhankelijk.

| Plan | Primaire knop | Doel | Secundair |
|---|---|---|---|
| `pro` | `Set up your first workshop` | `/boards` | `Read the facilitator guide` (Help Centre) |
| `premium` | `Open your boards` | `/boards` | `Manage subscription` |
| `chosen_few` | `Open your boards` | `/boards` | `Choose your celestial residence` (`/profile`) |

Vervang tegelijk *"Your new perks are being unlocked"* — *perks* staat in geen enkel productdocument. Beter: *"Your plan is active. It can take a few seconds before everything appears."*

**ADVIES (klein).** De foutvariant heeft `Payment received?` als H1. Een vraagteken in een kop laat de lezer denken dat er iets mis is met zijn geld. Volg de regel uit het Playbook (*wat er gebeurde, waarom, wat nu*):

> **We have not seen your payment yet**
> This can take a minute. Your account updates automatically as soon as the payment provider confirms it — you do not have to pay again. If nothing changes within an hour, email farid@stickynotes.club with your order reference.

---

### B3 — `/boards` is de eerste pagina na inloggen en noemt het woord workshop niet

**FEIT.** `HomeController::index()` stuurt elke ingelogde bezoeker door naar `/boards`. `boards/index.html` bevat: H1 *My Boards*, ondertitel *"Private boards for your own sticky notes — and for collaborating with people you invite."*, knop *New Board*, een lege staat *"No boards yet / Create your first private board to get started."* Het woord *workshop* komt op de hele pagina niet voor.

**Tweede-orde-effect.** De net betalende facilitator moet zelf ontdekken dat een workshop geen apart object is maar een modus binnen een bord, en dat je die aanzet in een paneel dat pas zichtbaar wordt nadat je een bord hebt gemaakt en geopend. Dat is architectonisch een goede keuze (besluit B1 in het stappenplan: één borden-tabel, geen tweede boardtype) — maar de interface moet die keuze uitleggen, en dat doet ze niet.

**ADVIES, drie ingrepen.**

*Eén.* Maak de ondertitel planbewust. Voor iemand die mag faciliteren:

> Private boards for your sticky notes, your collaboration and your workshops. Every workshop runs on a board — create one, set the question, then invite the room.

*Twee.* Geef de lege staat een dubbele uitgang voor een facilitator:

> **No boards yet**
> A board is where a workshop happens. Create one, write the question, and share the link when the room is ready.
> [ Create a board for a workshop ] [ Create an empty board ]

Beide knoppen openen hetzelfde formulier; de eerste kiest alvast een geschikt sjabloon (Brainstorm of Retro) en zet `enable=1` voor workshopmodus klaar. **AANNAME**: dit haalt de belangrijkste onzekerheid weg zonder een tweede boardtype te introduceren, en blijft dus binnen besluit B1.

*Drie.* Toon op de bordkaart of een bord een workshop is, en in welke stand. Nu zie je alleen naam, notitieaantal en personen. Een klein chipje `Workshop · Preparing` maakt de lijst bruikbaar voor iemand die zeven sessies per maand draait.

---

### B4 — De app legt workshops nergens uit aan wie ze niet heeft

**FEIT.** De **Workshop**-knop op de bordpagina staat achter `@canFacilitate` (`boards/show.html`:125). Voor Club Member en Club Host bestaat het element niet. Er is geen alternatieve tekst, geen uitleg, geen upsell.

**FEIT.** De enige upsells in de app wijzen naar **Club Host**: het blok op `/boards` (*"Want to collaborate on your boards?"*) en het Share-paneel (*"Sharing and collaboration are Club Host features."*). Club Facilitator wordt in de hele applicatie nergens aangeboden.

**Tweede-orde-effect.** Dit is de spiegel van A2. De homepage verkoopt workshops, de app verkoopt Club Host, en het plan waar de omzet vandaan moet komen wordt binnen het product nooit genoemd. Wie via de wall of een uitnodiging binnenkomt — de grootste toestroom van gratis gebruikers — hoort nooit dat workshops bestaan.

**ADVIES.** Toon de Workshop-knop wél, maar in uitgeschakelde staat met een paneel dat uitlegt wat je mist. De rechtencontrole op de server verandert niet; dit is puur weergave.

> **Workshop**
> Turn this board into a guided session: one shared question everyone sees, a timer the whole room counts down together, and participants who join with a link or QR code — no account, no install.
> Running a workshop is part of Club Facilitator.
> [ See what Club Facilitator includes → ] `/pricing`

Voeg dezelfde regel toe aan het bestaande upsellblok op `/boards`, als tweede zin — niet als tweede blok.

---

### ~~B5 — De vraag van de sessie is het kleinste element op het scherm van de deelnemer~~ — VERVALLEN

> **Getoetst en onjuist gebleken op 22 augustus 2026.** Farid heeft het deelnemersscherm op een telefoon doorlopen tijdens een echte sessie: de instructie zakt daar níet onder een rij chips weg. De bevinding vervalt en actie **S1.11 is geschrapt**.

Wat er wél waar was, en waarom dat niet genoeg was:

**FEIT.** In `_workshop_bar.html` staat de instructie (regels 224–242) in de broncode *onder* de statuschip, de timer, de chips *Input closed*, *Notes hidden until reveal* en *Arranging locked*, de aanwezigheidsteller en de statusknoppen. Voor deelnemers rendert hij als `class="mt-2 text-sm text-gray-800"`.

**AANNAME, ONJUIST.** Ik leidde uit die volgorde en die klassen af dat de vraag op een telefoon onder vier tot zes chips zou wegzakken. Dat klopt niet: voor een deelnemer verschijnt maar een deel van die chips tegelijk — `x-show` verbergt de meeste in de meeste toestanden — en de balk blijft daardoor kort.

**LES VOOR DE REST VAN DIT DOCUMENT.** Broncodevolgorde is geen schermvolgorde zodra `x-show` in het spel is. Elke andere uitspraak in dit rapport over visuele hiërarchie of mobiel gedrag rust op dezelfde soort redenering en verdient dezelfde toets voordat er iemand aan gaat bouwen. Ze staan alle als **AANNAME** gemarkeerd; deze is de eerste die is nagelopen, en hij hield geen stand.

---

### B6 — Eén van de drie sessieknoppen is een zelfstandig naamwoord

**FEIT.** `_workshop_bar.html`, regels 177–197. Drie toggles naast elkaar:

| Uit | Aan |
|---|---|
| `Close input` | `Open input` |
| `Silent brainstorm` | `Reveal all notes` |
| `Lock arranging` | `Allow arranging` |

De eerste en derde zijn werkwoorden. De tweede is een naam. Een facilitator die *Silent brainstorm* leest, kan niet zien of dat betekent "stille brainstorm staat aan" of "klik om er een te beginnen" — en de knop ernaast (*Close input*) leert hem het tweede aan, terwijl de chip erboven (*Notes hidden until reveal*) het eerste suggereert.

**ADVIES.** `Start silent brainstorm` ↔ `Reveal all notes`. Vier extra tekens, en het patroon van de rij klopt weer.

Bijkomend: de chip **Notes hidden until reveal** is jargon voor iemand die dertig seconden geleden is binnengekomen. Beter: **Everyone sees only their own notes**.

---

### B7 — Kleinere microcopy in de balk en de filterbalk

**FEIT / ADVIES**, alles in `_workshop_bar.html` en `_notes_area.html`:

| Nu | Waarom het wringt | Voorstel |
|---|---|---|
| `Clear` (timer, r.167) | Wist wat? De buren heten Pause / Resume / +1 min. | `Stop timer` |
| `Start` (naast het minutenveld, r.151) | Tweede "Start" in dezelfde balk, naast de statusknop die straks *Start the workshop* heet. | `Set timer` |
| `Arranging locked` (r.58) | Zelfstandignaamwoordconstructie. | `Moving notes is locked` |
| `3 online of 8` (r.100–103) | Leest als een halve zin. | `3 of 8 here` |
| `time's up` (r.42) | Prima, maar de rest van de balk gebruikt geen samentrekkingen. | `Time is up` |
| `Clear` (tagfilter, `_notes_area.html`:135) | Derde betekenis van hetzelfde woord. | `Show all` |
| `3 votes left of 3` (`_notes_area.html`:31–32) | Het tweede getal voegt niets toe zolang je nog niets hebt gestemd. | `3 of 3 votes left` |

---

### B8 — Foutmeldingen verdwijnen na vijf seconden

**FEIT.** `layout.html`, regel 342: `x-init="setTimeout(() => show = false, 5000)"` staat om **alle** flashsoorten heen, dus ook om `flash.error`. Eén `x-data` omhult bovendien alle vier de blokken, zodat één klik op één sluitknop ze allemaal wegneemt.

**FEIT.** Het Playbook zegt: *"Success messages confirm the result and disappear without blocking work"* — over succes, niet over fouten. En: *"Error messages follow: what happened, why if known, and what the user can do next."* Een melding die verdwijnt voordat je hem gelezen hebt, doet dat laatste niet.

**ADVIES.** Splits de timer: `success` en `info` verdwijnen na 5 seconden, `error` en `warning` blijven staan tot de gebruiker ze wegklikt. Dit is precies de regel die `boardApi.js` al kent (`isFatalError()` maakt daar meldingen sticky) — de flashlaag loopt achter op de eigen standaard van het project.

---

### B9 — Een onbekende foutcode komt ongefilterd op het scherm

**FEIT.** `boardApi.js`, regels 116–118:

```js
if (json && json.error && json.error !== 'conflict') {
    return json.error
}
```

Een code die niet in `ERROR_MESSAGES` staat, wordt letterlijk aan de gebruiker getoond.

**ADVIES.** Vervang door de bestaande vangnettekst en log de code naar de console:

```js
if (json && json.error && json.error !== 'conflict') {
    console.warn('Unmapped board error code:', json.error)
    return fallback || "Something went wrong — try again"
}
```

---

### B10 — Bevestigingsteksten die de toon of de gevolgen missen

**FEIT / ADVIES:**

| Bestand | Nu | Voorstel |
|---|---|---|
| `show.html`:678 | `Create a new link and kill this one? Anyone still using the old link or QR code loses access.` | `Replace this workshop link? The current link and QR code stop working immediately. Anyone who has already joined stays in the session.` |
| `show.html`:148 | `Are you sure you want to leave this board?` | `Leave this board? You lose access to it. The sticky notes and comments you added stay on the board.` |
| `show.html`:494 | `Revoke this share link? Anyone using it will lose access.` | Goed. Alleen `Revoke this link? Everyone using it loses access immediately. Their contributions stay on the board.` |

De regel eronder is dezelfde in alle drie: de Constitution eist dat een waarschuwing benoemt *wat verdwijnt*. "Loses access" zegt niet of de bijdragen ook weg zijn — en dat is de vraag die iemand stelt voordat hij op de knop drukt.

---

### B11 — Het deelnemersscherm heet geen workshop en toont twee namen voor één persoon

**FEIT.** `boards/shared.html`:14–24. Het chipje bovenaan is `🔗 Shared board`. Daaronder: `Board by {{ @boardOwner.display_name ?: @boardOwner.username }} • 12 notes`.

Voor een workshopdeelnemer betekent dat: hij is via een QR-code op iets beland dat *Shared board* heet, terwijl hem een workshop is aangekondigd; en hij ziet de gebruikersnaam van de eigenaar terwijl de balk eronder *facilitated by* met de ingevulde facilitatornaam toont. Twee namen voor dezelfde persoon op één scherm. Bij `anonymous_notes` is dat extra vreemd: de namen bij de notes zijn dan verborgen, en de eigenaar staat bovenaan met naam en toenaam.

**ADVIES.** Als `WorkshopService::isWorkshop($board)`: toon `🎯 Workshop` in plaats van `🔗 Shared board`, en vervang de metaregel door `Facilitated by {{ @workshopFacilitatorName ?: @boardOwner.display_name }} · {{ n }} sticky notes`. Buiten workshopmodus blijft alles zoals het is.

---

### B12 — De resultatenpagina is het beste verkoopmoment van het product en verkoopt niets

**FEIT.** `boards/results.html` bevat: statuschip, bordnaam, instructie, metaregel, printknop, Markdown-knop, ranking, groepen en alle notes. Er staat geen enkele verwijzing naar StickyNotes.club, geen uitleg wat dit is, en geen actie voor de lezer.

**FEIT.** De pagina is bereikbaar op `/b/@slug/results` én `/s/@token/results`, is zichtbaar voor iedereen zodra de sessie is afgerond, en is expliciet bedoeld om te delen met mensen die er niet bij waren (`07`, sectie 8; Playbook: *"A result is what remains"*).

**Tweede-orde-effect.** Een manager of collega die deze pagina toegestuurd krijgt, is de best gekwalificeerde lead die dit product kan krijgen: hij ziet het resultaat van een goed gelopen sessie, met echte inhoud, voordat hij ooit een marketingpagina heeft gezien. Op dit moment kan hij daar niets mee.

**ADVIES.** Eén rustige strook onder aan de pagina, buiten de print-CSS (`class="no-print"`), alleen zichtbaar voor wie niet is ingelogd:

> ### This session ran on StickyNotes.club
> One facilitator invites the room with a link or QR code. No accounts, no installs for participants. The result stays on this page.
> [ See how it works → ] `/` &nbsp;·&nbsp; [ Read the facilitator guide → ] Help Centre

**FEIT (klein, apart).** Regel 72 gebruikt `date('j F Y', …)` — *21 August 2026*. De Constitution schrijft **YYYY/MM/DD** voor en `boards/index.html` en de share-links gebruiken `Y/m/d`. Twee datumnotaties binnen één product. Kies er één; als het `j F Y` wordt, hoort dat besluit in de Constitution.

---

### B13 — De groeimotor via deelnemers wordt niet aangezet

**FEIT.** `boards/shared.html`:158–165. Voor uitgelogde bezoekers staat helemaal onderaan:

> Made with **StickyNotes.club** — create your own sticky notes board for free.

Dat is de volledige acquisitie richting maximaal vijftig deelnemers per sessie. De link gaat naar `/`, de marketinghomepage, waar de enige zichtbare prijs €14,99 is — terwijl de regel *for free* belooft.

**ADVIES.** Verplaats de uitnodiging naar het moment waarop hij verdiend is: **na afloop van de sessie**, wanneer de deelnemer de resultaten heeft gezien. Op dat moment tonen, in het gedeelde bord én op de resultatenpagina:

> **That was a StickyNotes.club workshop.**
> Want to run one yourself? One person sets it up; everyone else joins with a link. Participants never need an account.
> [ See how it works → ]

En laat de huidige regel tijdens de sessie staan zoals hij is: klein, grijs, niet in de weg. Iemand die aan het meedoen is, moet niet worden verkocht.

**BESLUIT NODIG.** Zie §8, besluit 5 — dit is de enige plek in dit document waar ik voorstel om marketing te richten op mensen die geen klant zijn en er niet om hebben gevraagd. Het past binnen *Calm software beats noisy software* zolang het één blok is, ná afloop, zonder herhaling.

---

## 5. Bevindingen — C. Content, toon en terminologie

### C1 — De wereldwijde wall heeft twaalf namen

**FEIT.** `wall.html`, regels 22–42. Een inline script overschrijft de server-gerenderde H2 met een willekeurige keuze uit twaalf titels: *Sticky Notes From Another Planet*, *Intergalactic Sticky Notes Board*, *Sticky Notes Across the Universe*, *The Universal Sticky Wall*, *Space Notes: A Global Sticky Collection*, *Cosmic Sticky Notes*, *Notes Beyond Earth*, *The Galactic Sticky Stream*, *Planet of Sticky Notes*, *Sticky Notes: No Boundaries*, *The Interstellar Note Board*, *Sticky Notes From Everywhere*.

**FEIT.** De Public Communication Specification §11 schrijft: *"Do not introduce a new public label to make a message sound more exciting."* De canonieke term is **worldwide wall**. De Constitution noemt onder de drift-signalen: *"several names exist for the same concept."*

**FEIT.** De crawler ziet de server-gerenderde titel, de bezoeker een andere — bij elke pageview.

**ADVIES.** Vervang door één vaste kop. Het speelse element mag blijven bestaan; het hoort alleen niet in de naam van het hoofdobject van de pagina.

> ## Sticky notes from all over the world
> and a few from further away 🌙

**BESLUIT NODIG** als je hieraan gehecht bent — zie §8, besluit 6.

---

### C2 — Amerikaans Engels op twee plaatsen

**FEIT.** `wall.html`:9 — *"Post **colorful** sticky notes"*. `pricing.html`:99 — *"Post instant photos with **colorful** frames"*. De rest van het product is consequent Brits (organise, colour, licence), en de E-02-audit van 21 augustus meldt dat negen templates hierop zijn gecorrigeerd. Deze twee zijn blijven staan.

**ADVIES.** `colourful`. En in dezelfde regel: *instant photos* → **Instant Photos** (hoofdletters, canonieke term uit de Constitution).

---

### C3 — Verboden superlatieven

**FEIT.** De Public Communication Specification §9 verbiedt superlatieven en noemt **perfect** met naam. In het product staat:

- `pricing.html`:21 — *"**Perfect** for getting started"*
- `PricingController.php`:18 (meta description) — *"Choose your **perfect** plan at StickyNotes.club"*
- `pricing.html`:93 — *"**Beautiful** premium pastel note colours"*

**ADVIES.** *"A good place to start"*, *"Find the plan that fits how you work"*, *"Pastel sticky-note colours"*.

---

### C4 — *like* en *heart* zijn hetzelfde en heten anders

**FEIT.** De canonieke term is **heart** (Constitution: *"a private-board heart is a personal toggle"*, publieke notes hebben een *heart count*). In de interface staat:

- `pricing.html`:43 — *"**Like** and share notes with others"*
- `layout.html` accountmenu en mobiel menu — *"**Liked** notes"*, route `/wol`
- de facilitatorbalk en de bordpanelen — consequent *hearts*

**ADVIES.** Één woord. `Hearted notes` in het menu (of `Notes you hearted`), en *"Heart and share sticky notes"* op de prijspagina. De route `/wol` mag blijven; die is niet zichtbaar in de tekst.

---

### C5 — *note* waar *sticky note* verplicht is

**FEIT.** Het Playbook: *"**Sticky note** is mandatory in titles, navigation, buttons, first mentions and formal definitions. **Note** is allowed only as a natural shorthand after the object is clear."*

In navigatie en knoppen staat nu: `My notes`, `Create note`, `Liked notes`, `New note` (tooltip), `Create a new note` (aria-label), `Add Note` (bord en gedeelde weergave), `Add a note to this board` (paneelkop), `📝 3 notes` (bordkaart), `12 notes` (bordkop en resultatenpagina).

**ADVIES.** Corrigeer in elk geval de vier plekken waar de regel hard is — navigatie en knoppen:

| Nu | Voorstel |
|---|---|
| `My notes` | `My sticky notes` |
| `Create note` / `New note` / `Create a new note` | `New sticky note` (overal hetzelfde, ook als aria-label) |
| `Liked notes` | `Hearted sticky notes` |
| `Add Note` | `Add a sticky note` |

Binnen de tekst van een paneel of een teller mag *notes* blijven staan; daar is het object al vastgesteld.

---

### C6 — Hoofdlettergebruik loopt door elkaar

**FEIT.** Naast elkaar in dezelfde interface: `My Boards`, `New Board`, `Create Board`, `Board Settings`, `Add Note`, `Create Account`, `Confirm Password` (Title Case) tegenover `Choose your plan`, `Create view link`, `Create workshop link`, `Set up the session`, `Get people in`, `Run the session`, `Close voting`, `Start voting` (sentence case).

**ADVIES.** Sentence case overal, behalve productnamen (Club Member, Club Host, Club Facilitator, Chosen Few, Instant Photo, View link, Post link). Dat is bovendien de stijl die het Playbook impliceert met zijn eigen voorbeelden (*Create board*, *Send invitation*, *Delete note*).

---

### C7 — De About-pagina beschrijft het product van vóór D-30

**FEIT.** `app/resources/pages/about.md` bevat het woord *workshop* nul keer. De pagina opent met de wereldwijde wall, behandelt private boards als tweede context, en beschrijft de reis van een idee als *Capture → Share → Discuss → Organise → Collaborate → Execute*.

**FEIT.** Besluit **D-30**, genomen op 21 augustus 2026, luidt: *"Facilitated sessions are the primary use of StickyNotes.club and the lead commercial story."*

**Tweede-orde-effect.** Voor een product zonder testimonials en zonder bekende naam is de About-pagina de belangrijkste vertrouwenspagina die er is: daar staat wie je bent, waar het draait en waarom het bestaat. Als die pagina een ander product beschrijft dan de homepage, is dat precies de plek waar twijfel wordt bevestigd in plaats van weggenomen.

**ADVIES.** Herschrijf de eerste twee secties zodat sessies vooraan staan, **zonder** de belofte te vervangen — D-30 zegt uitdrukkelijk dat *A place where ideas can grow together* de paraplu blijft. Concreet voorstel voor de opening:

> # About StickyNotes.club
>
> StickyNotes.club is a place where ideas can grow together.
>
> Most of the time that happens in a room: a retrospective, a class, a training group, a team deciding what to do next. Getting a group to think together usually costs more setup than the thinking is worth — accounts, installs, a licence per seat, a tool nobody opens again afterwards. StickyNotes.club lets one person start a session in minutes, lets everyone else join with a link, and leaves a result that outlives the meeting.
>
> Sometimes an idea starts smaller: a quick thought you want to keep, or share with the world. That still works here too.

Daarna kunnen *Public inspires. Private builds.*, *Keeping things simple*, *How it started* en *Who is behind StickyNotes.club* vrijwel ongewijzigd blijven.

**FEIT (klein).** Regel 55 gebruikt `farid﹫stickynotes.club` met een lookalike-teken in plaats van een @. Dat is niet te kopiëren, niet aanklikbaar, en een schermlezer maakt er iets onbegrijpelijks van. Voor de contactweg van een product zonder supportafdeling is dat te veel offer voor te weinig spambescherming. Maak er een gewone `mailto:`-link van, of verwijs naar het contactadres in het Help Centre.

---

### C8 — De wall werft de verkeerde gebruiker

**FEIT.** `wall.html`:96–109:

> **Want to see more notes?**
> Create a free account and join our community of note writers around the world!
> [ Sign up for free ] [ Log in → ]

**FEIT.** Wat een account op deze pagina daadwerkelijk verandert: `HomeController::wall()` toont 12 notes per pagina voor uitgelogde bezoekers en 48 voor ingelogde.

**Tweede-orde-effect.** De belofte is technisch waar maar leest als een muur, en hij trekt precies de gebruiker aan die nooit gaat betalen: iemand die meer publieke notes wil lezen. Ondertussen staat op dezelfde pagina één alinea over workshops, halverwege, zonder gewicht.

**ADVIES.** Vervang het blok door een uitnodiging die iets doet in plaats van iets belooft, en laat het aantal notes met rust:

> ### Add your own sticky note
> A free Club Member account lets you publish sticky notes on the worldwide wall, keep drafts and take part on any board you are invited to.
> [ Create a free account ] [ Log in ]

En schrap het uitroepteken, *our community of note writers* en de dubbele CTA-blokken (zie A4 en C9).

---

### C9 — Zeven CTA's op één pagina

**FEIT.** `/wall` toont voor een uitgelogde bezoeker: *Get started — it's free*, *Log in →*, *All countries →*, *See how workshops work*, *Pricing →*, *Sign up for free*, *Log in →* (nogmaals). Twee daarvan zijn hetzelfde met een ander label, twee andere zijn letterlijk hetzelfde.

**FEIT.** Het Playbook: *"Give one screen or component one dominant next action."*

**ADVIES.** Eén CTA-blok bovenaan (registreren + inloggen als tekstlink), één blok onderaan (het workshopblok uit C8/A6), en verder niets. De landenchips en *All countries →* zijn navigatie, geen CTA, en mogen blijven.

---

### C10 — Toon: drie regels die uit de stijl vallen

**FEIT / ADVIES.** Alle drie in strijd met §9 van de Public Communication Specification (*avoid hype without evidence, corporate language, filler*):

| Bestand | Nu | Voorstel |
|---|---|---|
| `show.html`:514 | *"Share links let anyone view this board — or even post sticky notes on it — without you emailing a thing. Sharing and collaboration are Club Host features."* | *"A share link lets people open this board without an invitation — read-only, or with permission to add sticky notes. Sharing is part of Club Host."* |
| `wall.html`:99 | *"join our community of note writers around the world!"* | zie C8 |
| `billing/success.html`:44 | *"Your new perks are being unlocked"* | *"Your plan is active."* |

---

## 6. Bevindingen — D. Vindbaarheid, vertrouwen en meten

### D1 — `robots.txt` sluit elke publieke sticky note uit ★

**FEIT.** `www/robots.txt` bevat `Disallow: /notes`. In robots.txt is dat een **prefixregel**: hij dekt `/notes`, `/notes/create`, én `/notes/123` — de publieke detailpagina van elke sticky note.

**FEIT.** `NoteController::show()` vereist géén login voor een publieke note; alleen voor een Draft. `GET /notes/@id` is dus een openbare pagina.

**FEIT.** De Constitution formuleert het indexeren als productbelofte: *"Public sticky notes and Instant Photos may be crawled, indexed, cached and shown by external search engines."* De interface waarschuwt gebruikers hiervoor vóór publicatie. Het product doet vervolgens het tegenovergestelde.

**Tweede-orde-effect.** De hele long-tail-laag van het product — elke publieke note, elke landenpagina die ernaar linkt — bestaat niet voor zoekmachines. Dat is de goedkoopste organische instroom die dit product heeft en hij staat uit.

**ADVIES.** Google en Bing hanteren de langste overeenkomende regel, dus dit werkt:

```
# Private/authenticated sections
Disallow: /admin
Disallow: /api/
Disallow: /profile
Disallow: /settings
Disallow: /wol
Disallow: /verify-email
Disallow: /reset-password
Disallow: /forgot-password

# Sticky notes: the list and the editors are private, the notes themselves are public
Disallow: /notes
Disallow: /notes/create
Disallow: /notes/*/edit
Allow: /notes/

Sitemap: https://stickynotes.club/sitemap.xml
```

**Belangrijk:** controleer daarna in Google Search Console met de robots-tester of `/notes/123` als *toegestaan* wordt gerapporteerd. En zorg dat Drafts niet per ongeluk bereikbaar zijn — dat is nu al goed geregeld in de controller, maar het wordt met deze wijziging belangrijker.

**BESLUIT NODIG.** Zie §8, besluit 7 — indexeren van gebruikersinhoud brengt moderatieverantwoordelijkheid met zich mee, en de Report-knop uit de D-24-spec bestaat nog niet.

---

### D2 — De sitemap is statisch en telt acht URL's

**FEIT.** `www/sitemap.xml` is een handgeschreven bestand met `/`, `/wall`, `/pricing`, `/register`, `/login`, `/about`, `/terms`, `/privacy`. Er staan geen landenpagina's (`/c`, `/c/@country`) in en geen notepagina's.

**ADVIES.** Genereer hem. Eén route `GET /sitemap.xml` in `routes.php` en een kleine controller die de statische pagina's, `/c`, alle landenpagina's en alle publieke notes uitschrijft, met `lastmod` uit `updated_at`. Haal `/login` eruit (die hoort niet in een sitemap) en overweeg `/register` te laten staan.

---

### D3 — Er is geen footer

**FEIT.** Het enige `<footer>`-element in `layout.html` (regels ~485–490) is een vaste pil rechtsonder:

```
Number of active users: {{ @activeUserCount }} • Total notes: {{ @totalNoteCount }}
```

**FEIT.** Terms en Privacy zijn daardoor alleen bereikbaar vanaf: de laatste sectie van de homepage (als kleine tekstregel), het registratieformulier, het join-scherm en het roze CTA-blok onderaan `/wall` voor uitgelogde bezoekers. Op `/pricing` — de pagina die naar een betaling leidt — staat geen enkele link naar de voorwaarden. Voor een ingelogde gebruiker zijn ze nergens in de interface te vinden.

**Tweede-orde-effect.** Dit is tegelijk een vertrouwenskwestie (een betaalpagina zonder voorwaarden leest als een pagina die iets verbergt) en een risico voor een EU-dienst die abonnementen verkoopt aan consumenten en zakelijke afnemers.

**ADVIES.** Eén echte footer in `layout.html`, op elke pagina, met vier kolommen: **Product** (Worldwide wall, Countries, Pricing, How it works), **Help** (Help Centre, Contact), **Legal** (Terms, Privacy, Community Guidelines), **Account** (Log in / Create account, of Settings als je bent ingelogd). Daaronder één regel: `A place where ideas can grow together. · Built and run in the Netherlands.`

---

### D4 — De gebruikersteller staat op elke pagina en werkt tegen je

**FEIT.** Dezelfde vaste pil toont *Number of active users: N • Total notes: N* op **elke** pagina, inclusief `/`, `/pricing` en de checkoutbevestiging.

**FEIT.** Het frontpagevoorstel zegt expliciet: *"Geen user- of note-counters in de primaire conversieflow zolang de aantallen klein zijn."*

**AANNAME.** Bij een pre-launchproduct zijn die getallen klein, en een klein getal naast een prijs van €14,99 is een argument om niet te kopen. Een groot getal zou een goed vertrouwenssignaal zijn — dit is er het spiegelbeeld van.

**ADVIES.** Haal de teller uit de vaste balk. Als je hem wilt houden: alleen op `/wall`, waar het over de community gaat, en pas weer op de commerciële pagina's zodra de getallen indruk maken.

---

### D5 — Meta titles en descriptions van de sleutelpagina's

**FEIT / ADVIES.** De homepage is goed (`Run a focused workshop in minutes`). De rest niet:

| Pagina | Nu | Voorstel |
|---|---|---|
| `/pricing` | title: `Pricing Plans`<br>desc: `Choose your perfect plan at StickyNotes.club. From a free Club Member account to Club Host and Club Facilitator — pick the plan that fits.` | title: `Pricing — one facilitator, no seat licences`<br>desc: `Run workshops for up to 50 people from € 14.99 a month. Participants join with a link or QR code and never pay or register. Free plan available.` |
| `/wall` | title: `The public sticky notes wall`<br>desc: `Read sticky notes from people all over the world…` | title: `The worldwide sticky notes wall` (canonieke term)<br>desc: goed zoals hij is |
| `/about` | onbekend, zie `PageController` | title: `About StickyNotes.club`<br>desc: `An independent product from the Netherlands for running focused workshops, keeping private boards and sharing a thought with the world.` |

Let op de lengte: titles onder 60 tekens, descriptions onder 155.

**FEIT (klein).** `layout.html` gebruikt één vast `og:image` (`/img/stickynotes-og.jpg`) voor elke pagina, inclusief de resultatenpagina. Een gedeelde resultatenpagina is precies het moment waarop een eigen preview iets zou doen. Lage prioriteit.

---

### D6 — Core Web Vitals: wat ik uit de code kan zeggen

**FEIT.** De homepage doet het goed: `fetchpriority="high"` op het herobeeld, `width`/`height` op alle vijf de beelden (dus geen layout shift), `loading="lazy"` op alles behalve de hero, WebP, en het lettertype is self-hosted met `font-display: swap`. Alpine laadt met `defer`.

**FEIT.** Er zit geen `srcset`/`sizes` op de beelden, terwijl `07` daarom vraagt. Het herobeeld is 1440×1076 en wordt op een telefoon in volle breedte geladen.

**FEIT.** Ik heb geen laadtijden gemeten. **Alles hierboven is codeanalyse, geen meting.**

**ADVIES.** Voeg `srcset` toe met een 720px-variant voor mobiel; dat is de enige duidelijke winst die ik uit de code kan afleiden. Meet daarna één keer met PageSpeed Insights op `/` en `/pricing` en beslis pas dan of er meer nodig is.

---

### D7 — Er wordt niets gemeten ★

**FEIT.** In `app/resources/views`, `app/resources/js` en `www/index.php` komt geen enkele verwijzing voor naar een analyticsscript, event-tracking of een teller. Het frontpagevoorstel definieert vijf events (`homepage_workshop_cta_clicked`, `homepage_how_it_works_clicked`, `homepage_public_wall_clicked`, `homepage_pricing_clicked`, `facilitator_registration_started`) en een funnel (`Homepage → facilitator registration → workshop created → first external participant joined → workshop started`). Geen ervan bestaat.

**Tweede-orde-effect.** Elke wijziging in dit document is dan een gok. Je kunt niet zien of de nieuwe CTA werkt, waar mensen afhaken tussen registratie en betaling, of hoeveel deelnemers een sessie werkelijk haalt.

**ADVIES.** Kies iets kleins en privacyvriendelijks (Plausible of een self-hosted Umami) zodat het zonder cookiebanner kan, en meet in eerste instantie alleen de vijf events plus de vier funnelstappen. **Doe dit vóór de andere wijzigingen**, anders weet je over een maand nog steeds niets.

---

## 7. Bevindingen — E. Prijzen en checkout

### E1 — Vier gelijkwaardige kaarten, en de grap weegt even zwaar als het hoofdplan

**FEIT.** `pricing.html`. Club Facilitator heeft `border-2 border-pastel-mint` met een gradient. Chosen Few (€ 999.999,99) heeft `border-2 border-pastel-purple` met een gradient. Visueel even zwaar.

**FEIT.** `07` zegt over Chosen Few: *"mag op de prijspagina een speels element blijven, maar hoort niet in de primaire conversieflow."*

**ADVIES.** Laat Chosen Few staan — hij past bij het merk — maar haal het gewicht eraf: gewone rand, geen gradient, en zet hem visueel apart (bijvoorbeeld als smallere kaart of onder een streepje met de kop *And for the very few*). Het hoofdplan moet de zwaarste kaart op de pagina zijn.

---

### E2 — Geen vergelijking, geen limieten naast elkaar

**FEIT.** De vier kaarten gebruiken elk hun eigen formulering van dezelfde limieten (*Post up to 2 sticky notes per day*, *Post up to 12 sticky notes per day (6x more)*, *Everything in Club Host*). Er is geen tabel waarin je bordlimiet, dagelijkse publicatielimiet, deelnemersplafond, share links en workshopcontrols naast elkaar ziet.

**FEIT.** Dit staat al open in het dossier: de vier-tier-vergelijking is het grootste resterende deel van V-05.

**ADVIES.** Eén compacte tabel onder de kaarten, zes rijen. Getallen uit de settings, nooit uit de template — dezelfde regel die op de homepage al geldt.

---

### E3 — Btw, opzeggen en terugbetalen staan niet bij de knop

**FEIT.** Bij elke betaalde kaart staat *"/month, ex. VAT"* en verder niets. Geen opzegregel, geen proefperiode, geen terugbetalingsvoorwaarde, geen betaalmethoden, geen link naar de voorwaarden.

**ADVIES.** Eén regel direct onder elke betaalknop (zie ook A7):

> Monthly. Cancel at any time from your settings. VAT is added at checkout where it applies.

**BESLUIT NODIG.** §8, besluit 4.

---

### E4 — Het hoofdplan verdwijnt als de omgevingsvariabele leeg is

**FEIT.** De Club Facilitator-kaart staat in `pricing.html` binnen `<check if="{{ @proPurchasable }}">`. Zonder `CREEM_PRODUCT_PRO` verdwijnt de kaart volledig, terwijl de homepage onveranderd volledig over workshops gaat (het prijsblok daar is hardcoded en verdwijnt níet) en de navigatieknop naar `/register?plan=pro` blijft wijzen (zie A9).

**AANNAME.** Dat is een randgeval, maar wel een met maximale schade: de bezoeker leest een pagina over workshops en vindt op de prijspagina geen enkele manier om er een te draaien.

**ADVIES.** Toon de kaart altijd, maar vervang de knop door `Coming soon` of `Contact us` wanneer het plan niet koopbaar is. Dat is bovendien wat de Public Communication Specification §6 voorschrijft voor niet-beschikbare functionaliteit: label het expliciet in plaats van het te verbergen.

---

## 8. Het actieplan

### Leeswijzer

**Impact** is de verwachte invloed op conversie of activatie. **Effort** is een schatting van mijn kant, in uren, voor iemand die deze codebase kent. Alles onder S0 en S1 is tekst of enkele regels code; niets ervan raakt de database of het rechtenmodel.

---

### Sprint 0 — Vandaag of morgen (samen ± 4–6 uur)

Dit zijn de ingrepen waarvan ik zou zeggen: als je vandaag maar één ding doet, doe dan deze lijst. Ze zijn allemaal klein, geen ervan is omstreden, en samen halen ze de vier naden uit §1 grotendeels weg.

| # | Actie | Bevinding | Bestand(en) | Effort |
|---|---|---|---|---|
| S0.1 | Statusknoppen actielabels geven (`ACTIONS`-tabel + `actionLabel()`) | **B1** | `Services/WorkshopService.php`, `Controllers/BoardController.php` | 1 u |
| S0.2 | Bevestigingsflashes per overgang herschrijven | B1 | `Controllers/BoardController.php` ~757 | 30 m |
| S0.3 | Bevestigingsdialoog bij *Finish the workshop* | B1 | `_workshop_bar.html`, `boards/show.html` | 30 m |
| S0.4 | Betaalbevestiging: knoppen per plan naar `/boards` | **B2** | `billing/success.html` | 30 m |
| S0.5 | `robots.txt` corrigeren zodat publieke notes indexeerbaar zijn | **D1** | `www/robots.txt` | 10 m |
| S0.6 | *Best value* verplaatsen naar Club Facilitator | **A2** | `pricing.html` | 10 m |
| S0.7 | Foutflashes niet meer automatisch laten verdwijnen | B8 | `layout.html` | 15 m |
| S0.8 | `Silent brainstorm` → `Start silent brainstorm`; `Clear` → `Stop timer`; `Set timer`; `3 of 8 here` | B6, B7 | `_workshop_bar.html` | 20 m |
| S0.9 | Superlatieven en Amerikaans Engels weg (`perfect` 2×, `colorful` 2×, `Beautiful`) | C2, C3 | `pricing.html`, `wall.html`, `PricingController.php` | 15 m |
| S0.10 | Willekeurige walltitels vervangen door één vaste kop | C1 | `wall.html` | 15 m |
| S0.11 | Onbekende foutcode niet meer rauw tonen | B9 | `boardApi.js` | 10 m |
| S0.12 | Gebruikersteller weghalen van `/` en `/pricing` | D4 | `layout.html` | 15 m |

**Definition of done voor sprint 0:** `php scripts/check-templates.php`, `php scripts/check-render.php` en `php scripts/test-board-rights.php` groen, plus één doorloop met twee browsers over de statusovergangen (de labels zijn nu anders in de balk én in het paneel — die twee moeten hetzelfde zeggen).

---

### Sprint 1 — Deze week (samen ± 1,5 dag)

| # | Actie | Bevinding | Bestand(en) | Effort |
|---|---|---|---|---|
| S1.1 | **Analytics installeren** en de vijf events + vier funnelstappen meten | **D7** | `layout.html`, CTA's | 3 u |
| S1.2 | Labelregister toepassen (zie §9): één woord per actie, overal | A4, C4, C5, C6 | ± 10 templates | 2 u |
| S1.3 | Echte footer op elke pagina | **D3** | `layout.html` | 1,5 u |
| S1.4 | `/boards`: workshopcontext in ondertitel, lege staat en bordkaart | **B3** | `boards/index.html`, `BoardController` | 2 u |
| S1.5 | Registratiepagina planbewust maken | **A3** | `auth/register.html`, `AuthController` | 1 u |
| S1.6 | Plankeuze meesturen met de verificatielink | A8 | `AuthController` | 1,5 u |
| S1.7 | Eerste-login-flash in plaats van *Welcome back!* | A8 | `AuthController` | 20 m |
| S1.8 | Workshop-upsell voor Club Member en Club Host | **B4** | `boards/show.html`, `boards/index.html` | 1,5 u |
| S1.9 | CTA in de navigatie echt primair maken, desktop én mobiel | A5 | `layout.html` | 1 u |
| S1.10 | `facilitatorCta` naar `BaseController` en gebruiken in de nav | A9 | `BaseController`, `layout.html` | 20 m |
| ~~S1.11~~ | ~~Instructie boven de chips voor deelnemers~~ — **geschrapt op 22-08: op een telefoon getoetst, de bevinding klopte niet** | ~~B5~~ | — | — |
| S1.12 | Bevestigingsteksten *kill this one* / *leave board* / *revoke* | B10 | `boards/show.html` | 30 m |

---

### Sprint 2 — Voor de launch (samen ± 2 dagen)

| # | Actie | Bevinding | Effort |
|---|---|---|---|
| S2.1 | Resultatenpagina: afsluitende strook voor uitgelogde lezers | **B12** | 1 u |
| S2.2 | Deelnemersuitnodiging ná afloop van de sessie | **B13** | 2 u |
| S2.3 | About-pagina herschrijven naar D-30 | **C7** | 1,5 u |
| S2.4 | Gebruikssituaties op de homepage (retro, les, planning, community) | **A6** | 1,5 u |
| S2.5 | Vertrouwensregel onder elke betaalknop + hostinginformatie in de footer | A7, E3 | 45 m |
| S2.6 | Vergelijkingstabel op `/pricing`, getallen uit de settings | E2 | 3 u |
| S2.7 | Chosen Few visueel ondergeschikt maken | E1 | 30 m |
| S2.8 | Club Facilitator-kaart altijd tonen, knop wisselt bij niet-koopbaar | E4 | 45 m |
| S2.9 | Meta titles en descriptions herschrijven | D5 | 45 m |
| S2.10 | Gedeelde weergave: workshopchip en één naam voor de facilitator | B11 | 1 u |
| S2.11 | `/wall`: één CTA-blok, nieuwe tekst, geen dubbele knoppen | C8, C9 | 1 u |
| S2.12 | Datumnotatie gelijktrekken (resultatenpagina versus de rest) | B12 | 20 m |

---

### Later — na de eerste meetweek

| # | Actie | Bevinding |
|---|---|---|
| L1 | Sitemap genereren in plaats van handmatig bijhouden | D2 |
| L2 | `srcset`/`sizes` op de homepagebeelden, daarna één PageSpeed-meting | D6 |
| L3 | `og:image` per pagina, met een eigen beeld voor de resultatenpagina | D5 |
| L4 | Landingspagina's per situatie (retrospective, onderwijs, training) | A6 |
| L5 | Testimonials, zodra er echte zijn — en geen dag eerder | `07` open vraag 5 |
| L6 | A/B-test op de hero-copy en het CTA-label | `07` |

---

## 9. Het labelregister

Dit is de tabel waarnaar S1.2 verwijst. Eén canoniek label per actie, alle andere varianten vervallen.

| Actie | Canoniek label | Vervangt |
|---|---|---|
| Account aanmaken | **Create a free account** | Create Account, Get started today, Get started — it's free, Sign up for free, Create free account |
| Inloggen | **Log in** | Login, Sign in |
| Uitloggen | **Log out** | Sign out |
| Profiel | **Profile** | My Profile |
| Help | **Help Centre** | Help |
| Voorwaarden | **Terms** (linktekst) / *Terms of Service* (paginatitel) | Terms and Conditions |
| Publieke sticky note maken | **New sticky note** | Create note, New note, Create a new note |
| Eigen sticky notes | **My sticky notes** | My notes |
| Gehartte notes | **Hearted sticky notes** | Liked notes |
| Sticky note op een bord | **Add a sticky note** | Add Note |
| Bord maken | **Create a board** | New Board, Create Board |
| Bordinstellingen | **Board settings** | Board Settings |
| Bordenoverzicht | **My boards** | My Boards |
| Waarderen | **heart** (werkwoord en zelfstandig naamwoord) | like |
| Publieke wall | **worldwide wall** | de twaalf willekeurige titels |

**Regel voor hoofdletters:** sentence case, behalve productnamen (Club Member, Club Host, Club Facilitator, Chosen Few, Instant Photo, View link, Post link, Workshop link).

**Regel voor samentrekkingen:** de foutteksten in `boardApi.js` gebruiken ze (*You're*, *hasn't*, *can't*), de marketingpagina's niet. Dat mag, maar leg het vast: **samentrekkingen in de interface, voluit in marketing en beleid.** Nu is het toeval, en toeval wordt bij de volgende tekst een inconsistentie.

---

## 10. Besluiten die van jou zijn

| # | Besluit | Waarom het niet van mij is | Belangrijkste tweede-orde-effecten |
|---|---|---|---|
| 1 | ~~**Komt er een risicoloze ingang naar workshops?**~~ (A1) — **genomen 24-08: zichtbaarheid, geen nieuw product. Zie §0b.** | Prijsstrategie. | *Gratis plan zichtbaar maken op `/`* — kost niets, is al waar, maar leidt aandacht naar een plan dat geen workshops kan; je vangt de twijfelaar en verliest een deel van de directe kopers. *Eén gratis workshop per account* — het sterkste bewijs dat je hebt, want het product overtuigt in gebruik; kost bouwwerk (een teller) en je moet beslissen wat er met het resultaat gebeurt als iemand niet upgradet. *14 dagen proef* — bekend patroon, hoogste conversie, maar vraagt om creditcardafhandeling die je nu niet hebt en om een opzegflow die klopt. *Niets veranderen* — houdt de belofte zuiver (geen trial beloven die er niet is) en accepteert een lage conversie tot je social proof hebt. |
| 2 | ~~**Mag iemand `/boards` in vóór e-mailverificatie?**~~ (A8) — **genomen 24-08: ja met banner, wall en gastlink pas ná verificatie. Zie §0b.** | Raakt misbruikbestrijding en de D-24-moderatiespec. | *Ja, met banner* — kortere weg naar de eerste wow, en de bezoeker ziet het product vóór hij betaalt. Kosten: ongeverifieerde accounts kunnen borden maken, dus je hebt een opruimtaak nodig en een limiet. *Nee* — houdt de misbruikdrempel hoog, maar de mailuitstap blijft de duurste stap in de funnel. |
| 3 | **Wordt Club Facilitator het visuele hoofdplan op `/pricing`?** (A2, E1) | Positionering en omzetmix. | *Ja* — de funnel wordt consistent en de gemiddelde orderwaarde stijgt; risico is dat je Club Host-kopers verliest die anders wél waren ingestapt. *Nee* — meer instappers op €4,99, maar dan moet de homepage óók Club Host aanbieden, want de huidige situatie (homepage verkoopt A, prijspagina beveelt B aan) is de slechtste van de drie. |
| 4 | **Wat is de opzeg- en terugbetalingsregel, en mag die bij de knop staan?** (A7, E3) | Juridisch; hoort in dezelfde ronde als V-12 en artikel 14 DSA. | Zonder regel staat er nu niets, en niets lezen bij een betaalknop is voor een deel van de bezoekers een reden om niet te klikken. Met regel moet die woordelijk kloppen met de Terms — de Public Communication Specification eist dat expliciet. |
| 5 | **Mag de deelnemer na afloop een uitnodiging zien?** (B13) | Raakt *Calm software beats noisy software*. | *Ja* — de sterkste groeimotor die je hebt, en het moment klopt (na afloop, niet tijdens). Risico: de facilitator wordt niet gevraagd of zijn deelnemers marketing te zien krijgen op zijn sessie. *Ja, maar de facilitator kan het uitzetten* — netter, kost één instelling en één kolom. *Nee* — je houdt de sessie schoon en laat de groei liggen. |
| 6 | **Blijven de twaalf willekeurige walltitels?** (C1) | Merkgevoel. | *Weg* — consistent, canoniek, en de crawler ziet hetzelfde als de bezoeker. *Blijven* — leuk voor terugkerende bezoekers, maar in strijd met je eigen specificatie §11 en met het drift-signaal in de Constitution; leg dan vast dat dit een bewuste uitzondering is, anders wordt het over een half jaar opnieuw als fout gemeld. *Compromis*: één vaste kop, en de speelse variant als kleine ondertitel die wél mag wisselen. |
| 7 | **Mogen publieke sticky notes geïndexeerd worden voordat de Report-knop bestaat?** (D1) | Moderatie en DSA. | *Ja, nu* — je wint direct organisch bereik, en de Constitution belooft het al. Maar geïndexeerde gebruikersinhoud zonder meldknop is precies het gat dat fase 1 van de D-24-spec moet dichten, en de voortgangsnotitie meldt dat het Help Centre nu verwijst naar een e-mailroute. *Wachten tot D-24 fase 1 draait* — veiliger, en het kost je twee tot drie dagen vertraging. Dit is het enige punt in dit rapport waar ik *niet* zou adviseren om "done is better than perfect" te volgen. |

---

## 11. Wat ik niet heb kunnen verifiëren

Volledigheidshalve, zodat je weet waar dit document zwak staat:

- **De werkelijke visuele hiërarchie.** Ik heb templates gelezen, geen schermen gezien. Alle uitspraken over "valt onder de vouw", "het kleinste element op het scherm" en het mobiele menu zijn afgeleid uit klassen en volgorde in de HTML, en staan hierboven als **AANNAME** gemarkeerd. Eén doorloop met een telefoon bevestigt of ontkracht ze in twintig minuten. **Voor B5 is dat inmiddels gebeurd, en de aanname hield geen stand** — zie het verificatielogboek hieronder.
- **De negen transactionele e-mailtemplates.** Die staan al op je eigen lijst van niet-nagelopen zaken. De uitnodigingsmail en de verificatiemail zitten allebei middenin een funnel die ik hierboven wél heb doorgemeten.
- **Het Help Centre zelf.** Zestien pagina's, op 21 augustus al door je eigen E-02-audit gehaald. Ik heb alleen de verwijzingen ernaartoe getoetst.
- **Laadtijden.** Geen enkele meting. §D6 is codeanalyse.
- **De adminsectie.** Buiten scope.
- **Of `/notes/@id` daadwerkelijk uit de index is.** Ik heb de regel in `robots.txt` en de openbaarheid van de route geverifieerd; of Google de pagina's ook werkelijk heeft laten vallen, zie je in Search Console.

### Verificatielogboek

Aannames uit dit rapport die na publicatie tegen de werkelijkheid zijn gehouden. Dit lijstje hoort te groeien; een aanname die nooit wordt getoetst, blijft een gok met een nette opmaak.

| Datum | Bevinding | Hoe getoetst | Uitkomst |
|---|---|---|---|
| 2026-08-22 | **B5** — de instructie zakt op een telefoon onder een rij chips | Farid liep het deelnemersscherm door op een telefoon tijdens een echte sessie | **Onjuist.** De meeste chips staan achter `x-show` en verschijnen niet tegelijk, dus de balk blijft kort. Bevinding vervallen, actie S1.11 geschrapt. |
| 2026-08-23 | **A5** — de primaire CTA is op mobiel onvindbaar | Rooktest na de deploy van sprint 0 en 1, op een telefoon | **Juist, en verholpen.** De knop *Start* staat nu naast de hamburger. |
| 2026-08-23 | **E2** — de vergelijkingstabel schuift op mobiel binnen zijn eigen container | Rooktest na de deploy van sprint 2 | **Juist.** De pagina zelf schuift niet mee. |
| 2026-08-23 | **D1** — publieke sticky notes zijn weer indexeerbaar | `robots.txt` live gecontroleerd; Search Console moet nog crawlen | **Regel klopt.** Of Google de pagina's ook werkelijk opneemt, is pas over weken zichtbaar. |
| 2026-08-24 | **C7** — het lookalike-teken in het e-mailadres is een fout | Aan Farid voorgelegd nadat het was rechtgezet | **Geen fout.** Het is een bewuste maatregel tegen spam-scrapers. Teruggedraaid en vastgelegd in `App\Helpers\ContactHelper`; de DSA-kant blijft vraag 4 voor de jurist. |
| 2026-08-24 | **`is_flagged`** — het besluit 'Content hidden' verbergt de note | Twee notes in een echte database, de echte modelklasse gevraagd wat een bezoeker ziet | **Onjuist, en verholpen.** Geen enkele publieke query las de vlag. Gerepareerd in de datalaag plus een 404 op de detailpagina; `test-report-flow.php` §15 test nu het gevolg in plaats van de intentie. |
| 2026-08-24 | **`robots.txt`** — de deploy had de nieuwe regel niet meegenomen | Responseheaders opgevraagd op productie | **Onjuist.** De deploy was in orde; Cloudflare serveerde een gecachete kopie met `max-age=2592000`, een waarde die de app zelf nooit had gezet. Cache geleegd, en `Cache-Control` staat nu bij de bron — voor `robots.txt` in de Caddyfile en voor de gegenereerde sitemap in de controller. |
| 2026-08-23 | Sitemap onleesbaar door host-mismatch tussen `www` en apex | Search Console-property nagekeken: het is de apex, en de sitemap bevat apex-URL's | **Onjuist.** Mijn hypothese klopte niet. Resterende kandidaten: een tijdelijke verwerkingsfout aan Google-zijde, of Cloudflare dat Googlebot op dat pad blokkeert. Te onderscheiden met URL-inspectie op `/sitemap.xml`. **Opgelost op 24-08, zie de regel hieronder.** |
| 2026-08-24 | **Sitemap "Kan niet ophalen"** — de oorzaak zit tussen Google en de edge, niet in het bestand | Live opgehaald: geldige XML, ~40 URL's, juiste `Content-Type`, `robots.txt` blokkeert niets, `www/sitemap.xml` bestaat niet meer. Daarna Purge by URL in Cloudflare en URL-inspectie live getest | **Gecachete 404, dezelfde val als bij `robots.txt`.** `/sitemap.xml` was een statisch bestand zónder eigen `Cache-Control` en kreeg dus de dertig dagen van Cloudflare; het is verwijderd toen `SitemapController` het overnam, en elke PoP die in dat gat een 404 ophaalde, hield die vast. Cloudflare cachet per datacenter, dus het bestand klopte voor iedereen behalve voor de PoP waar Googlebot landde. Alleen `robots.txt` was op 24-08 met de hand geleegd, `/sitemap.xml` niet. Nu wel. |
| 2026-08-24 | **`X-Robots-Tag: noindex` op de sitemap blokkeert de verwerking** | Nagezocht: Rank Math en Yoast sturen die header standaard mee en die sitemaps worden verwerkt. De melding in Search Console komt uit de URL-inspectie, die élke URL als *pagina* beoordeelt | **Onjuist — en juist het bewijs dat het ophalen wérkt.** Google kan die header alleen melden als hij de response heeft binnengehaald. De header is desondanks weggehaald: hij beschermde tegen iets wat vrijwel nooit gebeurt en onschadelijk is als het gebeurt, en kostte een rood kruis op precies de plek waar je wilt kunnen zien of er écht iets mis is. Hij stond er bovendien zonder toelichting — het enige commentaarloze besluit in dat bestand. |
| 2026-08-24 | **`$this->db` in `App\Models\User`** — de property bestond niet, terwijl vier methodes hem gebruikten | Foutmelding op productie na het inloggen met een nieuw account; daarna de klasse en de andere modellen nagekeken | **Bestaande bug, niet van besluit 2.** `findByResetToken()` gaf zonder `try/catch` een 500 op elke wachtwoordherstellink. Opgelost door de property toe te voegen die `Board`, `BoardNote`, `UserSession` en `BoardShareLink` al hebben. `php -l` was groen — dit is werk voor `check-render.php`, dat de auth-routes nog niet dekt. |
| 2026-08-24 | **Besluit 1 en 2** — gebouwd | Farid: de vier scripts en `php -l` op alle gewijzigde bestanden, plus een doorloop met een nieuw account | **Groen.** Zie de paragraaf hierboven voor wat er is gebouwd en welke afwijking (de derde gate op `invite()`) bewust is. |
| 2026-08-24 | De handmatige controlelijst na D-24 fase 1 en L1–L3 | Farid heeft de vijf punten zelf doorlopen: de vier scripts op zijn eigen machine, de *Content hidden*-toets met twee browsers, `/sitemap.xml` op de server, de PageSpeed-meting ná de deploy en het opnieuw indienen van de sitemap | **Juist.** Alle waarnemingen kwamen overeen met wat in §0b staat beschreven. De sitemapvraag uit de regel hierboven blijft open — opnieuw indienen onderscheidt de twee kandidaten niet; URL-inspectie wel. |

**Wat deze ene toets leert.** Broncodevolgorde is geen schermvolgorde zodra `x-show` in het spel is. Dat raakt niet alleen B5: elke uitspraak in dit rapport over visuele hiërarchie of mobiel gedrag is op dezelfde manier afgeleid. Ze staan alle als **AANNAME** gemarkeerd, en ze verdienen alle dezelfde toets voordat er iemand aan gaat bouwen. In het bijzonder geldt dat voor A5 (de mobiele CTA), B11 en D4.

---

## 12. Eén laatste observatie

Het valt op hoeveel van deze bevindingen **restanten van een eerdere positionering** zijn. De About-pagina, de wall-CTA's, de *Best value*-badge op Club Host, de betaalbevestiging die naar `/notes/create` wijst, de teller in de footer, de upsells die alleen Club Host noemen — dat is allemaal correct gebouwd voor het product zoals het vóór 16 augustus was. Op 16 augustus is de homepage omgezet en op 21 augustus is D-30 genomen, en de rest van het product is nog niet meeverhuisd.

Dat maakt het werk overzichtelijker dan het lijkt. Er is geen enkele plek waar je een verkeerde beslissing moet terugdraaien. Je moet één beslissing die je al genomen hebt, doortrekken naar de plekken die hem nog niet kennen.

Als je de lijst in sprint 0 en sprint 1 afwerkt, is dat grotendeels gedaan.
