# Frontpagevoorstel StickyNotes.club

Status: concept voor development  
Datum: 16 augustus 2026  
Strategische keuze: workshop-first, met de publieke wall als secundaire community- en acquisitielaag

## 1. Doel van de pagina

De frontpage moet binnen vijf seconden duidelijk maken:

1. StickyNotes.club is een tool voor begeleide workshops en brainstormsessies.
2. Deelnemers doen zonder account of installatie mee via een link of QR-code.
3. Eén facilitator kan de sessie sturen, ideeën verzamelen en gezamenlijk prioriteren.
4. De publieke sticky-notes wall bestaat nog, maar is niet langer het hoofdproduct.

Primaire doelgroep: facilitators, teamleads, scrum masters, docenten, trainers en organisatoren van kleine groepssessies.

Primaire conversie: een bezoeker start de registratie voor Club Facilitator.  
Secundaire conversie: een bezoeker bekijkt hoe workshopmodus werkt of opent de publieke wall.

## 2. Positionering en kerncopy

Aanbevolen productomschrijving:

> StickyNotes.club helps you run focused workshops in minutes. Invite up to 50 people with a link or QR code, collect ideas and vote on what matters—no accounts or installs for participants.

Aanbevolen kernbelofte:

> Run a focused workshop in minutes.

Ondersteunende bewijslijn:

> One facilitator · Up to 50 participants · No per-seat pricing

## 3. Globale paginaopbouw

1. Navigatie
2. Hero: workshopbelofte + hoofdbeeld
3. Herkenbaar probleem
4. Van QR-code naar gezamenlijk besluit in drie stappen
5. Accountloos deelnemen
6. De facilitator bestuurt het gesprek
7. Van losse ideeën naar prioriteiten
8. Private boards als blijvende werkruimte
9. Publieke wall als secundaire communitylaag
10. Prijs en plan
11. FAQ
12. Finale CTA en footer

## 4. Specificatie per sectie

### Sectie 1 — Navigatie

**Doel**  
De bezoeker direct naar het product, de werking en de prijs leiden zonder de navigatie te laten concurreren met de hero.

**Desktopindeling**

- Links: logo + `StickyNotes.club`.
- Midden/rechts: `How it works`, `Public wall`, `Pricing`, `Help`.
- Rechterzijde: tekstlink `Log in` en primaire knop `Start a workshop`.

**Mobiel**

- Logo links.
- Primaire knop `Start` zichtbaar.
- Overige links in een eenvoudig menu.

**Routes**

- `How it works` → `#how-it-works`
- `Public wall` → `#public-wall`
- `Pricing` → `/pricing`
- `Help` → `https://docs.stickynotes.club/`
- `Log in` → `/login`
- `Start a workshop` → `/register?plan=pro`

**Ontwerpregel**  
Gebruik één primaire knop. Maak `Public wall` geen concurrerende gekleurde CTA.

---

### Sectie 2 — Hero

**Doel**  
In één scherm de doelgroep, uitkomst en belangrijkste drempelverlager communiceren.

**Copy**

Eyebrow:

> Workshops without sign-up friction

H1:

> Run a focused workshop in minutes.

Subheading:

> Invite up to 50 people with a link or QR code. Collect ideas, guide the conversation and vote on what matters—no accounts or installs for participants.

Primaire CTA:

> Start a workshop

Secundaire CTA:

> See how it works

Bewijslijn onder de CTA's:

> One facilitator · Up to 50 participants · No per-seat pricing

**Layout**

- Desktop: copy links, productbeeld rechts; verhouding ongeveer 42/58.
- Mobiel: copy, CTA's, bewijslijn en daarna het productbeeld.
- Geen achtergrondvideo, carousel of automatisch bewegende interface.

**Screenshot S01 — Hero facilitator view**

- Desktopbeeld van een actieve workshop op een private board.
- Toon de workshopbar met status `Workshop running`, timer, instructie en `Close input`.
- Toon 9–12 notes verdeeld over drie duidelijke kolommen.
- Laat 4–6 aanwezige deelnemers zien als de interface dat ondersteunt.
- Gebruik neutrale demo-inhoud, bijvoorbeeld een retrospective: `What helped us move faster?`
- Verberg accountmenu, e-mailadres en overige persoonlijke gegevens.
- Aanlevering: 1440×900 px, 2× pixel density, WebP; centrale crop moet ook op mobiel bruikbaar zijn.
- Alt-tekst: `Facilitator view of a live StickyNotes.club workshop with a timer, shared instruction and participant notes.`

