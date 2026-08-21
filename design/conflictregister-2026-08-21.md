# Conflictregister — designdocumenten vs. implementatie

> Status: concept ter beoordeling
> Datum: 21 augustus 2026
> Aanleiding: de designdocumenten lopen achter op de code. Dit register maakt per punt zichtbaar wat er staat, wat de software werkelijk doet, wie leidend is en welke tekst dat oplost.
> Scope: `00_Product_Constitution.md`, `01_Product_Model.md`, `02_Product_Playbook.md` tegenover de codebase `stickynotes-club`.

## Voortgang

| # | Status |
|---|---|
| C-05 | **verwerkt** op 21 augustus 2026 — sessiecontext, levenscyclus en invarianten in 01 (v1.7), Workshop rules in 02 (v1.7), grenzen in 00 (v1.5) |
| C-06 | **verwerkt** op 21 augustus 2026 — D-30 in 00 (v1.3), positionering herschreven in 02 (v1.4) |
| C-07 | **verwerkt** op 21 augustus 2026 — vier tiers in 01 (v1.5) en 02 (v1.5), D-29-poort gesloten, downgrade-route herzien |
| C-08 | **verwerkt** op 21 augustus 2026 — 01, 02 en drie Help Centre-pagina's bijgewerkt |
| C-09 | **verwerkt** op 21 augustus 2026 — workshoplink als derde toegangsvorm in 01 (v1.6) en 02 (v1.6); Terms-lacune als V-12 |
| C-10 | **verwerkt** op 21 augustus 2026 — 01 en 02 bijgewerkt |
| C-11 | **verwerkt** op 21 augustus 2026 — vijf templates bijgewerkt |
| C-12 | **verwerkt** op 21 augustus 2026 — duplicatie geratificeerd als gewoon bordbeheer in 01 (v1.8) en 02 (v1.8), verbod in D-19 ingetrokken |

**Nummering.** De C-nummers begonnen in dit register bij C-01 en botsten met de bestaande CONFLICT-markers C-01 tot en met C-04 in `03_Product_Design_Notes.md`. Ze zijn op 21 augustus 2026 hernummerd naar C-05 tot en met C-11 en als markers in het reviewregister van 03 opgenomen, met de bijbehorende beslissingen in de decision log. Dit document is vanaf nu de uitgebreide toelichting; **03 is de bron**.

**Alle conflicten zijn afgehandeld.** Wat resteert is geen conflict maar werk: de navigatie van `04_Help_Center_Architecture.md` is nog capture-first opgebouwd en heeft geen plaats voor een sessie — er staat nergens hoe je er een leidt of aan meedoet. Verder het onderstaande.

**Openstaand werk dat uit deze rondes volgt:** een juridische review van de Terms voor deelname zonder account (V-12), een keuzestap bij downgrade met een read-only-toestand op het bord zelf (D-13, V-05), en de prijspagina die de resultatenpagina nog niet noemt terwijl die bestaat.

De bestuursregel uit §0 is op 21 augustus 2026 vastgesteld als **[DECISION D-31]** en staat in `00_Product_Constitution.md` (v1.4) onder *Governance*, met een tiebreaker voor het grijze gebied. Hij bekrachtigt met terugwerkende kracht de oplossingen van C-06, C-08, C-10 en C-11, die op die regel zijn gemaakt voordat hij bestond.

---

# 0. Bestuursregel

Dit register hangt aan één regel. Zonder die regel is "de code is leidend" een uitspraak die de Constitution stilzwijgend afschaft.

Voorstel, toe te voegen aan `00_Product_Constitution.md` onder **Governance**:

> For **behaviour** — what the product actually does — the implementation is authoritative. A difference between a design document and the code is a documentation defect and is corrected in the document, unless the implementation crosses an explicit boundary set in the Constitution or the Product Model.
>
> For **intent** — purpose, positioning, product boundaries, plan promises and release gates — the documents are authoritative. A difference is a product finding, is recorded in the Design Notes and is resolved by a decision, not by the code that shipped first.

