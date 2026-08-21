# Juristenbriefing — deelnemen zonder account (V-12)

> Status: concept ter beoordeling door een jurist
> Datum: 21 augustus 2026
> Aanleiding: V-12, opgeworpen op 21 augustus 2026 onder C-09. Iemand levert inhoud aan een privébord zonder ooit een account te maken en dus zonder de voorwaarden te aanvaarden. De Terms of Service noemen die situatie nergens.
> Opgesteld door: Claude, geen jurist. Alles onder *Feiten* is nageslagen in de code; alles onder *Aannames* en *Concepttekst* moet worden getoetst voordat er iets live gaat.

---

## 1. Waar het over gaat, in één alinea

StickyNotes.club heeft sinds de workshopmodus een derde toegangsvorm naast "lid" en "uitgenodigde deelnemer": een **gastlink**. Wie die link of de bijbehorende QR-code opent, kiest een bijnaam en doet mee. Hij maakt geen account aan, aanvaardt dus geen voorwaarden, en levert vervolgens inhoud aan een bord van iemand anders — sticky notes, comments, harten en stemmen. Die inhoud blijft daar staan, ook als hij weggaat. De Terms of Service beschrijven wel gedeelde links, maar gaan er overal van uit dat er een account is.

---

## 2. Feiten, geverifieerd in de code op 21 augustus 2026

| Onderwerp | Wat de software doet | Waar |
|---|---|---|
| Toegang | Een deellink met `allows_guests = 1` laat deelname zonder account toe | `board_share_links`, migratie 013 |
| Identiteit | Elke deelnemer krijgt een rij in `board_participants` met een bijnaam en een gasttoken; het account is optioneel | migratie 011 |
| Wat een gast mag | Sticky notes plaatsen, comments plaatsen, één hart en één stem per note | `actor_key` met `UNIQUE(note_id, actor_key)` |
| Wat een gast niet mag | Uitnodigen, toegang beheren, links maken of intrekken, bordinstellingen wijzigen, andermans inhoud bewerken | `BoardService` |
| Vervaltermijn | Een gastlink krijgt **altijd** een vervaltijd: standaard 24 uur, maximaal 168 uur (7 dagen) | `BoardController::GUEST_LINK_DEFAULT_EXPIRY_HOURS` en `SHARE_LINK_MAX_EXPIRY_HOURS` |
| Intrekken | De eigenaar kan de link intrekken of de deelnemer verwijderen; de bijdragen blijven staan | `BoardService`, D-23 |
| Bewaartermijn bijnaam | Een nachtelijk script (03:45 UTC, `docker/crontab`) vervangt de bijnaam door **Participant** en wist het gasttoken na 30 dagen zonder activiteit; de bijdragen blijven | `scripts/cleanup_guest_participants.php`, `RETENTION_DAYS = 30` |
| Wat de gast te zien krijgt bij het meedoen | Een alinea over wat er wordt bewaard en hoe lang, plus links naar Privacy en Terms. Geen vinkje, geen akkoordknop | `app/resources/views/boards/join.html` |
| Wat de Terms zeggen | Niets over gasten, workshoplinks of deelnemen zonder account. §4 verbindt de leeftijdsgrens van 16 aan het **maken van een account**. §11 laat de gebruiker een licentie verlenen — iets wat een gast nooit doet. §13 beschrijft deellinks vanuit de eigenaar, niet vanuit degene die binnenkomt | `app/resources/pages/terms.md` |
| Wat de Privacy Policy zegt | Wél correct: workshoplinks, de bijnaam, de vervaltijd, het intrekken en de scheiding van bijnaam en bijdragen na 30 dagen staan er beschreven en zijn tegen de code gecontroleerd | vastgelegd onder C-09 |

---

## 3. De vijf gaten, van groot naar klein

**3.1 Er is geen overeenkomst.** De gast ziet een link naar de Terms en klikt niet op iets wat akkoord betekent. Dat is *disclosure*, geen aanvaarding. Gevolg: de verplichtingen die de Terms aan gebruikers opleggen — §14 Acceptable use voorop — binden hem vermoedelijk niet contractueel. Verwijderen wegens strijd met de huisregels rust dan op een zwakkere grond dan bij een lid.