---

### Sectie 3 — Het herkenbare probleem

**Doel**  
Uitleggen waarom de accountloze workshopflow waardevol is, zonder concurrenten te noemen.

**Heading**

> Less setup. More useful conversation.

**Body**

> Workshops lose energy when people first have to create accounts, install an app or learn a complicated canvas. StickyNotes.club lets the room start contributing while the question is still fresh.

**Drie korte punten**

- `No participant accounts`
- `No software to install`
- `No complicated workspace to explain`

**Visual**  
Geen extra screenshot. Gebruik veel witruimte en drie rustige tekstblokken. De hero heeft het product al getoond.

---

### Sectie 4 — Van QR-code naar besluit

Anchor: `#how-it-works`

**Heading**

> From QR code to shared decision.

**Stap 1**

Titel: `Invite the room`  
Tekst: `Share a temporary link or put the QR code on screen. Participants choose a nickname and join from their phone or laptop.`

**Stap 2**

Titel: `Guide the session`  
Tekst: `Set the question, run the timer, collect ideas silently and decide when input opens or closes.`

**Stap 3**

Titel: `Choose what matters`  
Tekst: `Discuss the ideas, use dot voting and leave the session with visible priorities on the board.`

**Layout**

- Desktop: drie stappen horizontaal met een duidelijke 1–2–3-volgorde.
- Mobiel: verticaal.
- Gebruik kleine interfacecrops, geen generieke illustraties.

**Screenshot S02 — Join-flow composite**

- Linkerkant: facilitatorweergave `Show on screen` met QR-code én uitgeschreven URL.
- Rechterkant: mobiel scherm waarop een deelnemer een nickname kiest.
- Gebruik een staging- of verlopen workshoplink; publiceer geen actieve toegangscode.
- Aanlevering: één samengestelde afbeelding van 1600×900 px, WebP.
- Alt-tekst: `A workshop QR code beside the mobile nickname screen used to join without an account.`

---

### Sectie 5 — Accountloos deelnemen

**Doel**  
De belangrijkste differentiator afzonderlijk laten landen.

**Heading**

> Anyone with the link can take part.

**Body**

> Participants do not need an account, paid plan or installation. They choose a nickname and can add, edit and delete their own notes, comment, use hearts and vote while the workshop link is active.

**Supporting copy**

> Workshop links always expire and can be replaced or revoked by the facilitator.

**Layout**

- Screenshot links; copy rechts.
- Op mobiel screenshot boven de tekst.

**Screenshot S03 — Participant board on mobile**

- Mobiele participantweergave tijdens een actieve sessie.
- Toon de gedeelde instructie en timer.
- Toon de primaire actie `Add Note` duidelijk.
- Gebruik maximaal 5–6 notes zodat het scherm leesbaar blijft.
- Toon geen facilitatorcontrols.
- Aanlevering: 1170×2532 px of vergelijkbare moderne telefoonverhouding, WebP.
- Alt-tekst: `Mobile participant view of an active workshop with a shared question, timer and Add Note button.`

---

### Sectie 6 — De facilitator bestuurt het gesprek

**Doel**  
Laten zien dat dit meer is dan een gedeeld prikbord.

**Heading**

> Keep the room focused without breaking its flow.

**Featurelijst**

- `Shared instruction` — verander de focus tijdens de sessie.
- `Synchronized timer` — start, pauseer, hervat of voeg een minuut toe.
- `Open or close input` — bepaal wanneer nieuwe ideeën binnenkomen.
- `Silent brainstorm` — deelnemers zien eerst alleen hun eigen ideeën.
- `Participant preview` — controleer vooraf wat de groep zal zien.
- `Spotlight, discussed state and ordering lock` — alleen tonen nadat deze controls in productie en documentatie zijn bevestigd.

**Layout**

- Groot screenshot rechts.
- Links een verticale lijst; bij hover hoeft niets interactiefs te gebeuren.
- Geen zes losse screenshots: één goed gekozen facilitatorbeeld moet de samenhang tonen.

