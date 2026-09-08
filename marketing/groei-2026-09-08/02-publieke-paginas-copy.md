# Publieke pagina’s — concrete copy en opbouw

8 september 2026. Engelse publicatiecopy passend bij de huidige Engelstalige app; briefing en toelichting in het Nederlands. Voorstel voor de developer; niet geïmplementeerd of live getest. Feitenbasis en beperkingen staan in 01. Prijzen en limieten hieronder zijn templatevelden die uit bestaande productbronnen moeten komen.

## Homepage /

**Paginatitel:** Online sticky notes for ideas, plans and workshops

**Meta description:** Keep ideas on a private board, organise your plans and work with others. Start free, or run guided workshops with guest participation by link or QR code.

### Navigatie

Logo → /; How it works → /#how-it-works; Workshops → /#workshops; Pricing → /pricing; Help Centre → https://docs.stickynotes.club/; Log in → /login; primaire knop **Start free** → /register.

Worldwide wall en About blijven via de footer bereikbaar; de wall krijgt ook een eigen sectie op de homepage. Op mobiel dezelfde informatiehiërarchie. Gebruik voor ingelogde gebruikers de bestaande accountnavigatie en boardroute.

### Eerste scherm

**Online sticky notes for your ideas, plans and shared work.**

Keep your thoughts together on a private board. Plan your week, collect ideas or work with other people. When you need to guide a group, turn a board into a workshop.

**Start free** → /register

**Explore workshops** → /#workshops

Free includes {{free_board_limit}} private board of your own. No credit card needed. Publishing on the worldwide wall is optional.

**Beeldopdracht:** een echte screenshot van een bestaand privéboard met zelfgemaakte, niet-klantgebonden voorbeeldnotities. Toon “My week”, drie herkenbare taken en kolommen. Label het als voorbeeldboard. Houd tekst op het beeld ook als HTML in de sectie beschikbaar. Geen verzonnen interface, klantenlogo’s of gebruikscijfers.

### #how-it-works — Choose how you want to use it

**For yourself**
Keep a weekly plan, collect ideas or organise a personal project. Start with a free private board.
Link: **Make your first board** → https://docs.stickynotes.club/use-sticky-notes-for-yourself/

**With other people**
Invite people to a board you own and develop ideas together. Club Host adds invitations and View or Post links. Invited Participants can use free accounts.
Link: **See shared-board plans** → /pricing

**For a workshop**
Guide a session with an instruction, timer, silent brainstorm and voting. With Club Facilitator, guests join through a link or QR code without creating an account.
Link: **See the workshop flow** → /#workshops

### Your own board, one useful next step

1. Create a board. Choose Blank, Week planner or Kanban.
2. Add what is on your mind. Give each idea or task its own note.
3. Arrange it as things change. Keep using the board on your own, or choose a plan that lets you invite others.

**Private-board notes do not use your daily Public publication allowance.**

### #workshops — From individual ideas to a shared result

Prepare the question. Let people contribute. Discuss and prioritise the notes, then keep the outcome on a results page.

- Participants join with a link or QR code — no account or installation.
- Collect ideas silently, then reveal them for discussion.
- Guide the session with an instruction and timer, and decide when input opens or closes.
- Use dot voting to make priorities visible.
- Finish with notes and facilitator-labelled decisions and actions, ready to print or save as PDF, copy as Markdown or download as CSV.

**Club Facilitator: €{{facilitator_price}} per month, excluding VAT. Up to {{participant_limit}} participants per workshop. Participants do not pay.**

**Choose Club Facilitator** → /register?plan=pro if purchasable; otherwise **See workshop availability** → /pricing. No enabled purchase promise when the configured product is unavailable.

Secondaire link: **Read the workshop guide** → https://docs.stickynotes.club/run-a-workshop/

Beeld: echte korte opname van deelnemen, stille input, onthullen en resultaten. In het eerste releaseblok volstaan drie echte screenshots met bijschriften; een video is geen voorwaarde om duidelijkere copy te publiceren.

### Public wall or private board?

**Your private boards**
For your own work and the people you give access to. They do not appear on the worldwide wall.

**The worldwide wall**
An optional place to publish an individual thought for others to discover. Public notes and private-board notes are separate.

**Explore the public wall** → /wall

