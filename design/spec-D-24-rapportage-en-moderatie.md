# Spec — rapportage en moderatie (D-24)

> Status: concept ter beoordeling
> Datum: 21 augustus 2026
> Aanleiding: D-24 is als gedrag vastgesteld op 22 juli 2026 en staat sindsdien als *"implementation and legal verification required"*. In de code bestaat alleen een adminvlag. Dit document maakt er een uitvoerbare opdracht van, inclusief de juridische toets die vóór launch af moet.
> Taal: dit is een werkdocument, dus Nederlands. De teksten die de gebruiker te zien krijgt staan er in het Engels in, klaar om over te nemen.

---

## 1. De situatie vandaag, geverifieerd

**Wat er is.** `notes.is_flagged` met `AdminController::toggleNoteFlag()`, en verder verwijderen en bewerken van notes, bordnotes, borden en gebruikers vanuit `/admin`. Elke adminactie schrijft naar `admin_audit_log` via `AdminAuditLogger` — actor, actie, resourcetype, resource-id, details, IP, user-agent en tijdstip. Dat is een bruikbare basis: het auditspoor dat D-24 eist bestaat al voor de handelingen die er zijn.

**Wat er niet is.** Geen `reports`-tabel, geen route, geen knop, geen zaaknummer, geen notificatie, geen bezwaar, geen bewaartermijn. `grep -rn "report" app/config/routes.php` geeft niets terug.

**Wat er wél beloofd werd.** Het Help Centre schreef tot vandaag letterlijk: *"Use **Report** on the relevant sticky note, comment or board."* Die knop bestaat niet. Dat is op 21 augustus 2026 rechtgezet — `community-guidelines.md` en `privacy-and-safety.md` wijzen nu naar het e-mailadres en zeggen erbij dat de knop nog komt. **Dat is een pleister, geen oplossing:** een meldroute die alleen uit een e-mailadres bestaat is voor een Nederlandse hostingdienst niet genoeg (zie §2).

---

## 2. Het juridische kader, en waarom het meevalt

StickyNotes.club is naar Europees recht een **hostingdienst** en waarschijnlijk ook een **online platform** (het verspreidt op verzoek van gebruikers informatie onder het publiek — de worldwide wall). Dat maakt hoofdstuk III van de digitaledienstenverordening (DSA) van toepassing. In Nederland houdt de **ACM** hier sinds februari 2025 toezicht op, als digitaledienstencoördinator onder de Uitvoeringswet digitaledienstenverordening.

**Artikel 19 DSA scheelt je het meeste werk.** Dat artikel bepaalt: *"This Section, with the exception of Article 24(3) thereof, shall not apply to providers of online platforms that qualify as micro or small enterprises."* Sectie 3 is artikel 19 tot en met 28. Voor een eenmanszaak betekent dat concreet dat het volgende **niet** geldt:

| Artikel | Onderwerp | Geldt voor jou |
|---|---|---|
| 20 | Intern klachtenafhandelingssysteem | Nee (art. 19) |
| 21 | Buitengerechtelijke geschillenbeslechting | Nee (art. 19) |
| 22 | Trusted flaggers | Nee (art. 19) |
| 23 | Maatregelen tegen misbruik van het meldsysteem | Nee (art. 19) |
| 24 lid 1–2 | Transparantierapportage voor platforms | Nee (art. 19) |
| 24 lid 3 | Doorgeven van bevelen/gegevens aan de Commissie | **Ja** — de uitzondering op de uitzondering |
| 25–28 | Dark patterns, advertenties, aanbevelingssystemen, minderjarigen | Nee (art. 19) |
| 15 | Transparantieverslag voor tussenhandeldiensten | Nee — art. 15 lid 2 sluit micro en klein uit |

Wat **wel** geldt, ongeacht je omvang:

| Artikel | Onderwerp | Wat dat hier betekent |
|---|---|---|
| 11 | Contactpunt voor autoriteiten | Eén elektronisch contactpunt, vindbaar gepubliceerd |
| 12 | Contactpunt voor gebruikers | Idem voor gebruikers, en niet uitsluitend via een chatbot |
| 14 | Voorwaarden | De Terms moeten je moderatiebeleid in begrijpelijke taal beschrijven — raakt V-12 |
| **16** | **Meldmechanisme** | **Een elektronisch, makkelijk toegankelijk en gebruiksvriendelijk mechanisme voor voldoende nauwkeurige en onderbouwde meldingen van illegale inhoud. Dit is het artikel dat de Report-knop afdwingt.** |
| **17** | **Motivering (statement of reasons)** | Bij elke beperking een duidelijke, specifieke motivering aan de betrokkene |
| 18 | Melding van vermoedens van strafbare feiten | Bij dreiging voor leven of veiligheid: informeer de politie |