**Vastgesteld op 21 augustus 2026 als D-31**, met een tiebreaker voor het grijze gebied: een passage die *beschrijft* is gedrag, een passage die *toestaat, verbiedt, belooft of een poort zet* is bedoeling — en bij twijfel geldt bedoeling. Code die de bedoeling inhaalt wordt niet teruggedraaid of geblokkeerd, maar als CONFLICT vastgelegd en beslecht vóór de volgende release die hetzelfde gebied raakt. De regel staat in `00_Product_Constitution.md` onder *Governance*.

Dat onderscheid verdeelde de conflicten hieronder in de conflicten die je gewoon wegschrijft en de conflicten die een besluit van jou vroegen. C-12 kwam er later bij, gevonden tijdens het uitwerken van C-05.

**Legenda**

- **Richting: code leidend** — document corrigeren, geen besluit nodig.
- **Richting: document leidend** — besluit nodig, code is een bevinding.
- Conceptteksten staan in het Engels, in de stijl van de bestaande documenten, zodat ze rechtstreeks overneembaar zijn.

**Overzicht**

| # | Onderwerp | Richting | Documenten | Inspanning |
|---|---|---|---|---|
| C-05 | Workshopmodus ontbreekt volledig | document leidend | 00, 01, 02, 04 | groot |
| C-06 | Positionering en tagline (D-01) | document leidend | 00, 02 | middel |
| C-07 | Plannamen en Club Facilitator (D-29) | document leidend | 01, 02 | middel |
| C-08 | Soft delete en Undo (D-21) | code leidend | 01, 02, Help Centre | klein |
| C-09 | Gasten en linktoegang (D-23) | code leidend | 01, 02 | middel |
| C-10 | Voting-melding | code leidend | 01, 02 | zeer klein |
| C-11 | Delete-bevestigingen en terminologie | gemengd | 02 + code | klein |
| C-12 | Bordduplicatie (D-19) | document leidend | 01, 02 | klein |

---

# C-05 — Workshopmodus bestaat niet in de designdocumenten

**Dit was het hoofdprobleem. C-06 tot en met C-11 zijn er grotendeels gevolgen van, en C-12 kwam bij het oplossen ervan boven water.**

## Wat de documenten zeggen

Het woord **workshop** komt **nul keer** voor in `00_Product_Constitution.md`, `01_Product_Model.md`, `02_Product_Playbook.md` en `04_Help_Center_Architecture.md`. Hetzelfde geldt voor *guest*, *timer*, *spotlight*, *lobby* en *QR*. Het woord *facilitator* komt drie keer voor, uitsluitend als onderdeel van de plannaam **Club Facilitator** — nooit als rol in het product.

`00_Product_Constitution.md`, sectie *Who we serve*, beschrijft de doelgroep als mensen die:

> - quickly capture and share a thought;
> - discover ideas from other people;
> - brainstorm alone or with others;
> - organise a growing collection of ideas;
> - turn loose thoughts into a shared outcome.
>
> It should work for an individual without feeling like team software and for a small group without requiring project-management training.

## Wat de code doet

Zeven migraties (011 tot en met 017) en drie services voeren een compleet nieuw productcontext in:

- `board_participants` als identiteitslaag voor deelnemers **zonder account** (migratie 011);
- `App\Services\BoardActor` — "wie handelt er op dit bord", met `actor_key` `u:<id>` / `p:<id>`;
- `App\Services\WorkshopService` — sessiestatus `off|draft|lobby|running|closed|archived`, `input_locked`, `reveal_mode`, servergezaghebbende timer, spotlight, deelnemerslimiet;
- lobby, silent brainstorm, QR-deelname, gemarkeerd-als-besproken, arrangement lock, resultatenpagina met ranking, Markdown-export, anonieme notes;
- `board_share_links.allows_guests` — een deellink die accountloze deelname toestaat.

De homepage verkoopt dit als hoofdproduct (`app/resources/views/home.html`, H1: *"Run a focused workshop in minutes."*).

## Richting

**Document leidend** — maar niet in de zin dat de code fout is. De code is de facto een tweede productcontext binnengelopen zonder dat 00 en 01 die kennen. Zolang dat zo is, kan geen enkele regel in 02 over rollen, rechten, verwijderen of communicatie kloppen, want ze zijn geschreven voor een wereld met alleen *Owner* en *Participant*.