**3.2 Er is geen licentie op zijn inhoud.** §11 is geformuleerd als *"You give us a non-exclusive, worldwide and royalty-free licence to host, store, reproduce, format and display your content"*. Een gast geeft die nooit. Toch wordt zijn sticky note gehost, weergegeven aan de rest van de zaal, meegenomen in back-ups en geëxporteerd naar de resultatenpagina. In de praktijk zal een impliciete licentie worden aangenomen — hij plakt zijn notitie immers zelf op het bord — maar dat is een aanname en geen afspraak.

**3.3 De leeftijdsgrens hangt aan het verkeerde moment.** §4 zegt: *"You must be at least 16 years old to create an account or use StickyNotes.club"*, en werkt dat vervolgens alleen uit voor het aanmaken van een account. Een gast maakt geen account. En juist de doelgroep uit `07_frontpage-voorstel` — docenten en trainers — zet een QR-code voor een klas op het scherm. **Dit is het punt waar ik me het meeste zorgen om maak**, omdat het niet alleen een contractueel gat is maar ook een AVG-vraag: verwerking van persoonsgegevens van kinderen, en de vraag wie daarvoor de grondslag levert.

**3.4 Onduidelijk wie verwerkingsverantwoordelijke is.** Een facilitator die namens zijn werkgever of school een sessie draait, bepaalt doel en middelen van wat er op dat bord gebeurt. Is StickyNotes.club dan verwerker voor die organisatie, of zelfstandig verantwoordelijke, of zijn ze gezamenlijk verantwoordelijk? Voor een betalende zakelijke klant wordt dit vrijwel zeker een vraag bij de inkoop, inclusief het verzoek om een verwerkersovereenkomst.

**3.5 De gast kan zijn eigen inhoud later niet weghalen.** Hij kan niet inloggen. Na 30 dagen wordt zijn bijnaam losgekoppeld van zijn bijdragen, wat de bijdragen praktisch anoniem maakt, maar in de tussentijd is er geen zelfbedieningsweg. Een verzoek loopt via de mail, en de eigenaar van het bord kan de note verwijderen.

---

## 4. Wat ik aanraad, en in welke volgorde

1. **Nu meteen, zonder jurist:** niets beweren wat niet klopt. In de documenten staat sinds vandaag dat gastbijdragen **niet** door de Terms worden gedekt zolang die niet zijn uitgebreid. Dat is al gebeurd (V-12 in `03_Product_Design_Notes.md`).
2. **Met de jurist, in één ronde:** de vragen uit §5 en de concepttekst uit §6. Neem hier ook artikel 14 DSA uit `spec-D-24-rapportage-en-moderatie.md` in mee — dat vraagt óók om een aanpassing van de Terms, en twee keer langs dezelfde jurist voor hetzelfde document is zonde.
3. **Pas daarna in het product:** het akkoordmoment op het join-scherm aanpassen als de jurist dat nodig acht. Het scherm moet in zestig seconden af — dat is een productbelofte ("no accounts, no installs") — dus als er een vinkje bij moet, dan één, met één zin.

---

## 5. Vragen aan de jurist

1. **Aanvaarding.** Is een link naar de Terms op het join-scherm voldoende om een gast te binden, of is een expliciete handeling nodig? Zo ja: volstaat "By joining you agree to the Terms" boven de knop, of moet er een vinkje bij?
2. **Licentie.** Is een impliciete licentie op de inhoud van een gast houdbaar, of moet §11 uitdrukkelijk naar hem verwijzen?
3. **Leeftijd.** Mag een gast jonger dan 16 zijn? Zo nee, hoe leg je dat af te dwingen zonder een account? Zo ja, welke grondslag geldt voor de verwerking van zijn gegevens, en wie moet daarvoor zorgen — wij of de facilitator?
4. **Rolverdeling.** Is StickyNotes.club bij een zakelijke of schoolsessie verwerker of zelfstandig verantwoordelijke? Is er een verwerkersovereenkomst nodig, en zo ja, moet die bij het Club Facilitator-plan worden aangeboden?
5. **Verantwoordelijkheid van de facilitator.** Kunnen we in de Terms opnemen dat de facilitator verantwoordelijk is voor wie hij uitnodigt en voor de rechtmatigheid van wat hij op dat bord laat verzamelen? Is dat afdwingbaar?
6. **Rechten van de gast.** Volstaat het e-mailadres voor inzage- en verwijderverzoeken, gegeven dat er geen inlog is? Is de scheiding van bijnaam en bijdragen na 30 dagen voldoende als bewaarbeperking?
7. **Moderatie.** Op welke grond kan inhoud van een gast worden verwijderd als hij geen partij is bij de Terms — de huisregels van de eigenaar, ons eigen beleid, of alleen onrechtmatigheid?
8. **Samenloop met artikel 14 DSA.** De Terms moeten het moderatiebeleid in begrijpelijke taal beschrijven. Kan dat in dezelfde wijzigingsronde?