**De conclusie in één zin:** je hoeft geen klachtenportaal, geen geschillenbeslechting en geen jaarverslag te bouwen, maar een meldmechanisme (16) en een motiveringsbrief (17) zijn niet optioneel, ook niet voor een eenmanszaak.

Een e-mailadres alléén voldoet vermoedelijk niet aan artikel 16: het mechanisme moet *"easy to access and user-friendly"* zijn en moet meldingen kunnen opnemen die de exacte elektronische locatie van de inhoud bevatten. Een knop naast de inhoud levert die locatie automatisch; een e-mail vraagt de melder om zelf een URL te plakken. **Deze aanname is de eerste vraag voor de jurist in §9.**

---

## 3. Datamodel

Eén tabel erbij. Het auditspoor bestaat al.

```sql
CREATE TABLE reports (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    case_reference   TEXT NOT NULL UNIQUE,      -- SN-2026-000123, zichtbaar voor de melder
    target_type      TEXT NOT NULL CHECK (target_type IN ('note','board_note','comment','board')),
    target_id        INTEGER NOT NULL,
    target_url       TEXT NOT NULL,             -- bevroren: de inhoud kan later verdwijnen
    reporter_user_id        INTEGER DEFAULT NULL REFERENCES users(id) ON DELETE SET NULL,
    reporter_participant_id INTEGER DEFAULT NULL REFERENCES board_participants(id) ON DELETE SET NULL,
    reporter_email   TEXT DEFAULT NULL,         -- verplicht als er geen account is
    reason           TEXT NOT NULL,             -- zie §4
    details          TEXT DEFAULT NULL,
    good_faith       INTEGER NOT NULL DEFAULT 0,-- artikel 16 lid 2 onder d
    status           TEXT NOT NULL DEFAULT 'received'
                     CHECK (status IN ('received','in_review','decided','withdrawn')),
    decision         TEXT DEFAULT NULL
                     CHECK (decision IS NULL OR decision IN
                            ('no_action','warning','content_removed','content_hidden',
                             'account_restricted','account_suspended','account_excluded')),
    decision_reason  TEXT DEFAULT NULL,         -- de motivering uit artikel 17
    decided_by       INTEGER DEFAULT NULL REFERENCES users(id) ON DELETE SET NULL,
    decided_at       DATETIME DEFAULT NULL,
    evidence_expires_at DATETIME DEFAULT NULL,  -- zie §7
    legal_hold       INTEGER NOT NULL DEFAULT 0,
    created_at       DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);
CREATE INDEX idx_reports_status ON reports(status, created_at);
CREATE INDEX idx_reports_target ON reports(target_type, target_id);
```

**Waarom `target_url` erin staat en niet wordt afgeleid:** de gemelde inhoud is vaak precies wat verdwijnt. Een zaak die na verwijdering niet meer te reconstrueren is, is geen zaak.

**Waarom er geen `report_actions`-tabel is:** elke handeling van een beheerder loopt al door `AdminAuditLogger`. Een tweede logboek betekent twee waarheden.

**Geen aparte bezwaartabel.** Bezwaar loopt via het e-mailadres uit de motivering en wordt vastgelegd als een tweede besluit op dezelfde zaak. Artikel 20 geldt niet voor jou; een portaal bouwen is werk zonder verplichting.

---

## 4. Categorieën

Overnemen uit `community-guidelines.md`, want die staan er al en zijn dus al gepubliceerd:

`spam_or_scam`, `threats_or_harassment`, `privacy_or_personal_data`, `impersonation`, `illegal_or_dangerous`, `sexual_content_or_child_safety`, `other`.

Twee regels:

- **`sexual_content_or_child_safety` gaat vóór alles.** Deze categorie krijgt een eigen e-mailonderwerp, verschijnt bovenaan de wachtrij en kent geen "no action" zonder dat je de melding zelf hebt gelezen. Artikel 18 kan hier verplichten om de politie te informeren.
- **Auteursrecht heeft een eigen route** en zit bewust niet in de lijst; dat staat al zo in het Help Centre.