**Screenshot S04 — Silent brainstorm**

- Facilitatorbeeld waarin silent brainstorm actief is.
- De facilitator ziet alle demo-notes; in een kleine inset staat de participantweergave met alleen de eigen notes.
- Toon tevens de timer en actuele instructie.
- Aanlevering: 1600×1000 px, WebP.
- Alt-tekst: `Silent brainstorm in which the facilitator sees all notes while a participant sees only their own.`

---

### Sectie 7 — Van ideeën naar prioriteiten

**Doel**  
De uitkomst verkopen, niet alleen het verzamelen van notes.

**Heading**

> Turn a wall of ideas into visible priorities.

**Body**

> Move from collecting to discussing and voting without sending the group to another tool. Results remain visible on the board when the session finishes.

**Bewijspunten**

- Comments and hearts for lightweight feedback.
- Dot voting with a facilitator-controlled allowance.
- Results revealed when the facilitator closes the round.
- A finished board that can be shared read-only.

**Screenshot S05 — Voting results**

- Board na een gesloten stemronde.
- Toon stemmen op meerdere notes en een duidelijke topkeuze.
- Als `spotlight` en `discussed` werkelijk beschikbaar zijn, mag één besproken topnote geselecteerd zijn; anders niet tonen.
- Aanlevering: 1440×900 px, WebP.
- Alt-tekst: `Workshop board showing the results of a completed dot-voting round.`

---

### Sectie 8 — Private boards blijven bruikbaar

**Doel**  
Uitleggen dat de waarde niet eindigt wanneer de timer stopt.

**Heading**

> The session ends. The board stays useful.

**Body**

> Every workshop is built on a private board. Prepare it before the room joins, keep the results afterwards and share a read-only view with people who were not there.

**Kleine punten**

- Start with Blank, Retro, Kanban, Week planner or Brainstorm.
- Organise notes with columns, tags and due dates.
- Changes appear for active viewers without a manual refresh.

**Visual**  
Gebruik een crop van S05 of een kleine voor/na-compositie. Maak hiervoor geen zesde unieke fotoshoot als dezelfde demo-board kan worden hergebruikt.

---

### Sectie 9 — Publieke wall

Anchor: `#public-wall`

**Advies**  
Behouden, maar pas ná de workshop- en boardsecties. De wall ondersteunt het merkverhaal en geeft bezoekers iets te ontdekken zonder de hoofdpositionering over te nemen.

**Heading**

> Some ideas are meant to be shared with the world.

**Body**

> Outside your private workshops, the public wall is a place to publish a thought, discover notes from other countries and save an idea you love.

**Content**

- Toon maximaal drie actuele public notes.
- Gebruik bij voorkeur gecureerde product-, inspiratie- of demo-notes zonder persoonsgegevens.
- Toon datum, land, heart count en share count zoals in het product.
- Voeg geen oneindige wall, masonry-scroll of automatisch wisselende carousel toe.

**CTA's**

- Primair binnen deze sectie: `Explore the public wall` → `/`
- Secundair: `Share a public note` → `/register`

Omdat de sectie op de homepage zelf staat, moet de eerste route bij implementatie naar een aparte wallroute of een gefilterde wallweergave wijzen. Als `/` de nieuwe marketinghomepage wordt, is `/wall` de eenvoudigste route.

**Screenshot S06 — Public wall strip**

- Geen traditionele screenshot nodig als de developer drie echte note-cards server-side kan renderen.
- Als een statisch beeld nodig is: drie public notes op één rij, zonder hero of navigatie.
- Aanlevering: 1600×600 px, WebP.
- Alt-tekst: `Three public sticky notes from the StickyNotes.club worldwide wall.`

---

### Sectie 10 — Prijs en plan

**Doel**  
De gekozen hoofdfeature direct verbinden aan het relevante plan.

**Heading**

> One facilitator. A whole room. No seat licences.

**Uitgelicht plan**

`Club Facilitator — €14.99/month, excluding VAT`

**Samenvatting**

- Everything in Club Host.
- Up to 50 participants per workshop.
- QR-code participation without accounts.
- Facilitator controls, silent brainstorm and dot voting.
- Up to 15 private boards.

**CTA**

> Become a Club Facilitator

Route: `/register?plan=pro`