## Voorstel

Dit is te groot voor een tekstpatch. Minimaal nodig:

1. **`01_Product_Model.md` → Product contexts**: een derde context naast de worldwide wall en het private board. Voorstel:

   > **Workshop session.** A private board on which the Owner has switched on workshop mode. The board keeps its identity, notes and participants; workshop mode adds a session with a status, an input lock, a reveal mode and an optional timer. A session is temporary; the board that carries it is not. When the session ends, the board and its results remain available.

2. **`01_Product_Model.md` → Core objects**: `Participant record` opnemen als object dat losstaat van `Account`, met de expliciete regel:

   > A participant record represents one person's presence on one board. It exists for signed-in members and for people taking part without an account. It carries contributions, not rights: what someone may do follows from the board, the session and — for members — their account.

3. **`00_Product_Constitution.md` → Who we serve**: één bullet toevoegen, en dat is een positioneringsbesluit — zie C-06.

4. **`02_Product_Playbook.md`**: een sectie *Workshop rules* naast de bestaande *Collaboration*, met minimaal: wie de sessie stuurt, wat de deelnemer ziet in elke status, wat de timer wel en niet doet (signaal, geen slot), en dat een gesloten workshop bevriest maar moderatie doorloopt.

**Kosten van uitstel:** elk item hieronder krijgt anders een reparatie die opnieuw moet zodra dit alsnog wordt vastgelegd.

---

# C-06 — Positionering: workshop-first vs. D-01

## Wat de documenten zeggen

`00_Product_Constitution.md:23` en `:238`:

> **A place where ideas can grow together.**
>
> **[DECISION D-01] Resolved on 20 July 2026** — Use **A place where ideas can grow together.** as the official product promise and tagline.

`02_Product_Playbook.md:537`:

> Do not position the product as a heavy company platform or promise public boards.

De narratieve pijlers in `02` (regel 527 e.v.) zijn *Capture before it disappears*, *Give ideas room to grow*, *Bring related thoughts together*, *Grow ideas together*, *Keep control of what is public*.

## Wat de code doet

`home.html` leidt met *"Run a focused workshop in minutes."* en richt zich blijkens `07_frontpage-voorstel-stickynotes-club.md` op facilitators, teamleads, scrum masters, docenten en trainers. Dat is de doelgroep die 00 juist afbakent met *"without feeling like team software"*.

## Richting

**Document leidend.** Code kan niet vaststellen waar een product voor is. Je hebt aangegeven dat workshop-first een vastgesteld besluit is, dus dit is geen conflict meer maar een openstaande documentwijziging.

## Voorstel

**a. Nieuw besluit in `00_Product_Constitution.md` → Resolved decision**, direct onder D-01:

> **[DECISION D-30] Resolved on 21 August 2026** — Facilitated sessions are the primary use of StickyNotes.club and the lead commercial story. **A place where ideas can grow together** remains the product promise and tagline; it is not replaced. Public-facing surfaces may lead with the session outcome — *Run a focused workshop in minutes* — provided the promise remains the umbrella under which capture, private boards and the worldwide wall continue to sit. This supersedes the audience description in *Who we serve* and the pillar order in the Playbook's *Marketing and positioning*; it does not change D-01.

*Waarom de tagline blijft staan:* een productbelofte en een campagnekop hoeven niet dezelfde zin te zijn, maar ze mogen elkaar niet tegenspreken. "Ideas grow together" en "run a focused workshop" spreken elkaar niet tegen — een workshop is de scherpste vorm van samen ideeën laten groeien. Vervang je D-01, dan moet ook de wall, het private board en het Help Centre opnieuw worden ingekaderd, en dat is een veel groter karwei zonder aanwijsbaar voordeel.

**b. `00` → Who we serve**, de opsomming vervangen door:

> StickyNotes.club is for people who want to:
>
> - run a focused session with a group and reach a shared result;
> - take part in someone else's session without an account or an install;
> - quickly capture and share a thought;
> - brainstorm alone or with others;
> - organise a growing collection of ideas;
> - discover ideas from other people.
>
> It should work for one person leading a room without requiring facilitation training, for a participant who joined thirty seconds ago, and for an individual capturing a thought alone.

**c. `02` → Marketing and positioning**, de pijlervolgorde vervangen door:

> Use these narrative pillars where they are true, in this order:
>
> - **Get a room thinking together.**
> - **Take part without an account.**
> - **Turn loose ideas into a decision.**
> - **Keep the result after the session ends.**
> - **Capture before it disappears.**
> - **Keep control of what is public.**
>
> For commercial positioning, make **Get a room thinking together** the lead paid-value pillar. Capture and the worldwide wall support the story; they no longer lead it.

**d. `02:537` vervangen:**

> Do not position the product as a company-wide platform, a project-management system or a replacement for a whiteboard suite, and do not promise public boards. A session is small, temporary and led by one person. Boards remain private and access-controlled; public distribution happens through individual sticky notes on the worldwide wall.

**Raakt ook:** `04_Help_Center_Architecture.md` (de navigatie is capture-first opgebouwd) en `06 §11` (canonieke termen — *facilitator*, *participant*, *session* en *guest link* moeten daar bij).

---

# C-07 — Plannamen en Club Facilitator-entitlements

## Wat de documenten zeggen

`02_Product_Playbook.md:401`:

> Do not publish the new ladder, mechanically rename entitlement identifiers or rewrite current Help Centre claims until Club Facilitator pricing and entitlements are decided and the complete migration has been implemented and verified.

`01_Product_Model.md:371`:

> **[DECISION D-29] Resolved on 3 August 2026; entitlements and implementation pending** — Adopt **Club Member**, **Club Host**, **Club Facilitator** and **Chosen Few** … This is a naming and ordering decision only and does not itself change D-13 or D-27 entitlements.

`02:385` beschrijft de entitlements in drie plannen:

> Free includes one active, editable owned private board … Premium includes up to five … Chosen Few includes unlimited active owned private boards.

## Wat de code doet

`app/Helpers/RoleHelper.php:59-62` levert de vier namen live uit. Migratie `010_facilitator_tier.php` heeft de tier ingevoerd. `RoleHelper:157` documenteert een entitlement die in geen enkel designdocument staat:

> Club Facilitator (pro): setting `max_private_boards_pro`, default 15.

`pricing.html` toont de vier plannen als kopjes. Daarmee is de release-poort gepasseerd zonder dat de entitlements zijn vastgelegd.

## Richting

**Document leidend voor de poort, code leidend voor de feiten.** Dat de tier bestaat en 15 boards geeft, is een feit dat je overneemt. Dat hij verkocht mag worden voordat D-13/D-27 zijn uitgebreid, is een besluit dat nog niet genomen is.

## Voorstel

**a. `01_Product_Model.md`**, D-29 vervangen:

> **[DECISION D-29] Resolved on 3 August 2026; names published on <datum>; entitlements recorded on 21 August 2026** — **Club Member**, **Club Host**, **Club Facilitator** and **Chosen Few** are the public plan names, in that order. Club Member succeeds Free and Club Host succeeds Premium without changing their D-13 and D-27 entitlements. Club Facilitator adds: up to fifteen active owned private boards, workshop mode on owned boards, and participation by people without an account through a guest link, up to the configured participant limit.

**b. `02_Product_Playbook.md:385`**, de entitlement-alinea vervangen:

> Club Member includes one active, editable owned private board and full participation on boards to which the user is invited. Club Host includes up to five active owned private boards and the ability to invite others and share links. Club Facilitator includes up to fifteen active owned private boards and the ability to run workshop sessions with participants who have no account. Chosen Few includes unlimited active owned private boards. Board allowances are settings rather than constants; the numbers above are the current defaults and marketing must read them from the product rather than repeat them.

**c. `02:401`**, de poortzin vervangen door de resterende openstaande verificatie:

> The plan names are published. Verify that every entitlement claim on the pricing page, in checkout and in the Help Centre matches the configured limits, and that a downgrade from Club Facilitator follows the D-13 selection flow.