---

## 5. De flow

```
melder                        systeem                         beheerder
  |                              |                                |
  | Report-knop ---------------> | zaak aanmaken, SN-2026-000123  |
  |                              | e-mail: "we hebben je melding" |
  | <-- bevestiging met nummer   | e-mail naar beheerder ---------> wachtrij /admin/reports
  |                              |                                |
  |                              | <----------------- besluit + motivering
  |                              | e-mail naar melder (uitkomst)  |
  |                              | e-mail naar betrokkene (art. 17)|
  |                              |                                |
  | bezwaar per e-mail --------> | tweede besluit op dezelfde zaak |
```

**Wat de melder ziet.** Een dialoog met de categorieën uit §4, een tekstveld en één zin: *"Reports are read by a person. You will receive a case reference by email."* Voor iemand zonder account is het e-mailadres verplicht; anders is er geen manier om te bevestigen en geen manier om artikel 16 lid 5 na te komen.

**Wat de melder daarna krijgt.**

> **We received your report — SN-2026-000123**
>
> Thanks for telling us. A person reads every report; we do not use automated moderation.
>
> What you reported: <target_url>
> Reason: <reason>
>
> We will email you when a decision has been made. Keep this case reference if you need to get back to us.

**Wat de betrokkene krijgt zodra er iets wordt beperkt (artikel 17).** Dit is de tekst die het meeste juridische gewicht draagt; elk onderdeel hieronder is een eis uit dat artikel:

> **A decision about your content — SN-2026-000123**
>
> **What we did:** <maatregel> — <wat er precies is geraakt>
> **Where it applies:** your account on StickyNotes.club, worldwide.
> **How long:** <permanent | tot <datum> | tot je iets doet>
> **Why:** <feiten en omstandigheden, in gewone taal>
> **On what ground:** <de regel uit de Terms of Service of de Community Guidelines, geciteerd, of de wettelijke grond>
> **Automated means:** no. A person reviewed this and made the decision.
> **If you disagree:** reply to this email within six months and we will look at it again, free of charge. You can also take the matter to a court, or to the Dutch Authority for Consumers and Markets as the Digital Services Coordinator.

**Wat er niet in mag staan:** een verwijzing naar "ons team". Er is één persoon. Artikel 17 vraagt om duidelijkheid, en een verzonnen afdeling is het tegenovergestelde daarvan.

---

## 6. Rollen, minste bevoegdheid en het auditspoor

- De wachtrij `/admin/reports` valt onder de bestaande adminafscherming (`AdminController::beforeRoute`).
- Elke opening van een zaak die een privébord raakt, schrijft `AdminAuditLogger::log('view', 'report', $id, ['target' => ...])`. D-24 eist een auditrecord van **elke inzage**, niet alleen van elke handeling. Dat is nu het ontbrekende stuk: verwijderen wordt gelogd, kijken niet.
- Een besluit schrijft naast de zaak ook een auditregel met de maatregel.
- Een beheerder mag de tekst van een auteur alleen wijzigen voor een redactie die aantoonbaar nodig is (bijvoorbeeld een telefoonnummer weghalen), en die wijziging wordt gelogd inclusief de reden. Dat staat al zo in 01 en 02; het ontbreekt in de code.

---

## 7. Bewaartermijnen

Uit D-24, ongewijzigd overgenomen:

- gewone zaken: bewijs vervalt na **zes maanden** (`evidence_expires_at = created_at + 6 maanden`);
- ernstige of herhaalde misstanden: **twaalf maanden**;
- een gedocumenteerde legal hold (`legal_hold = 1`) schort het vervallen op;
- een nachtelijk script ruimt vervallen zaken op, net als `cleanup_deleted_board_notes.php` en `cleanup_guest_participants.php` dat doen. Wat overblijft is een geanonimiseerde regel — categorie, uitkomst, datum — zodat je later kunt zien hoe vaak iets voorkwam zonder te bewaren wie het was.

De bezwaartermijn van zes maanden en de bewaartermijn van zes maanden zijn met opzet gelijk: bewijs dat verdwijnt vóór de bezwaartermijn verstrijkt, maakt bezwaar onmogelijk.

---

## 8. Fasering

**Fase 1 — vóór launch. Dit is de poort.**