**Secundaire link**

> Compare all plans →

Route: `/pricing`

**Ontwerpregel**  
Toon op de frontpage niet vier even dominante prijskaarten. Eén Club Facilitator-kaart draagt de workshoppositionering; de volledige vergelijking blijft op `/pricing`. `Chosen Few` mag op de prijspagina een speels element blijven, maar hoort niet in de primaire conversieflow van de homepage.

---

### Sectie 11 — FAQ

Gebruik maximaal vijf vragen:

1. `Do participants need an account?`  
   No. They join an active workshop link, choose a nickname and take part without creating an account.

2. `Does everyone need a paid plan?`  
   No. Only the facilitator needs Club Facilitator. Participants take part for free.

3. `How many people can join?`  
   Up to 50 participants can join one workshop board.

4. `Can I use an existing board?`  
   Yes. An existing private board can be turned into a workshop without changing its notes or layout.

5. `What happens after the workshop?`  
   The board remains available to its Owner, and the outcome can be shared using a read-only View link.

Link onderaan:

> Visit the Help Centre →

---

### Sectie 12 — Finale CTA en footer

**Heading**

> Ready to get the room thinking together?

**Body**

> Set up the board, share the QR code and start collecting ideas in minutes.

**CTA's**

- Primair: `Start a workshop` → `/register?plan=pro`
- Secundair: `See pricing` → `/pricing`

**Footer**

- Product: Public wall, Pricing, Help Centre.
- Legal: Terms, Privacy, Community Guidelines.
- Account: Log in, Register.
- Korte merkregel: `A place where ideas can grow together.`
- Geen user- of note-counters in de primaire conversieflow zolang de aantallen klein zijn.

## 5. Definitieve screenshot-shotlist

| ID | Scherm | Waar gebruikt | Prioriteit |
| --- | --- | --- | --- |
| S01 | Actieve workshop, facilitator desktop | Hero | Essentieel |
| S02 | QR-code + nickname join-flow | Drie stappen | Essentieel |
| S03 | Actieve workshop, participant mobile | Accountloos deelnemen | Essentieel |
| S04 | Silent brainstorm, facilitator + participant inset | Facilitatorcontrols | Essentieel |
| S05 | Gesloten dot-voting met resultaten | Prioriteiten/resultaat | Essentieel |
| S06 | Drie gecureerde public notes | Publieke wall | Optioneel; liever live cards |

### Eén consistente demo-workshop

Gebruik voor S01–S05 één herkenbare demo-workshop, zodat de pagina één verhaal vertelt.

Aanbevolen board:

- Naam: `Product retrospective`
- Instructie: `What helped us move faster, and what should we change next?`
- Kolommen: `Worked well`, `Slowed us down`, `Try next`
- 9–12 korte notes, bijvoorbeeld:
  - `Clear ownership on small decisions`
  - `Fewer meetings, better preparation`
  - `Reviews waited too long`
  - `Decide the experiment before Friday`
  - `Keep the weekly customer call`
- Deelnemers: 6–8 neutrale voornamen of fictieve nicknames.

### Capturevoorwaarden

- Gebruik staging of een speciaal demo-account, nooit echte klantdata.
- Verwijder e-mailadressen, tokens, accountmenu's en browserchrome.
- Gebruik dezelfde boardachtergrond, notekleuren en voorbeeldinhoud in alle beelden.
- Zet browserzoom op 100% en gebruik een vaste viewport.
- Exporteer screenshots als WebP, met PNG als bronbestand.
- Richtwaarde: maximaal 250–350 KB per desktopbeeld en 150–250 KB per mobiel beeld.
- Lever voor elk beeld desktop- en mobiele crops aan als de centrale crop niet responsief werkt.
- Voeg beschrijvende alt-tekst toe; zet belangrijke marketingcopy niet uitsluitend in het beeld.

## 6. Responsive en technische richtlijnen