**Let op — apart risico, buiten dit register:** `CLAUDE.md` vermeldt dat `AuthController` de parameter `?plan=` negeert, terwijl `07` ervan uitgaat dat `/register?plan=pro` de registratieroute is. Als de homepage-CTA daarheen wijst, komt de bezoeker in een gewone registratie terecht. Dat is geen documentconflict maar wel een lek in de funnel die je nu bouwt.

---

# C-08 — Soft delete en Undo (D-21)

## Wat de documenten zeggen

`02_Product_Playbook.md:185`:

> Do not promise Undo, trash, a recovery period or restoration for deleted sticky notes, comments or boards; deletion is immediately permanent after confirmation.

`02:190` en `01:201` schrijven de bevestigingstekst letterlijk voor:

> **Delete this sticky note?** / **This permanently deletes the sticky note and all its comments, hearts and votes. This cannot be undone.** / **Cancel** / **Delete sticky note**

## Wat de code doet

Migraties 013 en 014 voeren soft delete in voor **alle** private boards, niet alleen workshopmodus. `BoardNote::delete()` zet `deleted_at` plus `deleted_by_actor`; `BoardNote::PURGE_AFTER_DAYS = 7`; een nachtelijk script wist definitief. De store `boardStatus.js` toont ~30 seconden een Undo (`UNDO_MS = 30000`) met een `undo_url` van de server. Het bord-notekaartje heeft **geen** bevestiging meer (`_note_card.html:157-170`). Publieke sticky notes op de wall worden nog wel hard verwijderd, met de bevestiging `Are you sure you want to delete this note?`.

Admin-moderatie is de uitzondering en verwijdert wel direct definitief.

## Richting

**Code leidend.** Twee verschillende objecten met twee verschillende levenscycli, en de documenten kennen er één.

**Geverifieerd, en dat scheelt werk:** noch `privacy.md` noch `terms.md` doet een belofte over het verwijderen van losse sticky notes. Beide gaan alleen over accountverwijdering (*"Account deletion cannot be undone"*, terms.md:281 — nog steeds waar) en over kopieën bij derden. **Deze wijziging vraagt dus geen juridische aanpassing.**

## Voorstel

**a. `02:185` vervangen:**

> Deletion is layered by object. A sticky note on a private board is removed from view immediately and can be restored by the same person for a short period; after that period it is purged and cannot be recovered. A Public sticky note, a comment and a board are deleted permanently at confirmation, with no Undo, trash or recovery period. Moderation deletion is always immediate and permanent. Never describe a purge window as a bin, an archive or a backup, and never promise recovery after it has passed.

**b. `02:190` en `01:201`** — bevestigingscopy splitsen:

> - **Sticky note on a private board:** delete without a confirmation dialog and offer **Undo** for about thirty seconds afterwards. The message reads **Sticky note deleted.** with the action **Undo**. Do not claim the deletion is permanent, because for that period it is not.
> - **Public sticky note:** heading **Delete this sticky note?**; body **This permanently deletes the sticky note and all its comments and hearts. This cannot be undone. Independent copies, screenshots, search results, caches and external AI use cannot be recalled.**; actions **Cancel** and **Delete sticky note**.
> - **Comment:** heading **Delete this comment?**; body **This permanently deletes the comment. This cannot be undone.**; actions **Cancel** and **Delete comment**.
> - **Board:** unchanged.

**c. D-21** aanvullen:

> **[DECISION D-21] … amended on 21 August 2026** — Private-board sticky notes use a short restore window instead of immediate permanence. The window is a product promise: state its existence, never its exact duration in a place that would become wrong when the setting changes. All other objects keep immediate permanent deletion.

**Raakt ook:** `docs/private-boards.md`, `docs/collaboration.md` en `docs/troubleshooting.md` in het Help Centre — daar staat vermoedelijk nog dat verwijderen definitief is. Niet gecontroleerd (zie §9).

---

# C-09 — Gasten en linktoegang (D-23)

## Wat de documenten zeggen

`02_Product_Playbook.md:143` en D-23 op `:273`:

> Explain that link users are not Participants, receive no comments, hearts, dot votes or board-management rights …
>
> Link access never creates Participant status or grants comments, hearts, dot votes or board-management rights.

En: alleen een Owner met **Premium of Chosen Few** mag een View- of Post-link maken; een Post-link werkt alleen voor een **ingelogde** gebruiker.

## Wat de code doet

- `board_participants` (migratie 011) geeft **iedere** deelnemer een identiteit, ook zonder account.
- `board_note_likes` en `board_note_votes` dragen `actor_key` met `UNIQUE(note_id, actor_key)` — expliciet ontworpen zodat een gast één hart en één stem heeft. Gasten stemmen en geven harten dus wél.
- `board_note_comments` heeft een `participant_id`.
- `board_share_links.allows_guests` (migratie 013) maakt accountloze deelname een expliciete keuze per link, met `expires_at` die voor iedereen geldt.
- Deelnemen kan via QR zonder account, tot `WorkshopService::participantLimit()`.

## Richting

**Code leidend.** Het onderliggende model is veranderd: rechten hangen niet meer aan "heb je een account" maar aan "welke actor ben je op dit bord".

## Voorstel

**a. `02:143` vervangen:**

> Keep board membership personal and invitation-led, and treat link access as a separate, weaker form of participation. An Owner whose plan allows collaboration may create a **View link** (read-only, no account needed), a **Post link** (a signed-in user may add sticky notes) or, in workshop mode, a **guest link** that lets someone take part without an account. A guest is not a Participant: they hold no board-management rights, cannot invite anyone and lose access the moment the Owner revokes the link or removes them. Within a session a guest may add sticky notes, comment, place hearts and use dot voting on the same terms as everyone else — a session is worthless if half the room can only watch. Every link may carry an expiry, and expiry applies to everyone including members.

**b. D-23** aanvullen:

> **[DECISION D-23] … amended on 21 August 2026** — Guest participation through an explicitly guest-enabled link is permitted in workshop mode. Guest access grants contribution and interaction inside the session, never board management, invitations or access to other boards. Enabling workshop mode must never retroactively turn an existing Post link into a guest link.

**c. `01_Product_Model.md` → Ownership and control rules**: vastleggen dat bijdragen blijven staan als een gast wordt verwijderd.

> Removing someone from a board ends their access; it never removes their contributions. Showing someone the door is not the same as cutting their input out of the result.

---

# C-10 — Voting-melding

## Wat de documenten zeggen

`02:245` en `01:262`, letterlijk voorgeschreven:

> Voting is open — you have used 0 of 3 votes. Votes stay hidden until the round is closed.

## Wat de code doet

`_notes_area.html:27-31` en `_notes_area_shared.html:27-28` tonen **votes left** in plaats van votes used. Dat was een bewuste verbetering: "used 2 of 3" is hoofdrekenen midden in een sessie.

## Richting

**Code leidend.** De code heeft gelijk.

## Voorstel

Beide plekken vervangen door:

> Voting is open — you have **2 votes left**. Votes stay hidden until the round is closed.

En de regel eronder toevoegen, omdat die het waarom vasthoudt:

> Show what remains, not what has been used. A participant needs to know how many decisions are still theirs to make, not how many they have already made.

**Gecontroleerd en in orde:** de keuze 1 / 3 / 5 / 10 dots met 3 voorgeselecteerd staat correct in `_notes_area.html:74-79`, precies zoals `02` voorschrijft.

---

# C-11 — Delete-bevestigingen en terminologie

## Wat de documenten zeggen

`02:323`:

> **Sticky note** is mandatory in titles, navigation, buttons, first mentions and formal definitions. **Note** is allowed only as a natural shorthand after the object is clear.

Plus de voorgeschreven bevestigingsteksten uit C-08.

## Wat de code doet

- `notes/show.html:225`, `notes/index.html:92`, `partials/notes-wall.html:42`: `confirm('Are you sure you want to delete this note?')` — mist de cascade, mist "cannot be undone", en gebruikt **note** in plaats van **sticky note**.
- `_note_card.html:315`: `confirm('Delete this comment?')` — kop klopt, body ontbreekt.
- `show.html:852`: `confirm('Delete this board and ALL of its notes? This cannot be undone.')` — inhoudelijk juist, wijkt af van de voorgeschreven formulering.

