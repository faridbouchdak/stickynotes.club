# Voortgang — de negen openstaande punten

> Datum: 21 augustus 2026, avond
> Bron: de negen punten uit de sessieafsluiting van diezelfde dag
> Werkwijze: code leidend voor gedrag, documenten leidend voor bedoeling (D-31). Alles wat hieronder als feit staat, is nagelopen in de code of gedraaid als test; alles wat aanname of advies is, staat als zodanig gemarkeerd.

---

## In één oogopslag

| # | Punt | Stand |
|---|---|---|
| 1 | V-06 — accountverwijdering | **Gebouwd en getest.** Twee open punten, beide buiten de code |
| 2 | V-12 — Terms zonder account | **Briefing en concepttekst klaar** voor de jurist |
| 3 | V-05 — keuzestap bij downgrade | **Gebouwd en getest.** Waarschuwing vooraf staat nog open |
| 4 | Help Centre-navigatie in `04` | **Afgerond.** 04 op v1.4, navigatie sessie-eerst |
| 5 | D-24 — rapportage en moderatie | **Gespecificeerd**, inclusief DSA-toets. Bouwen is fase 1 vóór launch |
| 6 | V-09, V-10, V-11 — verificatie | **Grotendeels geverifieerd.** Twee bevindingen, één nieuw conflict |
| 7 | E-02 — Engels en labels | **Afgerond en afgevinkt** |
| 8 | Prijspagina noemt resultatenpagina | **Klaar**, ook op de homepage |
| 9 | `AuthController` negeert `?plan=` | **Bleek al gebouwd.** Alleen `CLAUDE.md` liep achter |

Twaalf commits: acht in `stickynotes-club`, vier in `stickynotes.club`. Niets gepusht.

---

## Wat er onderweg boven water kwam, en niet op de lijst stond

**Accountverwijdering werkte helemaal niet.** `deleteAccount()` las het wachtwoord uit `findById()`, en die methode geeft het veld `password` niet terug. Elke poging eindigde op een undefined array key en dus een 500. De implementatiekloof uit punt 1 was daarmee niet het hele verhaal: de knop was kapot.

**En wat hij zou doen, klopte ook niet.** De oude versie liet het meeste aan `ON DELETE CASCADE` over, en die cascade haalt óók de bijdragen weg die op de borden van anderen staan. Wie zijn account opzegde, sloopte de retro van zijn team. Het abonnement liep intussen door bij Creem.

**De Report-knop bestaat niet, maar het Help Centre wees erop.** Letterlijk: *"Use **Report** on the relevant sticky note, comment or board."* Er is geen route, geen view en geen tabel. Dat is dezelfde soort onwaarheid als V-06, maar dan in de publieke documentatie. Vandaag rechtgezet naar de e-mailroute, met de mededeling dat de knop nog gebouwd wordt.

**Drie kapotte links.** `https://stickynotes.club/tos/` staat in drie Help Centre-pagina's; de route is `/terms`. `check-docs-links.php` controleert kennelijk alleen interne links.

**Nieuw conflict C-13.** De dagelijkse digest filtert overal op `deleted_at IS NULL`, met een goede reden. V-11 eist dat een auteur wiens note is verwijderd dat juist via die digest hoort. Vandaag hoort hij niets. Dat is een besluit van jou, niet een bug.

---

## Per punt

### 1. V-06 — accountverwijdering

**Gebouwd.** Migratie 019 (`author_deleted_at` op notes, board_notes en board_note_comments, plus één gereserveerd account dat niemand is) en een herschreven `User::deleteAccount()`.