**Understand who can see your notes** → https://docs.stickynotes.club/public-wall-private-board-workshop/

### Choose a plan for what you want to do

Free for one personal board. Club Host for more boards and collaboration. Club Facilitator for guided workshops.

**Compare plans** → /pricing

### Questions before you start

**Can I use it on my own?** Yes. Club Member includes {{free_board_limit}} private board for your own ideas or plans.

**Do I have to publish on the public wall?** No. You can use your private board without publishing anything.

**Can I only write two notes a day?** The daily allowance applies to publishing on the worldwide wall. Private-board notes do not use it.

**Does everyone need a paid account?** No. Invited Participants can use free accounts. Workshop guests join without an account. To contribute through an ordinary Post link, people need to sign in.

**Are workshops free?** Hosting guided workshops requires Club Facilitator or the applicable Chosen Few entitlement. The free plan lets you use your own board; guests joining a workshop do not pay.

### Afsluitende CTA

**Start with one board and one idea.**
Create your free account and make a private space for the things you want to remember.

**Start free** → /register

## Pricing /pricing

**Titel:** Choose the plan for what you want to do

**Intro:** Start with a board of your own, invite others to work together or guide a workshop. You can use StickyNotes.club without publishing on the worldwide wall.

### Club Member

**Free — Your own sticky notes**
€0 / month

- {{free_board_limit}} active, editable private board of your own.
- Private-board notes do not use a daily publication allowance.
- Join boards you are invited to with a free account.
- Publish up to {{member_public_limit}} notes per day on the worldwide wall.

Own-board invitations and guided workshops are not included.

**Create a free account** → /register

### Club Host

**Shared boards — More space, more people**
€{{host_price}} / month, excluding VAT

- Up to {{host_board_limit}} active, editable private boards of your own.
- Invite Participants to your boards by email. They can use free accounts.
- Share View links for reading and Post links for signed-in contributions.
- Pastel colours and Instant Photos.
- Publish up to {{host_public_limit}} notes per day on the worldwide wall.

Guided workshop mode and guest contribution without an account require Club Facilitator.

**Choose Club Host** → /register?plan=premium, with existing logged-in handling.

Developer: geverifieerde bestaande routes zijn /register?plan=premium en /checkout/premium voor Club Host. Behoud deze parameters; de zichtbare naam blijft Club Host.

### Club Facilitator

**Workshops — Guide the session, keep the result**
€{{facilitator_price}} / month, excluding VAT

- Everything in Club Host, with up to {{facilitator_board_limit}} owned boards.
- Up to {{participant_limit}} participants per workshop.
- Guest participation by link or QR code without an account.
- Instruction, timer, silent brainstorm and input controls.
- Voting and a finished results page with PDF printing, Markdown copy and CSV download.

One facilitator subscription. Participants do not pay.

**Choose Club Facilitator** → bestaande pro-route, alleen als afrekenen beschikbaar is.

Gebruik eventueel de badge **For guided workshops**, geen onbewezen “Most popular”.

### Vergelijking en footer

Eerst: eigen boards, eigen boards delen, bijdrage zonder account, workshopregie, resultatenexport. Daarna: publieke publicaties, kleuren en foto’s. Beschrijf gratis gastdeelname uitsluitend in de workshopcontext; verwissel Post links niet met workshoplinks. De tabel gebruikt bestaande rechtenfuncties en instellingen.

Onder de drie maandplannen: **Looking for Chosen Few? See the separate one-time upgrade.** → bestaande informatie in een ondergeschikte sectie op dezelfde pagina. Toon daar het echte bedrag, de Host-voorwaarde en blijvende versus abonnementsafhankelijke rechten; geen weggepoetste voorwaarden. Farid heeft met deze verplaatsing ingestemd.

Btw, betaalfrequentie, verlenging en annuleren blijven zichtbaar. De bedragen zijn bronprijzen exclusief btw; ontwikkelaar controleert correcte productie- en doelgroepweergave met de bestaande checkout en huidige voorwaarden. Deze opdracht bevat geen juridische wijziging en geen nieuw prijsmodel.

## Worldwide wall /wall

**The public sticky-note wall**
Read what people choose to share publicly, or publish a thought of your own. The wall is one part of StickyNotes.club; your private boards are separate.

Primair voor deze pagina: **Create a free account** → /register.