## Richting

**Gemengd, en hier is de code de zwakke partij.** Dit zijn geen bewuste verbeteringen maar achterstallige copy: de documenten schrijven betere teksten voor dan de app toont.

## Voorstel

Documenten ongewijzigd laten (op de C-08-splitsing na) en de app bijwerken. Concreet:

| Plek | Nu | Wordt |
|---|---|---|
| Publieke note verwijderen | `Are you sure you want to delete this note?` | `Delete this sticky note? This permanently deletes the sticky note and all its comments and hearts. This cannot be undone.` |
| Comment verwijderen | `Delete this comment?` | `Delete this comment? This permanently deletes the comment. This cannot be undone.` |
| Board verwijderen | `Delete this board and ALL of its notes? This cannot be undone.` | `Delete this board? This permanently deletes the board and all its sticky notes, comments, hearts and votes. It also removes all participants and pending invitations. This cannot be undone.` |

Daarnaast één brede check die niet in dit register past maar er wel uit volgt: **note** versus **sticky note** in knoppen en koppen door de hele app.

---

# 8. Gecontroleerd, geen conflict

Om het register te kalibreren — dit is nagelopen en klopt:

- **Dot-votingopties** 1 / 3 / 5 / 10 met 3 voorgeselecteerd: implementatie komt overeen met `02`.
- **Board-overzicht** toont `Last modified on YYYY/MM/DD` (`boards/index.html:147`), precies zoals Q-06 voorschrijft.
- **Terms en Privacy Policy** doen geen belofte over het verwijderen van losse sticky notes; de Undo-wijziging raakt ze niet.
- **Rapportage- en moderatieflow** (D-24, met categorieën als *Spam or scam*) is **niet** in de code aangetroffen — maar D-24 staat correct gemarkeerd als *"implementation and legal verification required"*. Documentatie loopt hier vóór de code en is daar eerlijk over. Dat is de gezonde variant.
- **Comment editing** wordt niet aangeboden, conform `02`.
- **Voting-rondes** kennen geen reset of heropening, conform `02`.

---

# 9. Wat ik niet heb gecontroleerd

- De zestien Help Centre-pagina's in `stickynotes.club/docs/`. C-08 en C-09 raken vrijwel zeker `private-boards.md`, `collaboration.md`, `run-a-workshop.md` en `troubleshooting.md`. Dat is een tweede ronde.
- `03_Product_Design_Notes.md` (815 regels). Mogelijk zijn een of meer van deze conflicten daar al geregistreerd als open vraag; ik heb alleen de kopstructuur gelezen. **Controleer dit vóór je D-nummers uitdeelt** — dubbele nummering is lastig terug te draaien.
- De negen transactionele e-mailtemplates.
- Of `07_frontpage-voorstel` inmiddels is vastgesteld dan wel nog concept is.

---

# 10. Volgorde

**Nu essentieel**

1. C-10 en C-11 — een uur werk, geen besluit nodig, direct minder onwaarheid in de app.
2. C-08 — de tekstpatches zijn klaar, alleen overnemen. Daarna de vier Help Centre-pagina's.
3. C-06 — je hebt het besluit al genomen; D-30 en de twee vervangen alinea's leggen het vast.

**Daarna**

4. C-07 — vraagt dat je de Club Facilitator-entitlements definitief bevriest. Zolang dat niet gebeurt, blijft elke prijsclaim formeel ongedekt.
5. C-09 — grotere tekst, maar zonder besluit uit te voeren.

**Als laatste, en met de meeste tijd**

6. C-05 — de workshopcontext in 00, 01 en 02. Dit is het enige item dat echt denkwerk vraagt in plaats van redactie. Doe het niet als zevende reparatie maar als één ronde waarin je de vijf voorgaande patches meeneemt.

Done is beter dan perfect: stap 1 tot en met 3 zijn samen ongeveer een dagdeel en halen de meest zichtbare onwaarheden eruit. Stap 6 mag een week later.