De volgorde is de kern. Eerst het abonnement opzeggen bij Creem (`POST /subscriptions/{id}/cancel`), buiten de transactie; lukt dat niet, dan wordt er niets verwijderd en krijgt de gebruiker een bruikbare melding. Dan, in één transactie: drafts weg; publieke sticky notes blijven zonder auteur, met een strookje tape op de wall; gegeven harten weg inclusief de opgeslagen teller; eigen borden volledig weg; bijdragen op andermans borden blijven als **Deleted user**; dot-stemmen blijven als anoniem aantal; deelnemersrijen verliezen naam en toegang; uitnodigingen aan dat e-mailadres weg; het beheerdersauditspoor blijft, zonder naam; betaalsporen losgekoppeld in plaats van gewist.

**Getest.** `scripts/test-account-deletion.php`, 32 controles tegen een wegwerpdatabase uit de echte migratieketen, inclusief het scenario waarin opzeggen bij Creem faalt. Alles groen.

**Blijft open, en allebei buiten de code:** de bewaartermijn van betaalgegevens (vraag voor de jurist) en het daadwerkelijk verwijderen van beschermde back-ups binnen 30 dagen (afspraak met Fly.io). Tot beide rond zijn blijft V-06 open staan.

### 2. V-12 — deelnemen zonder account in de Terms

`briefing-V-12-terms-deelname-zonder-account.md`: geverifieerde feiten uit de code in een tabel, vijf gaten van groot naar klein, acht vragen aan de jurist, en concepttekst voor een nieuwe §13a plus aanpassingen aan §4, §11 en §13.

**Het zwaarste punt is leeftijd.** §4 hangt de grens van zestien aan het *maken van een account*, en een gast maakt er geen. De doelgroep van je frontpagevoorstel zijn docenten met een QR-code op het schoolbord. Dat is geen theoretisch gat.

**Advies:** doe deze ronde samen met de wijziging die artikel 14 DSA vraagt (zie punt 5). Zelfde document, zelfde jurist.

### 3. V-05 — keuzestap bij downgrade

**Gebouwd.** Migratie 018 (`boards.keep_editable`), `/boards/editable` als keuzescherm met teller en een nette weigering bij te veel vinkjes, en read-only als **toestand** op het bord in plaats van de flash die na één klik verdween.

De hele sorteerregel is één query: `ORDER BY keep_editable DESC, created_at ASC, id ASC LIMIT <planlimiet>`. Gekozen borden winnen, lege plaatsen gaan naar de oudste borden, en er zijn nooit meer schrijfbare borden dan het plan toestaat. Zes SQLite-scenario's gedraaid, allemaal goed.

**Blijft open:** de waarschuwing *vóór* de downgrade. De keuze wordt nu achteraf aangeboden. Dat komt de belofte na, maar niet de volgorde. Ook open: de vier-tier-vergelijking van limieten en prijzen, en heractivatie na een upgrade.

### 4. Help Centre-navigatie in `04`

`04` staat op v1.4. Doelgroepen op volgorde van gebruik, met de deelnemer zonder account als tweede — en de opmerking erbij dat dat de grootste groep is en de slechtst bediende. Elf toptaken, sessie eerst. Navigatiemodel met *Run a session* bovenaan. Beide sessiepagina's in de inventaris. Een sessiepagina is een task guide, met twee extra regels: zeg wat de zaal ziet, en beschrijf de timer nooit als een slot.

In het Help Centre zelf is `nav_order` opnieuw gezet en de startpagina in dezelfde volgorde gebracht. **Niets hernoemd, geen permalink gewijzigd**, dus geen redirects nodig.

### 5. D-24 — rapportage en moderatie

`spec-D-24-rapportage-en-moderatie.md`. Eén tabel `reports`, de flow van melding tot besluit tot bezwaar, de motiveringsmail woord voor woord, bewaartermijnen, acceptatiecriteria en een fasering.

**Het juridische kader valt mee.** Artikel 19 DSA stelt micro- en kleine ondernemingen vrij van sectie 3: geen klachtenportaal, geen geschillenbeslechting, geen trusted flaggers, geen transparantieverslag. Wat wél geldt: artikel 16 (meldmechanisme), 17 (motivering), 18 (strafbare feiten) en de contactpunten uit 11 en 12. Toezicht ligt bij de ACM.