---

## 6. Concepttekst — NIET publiceren voor akkoord

Bedoeld als vertrekpunt, in de stijl en toon van de bestaande `terms.md`. De jurist mag hier met een streep doorheen.

### 6.1 Nieuwe paragraaf, in te voegen als **§13a. Taking part without an account**

> Some private boards can be joined without an account, through a workshop link or QR code that the board owner creates. This section applies to you if you take part that way. In this section, "you" means the person taking part, and "the facilitator" means the owner of the board.
>
> **What joining means.** By entering a nickname and joining a board, you agree to these Terms and to our Privacy Policy for as long as you take part. You do not create an account, and we do not ask you for a password or an email address.
>
> **What you may do.** While the session is open, you may add sticky notes, add comments, give hearts and take part in dot voting, on the same terms as anyone else on that board. You cannot invite people, manage access, change the board or edit anyone else's content.
>
> **Your content.** You keep ownership of what you add. You give us the same licence described in section 11, limited to that board and to what is needed to show the board to the people taking part, keep it available to the facilitator afterwards, back it up, moderate it and comply with the law.
>
> **What happens to your contributions.** What you add belongs to the board, not to your visit. Your sticky notes and comments stay on the board when the session ends, when your link expires, when the facilitator removes you and when we separate your nickname from your contributions. If you want something you added removed, ask the facilitator, who can delete any sticky note on their board, or contact us.
>
> **How long your link works.** A workshop link always expires. The facilitator chooses how long, up to a maximum set by us, and can revoke the link or remove you at any time.
>
> **Your nickname.** Your nickname is visible to everyone on the board while you take part. We separate it from your contributions after a period of inactivity described in our Privacy Policy; the contributions themselves remain.
>
> **Age.** You must be at least 16 years old to take part without an account. If you are younger, you may only take part with the permission of a parent, guardian or school, and the facilitator is responsible for obtaining that permission.
>
> **Acceptable use.** Section 14 applies to you in the same way as to anyone with an account. We may remove content that breaks it, and we may block a workshop link.

### 6.2 Aanpassing van **§4. Eligibility**

Vervang de eerste zin door:

> You must be at least 16 years old to create an account. Section 13a explains the age rule for taking part in a workshop without an account.

### 6.3 Aanpassing van **§11. Your content**

Voeg toe na de eerste alinea:

> This section applies both to people with an account and to people taking part in a workshop without one. Section 13a explains how it is limited in that case.

### 6.4 Aanpassing van **§13. Private boards and sharing**

Voeg toe aan de lijst met verantwoordelijkheden van de eigenaar:

> - deciding whether people may take part without an account, and taking responsibility for who is in the room when they can.

---

## 7. Wat er in het product verandert als dit wordt vastgesteld

- `boards/join.html`: één zin boven de knop — *"By joining you agree to the Terms of Service and the Privacy Policy."* — en niets meer dan dat, tenzij de jurist een vinkje eist.
- De vermelding van de leeftijdsgrens op datzelfde scherm, kort.
- `03_Product_Design_Notes.md`: V-12 afvinken met de datum van het juridische akkoord.
- `01` en `02`: de zin dat gastbijdragen niet door de Terms worden gedekt, kan dan weg.

---

## 8. Bronnen

Alle feiten in §2 komen uit de codebase `stickynotes-club`, gecontroleerd op 21 augustus 2026. De genoemde bestanden en constanten zijn in die tabel opgenomen zodat de jurist ze kan laten verifiëren zonder de code te lezen.