- Mobile first; belangrijke copy en CTA moeten vóór het eerste screenshot staan.
- Maximale contentbreedte circa 1200 px.
- Tekstkolommen maximaal ongeveer 65–70 tekens breed.
- Screenshots lazy-loaden, behalve S01 in de hero.
- S01 preloaden; alle beelden voorzien van vaste breedte en hoogte om layoutverschuiving te voorkomen.
- Gebruik `srcset`/`sizes` en AVIF/WebP met een passende fallback.
- Respecteer `prefers-reduced-motion`; de pagina heeft geen beweging nodig om begrepen te worden.
- Alle CTA's hebben één duidelijk label en een zichtbare focusstatus.
- Gebruik kleur niet als enige aanduiding voor workshopstatus, stemmen of beschikbaarheid.
- De publieke notes moeten server-side of statisch worden geladen; voorkom dat een trage wallfeed de hero blokkeert.

## 7. Analytics en acceptatiecriteria

### Primaire events

- `homepage_workshop_cta_clicked`
- `homepage_how_it_works_clicked`
- `homepage_public_wall_clicked`
- `homepage_pricing_clicked`
- `facilitator_registration_started`

### Belangrijkste funnel

`Homepage → facilitator registration → workshop created → first external participant joined → workshop started`

### Acceptatiecriteria

- Een nieuwe bezoeker kan na vijf seconden correct omschrijven dat dit een workshoptool is.
- De primaire CTA staat boven de vouw op desktop en mobiel.
- `Club Facilitator` en accountloos deelnemen zijn op de homepage zichtbaar zonder naar Pricing te gaan.
- De publieke wall staat niet boven de workshopuitleg.
- Geen CTA claimt een gratis trial zolang die niet werkelijk bestaat.
- Alle getoonde controls bestaan in productie en zijn beschreven in het Help Centre.
- De homepage haalt op mobiel geen onnodige grote beelden binnen.

## 8. Feiten, aannames en open vragen

### Geverifieerde feiten

- De huidige homepage leidt met `Share your thoughts with sticky notes`.
- De huidige homepage toont de publieke Universal Sticky Wall vóór de productuitleg.
- De actuele prijspagina positioneert Club Facilitator als `Run guided sessions with anyone` voor €14.99 per maand exclusief btw.
- Club Facilitator ondersteunt volgens de actuele prijspagina maximaal 50 deelnemers, QR-deelname zonder account, facilitatorcontrols, silent brainstorm, dot voting en undo bij verwijderde workshopnotes.

### Aannames in dit voorstel

- De primaire commerciële doelgroep is de facilitator, niet de losse publieke-note-auteur.
- `/register?plan=pro` blijft de correcte registratieroute.
- De homepage kan van marketingpagina worden voorzien terwijl de publieke wall naar `/wall` of een vergelijkbare route verhuist.
- Er is geen gratis trial; daarom wordt die niet beloofd.

### Open vragen vóór development

1. Wordt `/` de nieuwe marketinghomepage en verhuist de wall naar `/wall`, of blijft de wall technisch onderdeel van `/` onderaan de pagina?
2. Zijn spotlight, besproken-status en ordering lock op dit moment productiefunctionaliteit? Zo niet, niet tonen.
3. Geldt soft delete met Undo alleen binnen workshopmodus, of voor alle boardnotes? Dit moet vóór publicatie worden afgestemd met Help Centre, Terms en productmodel.
4. Kan de registratie voor Club Facilitator direct starten zonder onmiddellijke betaling? Pas de CTA-copy aan als checkout direct volgt.
5. Zijn er echte testimonials of aantoonbare workshopresultaten? Voeg geen social-proofsectie toe totdat die beschikbaar en publiceerbaar zijn.

## 9. KISS-releasevolgorde

### Nu essentieel

1. Nieuwe hero en navigatie.
2. Drie-stappen-uitleg.
3. S01–S05 vastleggen.
4. Accountloze deelname en facilitatorcontrols uitleggen.
5. Club Facilitator-prijsblok.
6. Publieke wall reduceren tot drie cards onderaan.
7. Finale CTA en basisanalytics.

### Later verbeteren

- Testimonials en concrete klantresultaten.
- Korte productvideo.
- Branchespecifieke landingspagina's voor retrospectives, onderwijs en trainingen.
- A/B-tests op hero-copy en CTA-labels.
- Dynamische public-wall-curatie.

Done is voor de eerste release belangrijker dan een uitgebreide animatie, video of interactieve demo. Eén overtuigende hero, vijf consistente productscreens en een duidelijke facilitator-CTA zijn voldoende om de positionering recht te trekken.