1. Migratie `reports`.
2. Report-knop op publieke sticky note, bordnote, comment en bord, ook voor deelnemers zonder account.
3. Zaak aanmaken met zaaknummer, bevestigingsmail naar de melder, meldingsmail naar de beheerder.
4. `/admin/reports`: wachtrij, zaakdetail, besluit met motivering, koppeling naar de bestaande verwijder- en vlagacties.
5. Motiveringsmail volgens §5.
6. Auditregel bij inzage.
7. Help Centre terug naar de knop, en de Terms uitbreiden met het moderatiebeleid (artikel 14, samen met V-12).

*Schatting: twee tot drie dagen werk. Dat is de prijs van launchen zonder juridisch gat.*

**Fase 2 — na launch, als het volume erom vraagt.**

8. Opruimscript voor vervallen bewijs.
9. Herhaling zichtbaar maken: hoe vaak is deze auteur eerder gemeld.
10. Maatregelen met een einddatum (tijdelijke beperking die vanzelf afloopt).
11. Eenvoudige cijfers: aantal meldingen per categorie per maand. Niet verplicht (art. 15 lid 2 en art. 19), wel nuttig.

**Bewust niet:** intern klachtenportaal, trusted flaggers, geschillenbeslechting, transparantieverslag. Artikel 19 ontslaat je daarvan, en ze bouwen kost meer dan ze opleveren zolang je klein bent. **Let op:** die vrijstelling hangt aan je omvang. Groei je uit micro of klein, dan geldt er een overgangstermijn van twaalf maanden en daarna gelden artikel 20 tot en met 28 alsnog.

---

## 9. Vragen voor de jurist

1. Voldoet een e-mailadres aan artikel 16, of is een knop bij de inhoud vereist? Dit bepaalt of fase 1 een launchblokkade is of niet.
2. Is StickyNotes.club een *online platform* in de zin van artikel 3, of alleen een hostingdienst? De worldwide wall verspreidt inhoud onder het publiek; privéborden doen dat niet. Als het geen platform is, vervalt sectie 3 sowieso en blijft alleen sectie 2 over.
3. Valt de eenmanszaak aantoonbaar onder *micro of klein* volgens Aanbeveling 2003/361/EG, en hoe leg je dat vast voor het geval de ACM ernaar vraagt?
4. Moet het contactpunt uit artikel 11 en 12 apart en zichtbaar op de website staan, of volstaat de vermelding in het Help Centre en de Terms?
5. Is de motiveringstekst uit §5 volledig voor artikel 17, en klopt de verwijzing naar de ACM als beroepsinstantie?
6. Wanneer treedt artikel 18 in werking, en wat is de juiste route naar de Nederlandse politie?
7. Bewaartermijn: is zes maanden verdedigbaar, gelet op verjaringstermijnen bij onrechtmatige publicatie?
8. Moeten de Terms het moderatiebeleid uitschrijven (artikel 14), en kan dat in dezelfde ronde als V-12?

---

## 10. Acceptatiecriteria

- [ ] Een gemelde publieke sticky note levert binnen één minuut een zaak met zaaknummer op, en de melder krijgt een e-mail.
- [ ] Een deelnemer zonder account kan melden, met verplicht e-mailadres.
- [ ] Een zaak is niet af te sluiten zonder maatregel én motivering.
- [ ] De motiveringsmail bevat alle zes onderdelen uit §5.
- [ ] Het openen van een zaak op een privébord levert een auditregel op met actor, tijdstip en doel.
- [ ] Verwijderen via een zaak gebruikt de bestaande admin-verwijderroute en is dus onmiddellijk en definitief (C-08).
- [ ] Het Help Centre beschrijft de knop pas nadat hij bestaat.
- [ ] Een geautomatiseerde test dekt de hele keten, in de stijl van `scripts/test-account-deletion.php`.

---

## 11. Bronnen

- Digital Services Act, artikelen 11, 12, 14, 15, 16, 17, 18 en 19 — <https://www.eu-digital-services-act.com/Digital_Services_Act_Articles.html>
- Artikel 19 (uitzondering micro en klein) — <https://www.eu-digital-services-act.com/Digital_Services_Act_Article_19.html>
- Artikel 15 lid 2 (uitzondering transparantieverslag) — <https://www.eu-digital-services-act.com/Digital_Services_Act_Article_15.html>
- Nederlands toezicht door de ACM sinds februari 2025 — <https://www.rijksoverheid.nl/actueel/nieuws/2025/02/03/nederlands-toezicht-van-start-op-digitale-diensten-die-onder-de-dsa-vallen>