**Fase 1 is de launchpoort:** melden, zaaknummer, wachtrij, besluit met motivering, auditregel bij inzage. Schatting twee tot drie dagen.

### 6. V-09, V-10, V-11

`scripts/test-note-cascades.php`, 31 controles, allemaal groen. Soft delete bewaart comments, harten en stemmen zolang herstel kan; herstellen brengt alles terug; opruimen wist de rij mét zijn cascade terwijl de stemronde blijft; een bord verwijderen neemt alles mee; een publieke note neemt zijn harten mee; geen enkele opgeslagen `likes_count` loopt uit de pas.

De autorisatiegrens van V-11 bleek al gedekt door `test-board-rights.php`. Twee bevindingen: het technische logboek is niet duurzaam (wie een note verwijderde staat op de rij zelf en verdwijnt dus mét de rij na zeven dagen), en de digest kan een verwijdering niet melden — dat laatste is C-13.

### 7. E-02

Volledige audit over zestien Help Centre-pagina's, drie beleidspagina's, de designdocumenten en de templates. Het Help Centre bleek al schoon. Gecorrigeerd: *collaborators* in `terms.md`, *Organize your work* en *Help Center* in `05`, en negen templates met *Color*, *Frame Color*, *Note Color* en *colors*. Nagekomen: de kleine letter *member* in de bordinterface — de bordkop telde "3 members" waar het eigenaar plus Participants zijn, dus nu "3 people". E-02 is afgevinkt met de volledige bevindingenlijst erbij.

Bewust ongemoeid: *"Not a member?"* op de inlogpagina en *"Members only"* op de 401. Die gaan over clublidmaatschap, niet over een bordrol.

### 8. Prijspagina

De resultatenpagina staat er nu, op de prijspagina én op de homepage, met ranking, besluiten, actiepunten, printen en Markdown-export. De oude notitie in `pricing.html` dat de pagina "nog niet bestaat" is verwijderd — die was sinds fase 4 achterhaald.

### 9. `?plan=`

Werkt al. `rememberRequestedPlan()` leest de parameter op `/register`, toetst bestaan én koopbaarheid, en `destinationAfterLogin()` stuurt na inloggen naar `/checkout/<plan>`. De CTA's op home en prijspagina wijzen er correct heen. Alleen `CLAUDE.md` beweerde nog het tegendeel; dat is gecorrigeerd.

---

## Wat jij moet doen

**Voor de eerstvolgende deploy**

1. `php app/database/migrate.php` — migraties 018 en 019 staan klaar.
2. `php scripts/test-account-deletion.php` en `php scripts/test-note-cascades.php` op je eigen machine draaien. Beide draaiden hier groen tegen de echte migratieketen; op jouw omgeving is het een minuut werk en dan weet je het zeker.
3. Een doorloop met twee browsers voor de twee nieuwe schermen: `/boards/editable` en de read-only-banner op een bord.

**Deze week**

4. De jurist bellen, met beide documenten tegelijk: V-12 én de Terms-wijziging die artikel 14 DSA vraagt.
5. C-13 beslissen: krijgt de digest een *Removed while you were away*-blok, of vervalt die eis uit V-11?

**Vóór launch**

6. Fase 1 van de D-24-spec bouwen. Zolang die knop er niet is, staat er in het Help Centre dat hij nog komt — en dat is eerlijk, maar niet houdbaar.

---

## Wat ik niet heb gedaan

- De negen transactionele e-mailtemplates, nog steeds niet nagelopen.
- De vier-tier-vergelijking van limieten, prijzen, checkout en btw-weergave (het grootste resterende deel van V-05).
- De browsercontroles van V-10: UTC-publicatietijd, de landensnapshot, de deelteller en de Public → Draft-reset.
- Het opruimen van afbeeldingen op schijf van borden die met een account zijn verwijderd. De rijen gaan mee, de bestanden blijven staan. Klein, maar het groeit.