Duidelijke secundaire route: **Want a board for yourself? Start with a free private board.** → /#how-it-works.

Behoud publicatiewaarschuwingen in het daadwerkelijke publicatieproces. Geen automatische publicatie tijdens aanmelden en geen suggestie dat wall-content rechtstreeks naar boards kan worden verhuisd. Gebruik “people around the world” niet als bewijs van een bestaande actieve community.

## About /about — vervang opening, behoud herkomst en contact

**Sticky notes for the things you want to keep thinking about.**

A thought for later. A plan for the week. A question you want a group to explore. StickyNotes.club gives those things a place on a private board, with familiar sticky notes you can organise and return to.

You can use it on your own, invite others to work together, or run a guided workshop. Individual thoughts can also be published on the worldwide wall. You choose that public step; it is not required to use your own board.

StickyNotes.club is an independent product created by Farid Bouchdak in the Netherlands. It grew from an interest in how a small written thought can help people think and connect.

Behoud het bestaande geverifieerde ontstaansverhaal, contact en beleidslinks. Vermijd absolute tijdwinstclaims en onbewezen succesverhalen. Neem technische hostingdetails alleen over als die nog actueel zijn.

## Registratie en eerste board

Gratis route: **Create your free account**. Subtekst: **Start with {{free_board_limit}} private board for your own ideas and plans. No credit card needed.**

Betaalde route: **Create your account for {{plan_name}}**. Subtekst: **Creating an account is free. Confirm your email to continue to payment for {{plan_name}}.** Behoud planselectie over login en verificatie; toon geen gratis workshopproefperiode.

Lege boardlijst: **What would you like to keep together?** / **Make a week planner, collect ideas or start a blank board.** / knop **New board**. Een bestaande betalende facilitator behoudt de passende workshopactie. Geen verplicht profiel, openbare notitie of extra keuzevragen voordat iemand een board kan maken.

## Begripstest vóór en na

Laat vijf nieuwe proefpersonen de pagina kort zien, zonder uitleg. Vraag: wat kun je hiermee doen; kun je het alleen gebruiken; wie ziet je eigen notes; welk plan heb je nodig om anderen uit te nodigen; geldt “twee per dag” ook voor je board? Laat één persoon per mobiel/desktop de gratis route uitvoeren. Streef als intern vrijgavecriterium naar vier van vijf juiste antwoorden op de kernvragen; dit is een kleine kwalitatieve test, geen statistisch conversiebewijs.


## Chosen Few — concrete ondergeschikte presentatie

**Besluit bevestigd door Farid.** Drie normale abonnementskaarten, daarna de vergelijking van die drie. Pas daaronder één rustige tekstregel met een uitklapbare toelichting. Geen vierde kolom, prijsbadge, gradient, aanbeveling of primaire CTA bij de drie plannen.

Gesloten zichtbaar: **Looking for Chosen Few?**

Uitgeklapt:

**Chosen Few is a separate one-time upgrade.**

It costs €{{chosen_few_price}} once, excluding VAT, on top of a Club Host subscription at purchase. It is not a monthly plan, and you do not need it for ordinary shared boards or guided workshops.

The upgrade includes the documented permanent Chosen Few rights: no plan-level limit on Public publications or owned boards, collaboration and workshop access, and celestial residence. Workshop participant limits and other technical and safety limits still apply. Pastel colours and Instant Photos require an active eligible subscription.

**Read the full details** → https://docs.stickynotes.club/plans-and-subscriptions/#chosen-few-a-separate-one-time-upgrade

**View the Chosen Few upgrade** → bestaande gekozen-few-registratie/checkoutflow, als bescheiden tekstlink binnen het geopende blok. Toon vooraf dezelfde echte prijs en voorwaarden. Geen aankoopactie aan het openen van de toelichting koppelen.

Developer: gebruik bij voorkeur het native HTML-element `details` met `summary` voor toetsenbord- en schermlezertoegang. Het onderdeel heet in code niet “hidden pricing”: het blijft vindbare informatie. Gebruik de bestaande Chosen Few-prijs uit Plans; formatteer niet naar een betaalbaar ogend afgerond bedrag. De Help Centre-planvergelijking krijgt eveneens drie maandkolommen en houdt de specifieke upgrade-uitleg eronder.
