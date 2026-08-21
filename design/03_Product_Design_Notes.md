# Product Design Notes

> Status: living document
> Role: evidence, open questions, proposals and decisions that are not yet enduring rules
> Last reviewed: 21 August 2026

## How to use this document

- Add discoveries with their source or context.
- Keep open questions framed as decisions that can be answered.
- Separate current behaviour from proposals.
- Move accepted structural decisions to the Product Model or Playbook.
- Move user-facing, implemented behaviour to the Help Centre.
- Keep rejected ideas when the rationale will prevent repeated discussion.

## Review register

Use this as the master checklist while reviewing all five design documents.

- **ERROR** means a demonstrable correction; check it after fixing and verifying the affected files.
- **CONFLICT** means two sources disagree; choose which becomes authoritative before editing public claims.
- **DECISION** needs an explicit product or editorial choice.
- **VERIFY** needs evidence from the working product, checkout, operation or deployment.

Do not only tick an item. Add the outcome to the decision log or verification record, update every affected file and then check the box.

### Errors

- [x] **[ERROR E-01] Broken Help Centre routes — resolved on 20 July 2026.** All source links now use `/plans-and-subscriptions/` and `/organise-your-work/`. Repository history contains no matching old permalinks, so redirects were not required. Affects: several `docs/*.md` pages and Help Centre Architecture.
- [x] **[ERROR E-02] Inconsistent labels and English variants — resolved on 21 August 2026.** **Plans & subscriptions**, British English and British-English permalinks are canonical. **Owner** and **Participant** are the only board-role labels; member, collaborator, Editor, Viewer and Commenter are not canonical roles. The full audit was run on 21 August 2026 across the sixteen Help Centre pages, the three policy pages, the design documents and the application templates. Findings and corrections: the Help Centre was already clean — no US spelling, all fifteen permalinks British, the page title **Plans & subscriptions** correct, and the share-link wording already matching the amended D-23; `terms.md` said *collaborators* where **Participants** is canonical; `05_Documentation_Specification.md` carried *Organize your work* and *Help Center*; the interface still used *Color*, *Frame Color*, *Note Color* and *colors* in nine templates. All of these were corrected. Deliberately left in place: the sentences in `private-boards.md`, `01`, `02`, `03` and `04` that name Viewer, Editor and Commenter in order to state that those roles do **not** exist — contextual mentions of rejected terms, permitted by the rule below. Not touched: `www/js/app.js`, a minified bundle. Affects: product copy, all design files, Help Centre pages and policies.
- [x] **[ERROR E-03] Infrastructure contradiction — resolved on 20 July 2026.** Hetzner has been replaced by Fly.io. The application, database and stored content are hosted by Fly.io in Amsterdam; the domain uses Cloudflare for DNS, network delivery and security. `about.md` and `privacy.md` now agree. Affects: About and Privacy Policy.

### Conflicts

- [x] **[CONFLICT C-01] Public boards versus private-only boards — resolved on 20 July 2026.** Boards remain private and access-controlled. Only individual sticky notes can be public on the worldwide wall. Public boards and board publishing are rejected from the product model. Affects: Product Model, Playbook terminology, Help Centre and policies.
- [x] **[CONFLICT C-02] Editable versus immutable notes — resolved on 20 July 2026; privileged-editing boundary refined under D-24 on 22 July 2026.** Authors can edit all their sticky notes. Authorised moderators and administrators may view content when D-24 permits, hide, remove or restore it, and alter text only for a narrowly necessary, audited redaction. Board owners and ordinary Participants cannot rewrite another author’s note. Affects: product behaviour, Product Model, Help Centre and policies.
- [x] **[CONFLICT C-03] “Note” versus “sticky note” — resolved on 20 July 2026.** **Sticky note** is the canonical product term and must be used in titles, navigation, buttons, first mentions and formal definitions. **Note** is allowed as shorthand afterwards when unambiguous. Do not use post, card, item or content as alternative product names. Affects: all five design files, interface and Help Centre.
- [x] **[CONFLICT C-04] Personal capture versus the current context model — resolved on 20 July 2026.** Personal capture uses Drafts and unshared private boards that are hidden from other ordinary users. Authorised platform moderators and administrators retain privileged access to all Drafts, boards and sticky notes. There is no separate personal inbox or third content context. Affects: Constitution, Product Model, onboarding, Help Centre and Privacy Policy.

The seven conflicts below were found on 21 August 2026 by comparing the design set against the application code. They share one cause: workshop mode shipped without passing through this register. C-05 is the structural conflict; C-06 to C-11 are largely its consequences.

- [x] **[CONFLICT C-05] Workshop mode exists in the product and in no design document — resolved on 21 August 2026.** The session is described as a third product context in the Product Model, with its own lifecycle, its own invariants and a *Workshop rules* section in the Playbook. The Constitution's product boundaries now state what a session is deliberately not. Still open: the Help Centre Architecture navigation is built capture-first and has no place for running or joining a session, and `04` records no session page type. The words *workshop*, *guest*, *timer*, *spotlight*, *lobby* and *QR* appear nowhere in the Constitution, Product Model, Playbook or Help Centre Architecture, while migrations 011 to 017 and `WorkshopService`, `BoardActor` and `BoardParticipant` implement a complete session context with participants who have no account. The homepage sells it as the primary product. Until the context is described, no rule about roles, rights, deletion or communication can be complete, because all of them were written for a world with only Owner and Participant. Resolve by adding a third product context to the Product Model, a participant record as an object distinct from an account, and a *Workshop rules* section to the Playbook. Affects: Constitution, Product Model, Playbook, Help Centre Architecture, Help Centre pages.
- [x] **[CONFLICT C-06] Positioning: facilitated sessions versus capture-first — resolved on 21 August 2026 under D-30.** The site leads with *Run a focused workshop in minutes* and addresses facilitators, while *Who we serve* described an audience explicitly not served by team software and the Playbook pillars led with capture. Resolved by making facilitated sessions the primary use and lead commercial story while keeping D-01 as the product promise. Affects: Constitution (v1.3), Playbook (v1.4); Help Centre Architecture navigation still follows the old order.
- [x] **[CONFLICT C-07] Plan names published before the entitlement gate was passed — resolved on 21 August 2026.** The entitlements the product already grants are now recorded in D-29 and the Product Model, and the gate is replaced by the verification that genuinely remains. D-29 required that the ladder not be published until Club Facilitator pricing and entitlements were decided and the migration verified. `RoleHelper` serves the four names, migration `010_facilitator_tier.php` created the tier and the pricing page sells it, while D-13 and D-27 still describe three plans and no document records the Club Facilitator entitlement that the code applies (`max_private_boards_pro`, default 15). Resolve by recording the entitlement in D-29 and the Playbook plan rules, then replacing the gate with the verification that genuinely remains. Affects: Product Model, Playbook, pricing page, checkout, Help Centre.
- [x] **[CONFLICT C-08] Deletion: immediate permanence versus soft delete with Undo — resolved on 21 August 2026 under the D-21 amendment.** Migrations 013 and 014 introduced soft delete with a restore path for every private board, not only workshop boards, while D-21 forbade promising Undo. Resolved by layering deletion per object: private-board sticky notes get a restore window, Public sticky notes, comments and boards stay immediately permanent, and moderation deletion is always permanent. Checked: Terms and Privacy Policy make no promise about individual sticky-note deletion, so no policy change was required. Affects: Product Model, Playbook, `troubleshooting.md`, `collaboration.md`, `sticky-notes.md`.
- [x] **[CONFLICT C-09] Guests contribute where D-23 says link users cannot — resolved on 21 August 2026.** D-23 is amended with a third link type. Note for the record: the **public** documentation was not behind here. The Privacy Policy and *Privacy & safety* already described workshop links, the nickname, the expiry, revocation and the 30-day separation of nickname from contributions, and all of it was verified against the code. Only the Product Model and the Playbook were out of date. One genuine gap remains, recorded as V-12: the Terms say nothing about taking part without an account. D-23 states that link access never grants comments, hearts, dot votes or Participant status. `board_participants` gives every attendee an identity with or without an account, `actor_key` carries a guest's single heart and single vote, `board_note_comments` holds a `participant_id`, and `board_share_links.allows_guests` makes accountless participation an explicit per-link choice. The rights model changed from *do you have an account* to *which actor are you on this board*, and the documents do not know it. Affects: Product Model, Playbook, Help Centre.
- [x] **[CONFLICT C-10] Voting notice: votes used versus votes left — resolved on 21 August 2026.** V-03, the Product Model and the Playbook prescribed **you have used 0 of 3 votes**; the product shows votes remaining. The implementation is the better one: a participant needs to know how many decisions are still theirs, not how many they have made. Documents corrected to the product. Affects: Product Model, Playbook, V-03.
- [x] **[CONFLICT C-11] Delete confirmations diverged from the prescribed copy — resolved on 21 August 2026.** Here the documents were right and the product was behind: the Public sticky-note control read *Are you sure you want to delete this note?* without the cascade, without the external-copy warning and using **note** where C-03 makes **sticky note** mandatory; the comment control carried only the heading; the board control used its own wording. Five templates were corrected and the Public confirmation is now status-aware, because the external-copy warning is true for a published sticky note and misleading for a Draft. Affects: `notes/show.html`, `notes/index.html`, `partials/notes-wall.html`, `boards/_note_card.html`, `boards/show.html`, V-09.

### Product decisions

- [x] **[DECISION D-01] Canonical product promise.** Resolved on 20 July 2026: use **A place where ideas can grow together.** as the official product promise and tagline. Use the full sentence with “StickyNotes.club is” only when grammatically necessary in ordinary prose.
- [x] **[DECISION D-02] Personal capture model.** Resolved on 20 July 2026: a worldwide-wall sticky note remains hidden from other ordinary users while it is a Draft; an unshared private board remains hidden from other ordinary users. Authorised platform moderators and administrators retain privileged access. No separate personal inbox is needed.
- [x] **[DECISION D-03] Nature of responses.** Resolved on 20 July 2026: on the worldwide wall, a signed-in user can place a heart and no other public response exists. On private boards, invited participants can comment under a sticky note, place a heart and use dot voting. Comments are ordinary comments, not sticky notes, and have no Draft/Public status.
- [x] **[DECISION D-04] Candidate feature scope.** Resolved for the current roadmap on 20 July 2026; image-content boundary clarified by Q-01 on 22 July 2026: search, an in-product activity screen, pins, priority, general attachments and bulk, board-level or structured export are parked rather than planned. Q-01’s single image is content inside the defined sticky-note or Instant Photo object, not a general attachment system; URLs, link previews and other uploaded file types remain absent. Saving one sticky note as an image already exists under D-11, and favourite behaviour already exists through public hearts and the Wall of Love under D-10. The D-08 daily email digest belongs to the current notification model rather than this candidate-feature list. Archiving a complete private board is the only future product feature currently under consideration. The V-04 real-time, autosave, conflict and failure requirements improve the reliability of existing private-board capabilities and therefore do not add a separate candidate feature.
- [x] **[DECISION D-05] Note and board lifecycle controls.** Resolved on 20 July 2026: individual sticky notes have no Completed or Archived status. The only future archive feature under consideration applies to a complete private board, including all sticky notes, comments, hearts and dot votes; only the Owner or an authorised platform moderator or administrator may archive it.
- [x] **[DECISION D-06] Default visibility.** Resolved on 20 July 2026: a worldwide-wall sticky note starts as a Draft hidden from other ordinary users and becomes visible to them after deliberate publication as Public. A private-board sticky note inherits board access; an unshared board is hidden from other ordinary users. Authorised platform moderators and administrators can access all Drafts, boards and sticky notes.
- [x] **[DECISION D-07] Collaboration roles.** Resolved on 20 July 2026; Owner deletion boundary added on 21 July 2026: the only board roles are Owner and Participant. Participants join by invitation and receive full participation rights rather than a configurable role. Authors may edit and delete their own sticky notes and comments. On an active board, the Owner may delete any sticky note but may not edit another author’s text or separately delete another author’s comment. The Owner also manages invitations, Participant access and the board; moderators/admins remain separate platform roles.
- [x] **[DECISION D-08] Activity and notifications.** Resolved on 21 July 2026; mention email added under Q-03 on 22 July 2026: email is the only channel. A private-board invitation expires after 14 days and triggers an immediate email. Declining grants no access, appears to the Owner as **Declined** and sends no separate Owner email. Revoking Participant access takes effect immediately and sends the former Participant an immediate email. Explicitly mentioning one or more current board Participants sends each named person an immediate email. A scheduled daily job sends at most one activity digest and only when a private board accessible to the recipient has changed. No in-product activity inbox or other immediate emails for individual edits, comments, hearts or dot votes. Operational verification remains listed below.
- [x] **[DECISION D-09] Product search and filtering.** Resolved on 20 July 2026: product search does not exist and is not planned. Private boards can filter sticky notes by tags. The worldwide wall can filter Public sticky notes by country; this does not create public boards.
- [x] **[DECISION D-10] Favourite, pin and priority.** Resolved on 20 July 2026; removal lifecycle resolved on 21 July 2026: a heart on a Public sticky note is also a favourite and adds that sticky note to the user’s private Wall of Love. Unhearting removes the entry and subtracts one. Public → Draft, deletion and moderation removal clear all heart/favourite relationships; republishing does not restore them. Only that user can view the Wall. Private-board hearts do not appear there. Pin and priority do not exist and are not planned. Public profile visibility is parked. V-10 verifies implementation.
- [x] **[DECISION D-11] Export promise.** Resolved on 20 July 2026: a user can save an eligible individual sticky note as an image, but this option is unavailable for Drafts. Bulk, board-level and structured product export do not exist and are not planned. Requests for access to or portability of personal data continue through the privacy process by email and are not a product feature.
- [x] **[DECISION D-12] Post-publish experience.** Resolved on 20 July 2026; disclosure expanded under Q-05 on 22 July 2026: a Public sticky note appears immediately on the worldwide wall and the user receives a calm success message without confetti. The published sticky note can immediately be viewed, shared, edited or returned to Draft. Use contextual copy plus Privacy Policy and Terms to explain search indexing, persistent external copies, caches and external AI use. Do not use “the world’s largest wall”.
- [x] **[DECISION D-13] Core experience per tier.** Resolved on 22 July 2026; extended to four tiers and downgrade route revised on 21 August 2026 under C-07: Club Member can keep 1 owned private board active and editable, Club Host 5, Club Facilitator 15 and Chosen Few unlimited; boards joined as a Participant do not count. Only Club Host and above can send invitations or create share links, and only Club Facilitator and above can run a workshop session; Club Members can receive invitations and participate fully. Comments, private-board hearts, dot voting and private-board sticky-note tags and due dates are included on all plans. Daily Public sticky-note allowances count successful **Draft → Public** transitions, including republication, and reset at **00:00:01 UTC**. Draft and private-board creation or editing, edits to existing Public sticky notes and failed publication attempts do not count. On downgrade, the Owner selects which owned boards remain editable and sees all others listed before confirming; the remainder become read-only rather than archived, and upgrading restores editing on all of them. The earlier automatic-archival rule was withdrawn because archiving does not exist and a downgrade must not wait on a feature that has not been built.
- [x] **[DECISION D-14] Help-page length and granularity.** Resolved on 20 July 2026: “readable in under two minutes” is a soft guideline for ordinary Help Centre pages. Necessary privacy, billing, deletion, access, safety and troubleshooting information always takes precedence. Split pages by distinct user goal, not to satisfy a word-count limit.
- [x] **[DECISION D-15] Documentation language convention.** Resolved on 20 July 2026: use British English in all text and permalinks. **Plans & subscriptions** and `/organise-your-work/` are canonical. The old US-spelled permalink is intentionally not retained as a redirect so breakage is discovered early.
- [x] **[DECISION D-16] Understanding section.** Resolved on 20 July 2026: do not create a separate Understanding section. Keep practical concept explanations such as Public versus Private and dot-voting rules with the relevant Help Centre task; put broad product positioning on the marketing site; provide short contextual guidance in the interface at the point of choice.
- [x] **[DECISION D-17] Public → Private transition.** Resolved on 20 July 2026: no direct copy, move, reference, create-board-from or add-to-board flow is planned. Viewing, sharing and saving an eligible Public sticky note as an image remain independent actions and do not create board membership or transfer ownership.
- [x] **[DECISION D-18] Colour semantics.** Resolved on 20 July 2026: keep sticky-note colours expressive and do not assign product-wide meanings. Use visible tags or labels for explicit organisation. Informal board-specific colour conventions may exist, but meaning must never depend on colour alone.
- [x] **[DECISION D-19] Board shape and limits.** Resolved on 20 July 2026; Brainstorm layout verified on 21 July 2026: board creation offers Blank, Retro, Kanban, Week planner and Brainstorm templates. Blank and Brainstorm are structurally identical grids that can later change to columns; they differ only in default background and product framing. Retro, Kanban and Week planner start with columns. Sticky notes can be reordered within a row and moved between columns. Nine backgrounds are available, boards cannot be duplicated and currently grow without a product-defined limit.
- [x] **[DECISION D-20] Public-content lifetime and unpublishing.** Resolved on 20 July 2026; account-deletion exception added on 21 July 2026 and external-use consequence added under Q-05 on 22 July 2026: a Public sticky note remains Public without an automatic or author-selected expiry until its author returns it to Draft or deletes it, or authorised moderation removes it. If the author deletes their account first, the Public sticky note remains after de-attribution, loses author controls and receives the V-06 tape and accessible deleted-account state. Returning a sticky note to Draft removes it from the worldwide wall and current intentional discovery mechanisms but cannot recall independent copies, saved images, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred.
- [ ] **[DECISION D-21] Deletion and recovery — partly resolved; technical-backup period resolved on 22 July 2026; layered per object on 21 August 2026 under C-08.** A sticky note on a private board leaves the board immediately and can be restored by the same person for a short window, after which it is purged; the restore permission is deliberately identical to the delete permission. A Public sticky note, a comment and a board are deleted immediately and permanently after confirmation, with no Undo or recovery period, and moderation deletion is always permanent for every object. State that a restore window exists without stating its length in copy that a settings change would falsify. The original wording read: *Sticky-note, comment and board deletion is immediately permanent after confirmation, with no Undo or recovery period.* V-09 resolves ordinary cascades and canonical copy: sticky-note deletion includes its comments, hearts and dot votes; comment deletion affects only that comment; board deletion includes all board content and interactions and removes Participant access and pending invitations without deleting accounts. Account deletion follows V-06. Deleted data may remain in protected technical backups for no more than 30 days, without ordinary product access or user-facing recovery. Implementation, counters, backup expiry and the separate legally required record periods still require verification.
- [x] **[DECISION D-22] Board ownership.** Resolved on 20 July 2026: every board has exactly one non-transferable Owner. Ownership cannot be transferred to a Participant or reassigned by a moderator or administrator. The Owner remains involved while the idea develops. Deleting the Owner’s account permanently deletes every board owned by that account and all content and access attached to those boards.
- [x] **[DECISION D-23] Invitations and controlled share links.** Resolved on 20 July 2026; invitation lifecycle completed under D-08 on 21 July 2026; share-link model revised and authorisation verified on 23 July 2026: Participant access remains personal, account-based and invitation-led. Invitations expire after 14 days; declining grants no access; Participant revocation is immediate and triggers an email. Only an Owner with the D-13 Premium or Chosen Few collaboration entitlement may create a View or Post link; Participants cannot create links. A **View link** shows a read-only board to anyone with the link without requiring an account. A **Post link** additionally lets a signed-in StickyNotes.club user on any plan add sticky notes. Link users are not Participants and receive no comments, hearts, dot votes or board-management rights. Links are inaccessible without the Owner’s collaboration entitlement, while the Owner can revoke an existing link regardless of plan.
- [x] **[DECISION D-24] Platform moderation and administrative access — behaviour resolved on 22 July 2026; implementation and legal verification required.** Moderators and administrators use the same content-moderation capabilities and privileged access only for genuine moderation, support, security or legal work, with least privilege and an audit record of every view and action. They may hide, remove or restore content but may alter an author’s words only for a narrowly necessary, audited redaction. Reports target a sticky note, comment or board, return an immediate case reference and receive human final review. Proportionate outcomes range from no action and warnings through temporary restrictions to removal, suspension or permanent exclusion. Existing contributions remain unless separately removed. Decisions include reasons and a free six-month appeal; necessary evidence expires after six months for ordinary cases or twelve months for serious or repeated abuse, subject to documented legal holds. User-to-user blocking is not planned without direct communication or visible Public-author profiles. Verify the complete workflow and its DSA, privacy and emergency-reporting obligations before launch.
  - **Specified on 21 August 2026:** `design/spec-D-24-rapportage-en-moderatie.md` turns this decision into an executable brief — a single `reports` table, the flow from report to decision to appeal, the exact statement-of-reasons email, retention, and a two-phase plan in which phase one is the launch gate at roughly two to three days of work. **The legal picture is lighter than feared.** Article 19 DSA exempts micro and small enterprises from Section 3, so no internal complaint portal (Art. 20), no out-of-court dispute settlement (Art. 21), no trusted flaggers (Art. 22) and no platform transparency report (Art. 24(1)-(2)); Article 15(2) removes the intermediary transparency report as well. What does apply regardless of size: Article 16 (notice and action), Article 17 (statement of reasons), Article 18 (suspicions of criminal offences) and the contact points in Articles 11 and 12. In the Netherlands the ACM supervises this. **Found while specifying, and fixed the same day:** the Help Centre instructed people to *"Use **Report** on the relevant sticky note, comment or board"* — a control that does not exist anywhere in the application. `community-guidelines.md` and `privacy-and-safety.md` now name the email route and say the control is still being built. Three links to `https://stickynotes.club/tos/` were also broken; the route is `/terms`.
- [x] **[DECISION D-25] Public profile fields.** Resolved on 20 July 2026; account-deletion indicator and metadata lifecycle added on 21 July 2026; implementation verification required: a Public sticky note shows no author identity or profile route. It shows a UTC-derived **YYYY/MM/DD** publication date, the user-selected account country copied at sticky-note creation, a completed-action share count and an active-heart count. The country snapshot remains stable. Each successful **Copy link** or **Save as image**, including repeats, adds one. Public → Draft clears hearts/favourites, resets both counts and causes a later publication to receive a new date. After account deletion, the retained note keeps its metadata and other users’ hearts but loses the account relationship and author controls and shows the V-06 tape and accessible state. Public profile visibility remains parked and the Wall of Love remains user-only.
- [x] **[DECISION D-26] Note ownership inside boards.** Resolved on 21 July 2026: editing is reserved for the sticky note’s author and authorised platform moderators or administrators. Each private-board sticky note belongs to exactly one board and remains when its author leaves, loses access or deletes their account; after account deletion its displayed author becomes **Deleted user**. The author may delete it beforehand. On an active board, the Owner may permanently delete any sticky note, including a Participant’s, using the V-09 warning and cascade, technical logging and conditional daily-digest notification. This does not grant editing or separate deletion of another author’s comment. Moderator and administrator deletion remains under D-24. Draft/Public statuses do not apply to board sticky notes.
- [x] **[DECISION D-28] Private ownership and Public relinquishment.** Resolved on 22 July 2026: users retain ownership of content they create or share inside private boards. Publishing a sticky note or Instant Photo to the worldwide wall explicitly relinquishes ownership without transferring it to StickyNotes.club. The Public object is not linked visibly to a person; country is its only origin information. A private internal relationship remains while the account exists only for author controls and authorised moderation. Legal and policy alignment remain required.
- [x] **[DECISION D-29] Plan names, order and Club Facilitator entitlement.** Resolved on 3 August 2026; entitlement recorded on 21 August 2026 under C-07. Club Facilitator grants everything in Club Host plus workshop mode on owned boards, participation by people without an account up to the configured session limit (default 50), and up to fifteen active owned private boards (default), at a higher price than Club Host. Its daily publication allowance deliberately equals Club Host's. Chosen Few includes workshop mode. The stored role identifiers stay `user`, `premium`, `pro` and `chosen_few`. The public tier order is **Club Member → Club Host → Club Facilitator → Chosen Few**. Club Member replaces Free, Club Host replaces Premium, Club Facilitator is a new tier between Club Host and Chosen Few, and Chosen Few keeps its name. This decision establishes names and order only; Club Facilitator pricing, limits and entitlements still require a separate decision and implementation verification before public documentation changes.
- [x] **[DECISION D-30] Lead with facilitated sessions. Resolved on 21 August 2026.** Facilitated sessions are the primary use of StickyNotes.club and the lead commercial story. **A place where ideas can grow together** remains the product promise and tagline under D-01 and is not replaced; public surfaces may lead with the session outcome — *Run a focused workshop in minutes* — as long as the promise stays the umbrella over sessions, capture, private boards and the worldwide wall. Supersedes the audience description in *Who we serve* and the pillar order in the Playbook's *Marketing and positioning*. The worldwide wall is not demoted to a secondary product; it serves discovery rather than facilitation. Two claims now carry the positioning and must remain literally true because a prospect can check both in a minute: **one facilitator, no seat licences** and **no accounts or installs for participants**.
- [x] **[DECISION D-31] Which source is authoritative when a document and the code disagree. Resolved on 21 August 2026.** For **behaviour** — what the product actually does — the implementation is authoritative; a difference is a documentation defect and is corrected in the document, unless the implementation crosses an explicit boundary set in the Constitution or the Product Model. For **intent** — purpose, positioning, product boundaries, plan promises and release gates — the documents are authoritative, and a difference is a product finding recorded here rather than a fact to be written down. Tiebreaker: a passage that *describes* is behaviour, a passage that *permits, forbids, promises or gates* is intent; when it stays unclear, treat it as intent. Code that outruns intent is not reverted or blocked but recorded as a CONFLICT and settled before the next release touching the same area. The rule lives in the Constitution under *Governance* (v1.4). It retroactively ratifies the resolutions of C-06, C-08, C-10 and C-11, which were made on this assumption before it was decided.
- [x] **[DECISION D-27] Number of boards and plan limits.** Resolved on 20 July 2026; refined on 21 July 2026; extended to four tiers on 21 August 2026 under C-07: Club Member permits 1 active, editable owned private board, Club Host 5, Club Facilitator 15 and Chosen Few unlimited. Boards joined as a Participant do not consume the allowance. The numbers are settings with these defaults, not constants; copy that states them must read them from the product.
- [x] **[QUESTION Q-01] Sticky-note content types — behaviour resolved on 22 July 2026; accessibility and implementation verification required.** On the worldwide wall, a user publishes either a text sticky note or an **Instant Photo**: one image in a Polaroid-like frame with a caption. Both Public forms use the same Draft/Public lifecycle, publication allowance, metadata, hearts, sharing, moderation and deletion rules. On private boards, users create only sticky notes, each with one optional image. Images are the only uploaded file category and each is limited to **5 MB**. Sticky-note text and Instant Photo captions reject URLs and provide no links or previews. Images inherit the parent object’s visibility, ownership, moderation and deletion lifecycle. The current alternative text **Instant Photo** is inadequate; design and verify accessible alternative-text capture and presentation. Exact image formats, dimensions and processing remain implementation details. Q-01 does not change the D-13/V-05 plan entitlement for Instant Photos.
- [x] **[QUESTION Q-02] Edit history — resolved on 22 July 2026; implementation verification required.** Sticky notes and Instant Photos keep no history or previous versions. Accepted changes to text, caption, colour, tags and due date overwrite the current value; image replacement or removal and future alternative-text changes likewise create no version. Tags and due dates apply only where supported and never create a Public expiry. Autosave, unsaved local text, V-04 conflict handling and D-24 records remain separate reliability or accountability mechanisms and do not provide a revision timeline or restoration source.
- [x] **[QUESTION Q-03] Assignment and mentions — resolved on 22 July 2026; implementation verification required.** Sticky notes have no assignee, responsible person or assignment lifecycle. A private-board contribution may mention one or more current board Participants, and each mentioned person receives an immediate notification email. A mention draws attention only and never changes authorship, ownership, board access, edit or deletion rights, due date or responsibility. Public sticky notes and Instant Photos do not support mentions. Verify entry locations, duplicates, access changes, delivery and digest interaction.
- [x] **[QUESTION Q-04] Organisation details — resolved on 22 July 2026; implementation verification required.** Tags and due dates belong only to sticky notes on private boards, not to boards or Public content. Tags are scoped per board and automatically converted to lower case. The Owner and every current Participant may create, rename and delete them under ordinary board rights; tags cannot be merged. Deleting a tag removes only the label from affected sticky notes. A passed due date appears on the sticky note with a red clock icon and the expired date. Due dates cannot be filtered and send no reminder email or other notification; they remain visual attention signals without assignment or expiry semantics.
- [x] **[QUESTION Q-05] Public indexing and external AI use — resolved on 22 July 2026; implementation, policy and legal verification required.** Every Public sticky note and Instant Photo may be crawled, indexed, cached and shown by external search engines. Their public text and images may also be processed or used by external AI services, including to train, improve, evaluate or operate AI systems. There is no separate per-object search or AI opt-out. Drafts and private-board content remain unavailable for public crawling. Before publication, disclose external indexing, caching and AI use. Return to Draft, deletion or moderation removal stops public serving and future intentional discovery but cannot recall existing search results, caches, AI datasets, model training or other external uses. De-attributed Public content retained after account deletion remains eligible until moderation removes it.
- [x] **[QUESTION Q-06] Private-board recency — resolved on 22 July 2026; implementation corrected on 23 July 2026, verification required.** Show **Last modified on YYYY/MM/DD** on each board in the board overview. Board creation sets the initial value; accepted user-visible content, organisation, collaboration, access and board-setting changes update it. Merely opening or viewing a board, failed or unsaved attempts, background maintenance, backups and privileged access without a visible mutation do not. `Board::touch()` now provides one central activity clock and is called after successful mutations. The overview also derives historical activity from existing timestamps while preserving stable `created_at DESC` ordering. Do not show an inactivity label or threshold, send inactivity email or notification, or automatically archive, restrict or delete a board.
- [x] **[QUESTION Q-07] Commercial positioning — resolved on 22 July 2026; content and commercial verification required.** Private collaboration is the primary paid-value story. Use **Free is for capturing and joining. Premium is for bringing people together around your own ideas. Chosen Few is for people who want no practical plan-level volume limits.** Higher publication and board volume, organisation and personalisation support this narrative. Do not position payment mainly as escaping an artificial Free restriction, imply reduced collaboration rights for invited Free Participants or suggest that Chosen Few removes safety, content, file, technical or other non-plan boundaries. Q-07 changes no D-13 or D-27 entitlement.

### Verification items

- [x] **[VERIFY V-01] Board creation fields.** Resolved on 20 July 2026: board creation contains a required **Name** field, an optional **Description** field and a template choice with **Blank** selected by default. There is no visibility choice, central-question field or desired-result field; every board is private by definition. Template layouts are resolved under D-19 and V-08.
- [x] **[VERIFY V-02] Future board archive behaviour.** Resolved on 20 July 2026: archiving remains a future feature for a complete private board. An archive preserves all sticky notes, comments, hearts and dot votes indefinitely and is read-only for the Owner and existing Participants. The Owner can revoke existing access; pending invitations are cancelled, new invitations are unavailable and routine activity and daily-digest notifications stop. Only the Owner or an authorised platform moderator or administrator may archive, restore or permanently delete it. Restoration reactivates the board for remaining Participants without reviving cancelled invitations; privileged moderation remains available under D-24.
- [x] **[VERIFY V-03] Interaction details.** Resolved on 20 July 2026: Public signed-in users can place hearts. A Public sticky note offers **Copy link** to place its direct link on the clipboard and **Save as image** to generate an independent image suitable for storage or social media. Invited private-board Participants can post and delete their own comments, but cannot edit them. A private-board heart is a personal toggle: the first click changes it from light to red and adds one to the displayed count; the next click changes it back to light and subtracts one. Only the Owner starts and closes a voting round and chooses 1, 3, 5 or 10 dots per Participant, with 3 selected by default. A Participant may place at most one dot per sticky note, withdraw a vote while the round is active and see results only after the Owner closes it. There is no reset or reopening. Above the sticky notes, the active notice reads **Voting is open — you have 2 votes left. Votes stay hidden until the round is closed.**, showing what remains rather than what has been used (corrected on 21 August 2026 under C-10; the notice previously read **you have used 0 of 3 votes**). A vote control dims once the Participant is out of votes, but only on sticky notes they have not voted on, so withdrawing a vote always remains possible. After closure, the latest results appear with **Showing the results of the last voting round (closed 2026/07/20).**, using the actual closing date; each sticky note that received a vote shows a voting-round icon and count. Starting a new round permanently makes the previous round and its results unavailable without a warning. Immediate interaction emails do not exist; digest details remain under D-08, real-time behaviour under V-04 and the Public share counter under V-10. Plan availability is resolved under D-13.
- [x] **[VERIFY V-04] Real-time collaboration — resolved on 29 July 2026.** Accepted private-board sticky-note creation, editing, deletion and movement, comments, hearts, votes and voting-round state changes synchronise to other active viewers within approximately four to five seconds without a refresh, including through View and Post links. Editable sticky-note text autosaves after 1.5 seconds and on blur with visible saving, saved and failed states. Unsaved text is preserved locally through connection or server failure, with automatic and manual retry. Simultaneous text changes retain the local version and present **Save my version** or **Use theirs** instead of silently applying last-write-wins. Hearts, votes and position changes use the server-accepted state. Verified across two browsers and with an automated browser harness covering live changes, autosave, connection loss, failed requests, simultaneous edits and permission loss.
- [ ] **[VERIFY V-05] Current plan enforcement — scope extended on 21 August 2026 under C-07; selection step and read-only state built on 21 August 2026.** Compare documented limits and prices with application entitlements, checkout and tax display across all four tiers. Verify that a downgrade warns before it completes, requires the Owner to select which owned boards remain editable (1 for Club Member, up to 5 for Club Host, up to 15 for Club Facilitator), refuses an invalid selection, makes the remainder read-only without archiving, moving or deleting anything, states the read-only condition on the board itself and restores editing on every board after an upgrade.
  - **Built on 21 August 2026 (migration 018):** `boards.keep_editable` holds the Owner's choice. `BoardService::isOwnBoardWritable()` no longer picks the boards itself; `writableOwnBoardIds()` orders by `keep_editable DESC, created_at ASC, id ASC` and takes the plan's limit, so a chosen board always wins and unused places fall back to the oldest boards. `/boards/editable` is the selection screen, refuses more than the limit with a message rather than silently truncating, and is reachable before anything goes read-only. The board page states the condition itself: the flash that vanished on the next click was replaced by a banner that lasts as long as the state does, with the selection step for the Owner and a plain explanation for a Participant. The board overview shows the same prompt when an Owner is over the limit. Verified by six scenarios against SQLite (no choice, full choice, partial choice, over-choice, a limit that shrinks below the choice, limit 1) and by compiling every changed template.
  - **Still open:** the warning *before* a downgrade completes — today the choice is offered after the fact, which keeps the promise but not the order; the four-tier comparison of limits, prices, checkout and tax display; and restoration after an upgrade (expected to be automatic, because an unlimited plan short-circuits the query, but untested).
- [ ] **[VERIFY V-06] Account deletion — behaviour resolved on 21 July 2026; 30-day technical-backup period resolved on 22 July 2026; implemented and verified in code on 21 August 2026; legal record periods and backup deletion still open.** The confirmation must explain and the implementation must perform: remove profile, credentials, preferences, Drafts, personal heart relationships and the private Wall of Love; end future subscription renewal; permanently delete every owned board with its content and access; preserve sticky notes and comments on other Owners' boards under **Deleted user**; remove the account relationship from dot votes while preserving anonymous totals; retain Public sticky notes after removing their internal account relationship and author controls; add a small strip of tape at the top with the accessible explanation **This sticky note remains after its author deleted their account.**; warn that external copies cannot be recalled; deny ordinary product access and recovery from backups; and delete protected backup copies within 30 days.
  - **Found on 21 August 2026, and worse than the gap itself:** account deletion did not work at all. `deleteAccount()` read the password from `findById()`, which never returns that field, so every attempt ended in an undefined array key and a 500. The promise was not merely unimplemented; the button was broken.
  - **Also found:** what it would have done was wrong. The old implementation moved every sticky note to the `hal9000` administration account and left the rest to `ON DELETE CASCADE`, which also removes the author's contributions on **other people's** boards. A Participant closing their account would have taken their team's retrospective with them. The subscription meanwhile kept renewing at Creem, contradicting `terms.md`.
  - **Built (migration 019 plus a rewritten `User::deleteAccount()`):** cancellation at Creem happens first and outside the transaction — if it fails, nothing is deleted and the person gets an actionable message, because charging a deleted account monthly is worse than a deletion that succeeds ten minutes later. Then, in one transaction: Drafts removed; Public sticky notes de-attributed with `author_deleted_at` and the tape strip on the wall; hearts removed **including the stored `likes_count`** on the affected notes, which the cascade would have left stale; owned boards deleted whole; contributions elsewhere kept as **Deleted user** through an explicit `CASE` in the board queries; dot votes kept as anonymous rows with the actor key rewritten; participant rows stripped of name and access; invitations to that email address removed; the administration audit trail kept but de-attributed; payment records de-attributed rather than erased.
  - **Verified:** `scripts/test-account-deletion.php` runs the real model against a throwaway database built by the real migration chain, with 32 assertions split into *what had to go* and *what had to stay*, including the case where cancellation at Creem fails and deletion is therefore refused. `scripts/test-note-cascades.php` adds 31 more for the deletion cascades. Both were executed on 21 August 2026 and passed.
  - **Still open, and both are outside the code:** the retention period for billing and tax records (payment records are now de-attributed and kept, which is a choice a lawyer should confirm — Creem is merchant of record and holds the actual invoices), and the actual deletion of protected backup copies within 30 days, which is an operational commitment on Fly.io rather than something the application can assert. Until both are settled, V-06 stays open.
- [ ] **[VERIFY V-07] Publishing operation — partly resolved on 21 July 2026.** Repository `faridbouchdak/stickynotes.club`, branch `main`, Jekyll source `/docs`, Just the Docs configuration, `/docs/CNAME` for `docs.stickynotes.club` and `_config.yml` URL `https://docs.stickynotes.club` are locally confirmed. The working service uses GitHub Pages for automatic Help Centre deployment from `main`; failed builds are visible in GitHub Actions, and the canonical host serves valid HTTPS. Fly.io does not deploy the documentation. Cloudflare provides the domain and network layer but no deployment. Still verify preview behaviour, every British-English permalink, intentional redirect absence or presence, internal links, the production 404 path, cache behaviour and rollback.
- [x] **[VERIFY V-08] Brainstorm template layout.** Resolved on 21 July 2026: Blank and Brainstorm use the same grid structure and can both later change to columns. Only their default backgrounds and product framing differ. Retro, Kanban and Week planner start with columns.
- [ ] **[VERIFY V-09] Destructive copy and cascade — design resolved on 21 July 2026; copy corrected in the product on 21 August 2026 under C-11; cascade implementation unverified.** Deleting a sticky note removes its comments, hearts and dot votes with it; deleting a comment deletes only that comment; deleting a board permanently deletes all sticky notes, comments, hearts and dot votes and removes Participant access and pending invitations without deleting accounts. On a private board, sticky-note deletion uses no confirmation dialog and offers **Undo** afterwards under the D-21 amendment. For a Public sticky note use **Delete this sticky note?** / **This permanently deletes the sticky note and all its comments and hearts. This cannot be undone.** / **Cancel** / **Delete sticky note**, and for a Draft omit the external-copy sentence, since a Draft was never published; **Delete this comment?** / **This permanently deletes the comment. This cannot be undone.** / **Cancel** / **Delete comment**; and **Delete this board?** / **This permanently deletes the board and all its sticky notes, comments, hearts and votes. It also removes all participants and pending invitations. This cannot be undone.** / **Cancel** / **Delete board**. For Public sticky notes, also show the external-copy warning. Verify database cascades, corrected controls and count/result updates in the working product; cross-session visibility remains subject to V-04.
  - **Verified on 21 August 2026** with `scripts/test-note-cascades.php`, which runs the real `BoardNote` model against a throwaway database built by the real migration chain. Confirmed: a private-board sticky note is soft-deleted and keeps its comments, hearts and dot votes while it can still be restored; `restore()` brings all of it back and clears the record of who deleted it; after the retention window `findPurgeable()` selects it and `purge()` removes the row together with its comments, hearts, dot votes and tags, while the voting round itself survives; deleting a board removes its sticky notes, columns, members, invitations, share links, participants and voting rounds; deleting a Public sticky note takes its hearts with it. The cascade does what the copy now claims.
- [ ] **[VERIFY V-10] Public sticky-note metadata — behaviour resolved on 21 July 2026; implementation partly verified.** Store publication time in UTC and display **YYYY/MM/DD**, for example **2026/07/21**. Copy the user-selected account country to the sticky note at creation as an immutable snapshot; never infer it from IP. Add one share after each successfully completed **Copy link** or **Save as image**, including repeats, and describe the value as completed actions rather than unique people. Unhearting subtracts one and removes the Wall of Love entry. Public → Draft removes every public heart/favourite relationship and resets heart and share counts; republishing sets a new publication date with zero counts and does not restore favourites. Deletion or moderation removal deletes the relationships and counters with the sticky note. Account deletion retains the de-attributed Public sticky note, date, country and aggregate counts, removes heart relationships created by the deleted account and preserves other users’ hearts. Date format and country snapshot are confirmed in the product; verify the remaining counter, reset, deletion, moderation and account-deletion behaviour end to end.
  - **Partly verified on 21 August 2026.** The stored `likes_count` on `notes` was checked for drift against the actual rows in `note_likes` — none found — and account deletion now decrements it explicitly, which the database cascade did not (see V-06). Deleting a Public sticky note removes its hearts. Still unverified: the UTC publication time and **YYYY/MM/DD** display, the immutable country snapshot, the share counter after **Copy link**, the Public → Draft reset and republication. Those need a browser pass rather than a database test.
- [x] **[CONFLICT C-12] Board duplication exists while D-19 forbids it — raised and resolved on 21 August 2026.** Ratified as it works: ordinary board management, a named list of copied setup fields, the active-board allowance applies, a duplicated workshop starts in *preparing*. D-19's prohibition is withdrawn. Original finding: `POST /b/@slug/duplicate` copies a board's setup — name, description, layout, columns, background, workshop instruction — and deliberately none of its content, participants, links or session state; a duplicated workshop starts in *preparing*. D-19 says boards cannot be duplicated and that any duplication capability requires a new explicit decision, which makes this intent rather than behaviour under D-31. The Product Model now describes duplication as it works, with the D-19 prohibition marked superseded pending this ratification. To settle: confirm the copy boundary as the rule (a whitelist of copied settings, never copy-everything-except), confirm that the board limit applies to a copy, and decide whether duplication needs its own entitlement or follows ordinary board management.
- [ ] **[CONFLICT C-13] The daily digest cannot report a deletion, while V-11 requires it — raised on 21 August 2026.** `scripts/board_digest.php` filters on `deleted_at IS NULL` in every subquery, and the reasoning in the script is sound: a digest that says "this is on your board now" should not list something that is gone. V-11 nevertheless requires that an author whose sticky note was removed by the Owner learns about it in their conditional daily digest, and no immediate email is sent either — so today they learn nothing. Direction: **document leading**, because this is a promise rather than a description (D-31). Two ways out: give the digest a separate *Removed while you were away* section that names the board, the sticky note's first line and who removed it, or accept that removal is visible on the board itself and drop the digest requirement from V-11. The first keeps the promise and costs a query plus a template block; the second is honest but leaves an author who contributed and never returns that day with no signal at all. Affects: `scripts/board_digest.php`, the digest template, Product Design Notes (V-11).
- [ ] **[VERIFY V-12] Taking part without an account, in the Terms — raised on 21 August 2026 under C-09.** A guest contributes content to a private board without ever seeing the Terms of Service. `terms.md` does not mention guests, workshop links or participation without an account, so nothing states who owns a guest's contribution, which acceptable-use rules bind them or on what ground their content can be moderated. The board is private, so the D-28 public relinquishment does not cover it either. The join screen now links to both Terms and Privacy, which is disclosure rather than coverage. Have the Terms reviewed and extended for accountless participation; until then, do not describe guest contributions as governed by the Terms. Verified as already correct and needing no change: the guest link always carries an expiry (default 24 hours, maximum one week), and `cleanup_guest_participants.php` runs nightly at 03:45 UTC, replaces the nickname with **Participant** and clears the token after 30 days of inactivity while contributions remain.
  - **Briefing ready on 21 August 2026:** `design/briefing-V-12-terms-deelname-zonder-account.md` sets out the verified facts from the code, five gaps ranked by size and eight questions for a lawyer, with draft wording for a new §13a *Taking part without an account* plus adjustments to §4 (age), §11 (licence) and §13 (owner responsibility). The gap that worries most is age: §4 ties the sixteen-year limit to *creating an account*, and a guest creates none — while the audience the front page targets is teachers putting a QR code on a classroom screen. The draft wording must not be published before a lawyer has seen it. Combine this round with the terms change that Article 14 DSA requires (see `design/spec-D-24-rapportage-en-moderatie.md`); it is the same document and the same lawyer.
- [ ] **[VERIFY V-11] Owner removal of another author’s board sticky note — behaviour resolved on 21 July 2026; aligned with the D-21 amendment on 21 August 2026; implementation unverified.** On an active owned board, the Owner can delete any sticky note but cannot edit another author’s text or separately delete another author’s comment. Deletion removes the sticky note with its comments, hearts and dot votes and offers the Owner the same restore window as any other private-board deletion; record who removed it, so that a participant without an account can still be told who did. The V-09 confirmation dialog no longer applies to this object. Log actor, board, sticky note, author, timestamp and cascade outcome without retaining the deleted content body. Include the event in the affected author’s conditional daily digest while they still have access; do not send an immediate deletion email. Verify controls, authorisation, cascade, log and digest end to end. Moderator and administrator deletion remains subject to D-24’s privileged audit and notification safeguards.
  - **Verified on 21 August 2026, with two findings.** Authorisation was already covered by `scripts/test-board-rights.php`: an Owner may delete another author's sticky note, may not rewrite their text, and a Participant may do neither. The cascade and the restore window are covered by `scripts/test-note-cascades.php`. **Finding 1 — the technical log is not durable.** Who deleted a sticky note is recorded on the row itself (`deleted_by_actor`, with `deleted_at`), and that row is purged after the retention window. After seven days there is therefore no record left at all. V-11 asks for a log that survives the content; today it survives exactly as long as the content does. **Finding 2 — the digest does not carry the event.** `scripts/board_digest.php` filters on `deleted_at IS NULL` throughout, deliberately: the digest promises "this is on your board now". So a deletion never reaches the affected author's daily digest, which V-11 requires. This is a promise against a described behaviour, so under D-31 it is a product finding rather than a documentation defect: decide whether the digest gains a "removed" section or whether V-11 drops that requirement. Recorded as **[CONFLICT C-13]**.

### Code review record — 23 July 2026

Source: review of the current application code against the nineteen items in the remaining review queue. Finding code is implementation evidence, not end-to-end verification; open checklist items remain unchecked until their complete behaviour, failure cases and documentation alignment have been tested.

#### Functionality found in code

- **Q-01 — image content:** `ImageService.php` enforces a 5 MB (`5242880`) upload limit, accepts JPG, PNG and WebP and produces a square 800 × 800 JPEG. `NoteController` supports Instant Photos through `type=instant`, frame colours and an 80-character caption; `BoardNote` supports images on private-board sticky notes. Exact failure behaviour, lifecycle inheritance and accessible alternative text remain to be verified, so Q-01 is not closed.
- **Q-02 — current-value editing:** edits overwrite the current value and no history or recovery table was found in the schema. This matches the approved no-history model. V-04 now verifies autosave, failure recovery and conflicts; the broader Q-02 storage and interface audit remains open.
- **Q-04 — private-board organisation:** `board_note_tags`, `BoardNoteTag::normalize`, `tagFilter`, `board_notes.due_date` and `parseDueDate` implement tags and due dates with future, today and overdue states. No due-date filter or due-date notification was found, matching the approved boundary. Remaining work is targeted verification of management, deletion and permission cases.
- **V-05 — plan enforcement:** Creem checkout, webhook handling, `syncSubscription`, `recomputeRole` and the lapsed-account fallback in `BoardService::isOwnBoardWritable` were found. The fallback keeps the oldest boards within the Free allowance writable through `ORDER BY created_at ASC LIMIT`. `createShareLink` uses `canShareBoard()`, which combines `isOwner()` with `canCollaborate()`: View and Post link creation is therefore Owner-only and limited to the Premium or Chosen Few collaboration entitlement, while Post-link contribution remains available to signed-in users on any plan. On 23 July 2026, `revokeShareLink` was corrected to use plan-independent `canManageBoard()` ownership authorisation. `isShareLinkActive()` and `loadShareLinkOr404()` make existing links inaccessible after downgrade. Pricing, tax, checkout wording, downgrade selection and archival, restoration after upgrade and whether unrevoked links reactivate after upgrade still require verification.
- **V-04 — collaboration reliability:** resolved on 29 July 2026. Integer board versions, lightweight polling, partial board refreshes, autosave, local drafts, retry and explicit text-conflict handling are implemented. Polling was chosen instead of WebSockets for shared-hosting compatibility.

#### Partial implementation found

- **D-08 — notification operation:** `EmailService` contains invitation, mention and daily-digest email handling, and `board_digest.php` is scheduled for 06:30 UTC. The invitation expiry was corrected from **7** to the required **14 days** on 23 July 2026. No separate access-revocation email was found during the original review. The **Declined** state, invitation and revocation emails, daily scheduling and aggregation, access filtering, delivery failures and applicable email preferences still require end-to-end verification before D-08 can be closed.
- **Q-03 — mentions:** `BoardController` parses `@username` from comments, checks board access, excludes self-mentions and sends email. Only comment entry was found. Multiple recipients, duplicates, edits, access loss, accessible controls and delivery remain to be tested.
- **D-11 / D-12 — image saving and post-publish interface:** `noteImage.js` generates a PNG of the sticky-note display card at 2× resolution, includes the logo and uses Web Share on mobile. Filename, attribution and the exact calm success copy and placement of **View**, **Share**, **Edit** and **Return to Draft** remain open.
- **V-09 — destructive actions:** deletion routes and confirmations exist for sticky notes, comments, boards and members. Model-level cleanup exists, including photo cleanup in `BoardNote::delete` and board cleanup in `Board::delete`. Approved wording, permissions, complete database cascades and counter/result updates remain unverified.
- **V-10 / V-11 — Public metadata and Owner deletion:** heart and share counters through `NoteLike` and the share route, the admin flag and `deleteNote` were found. Public → Draft reset, republishing, moderation and account-deletion behaviour still require end-to-end verification. For Owner deletion, the authorisation boundary, cascade, content-free technical log and conditional digest remain unverified.
- **Q-05 — external discovery:** `www/robots.txt` and `www/sitemap.xml` exist, including a disallow list. No pre-publication warning was found, and crawler behaviour, removal from discovery, retained de-attributed Public content and Terms and Privacy Policy alignment remain open.
- **Q-06 — board recency:** the board overview now shows **Last modified on YYYY/MM/DD** using UTC timestamps. `Board::findByUser()` derives `last_activity_at` from board, sticky-note and interaction timestamps with creation as the fallback. `Board::touch(int $id)` updates `boards.updated_at` after successful mutations; 24 success-path calls cover sticky notes, comments, columns, hearts, voting, invitations, share links and access changes, while existing board-setting updates already touch the board. The helper was exercised against the real schema in a rolled-back transaction and the aggregate query returned expected historical dates. The temporary `last_activity_at DESC` sorting was removed on 23 July 2026 and the stable `created_at DESC` order restored. Targeted tests for deletion, failed or rolled-back actions, access control and UTC display remain open.

#### Not implemented or not demonstrated in this repository

- **E-02 — terminology and British English:** non-canonical **Member** labels in the application interface, including the board templates identified during review, were replaced with **Participant** on 23 July 2026. The broader Help Centre, policy, permalink and British-English audit was completed on 21 August 2026; see the review register for what was found and corrected.
- **D-21 / V-06 — retained records and account deletion:** `User::deleteAccount` only moves Public sticky notes to `hal9000` and deletes the account. No subscription cancellation, owned-board deletion, **Deleted user** preservation, full de-attribution or deletion from protected backups within 30 days was found. This remains the largest implementation gap and requires legal verification of separately required records.
- **D-24 — moderation operation:** only an administrative flag action, `toggleNoteFlag`, was found. Reporting, human review, proportionate measures, restrictions and suspensions, appeals, evidence expiry, audit logging and emergency escalation are not implemented.
- **V-07 — Help Centre publishing:** Help Centre content, permalinks and redirects are not present in the reviewed application repository. Verification belongs in the separate GitHub Pages Help Centre project.
- **Q-07 — commercial positioning:** a pricing page exists, but collaboration-first positioning requires a marketing and copy audit and is not demonstrated as complete by application code.

#### Review priorities after this code pass

1. Implement V-06 account deletion and D-21 retention safeguards.
2. **Implementation correction completed on 23 July 2026:** invitation expiry changed from 7 to 14 days. Complete D-08 end-to-end notification verification remains open.
3. Implement and legally verify D-24 before launch.
4. **Application cleanup completed on 23 July 2026:** non-canonical **Member** labels replaced with **Participant**. The wider E-02 content and policy audit remains open.

Ideas live here until they become product decisions. A bullet in “Future directions” is not a product commitment.

## Current discoveries

### The sticky note is the interface, not the product

The familiar sticky-note form lowers the cost of capturing a thought. The lasting value comes from what the thought can become through discovery, context, organisation and collaboration.

Implication: evaluate features by whether they advance an idea, not by whether they add capability to the note object.

### Documentation became product specification

Writing the Help Centre exposes missing states, unclear terminology and claims that cannot yet be verified. The documentation process is therefore an early product-design tool, not only a release task.

Implication: draft help content before implementation and verify it against the actual product before publication.

### Marketing naturally emerged from documentation

Clear explanations of public sharing, private boards and collaboration also communicate why the product matters. Helpful product truth is the preferred basis for marketing.

Implication: reuse the product model and Help Centre language rather than inventing a separate vocabulary of claims.

### Public and Private are two phases of one journey

Public notes support inspiration and discovery; private boards support development and collaboration. They form one conceptual product journey, but no direct product flow carries a Public sticky note across that boundary.

Implication: a transition could be valuable, but it must make visibility, ownership and copying behaviour explicit.

### The current documentation is ahead of verified detail

The Help Centre refers to invitations, permissions, private-board share links, comments, dot voting, real-time collaboration, tags, due dates, layouts and filters. D-23 was revised on 23 July 2026 to confirm View and Post links. The affected Help Centre source pages were aligned on 23 July 2026 with task guidance, privacy boundaries, plan rules, revocation and troubleshooting; publish the claims only after the remaining D-23 verification. Some other capabilities remain broad or use “depending on your account” language.

Implication: perform a product-to-documentation audit before treating every public claim as implemented fact.

### Terminology and link drift required correction

Resolved on 20 July 2026:

- broken links now use `/plans-and-subscriptions/` and `/organise-your-work/`;
- the canonical page label is **Plans & subscriptions**;
- all text and permalinks use British English;
- `docs/organize-your-work.md` became `docs/organise-your-work.md`.

Board-role terminology is resolved under **[ERROR E-02]** and **[DECISION D-07]**: use **Owner** and **Participant** only.

## Current product assumptions to verify

These statements appear in current documentation but need direct product verification:

| Area | Documented claim | Verification needed |
| --- | --- | --- |
| Accounts | Email verification unlocks all features | Confirm exact restrictions before verification |
| Public notes | Sticky notes have Draft and Public statuses; authors can edit and delete their notes | Confirm status controls, publication flow, limits and deletion behaviour |
| Boards | Owners can invite/remove participants; invited participants receive one consistent capability set | Confirm the implemented invitation and access-removal flow |
| Sharing | Participant access uses a 14-day email invitation and requires an account; View links allow accountless read-only access and Post links let signed-in users on any plan add sticky notes without becoming Participants | Verify invitations and Participant revocation, both link modes, authentication boundaries, immediate link revocation and the absence of extra Participant rights end to end |
| Collaboration | Real-time synchronisation, autosave and safe conflict/failure handling are implemented and verified | Keep Help Centre claims aligned with V-04 and the current interface |
| Interactions | Public responses are hearts; Public sharing uses **Copy link** or **Save as image**; private boards support non-editable comments, toggle hearts and Owner-controlled dot voting without reset, reopening, warning or round history | Resolved under V-03; digest details remain under D-08 and real-time behaviour under V-04 |
| Notifications | Immediate invitation and access-revocation emails plus a conditional daily private-board activity digest; declined invitations do not email the Owner | Verify scheduler, aggregation, access filtering, applicable preferences, deliverability and email classification |
| Organisation | Private-board sticky notes support board-scoped lower-case tags and visual-only due dates; tag filtering exists but due-date filtering does not; the worldwide wall filters Public sticky notes by country | Confirm tag controls, empty results, multi-tag behaviour, tag management and deletion, expired-date display and plan entitlements; do not call any control search or promise due-date notifications |
| External discovery | Public sticky notes and Instant Photos may be indexed by search engines and used by external AI services; Drafts and private-board content may not | Verify Publish disclosure, public metadata, sitemap and crawler configuration, removal after unpublishing or deletion, retained de-attributed Public content and aligned Terms and Privacy Policy |
| Board recency | **Last modified on YYYY/MM/DD**, a historical aggregate and central `Board::touch()` activity clock are implemented; the current recency-based sorting conflicts with Q-06 | Restore the previous board ordering; test creation fallback, accepted mutations, deletions, excluded reads and failures, access control, UTC display and consistency with D-08 |
| Commercial positioning | Existing entitlements already make initiating private-board collaboration paid while invited Free users participate fully; the value hierarchy was not explicit | Make private collaboration primary and volume, organisation and personalisation supporting; audit marketing, pricing, paywalls, checkout and onboarding without changing D-13 or D-27 |
| Board lifecycle | Public documentation currently presents archiving as available, but it is only a proposed future feature | Remove the current-capability claim until launch; use the resolved V-02 lifecycle and verify its implementation before publication |
| Plans | Free, Premium and Chosen Few limits match the public page | Confirm application entitlements and checkout |
| Account deletion | V-06 defines deletion, **Deleted user** contributions, retained de-attributed Public sticky notes, subscription non-renewal, interaction cleanup and a maximum 30-day protected-backup period | Implement and test the full warning, lifecycle and backup expiry; legally verify required-record retention periods |

## Earlier questions with a documented answer

The source notes contain exploratory questions that later public documents appear to answer. These answers are **documented**, not automatically verified implementation:

- **Can a sticky note be removed?** Yes. Authors can delete their own sticky notes, an Owner can delete any sticky note on an active owned board, authorised moderation can remove Public sticky notes, and authorised moderators and administrators can delete any board sticky note. Owner deletion never grants editing or separate deletion of another author’s comment. Deletion is immediately permanent; V-09 resolves the cascade and V-11 verifies Owner implementation.
- **Does public content expire automatically?** No. D-20 confirms that a Public sticky note remains Public until deliberate author action or authorised moderation. There is no automatic or author-selected expiry. If the account is deleted first, the sticky note remains after de-attribution with the V-06 tape and accessible state and can later be removed only through authorised moderation.
- **Are boards public?** No. **[CONFLICT C-01]** is resolved: boards remain private and access-controlled; only individual sticky notes can be public.
- **Can people view or edit boards?** Yes. D-07 defines one invited Participant role with full board participation; there is no separate read-only role. A participant may create sticky notes, edit and delete their own sticky notes, add and delete their own comments, place hearts and use dot voting. Verify the implementation against this model.
- **Can someone have several boards?** Yes. Free can keep 1 owned private board active and editable, Premium 5 and Chosen Few unlimited. Archived owned boards and boards joined as a Participant do not consume the active-board allowance under D-27.
- **Are colours meaningful?** Only as expression and personalisation. D-18 rejects product-defined colour semantics. Use tags or visible labels for explicit status, priority, category or board-specific meaning; never rely on colour alone.
- **What happens after Publish?** The sticky note appears immediately on the worldwide wall, a calm success message appears, and the author can view, share, edit or return it to Draft. Verify the exact implemented copy and control labels under D-12.

## Open design questions

### Sticky notes

#### [CONFLICT C-02] Can sticky notes be edited?

- Status: resolved on 20 July 2026.
- Decision: all sticky notes remain editable by their author. Authorised moderators and administrators may view content when D-24 permits, hide, remove or restore it, and alter text only for a narrowly necessary, audited redaction.
- Consequence: board owners and ordinary participants cannot rewrite someone else’s note. D-24 permits moderators to hide, remove or restore content but allows text alteration only for a narrowly necessary, audited redaction; it also defines reasons, logging, notification and appeal.
- Still needed: verify editable fields in the working product. V-04 covers cross-session visibility and Q-02 covers the separate edit-history decision.

#### Can sticky notes exist on multiple boards?

- Status: resolved on 20 July 2026.
- Decision: no. A private-board sticky note belongs to exactly one board and cannot simultaneously belong to multiple boards.
- Public boundary: **[DECISION D-17]** separately rules out copying, moving or referencing a Public sticky note into a private board.
- Consequence: similar material captured separately on another private board is a distinct sticky note with its own author, interactions and lifecycle; it is not shared membership.

#### [DECISION D-18] Should colours carry meaning?

- Status: resolved on 20 July 2026.
- Current evidence: classic and premium pastel colours are presented as personalisation and plan benefits.
- Decision: keep colour expressive and do not assign universal product meaning to sticky-note colours.
- Explicit organisation: use visible tags or labels for status, priority, category or other meaning.
- Board conventions: users may form informal colour conventions, but the interface and documentation must not rely on colour alone.
- Rationale: this preserves personalisation, avoids ambiguity and remains accessible without colour perception.

#### [DECISION D-19] What shape and limits should a board have?

- Status: resolved on 20 July 2026; Brainstorm layout verified on 21 July 2026.
- Templates:
  - **Blank** — An empty board, arrange it however you like.
  - **Retro** — Went well / To improve / Actions — great with dot-voting.
  - **Kanban** — To do / Doing / Done.
  - **Week planner** — A column for every weekday.
  - **Brainstorm** — Open grid for collecting ideas, vote on the best ones later.
- Layout: Blank and Brainstorm use the same grid structure and can later change to columns; only their default backgrounds and framing differ. Retro, Kanban and Week planner start with columns.
- Movement: sticky notes can be reordered within their current row and moved between columns in a column layout.
- Appearance: users can choose from nine board backgrounds.
- Duplication: boards cannot be duplicated.
- Growth: boards currently grow without a product-defined spatial or content limit. This is structured grid/column growth, not a freeform unlimited-canvas whiteboard.
- Change control: any future limit, duplication feature or different layout model requires a new explicit product decision.

#### [DECISION D-20] How long does a Public sticky note remain public?

- Status: resolved on 20 July 2026.
- Decision: a Public sticky note has no automatic or author-selected expiry.
- Lifetime: it remains Public until its author returns it to Draft or deletes it, or authorised moderation removes it under the applicable rules.
- Unpublishing: Return to Draft removes it from the worldwide wall and hides it from other ordinary users.
- External persistence: independent copies, saved images, screenshots, search results, caches, AI datasets, model training and other external uses may remain.
- Boundary: V-06 resolves account-deletion behaviour and sets a maximum 30-day protected-backup period without product recovery. Required billing, tax or legal-record periods remain open pending legal verification. Ordinary sticky-note deletion has no recovery period.
- Change control: automatic expiry or an author-selected lifetime requires a new explicit product decision and aligned interface, Help Centre, Privacy Policy and Terms changes.

#### [DECISION D-21] What happens when content is deleted?

- Status: permanence resolved on 20 July 2026; ordinary cascades and copy resolved on 21 July 2026; implementation verification remains under V-09.
- Permanence: deleting a sticky note, comment or board is immediately final after confirmation. There is no Undo control, trash, recovery period or restore flow.
- Sticky-note cascade and confirmation: permanently delete the sticky note and its comments, hearts and dot votes. Use **Delete this sticky note?**, **This permanently deletes the sticky note and all its comments, hearts and votes. This cannot be undone.**, **Cancel** and **Delete sticky note**.
- Comment cascade and confirmation: delete only that comment. Use **Delete this comment?**, **This permanently deletes the comment. This cannot be undone.**, **Cancel** and **Delete comment**.
- Board cascade and confirmation: permanently delete every sticky note, comment, heart and dot vote and remove Participant access and pending invitations without deleting participant accounts. Use **Delete this board?**, **This permanently deletes the board and all its sticky notes, comments, hearts and votes. It also removes all participants and pending invitations. This cannot be undone.**, **Cancel** and **Delete board**.
- Public context: also warn that independent copies, saved images, screenshots, search results, caches, AI datasets, model training and other external uses cannot be recalled.
- Still open: V-09 implementation and count/result verification; V-04 governs cross-session visibility; V-06 verifies account deletion, expiry from backups within 30 days and separately required records.

#### [DECISION D-05] Do sticky notes need explicit completed and archived states?

- Status: resolved on 20 July 2026.
- Decision: no. Individual sticky notes do not receive **Completed** or **Archived** system states.
- Future scope: the only archive feature under consideration applies to an entire private board and includes all of its sticky notes, comments, hearts and dot votes.
- Permission: only the Owner or an authorised platform moderator or administrator may archive a board.
- Archive behaviour under V-02: preserve every sticky note, comment, heart and dot vote indefinitely; make the board read-only for the Owner and existing Participants; allow the Owner to revoke access; cancel pending invitations; stop new invitations and routine notifications; and allow only the Owner or an authorised platform moderator or administrator to restore or permanently delete it. Active View and Post links may show only the read-only archive, Post links cannot accept new sticky notes and the Owner may still revoke either link.
- Documentation inconsistency: `docs/private-boards.md` and `docs/organise-your-work.md` currently describe archiving as available and must be corrected until implementation.

### Public → Private transition

#### [DECISION D-17] How should a public idea become private work?

- Status: resolved as not planned on 20 July 2026.
- Decision: do not add a direct copy, move, reference, create-board-from or add-to-board flow for a Public sticky note.
- Boundary: viewing, sharing or saving an eligible Public sticky note as an image does not create a board sticky note, board membership, a collaboration relationship or a transfer of ownership.
- Consequence: attribution, consent, discussion-history synchronisation and linked-deletion behaviour are unnecessary for the current product because no cross-context object relationship is created.
- Reopening condition: only reconsider this through a new explicit product decision; define visibility, attribution, consent, ownership, interactions and deletion before implementation.

### Collaboration

#### [DECISION D-07] What is the minimum role model?

- Status: resolved on 20 July 2026.
- Board roles: **Owner** and **Participant** only.
- Access: a person becomes a Participant through an invitation; there is no Viewer, Editor or Commenter role and no separately configurable participation level.
- Owner: invites and removes Participants, manages the board and may delete it. Once whole-board archiving exists, the Owner may archive it.
- Participant: can view the whole board, create sticky notes, edit and delete their own sticky notes, add and delete their own comments, place hearts and use dot voting.
- Boundary: neither the Owner nor another Participant may edit somebody else’s sticky note or separately delete somebody else’s comment. Another Participant cannot delete the sticky note; the Owner has the explicit active-board sticky-note deletion exception defined by D-26 and V-11. Moderator/Admin powers are separate platform powers.
- Ownership lifecycle: D-22 confirms exactly one non-transferable Owner. Deleting that Owner’s account deletes every board the account owns; there is no handoff or successor Owner.

#### [DECISION D-22] Can board ownership change?

- Status: resolved on 20 July 2026.
- Ownership: every board has exactly one Owner.
- Transfer: ownership cannot be transferred to a Participant or reassigned by a moderator or administrator.
- Rationale: the Owner should remain involved while the board’s idea develops, preserving context and responsibility.
- Account deletion: deleting the Owner’s account permanently deletes every board owned by that account, including all attached board content and participant access.
- Consequence: there is no co-ownership, handoff, successor Owner or ownerless-board state. The account-deletion flow must warn about every affected owned board before confirmation.
- Boundary: V-06 preserves private-board sticky notes and comments on other Owners’ boards under **Deleted user**, retains de-attributed Public sticky notes with the tape and accessible state, removes personal hearts and preserves only anonymous dot-vote totals. Protected backup copies expire within 30 days; required-record periods remain pending legal verification.

#### [DECISION D-23] Can someone use a private board without an account?

- Status: resolved on 20 July 2026; revised on 23 July 2026.
- Decision: yes, for read-only link access. A **View link** shows a read-only version of the board to anyone with the active link without requiring an account.
- Post link: a **Post link** provides the same viewing access and additionally lets a signed-in StickyNotes.club user on any plan add sticky notes.
- Participant entry: email invitation remains the only route to Participant status. The recipient signs in or creates an account and the invitation expires after 14 days.
- Link creation: only the Owner may create a View or Post link, and only while the Owner has the Premium or Chosen Few collaboration entitlement under D-13. A Participant cannot create a link regardless of their plan.
- Permissions: an invited Participant receives the complete Participant capability set under D-07. A link visitor or link contributor is not a Participant. Link access grants no comments, hearts, dot votes, invitations, access management or board settings.
- Authorship: a signed-in Post-link contributor remains the author of a sticky note they add and retains D-26 author controls while the link is active. Link revocation does not delete existing contributions.
- Revocation: the Owner can revoke a View or Post link at any time, including after downgrade; access through that link ends immediately. `revokeShareLink` now uses the plan-independent `canManageBoard()` Owner check.
- Downgrade: `isShareLinkActive()` and `loadShareLinkOr404()` make links inaccessible while the Owner lacks the collaboration entitlement. Verify whether an unrevoked link remains disabled or becomes active again after a later upgrade.
- Interface copy: heading **Share this board**; explanation **View links show a read-only version of this board to anyone with the link — no account needed. Post links also let signed-in StickyNotes.club users on any plan add sticky notes. Revoke a link at any time to disable it.**
- Decline: declining grants no access, appears to the Owner as **Declined** and sends no separate Owner email.
- Participant revocation: the Owner can remove Participant access. Removal takes effect immediately and sends the former Participant an immediate email.
- Boundary: sharing a Public sticky note is a separate Public action and does not grant private-board access.

#### What is the lifecycle of collaboration?

- Status: resolved under D-08 on 21 July 2026.
- Stages: Invite by email with 14-day expiry → Sign in or create an account → Accept and join as Participant, or decline without access → Contribute → Leave or lose access. Revoked access takes effect immediately and triggers an email to the former Participant. Whole-board Archive is a future state under V-02 rather than a current collaboration stage.
- Boundary: View and Post links are access capabilities, not board roles. They do not add recipients to the Participant lifecycle. Owner-account deletion is resolved under D-22: the owned board is deleted rather than transferred or left ownerless. Suspension and blocking belong to D-24 rather than the ordinary invitation lifecycle.

#### [QUESTION Q-03] Can a sticky note be assigned?

- Status: resolved on 22 July 2026; implementation verification remains.
- Assignment: no. There is no assignee, responsible-person field, acceptance, reassignment, assigned-to-me filter or assignment lifecycle.
- Mentions: private-board content may mention one or more people who are current Participants on that board. Each named Participant receives an immediate notification email.
- Meaning: a mention is an attention signal only. It does not change authorship, ownership, access, edit or deletion rights, due date or responsibility.
- Context: Public sticky notes and Instant Photos have no mention or assignment feature. Owner and Participant roles remain unchanged.
- Access: do not expose former, revoked or unrelated users as valid mention recipients. Filter the email using current board access at send time.
- Notification boundary: a mention email is an explicit exception to the daily-digest-only rule for routine edits. Whether the same event also appears in the daily digest, repeated mention handling, delivery failures and applicable preferences require operational verification under D-08.
- Verification: confirm supported mention entry locations, one and multiple recipients, duplicates, edits that add or remove mentions, revoked access, email content and delivery, and accessibility of the mention control.

#### [VERIFY V-04] How should simultaneous changes behave?

- Status: resolved on 29 July 2026; implemented and verified.
- Synchronisation: propagate accepted sticky-note creation, editing, deletion and movement, comments, hearts, votes and voting-round state changes to other active Participants without a page refresh.
- Saving: autosave editable sticky-note text and expose visible saving, saved and failed states.
- Failure: preserve unsaved local text through connection or server failure and provide a safe retry path.
- Conflict: if editable text changed on the server, retain the local version and show a conflict; do not silently apply last-write-wins.
- Authority: the server determines accepted heart, vote and position state and corrects optimistic local displays when necessary.
- Presence: continuous presence indicators are optional; protecting content is mandatory.
- Verification: passed across two browsers and with an automated browser harness covering live changes, autosave, connection loss, failed requests, simultaneous edits and permission loss. The interface uses local drafts, automatic and manual retry, and **Save my version** or **Use theirs** for text conflicts.

#### [QUESTION Q-02] Is edit history available?

- Status: resolved on 22 July 2026; implementation verification remains.
- Decision: no. Sticky notes and Instant Photos retain only the currently accepted state. There is no revision list, version viewer, comparison view or restore-version action.
- Editable current values: text, caption, colour, tags and due date overwrite their previous values after an accepted save. Image replacement or removal and future alternative-text changes also update the current object without producing a stored version.
- Context: Q-04 limits tags and due dates to sticky notes on private boards. A due date is not an automatic or author-selected Public expiry under D-20.
- Reliability boundary: autosave, locally preserved unsaved text and conflict handling protect an in-progress edit. They do not retain a prior accepted server value after the save or conflict is resolved.
- Accountability boundary: D-24 privileged-access audits and report evidence remain limited operational records. They are not visible as edit history and are not a routine content-restoration path.
- Deletion: because no versions exist, deleting the current object cannot reveal or restore an earlier version. The D-21/V-06 deletion and backup rules continue to govern the object itself.
- Verification: inspect storage, APIs and interface for unintended revision retention or history controls and test current-value overwrite alongside V-04 saving, retry and conflict protection.

### Plans and limits

#### [DECISION D-13] Which functionality belongs in the Free plan?

- Status: resolved on 22 July 2026.
- Current public limits: up to 2 sticky notes per day, classic colours, and liking/sharing public notes.
- Premium: up to 12 notes per day, pastel colours and framed instant photos.
- Chosen Few: unlimited notes, exclusive profile locations and membership status.
- Active, editable owned private boards: Free 1, Premium 5, Chosen Few unlimited. Archived owned boards and boards joined as a Participant do not count towards this allowance.
- Invitations: only Premium and Chosen Few can send private-board invitations. Free can receive invitations and participate fully.
- Included for all plans: comments, private-board hearts, dot voting and private-board sticky-note tags and due dates.
- Product consequence: Free supports personal board use and full invited participation, while initiating board collaboration is paid.

#### What happens at a limit?

- Status: resolved on 22 July 2026.
- Counter: count only successful **Draft → Public** transitions, including republication after a sticky note has returned to Draft. Creating or editing Drafts, creating or editing private-board sticky notes, editing an existing Public sticky note and failed publication attempts do not count.
- Decision: after the daily publication limit has been reached, block only publication. Keep all existing content and other available capabilities accessible. Restore publication at **00:00:01 UTC on the next day** and show the remaining wait or reset moment in the user’s local time.
- Downgrade: the Owner selects which permitted number of boards remain active and sees the others listed before confirming their archival. Excess boards are preserved read-only; restoration is blocked while it would exceed the current allowance.
- Principle: show the next available time explicitly without deleting or hiding existing work.

### Safety and moderation

#### [DECISION D-24] What does reporting look like end to end?

- Status: behaviour resolved on 22 July 2026; implementation and legal verification remain.
- Reporting: attach a report to a specific sticky note, comment or board. Reasons are spam or scam; threats, harassment or hate; privacy or personal data; impersonation; illegal or dangerous content; sexual content or child safety; copyright through a separate route; and other with an explanation. Confirm immediately with a case reference.
- Review: triage internally as Emergency, High, Normal or Low without publishing response-time promises until performance is verified. A human makes the final decision. Automation may prioritise, detect obvious spam or apply temporary protection, but not permanently remove content or exclude an account without human review.
- Actions: no action, warning, temporary visibility restriction, removal, named feature restriction, suspension for 24 hours, 7 days or 30 days, or permanent exclusion. Severity and repetition determine the measure; serious cases may skip lighter steps. Moderators may hide, remove or restore content and may alter text only for a narrowly necessary, audited redaction.
- Access effects: a restriction disables only named capabilities. A suspension blocks account use and pauses invitation acceptance and contribution without deleting the account, board relationship or existing content. Permanent exclusion revokes platform access and pending invitations without running the V-06 account-deletion cascade. Existing contributions remain unless separately removed. Owner removal remains a board-level access decision.
- Blocking: do not build user-to-user blocking while there is no direct messaging, following or visible Public-author profile. Use Owner access removal and reporting instead.
- Notifications: tell the affected author and, for board content, the Owner the action, scope, duration, policy or legal ground, relevant facts, material automation and appeal route. Tell the reporter the outcome without disclosing private account information. A recorded safety or legal reason may delay notice and must be periodically reviewed.
- Appeals: free for six months, handled by a different human reviewer where practicable, with a fourteen-day internal target. Restore content or access where possible and issue corrected notifications after a successful appeal.
- Evidence: retain only the reported content, necessary context, report, decision, reviewer, timestamps, action and appeal. Delete ordinary case evidence six months after the final decision and serious or repeated-abuse evidence after twelve months. Longer retention requires a documented legal hold.
- Spam and emergencies: combine invitation and publication rate limits, duplicate detection, account-verification friction and human review. Escalate imminent danger, child-safety material, credible threats and binding legal requests through a documented emergency path.
- Verification: test the entire workflow, privileged audit, evidence expiry and restoration. Legally verify DSA applicability, public policy wording, privacy periods and emergency-reporting duties before launch.

#### How are blocked or removed users represented on shared boards?

- Status: resolved under D-24 on 22 July 2026.
- User blocking: no separate user-to-user blocking feature is planned without direct messaging, following or visible Public-author profiles. Owners use Participant-access removal for a board; users report safety or policy problems.
- Restriction and suspension: preserve existing contributions and the board relationship. A named restriction affects only specified capabilities; suspension blocks account use and pauses invitations and contribution for its duration.
- Permanent exclusion: revoke platform access and pending invitations without applying account deletion. Existing contributions remain unless separately removed through moderation. Account deletion continues to follow V-06; Owner-account deletion still deletes owned boards under D-22.

### Sticky-note content

#### [QUESTION Q-01] Which content forms are supported?

- Status: behaviour resolved on 22 July 2026; accessibility and implementation verification remain.
- Worldwide wall: create either a text sticky note or an **Instant Photo**. An Instant Photo is one uploaded image shown in a Polaroid-like frame with a caption; it is not a sticky note with an optional attachment.
- Public lifecycle: apply the same Draft/Public lifecycle, publication allowance, metadata, hearts, sharing, moderation and deletion rules to text sticky notes and Instant Photos.
- Private boards: create only sticky notes, each with one optional uploaded image. There is no separate Instant Photo object on a board.
- Files: accept images only, with a maximum of **5 MB** for each uploaded image. Reject documents, audio, video, archives and every other uploaded file category. Exact accepted image formats, dimensions and processing remain implementation details.
- URLs: reject URLs in sticky-note text and Instant Photo captions. Do not create clickable links or link previews and do not provide URL or general-attachment controls. Q-01 does not alter profile fields or private-board comment behaviour.
- Lifecycle: the image inherits the parent object’s audience, author, moderation and deletion lifecycle and is deleted with it. Draft/Public transitions for worldwide-wall objects and board access rules continue to apply to the complete object.
- Accessibility: the present alternative text **Instant Photo** identifies only the object type and is not an adequate image description. Design and test accessible alternative-text capture, presentation and fallback before making complete accessibility claims.
- Plan boundary: Q-01 defines content forms, not plan entitlement. The existing Instant Photo entitlement remains under D-13 and V-05 unless changed by a separate decision.
- Verification: test the 5 MB boundary, rejected file categories, URL validation, failed and interrupted uploads, image removal and replacement, Draft/Public transitions, board permissions, deletion and moderation cascades, **Save as image**, and alternative-text behaviour.

### Account and data

#### [DECISION D-21, D-22 and D-26] What happens to shared content when an account is deleted?

- Status: behaviour resolved on 21 July 2026 and the maximum 30-day technical-backup period resolved on 22 July 2026; implementation, backup-expiry and required-record verification remain high priority under V-06.
- Owned boards: deleting the Owner’s account permanently deletes every board it owns, with all attached board content and access. Ownership is not transferred.
- Contributions on somebody else’s board: sticky notes and comments remain and their displayed author becomes **Deleted user**. The account-deletion flow should explain that the author may permanently delete these contributions before deleting the account.
- Drafts and personal collections: delete all Drafts, public and private heart relationships, and the private Wall of Love.
- Dot votes: remove the account relationship and preserve only anonymous aggregate totals.
- Public sticky notes: retain them on the worldwide wall after removing the internal account relationship and author controls. Add a small strip of tape at the top and the accessible explanation **This sticky note remains after its author deleted their account.** Publication date, country of origin, share count and heart count remain visible. Authorised moderation remains available.
- Subscription: end future renewal during account deletion. Deleted data may remain in protected technical backups for no more than 30 days, without ordinary product access or user-facing recovery. Any required billing, tax or legal records follow a separately documented, legally verified retention rule and contain as little product content as practicable.
- External persistence: warn that independent copies, saved images, screenshots, search results, caches, AI datasets, model training and other external uses cannot be recalled.
- Still open: implementation and verification of deletion from protected backups within 30 days, and the exact legally required billing, tax or other record-retention periods.
- It must align across interface, Help Centre, Privacy Policy and Terms.

#### [DECISION D-11] Is data export needed?

- Status: resolved on 20 July 2026.
- Decision: an eligible individual sticky note can be saved as an image. The action is unavailable while a worldwide-wall sticky note is a Draft. No bulk, board-level or structured product export is provided or planned.
- Verification: image format, dimensions, resolution, filename, attribution/metadata and availability for Public and private-board sticky notes.
- Privacy boundary: a person may request access to or portability of personal data by email through the privacy process. This does not promise a board export, every shared object or a reusable product format.
- Documentation rule: never present a privacy request as an export feature.

## Remaining review queue

This is the canonical queue after the review on 21 July 2026. Existing ERROR, DECISION and VERIFY identifiers remain stable so cross-references in the five design documents do not break. Resolved questions are not repeated here.

### Source cleanup

1. **E-02 — terminology and British English.** Completed on 21 August 2026. The Help Centre, policies, design documents and interface copy were audited for non-canonical role labels, US spelling, old permalinks, configurable-permission claims and share-link wording that no longer matches revised D-23. Contextual mentions of rejected terms remain where they are clearly labelled as rejected. Keep the check in the release routine rather than as an open item: new copy is where new variants enter.

### Product decisions

1. **D-21 / V-06 — retained records.** Implement and verify deletion from protected backups within the resolved maximum of 30 days; legally verify any different billing, tax or other required-record periods; then align the interface, Privacy Policy, Terms, infrastructure and processors.

### Implementation and operational verification

1. **D-08 — notification operation.** Verify the 14-day expiry, **Declined** state, immediate invitation, revocation and mention emails, daily send schedule, aggregation, mention/digest duplication, access filtering, delivery failures and applicable preferences and unsubscribe or transactional-email treatment.
2. **V-05 — plan enforcement.** Verify pricing, tax and checkout wording, entitlements, selected-board downgrade archival and restoration after upgrade.
3. **V-06 — account deletion.** Implement and test the complete resolved lifecycle, including owned-board deletion, retained contributions, de-attributed Public sticky notes, tape treatment, interactions, subscription non-renewal and the retention decision above.
4. **V-07 — Help Centre publishing.** Verify preview behaviour, every British-English permalink, redirects or their intentional absence, internal links, production 404 behaviour, caching and rollback.
5. **V-09 — destructive actions.** Verify the approved confirmation copy, permissions, database cascades and all counter and result updates.
6. **V-10 — Public metadata.** Verify share and heart counters, Public → Draft reset, republishing, deletion, moderation and account-deletion behaviour end to end.
7. **V-11 — Owner deletion.** Verify that an Owner can delete another author’s sticky note on an active owned board, including authorisation, cascade, technical log and conditional digest.
8. **D-24 — moderation operation.** Implement and test reporting, human review, proportional measures, restrictions and suspensions, notifications, six-month appeals, evidence expiry, spam controls, least-privilege audit logging, emergency escalation and successful restoration after appeal; complete legal verification before launch.
9. **Q-01 — image content.** Implement and test Public text sticky notes and Instant Photos, private-board sticky notes with an optional image, image-only uploads, the 5 MB limit, URL rejection, inherited lifecycle, failed uploads and accessible alternative text. Verify exact image formats and dimensions without changing D-13/V-05 plan entitlement.
10. **Q-02 — current-value editing.** Verify that storage, APIs and interface retain no user-facing version history or restore path while text, caption, colour, tags, due date, images and future alternative text correctly overwrite the current object. Test this with V-04 autosave, failures and conflicts.
11. **D-11 / D-12 interface details.** Verify saved-image format, dimensions, resolution, filename and attribution, plus the exact calm publication success copy and placement of View, Share, Edit and Return to Draft.
12. **Q-03 — mentions.** Verify supported private-board entry locations, one and multiple current-Participant recipients, duplicates, adding or removing mentions during edits, permission loss, accessible controls and notification-email delivery. Confirm that no assignment fields or semantics exist.
13. **Q-04 — private-board organisation.** Verify lower-case board-scoped tags, Owner and Participant management, absence of merging, label-only deletion, sticky-note-only due dates, the expired-date display and the absence of due-date filtering and notifications.
14. **Q-05 — external discovery.** Verify search-engine and AI crawler access, public metadata and sitemap inclusion, the pre-publication warning, removal from public routes and discovery mechanisms, retained de-attributed Public content and aligned Terms and Privacy Policy.
15. **Q-06 — board recency.** Implementation added on 23 July 2026: the overview displays **Last modified on YYYY/MM/DD**, historical timestamps feed `last_activity_at`, and `Board::touch()` records new successful mutations. Stable `created_at DESC` ordering has been restored. Test creation fallback, accepted mutations and deletions, excluded reads and failed or rolled-back actions, access control, UTC display, consistency with D-08 and the absence of inactivity notifications or automated lifecycle effects.
16. **Q-07 — commercial positioning.** Audit marketing, pricing, paywalls, checkout and onboarding for the collaboration-first value hierarchy and tier narrative. Verify every supporting volume, organisation and personalisation claim against D-13, D-27 and the implemented product.
17. **D-23 — controlled board links.** Creation and revocation authorisation verified on 23 July 2026: `createShareLink` requires both board ownership and the Premium or Chosen Few collaboration entitlement for View and Post links; Participants cannot create links. `revokeShareLink` now requires ownership without a current paid entitlement. “Any plan” describes the signed-in Post-link contributor. Existing links become inaccessible after downgrade through `isShareLinkActive()` and `loadShareLinkOr404()`. Help Centre source copy and related navigation were aligned on 23 July 2026. Determine and verify whether an unrevoked link remains disabled or automatically reactivates after upgrade, then verify unguessable tokens, accountless read-only View access, signed-in Post access, absence of Participant-only capabilities, author controls, immediate revocation, forwarding risk, non-indexing and cache behaviour, archived-board behaviour and consistent activity timestamps before publishing.

### Closed as no longer applicable

- Multiple-board limits are resolved under D-27.
- Public author fields are resolved under D-25.
- A private board cannot be partially published because boards remain private under C-01 and no Public ↔ Private transfer exists under D-17.
- A Participant contribution cannot become Public through a board workflow; any future proposal would require a new explicit decision on consent, attribution and lifecycle.
- The complete Free journey is resolved as one active personal board plus full participation on invited boards under D-13 and D-27.
- Infrastructure, English convention and the board-role matrix are resolved under E-03, D-15 and D-07 respectively.

## Future directions

The sections below are retained as research history, not as roadmap commitments. Under D-04, they are parked while whole-board archiving is the only future feature under consideration.

### AI-assisted organisation

Potential value: suggest groups, labels or summaries when a board becomes difficult to scan.

Guardrails:

- suggestions, not silent reorganisation;
- user confirmation before changes;
- clear handling of private content;
- no training or secondary use without an explicit legal and product basis;
- always allow the original view and content to remain intact.

### Keep inspiration and collaboration conceptually connected

Explain Public inspiration and private collaboration as parts of one idea journey, without promising a control that transfers a Public sticky note into a private board. Direct Public → Private copy, move and reference flows are not planned.

### Reuse documentation for onboarding and support

Help Centre sections can power contextual help and support answers when the content stays canonical and versioned. Avoid maintaining separate copies that drift.

## Decision log

### 2026-07-20 — Separate public reactions from private-board discussion

- Status: accepted
- Context: it was unclear whether responses should be comments, sticky notes or both, and whether the same interactions applied publicly and privately.
- Decision: on the worldwide wall, a signed-in user can place a heart on a Public sticky note; this is the only public response. On private boards, invited participants can comment under a sticky note, place a heart and use dot voting. Comments are ordinary comments rather than sticky notes and do not use Draft/Public statuses.
- Rationale: the public wall remains calm and lightweight, while private boards support richer discussion and collective decision-making.
- Consequences: public comments and public dot voting are out of scope. Participants can post and delete their own comments, but cannot edit them. A private-board heart toggles between light and red and adjusts the displayed count by one. Only the Owner starts and closes a voting round and selects 1, 3, 5 or 10 dots per Participant, with 3 as the default; Participants can place at most one dot per sticky note, withdraw a vote while the round is active and see results only after closure. There is no reset or reopening. The active notice reports used votes against the allowance; the closed notice shows the last round’s closing date and results, while voted-on sticky notes show a voting-round icon and count. Starting a new round permanently removes access to the previous round and its results without a warning. Digest presentation remains under D-08. Moderator and administrator actions remain governed by D-24.
- Affected docs: Product Model, Product Playbook, Product Design Notes and Help Centre

### 2026-07-20 — Use the short product promise

- Status: accepted
- Context: the design set used both a short tagline and a complete introductory sentence.
- Decision: use **A place where ideas can grow together.** as the canonical product promise and tagline. Use “StickyNotes.club is a place where ideas can grow together” only as a grammatical sentence in ordinary prose.
- Rationale: the short version is more distinctive, memorable and flexible beside the product name or logo.
- Consequences: marketing, onboarding and homepage reviews should treat the short version as canonical without forcing sentence fragments into normal prose.
- Affected docs: all design documents, website, onboarding and Help Centre

### 2026-07-20 — Use Drafts and unshared boards for personal capture

- Status: accepted
- Context: the product promise allows thoughts to remain personal, while the existing model described only the worldwide wall and private collaborative boards.
- Decision: a sticky note intended for the worldwide wall has **Draft** and **Public** statuses. Drafts are hidden from other ordinary users; publishing makes them Public on the worldwide wall, and unpublishing returns them to Draft. A private board without other participants acts as a personal workspace hidden from other ordinary users. Authorised platform moderators and administrators retain privileged access to every Draft, board and sticky note. No separate personal inbox is introduced.
- Rationale: this supports capture first and structure later while reusing the existing sticky-note and private-board models.
- Consequences: the interface and privacy information must accurately explain ordinary-user visibility and privileged administrative access. Board sticky notes inherit board access and do not use Draft/Public statuses. Authors can return Public sticky notes to Draft; external copies, search results, caches and prior AI use may remain.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes and Help Centre

### 2026-07-20 — Use “sticky note” as the canonical product term

- Status: accepted
- Context: imported internal notes used “note” as the object name, while the established product and Help Centre predominantly used “sticky note”.
- Decision: use **sticky note** in titles, navigation, buttons, first mentions and formal definitions. Use **note** only as shorthand afterwards when no confusion is possible.
- Rationale: the full term reinforces the StickyNotes.club identity and distinguishes the object from comments, posts and generic notes.
- Consequences: interface and documentation reviews must reject post, card, item or content as interchangeable names for a sticky note.
- Affected docs: all design documents, interface copy and Help Centre

### 2026-07-20 — Keep sticky notes editable

- Status: accepted
- Context: imported notes proposed immutable public sticky notes, while current public documents promise that people can edit their own content.
- Decision: authors can edit all their own sticky notes. Authorised moderators and administrators may view content when D-24 permits, hide, remove or restore it, and alter text only for a narrowly necessary, audited redaction. Board owners and ordinary Participants cannot edit another author’s note solely because of their board role.
- Rationale: authors retain control and can correct mistakes; administrative editing supports moderation and operational correction without granting broad peer-editing rights.
- Consequences: moderator and administrator edits require permitted-use, audit, attribution and author-notification rules under D-24. The interface, Help Centre, Terms and Privacy Policy must accurately describe the final moderation process before it is released.
- Affected docs: Product Model, Product Playbook, Product Design Notes, Help Centre, Terms and Privacy Policy

### 2026-07-20 — Keep all boards private

- Status: accepted
- Context: the imported Dutch playbook described public boards and board publishing, while the current product model separated public sticky notes from private boards.
- Decision: boards remain private and access-controlled. Public content consists of individual sticky notes on the worldwide wall. Boards cannot be published or converted into public boards.
- Rationale: this preserves the simple distinction **Public inspires. Private builds.** and avoids introducing a second board visibility model.
- Consequences: public distribution happens through sticky notes; D-17 confirms that no direct copy, move or reference flow from Public to Private is planned.
- Affected docs: Product Model, Product Playbook, Product Design Notes and Help Centre

### 2026-07-20 — Consider only whole-board archiving as a future feature

- Status: accepted
- Context: the design notes included Completed and Archived states for individual sticky notes and several unapproved candidate features. The public Help Centre also described board archiving as already available.
- Decision: individual sticky notes have no Completed or Archived system states. The only future feature currently under consideration is archiving an entire private board, including all sticky notes, comments, hearts and dot votes. Only the Owner or an authorised platform moderator or administrator may archive it. Other net-new feature candidates are parked.
- Rationale: this keeps the roadmap focused and preserves a complete board’s context as one coherent unit.
- Consequences: current Help Centre archive claims must be removed until launch. V-02 defines a read-only archive that preserves all board content and interactions indefinitely, retains existing viewing access subject to Owner revocation, cancels pending invitations, blocks new invitations and routine notifications, and can be restored or permanently deleted only by the Owner or an authorised platform moderator or administrator. Under revised D-23, active View and Post links may show only the read-only archive; Post links cannot accept new sticky notes and the Owner may revoke either link.
- Affected docs: Product Model, Product Playbook, Product Design Notes and Help Centre architecture

### 2026-07-20 — Use only Owner and Participant as board roles

- Status: accepted
- Context: the source notes proposed Owner, Editor, Viewer and possibly Commenter, while the product is intended to keep private-board collaboration simple.
- Decision: a board has one Owner and invited Participants. Every Participant receives the same contribution rights: view the board, create sticky notes, edit and delete their own sticky notes, add and delete their own comments, place hearts and use dot voting. The Owner manages invitations, Participant access and the board and, on an active board, may delete any sticky note without editing another author’s text or separately deleting another author’s comment. There are no separate Viewer, Editor or Commenter roles. Moderator/Admin remains a separate platform role.
- Rationale: one participation level makes invitations and collaboration understandable without a permission matrix.
- Consequences: existing references to members, collaborators and adjustable Participant permissions must be removed or corrected. D-22 confirms one non-transferable Owner and permanent deletion of owned boards when the Owner’s account is deleted. Revised D-23 adds View and Post links as access capabilities without creating additional board roles.
- Affected docs: Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Help Centre, Terms and Privacy Policy

### 2026-07-20 — Use email-only board notifications

- Status: accepted on 20 July 2026; invitation lifecycle completed on 21 July 2026
- Context: an in-product activity overview and many immediate notifications would add noise and create a separate feature surface.
- Decision: send an immediate email for a private-board invitation, which expires after 14 days. Declining grants no access, appears to the Owner as **Declined** and sends no separate Owner email. Revoking Participant access is immediate and sends the former Participant an immediate email. A scheduled daily job sends at most one activity digest to a recipient and only when at least one private board they can still access has changed since the previous digest. Do not send immediate emails for individual comments, hearts, dot votes or routine edits, and do not create an in-product activity inbox.
- Rationale: access changes remain timely and explicit while ordinary collaboration is summarised calmly.
- Verification needed: expiry enforcement, invitation and revocation delivery, the **Declined** state, send schedule, aggregation window, what counts as a change, representation of changes, access filtering at send time, delivery failures and applicable preferences and unsubscribe or transactional-email treatment.
- Affected docs: Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Help Centre and email copy

### 2026-07-20 — Keep filtering scoped and omit product search

- Status: accepted
- Context: the source notes raised product-wide search, while the existing product uses narrower navigation controls.
- Decision: product search is unavailable and not planned. Private boards can filter sticky notes by tags. The worldwide wall can filter Public sticky notes by country. Boards themselves remain private.
- Rationale: the existing filters support the two relevant contexts without introducing a new cross-context search feature or additional privacy surface.
- Consequences: interface and Help Centre copy must call these controls filters, not search. Help Centre search remains a separate documentation feature.
- Affected docs: Product Model, Product Playbook, Product Design Notes, Help Centre architecture and Help Centre

### 2026-07-20 — Use public hearts as favourites on the Wall of Love

- Status: accepted
- Context: favourite was listed as a possible future concept, but the product already preserves hearted Public sticky notes for each user.
- Decision: an active heart on a Public sticky note is both public appreciation and a favourite. It adds the sticky note to the user’s private Wall of Love, which only that user can view. Private-board hearts do not affect the Wall of Love. Pin and priority are not planned.
- Rationale: one familiar action supports both lightweight public recognition and later retrieval without adding another control.
- Parked possibility: a future profile might make the Wall of Love visible to other people, but this is not planned.
- Removal lifecycle added on 21 July 2026: unhearting removes the Wall of Love entry and subtracts one; Public → Draft, deletion and moderation removal clear all heart/favourite relationships; republishing does not restore them. V-10 verifies implementation. Wall ordering or pagination remains a separate implementation detail.
- Affected docs: Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Help Centre and profile/interface copy

### 2026-07-20 — Limit export to an individual sticky-note image

- Status: accepted
- Context: saving one sticky note as an image, bulk product export and legal access or portability requests were being discussed as if they were one capability.
- Decision: a user can save an eligible individual sticky note as an image, but not while it is a Draft. StickyNotes.club does not provide or plan bulk, board-level or structured export. A person may continue to request access to or portability of personal data through the privacy process by email.
- Rationale: this states the current note-level capability without weakening applicable privacy rights or promising a reusable export of all shared content.
- Consequences: Help Centre copy must document **Save as image** separately from product export and privacy requests. Verify image details and availability; policy copy must accurately state the privacy-request route, identity checks and response process.
- Affected docs: Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Help Centre and Privacy Policy

### 2026-07-20 — Keep the post-publish experience immediate and calm

- Status: accepted
- Context: the post-publish result and the right level of celebration were undefined, while public content can persist in systems outside StickyNotes.club.
- Decision: publication places the sticky note immediately on the worldwide wall and shows a simple success message without confetti. The author can immediately view, share, edit or return it to Draft.
- Transparency: state public visibility, search indexing and external AI use before publication; warn at Return to Draft and deletion that independent copies, screenshots, search results, caches, AI datasets, model training or other external uses may remain. Put the full transparency explanation in the Privacy Policy and the contractual boundary in the Terms.
- Rationale: the flow confirms success and preserves control without manufacturing excitement or hiding an important consequence of public sharing.
- Consequences: remove “the world’s largest wall” and other unsupported reach claims; verify exact interface copy and keep the Help Centre, Privacy Policy and Terms aligned.
- Affected docs: Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Help Centre, Privacy Policy, Terms and interface copy

### 2026-07-20 — Let Free participate and charge for initiating collaboration

- Status: accepted; daily-limit details completed on 22 July 2026
- Context: plan limits covered public sticky-note volume and visual options but did not define private-board ownership or collaboration entitlements.
- Decision: Free permits 1 active, editable owned private board, Premium 5 and Chosen Few unlimited. Archived owned boards and joined boards do not consume this allowance. Only Premium and Chosen Few can send invitations; Free can receive invitations and participate fully. Comments, private-board hearts, dot voting and private-board sticky-note tags and due dates are included on every plan. Daily Public sticky-note allowances count successful **Draft → Public** transitions, including republication, and reset at **00:00:01 UTC**. Draft and private-board creation or editing, edits to existing Public sticky notes and failed publication attempts do not count. A downgrade automatically archives active owned boards above the new allowance with the Owner’s authorisation; they remain preserved and read-only under V-02 and cannot be restored above the allowance.
- Rationale: Free supports personal board use and complete participation, while paid plans unlock initiating and scaling private-board collaboration.
- Verification: confirm the counter, reset and local-time explanation in the working product under V-05.
- Consequences: pricing, interface limits, checkout entitlements and Help Centre tables must match exactly. The downgrade path depends on V-02 archiving, must disclose its board-specific effects before confirmation and must never delete existing content.
- Affected docs: Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Plans & subscriptions, interface and checkout

### 2026-07-20 — Use two minutes as a soft Help Centre target

- Status: accepted
- Context: a strict two-minute reading rule could make ordinary guides focused but would force unsafe omissions from complex pages.
- Decision: aim for under two minutes on ordinary Help Centre pages without treating it as a requirement. Privacy, billing, deletion, access, safety, troubleshooting and other necessary consequences may take longer.
- Rationale: focus helps users, but completeness and successful task completion matter more than an arbitrary reading time.
- Consequences: split content only when users have distinct goals; never cut essential warnings, consequences or recovery steps to meet the target.
- Affected docs: Product Playbook, Product Design Notes, Help Centre architecture and all Help Centre pages

### 2026-07-20 — Do not create a separate Understanding section

- Status: accepted
- Context: proposed conceptual pages overlapped with practical Help Centre tasks, marketing positioning and contextual onboarding.
- Decision: keep necessary concepts beside their relevant Help Centre task, put broad product value and “why” narratives on the marketing site, and provide concise guidance in the interface at the point of choice. Do not create a separate Understanding section.
- Rationale: this reduces duplication, avoids thin pages and gives users explanations where they are most useful.
- Consequences: Public versus Private belongs with publishing and privacy tasks; dot-voting rules belong with private-board collaboration; wider positioning remains canonical on the marketing site.
- Affected docs: Product Playbook, Product Design Notes, Help Centre architecture, Help Centre, marketing site and contextual interface copy

### 2026-07-20 — Keep one product journey across Public and Private

- Status: accepted
- Context: public notes and private boards were being described as separate capabilities.
- Decision: treat them as two contexts in the lifecycle of an idea.
- Rationale: this explains the product more clearly and creates a coherent basis for future transitions.
- Consequences: the shared journey is conceptual rather than a transfer workflow. D-17 confirms that no direct Public → Private feature is planned; any future proposal must state visibility, ownership and copy/move behaviour before it can be considered.
- Affected docs: Product Constitution, Product Model, Help Centre architecture

### 2026-07-20 — Do not plan a direct Public → Private transfer

- Status: accepted
- Context: the design notes left open whether a Public sticky note could be copied, moved or referenced into a private board.
- Decision: no direct copy, move, reference, create-board-from or add-to-board flow is planned.
- Rationale: Public inspiration and private collaboration can remain one conceptual journey without adding cross-context ownership, consent and deletion complexity.
- Consequences: viewing, sharing and saving an eligible Public sticky note as an image remain independent actions. They do not create a board sticky note, add the author as a Participant or transfer ownership. Reconsideration requires a new explicit product decision.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes and Help Centre architecture

### 2026-07-20 — Keep each private-board sticky note on one board

- Status: accepted
- Context: it remained unclear whether one sticky note created inside a private board could simultaneously belong to several boards.
- Decision: each private-board sticky note belongs to exactly one board and cannot simultaneously belong to multiple boards.
- Rationale: one board context keeps access, ownership, interactions and deletion behaviour clear.
- Consequences: separately captured similar material is a distinct sticky note with its own lifecycle; shared multi-board membership must not be designed or documented.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes and Help Centre architecture

### 2026-07-20 — Documentation is part of product delivery

- Status: accepted
- Context: writing Help Centre content exposed gaps in product behaviour.
- Decision: draft documentation during design and verify it as part of release acceptance.
- Rationale: clear documentation improves the interface and prevents unsupported promises.
- Consequences: changes affecting users are not complete until relevant documentation is current.
- Affected docs: Product Constitution, Product Playbook, Help Centre architecture

### 2026-07-20 — Keep sticky-note colours expressive

- Status: accepted
- Context: colour is currently offered as expression and a plan benefit, while teams may want to use it for organisation.
- Decision: do not assign universal product meaning to sticky-note colours; use tags or labels for explicit meaning.
- Rationale: preserves personalisation, avoids ambiguity and supports accessibility.
- Consequences: informal board-specific conventions remain possible, but product behaviour and documentation never depend on colour alone. Any future semantic-colour proposal requires a new explicit decision.
- Affected docs: Product Model, Organise your work guide

### 2026-07-20 — Use structured board templates without a growth limit

- Status: accepted; Brainstorm layout verified on 21 July 2026
- Context: board shape, templates, backgrounds, duplication and growth limits were undocumented or open.
- Decision: offer Blank, Retro, Kanban, Week planner and Brainstorm as creation templates. Blank and Brainstorm use the same grid structure, can later change to columns and differ only in default background and framing. Retro, Kanban and Week planner start with columns. Allow reordering within a row and movement between columns, offer nine backgrounds, do not support board duplication and apply no product-defined growth limit today.
- Rationale: templates provide useful starting structure while the board remains lightweight and adaptable without becoming a freeform digital whiteboard.
- Verification: V-08 resolved the earlier inconsistency on 21 July 2026; Brainstorm’s **Open grid** description matches its implemented structure.
- Consequences: documentation must explain the five starting points and movement model accurately. Any future limit, duplication feature or different layout model requires a new decision.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Private boards and Organise your work

### 2026-07-20 — Keep Public sticky notes published until deliberate action

- Status: accepted
- Context: unpublishing was defined, but the default lifetime of a Public sticky note remained open.
- Decision: a Public sticky note does not expire automatically and has no author-selected expiry date. It remains Public until its author returns it to Draft or deletes it, or authorised moderation removes it.
- Rationale: a stable default is predictable, preserves author control and avoids countdowns, expiry warnings and accidental disappearance.
- Consequences: returning to Draft removes the sticky note from the worldwide wall and current intentional discovery mechanisms but cannot recall independent copies, saved images, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred. If the account is deleted first, V-06 retains and de-attributes the Public sticky note, which remains indexable and available for external AI use. Protected technical backups expire within 30 days without product recovery; required-record periods remain open pending legal verification. Ordinary content deletion has no recovery period.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Sticky notes, Privacy Policy, Terms and interface copy

### 2026-07-20 — Make content deletion immediately permanent

- Status: permanence accepted on 20 July 2026; cascade and copy accepted on 21 July 2026; maximum 30-day technical-backup period accepted on 22 July 2026; implementation, backup-expiry and required-record verification remain
- Context: sticky-note, comment and board deletion lacked a documented recovery rule and the current warnings use inconsistent terminology.
- Decision: after confirmation, deletion of a sticky note, comment or board is immediately permanent. There is no Undo, trash, recovery period or restore flow.
- Decision added on 21 July 2026: sticky-note deletion includes comments, hearts and dot votes; comment deletion affects only that comment; board deletion includes all board content and interactions and removes Participant access and pending invitations without deleting accounts. Use the exact object-specific headings, bodies and buttons defined under V-09.
- Open work: implement and test V-09 database cascades, controls and counter/result updates; implement and test the resolved V-06 account-deletion lifecycle and deletion from protected backups within 30 days; legally verify separately required billing, tax or other record-retention periods.
- **Partly superseded on 21 August 2026** — see *Give private-board sticky notes a restore window*. Sticky notes on a private board now have a short restore window; Public sticky notes, comments and boards keep the permanence decided here, and moderation deletion is permanent for every object.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes, Help Centre architecture, interface copy, Privacy Policy and Terms

### 2026-07-20 — Keep one non-transferable Owner involved

- Status: accepted
- Context: ownership transfer, multiple Owners and the fate of a board after Owner-account deletion were unresolved.
- Decision: every board has exactly one Owner and ownership cannot be transferred. The Owner remains involved while the idea develops. Deleting the Owner’s account permanently deletes every board that account owns, including all attached content and participant access.
- Rationale: continued Owner involvement preserves context and responsibility during the development of an idea.
- Consequences: there is no co-ownership, handoff, successor Owner or administrative reassignment. Account deletion must clearly warn about all owned boards before confirmation. V-06 defines retained **Deleted user** contributions, de-attributed Public sticky notes, interaction cleanup, subscription non-renewal and the maximum 30-day protected-backup period; implementation, backup-expiry testing and legal verification of required-record periods remain open.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Private boards, account deletion, Privacy Policy, Terms and interface copy

### 2026-07-20 — Require an account and email invitation for private boards; revised with controlled share links on 23 July 2026

- Status: accepted on 20 July 2026; revised on 23 July 2026
- Context: documentation mentioned share links and left open whether someone could view or contribute to a private board without an account.
- Original decision: an email invitation was the only entry path and every visitor or contributor required an account.
- Revised decision: email invitation remains the only route to Participant status. Only an Owner with the Premium or Chosen Few collaboration entitlement may create a View link for accountless, read-only access or a Post link that lets a signed-in StickyNotes.club user on any plan add sticky notes. Participants cannot create links. Link users do not become Participants and receive no comments, hearts, dot votes or board-management rights. The Owner must be able to revoke either link at any time, including after downgrade.
- Rationale: invitation-based participation preserves identifiable ongoing collaboration, while explicit View and Post links support lightweight sharing with a narrower, understandable permission boundary.
- Consequences: invitations retain their 14-day lifecycle and personal revocation flow. Help Centre, Privacy Policy, Terms and interface copy must distinguish invited Participants, anonymous View-link visitors and signed-in Post-link contributors; explain paid Owner-only creation, automatic inaccessibility after downgrade, forwarding and plan-independent Owner revocation; and avoid calling link access a board role. Public sticky-note sharing remains separate. Later-upgrade behaviour for an unrevoked link still requires an explicit verified rule.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Private boards, Collaboration, Privacy & safety, Terms and invitation interface/email copy

### 2026-07-20 — Restrict and audit privileged content access

- Status: access safeguards accepted on 20 July 2026; end-to-end behaviour accepted on 22 July 2026; implementation and legal verification remain.
- Context: moderators and administrators can view otherwise hidden content, but exceptional access, reporting, measures and accountability needed one complete workflow.
- Decision: allow privileged access only when moderation, support, security or legal work genuinely requires it. Limit access and audit every view and action. Moderators may hide, remove or restore content but may alter an author’s words only for a narrowly necessary, audited redaction. Use the D-24 reporting reasons, immediate receipt, human final review, proportionate action ladder, clear notifications, free six-month appeal, six- or twelve-month evidence period, spam controls and emergency escalation. Do not introduce user-to-user blocking without direct communication or visible Public-author profiles. Restriction, suspension or exclusion does not automatically delete existing contributions.
- Rationale: exceptional access can support safety and operations without turning private content into routinely accessible internal content or silently changing an author’s words. Human review, reasons and appeal keep decisions correctable.
- Open work: implement and test the workflow, legally verify DSA applicability, evidence periods, public wording and emergency duties, and confirm operational targets before making current-capability claims.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Privacy & safety, Community guidelines, Privacy Policy, Terms, moderation tooling and interface copy

### 2026-07-20 — Keep Public sticky notes free of author profile fields

- Status: accepted; metadata behaviour resolved on 21 July 2026 and requires implementation verification under V-10.
- Context: the product model left open which profile identity and contribution fields accompany a Public sticky note.
- Decision: display no author identity or profile route. Store publication time in UTC and display **YYYY/MM/DD**. Copy the user-selected account country at sticky-note creation and keep the snapshot. Count each successful **Copy link** and **Save as image**, including repeats, as one share action. Unhearting subtracts one. Public → Draft clears hearts/favourites, resets both counts and gives a later publication a new date; deletion or moderation removal deletes the relationships and counters. After account deletion, remove the account relationship and author controls, retain the Public sticky note and its metadata and other users’ hearts, and add the V-06 tape and accessible deleted-account state.
- Rationale: the worldwide wall centres the idea and its public context without introducing a public social profile.
- Consequences: there is no public-profile route from the sticky note. The Wall of Love remains user-only and public profile visibility remains parked. Date format and creation-country snapshot are confirmed; verify counter and lifecycle implementation under V-10 before treating interface or Help Centre wording as final.

### 2026-07-22 — Distinguish Private ownership from Public relinquishment

- Status: accepted.
- Decision: users retain ownership of content they create or share inside private boards. By publishing a sticky note or Instant Photo to the worldwide wall, the user explicitly relinquishes ownership of that Public content. The worldwide wall shows no person, profile or contribution history; the country snapshot is its only origin information. Publication date, share count and heart count may also appear.
- Control boundary: while the account exists, a private internal relationship remains so the user can edit, return to Draft or delete the Public object and authorised moderation can act. This is not public attribution and does not preserve ownership after publication.
- Consequences: explain the ownership consequence before **Publish** and in the Sticky notes, Privacy & safety and FAQ guides. Align the Terms and Privacy Policy and obtain legal review of the relinquishment language and any rights that cannot legally be waived.

> **[DECISION D-28] Resolved on 22 July 2026; legal and policy alignment required** — Private-board content remains owned by its creator. Publishing to the worldwide wall explicitly relinquishes ownership without transferring it to StickyNotes.club. Public presentation remains person-free, with country as the only origin information, while a private internal relationship temporarily supports author controls and moderation.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Sticky notes, Manage your profile, Privacy & safety and interface copy

### 2026-07-20 — Preserve board sticky notes after their author leaves

- Status: accepted; Owner deletion behaviour resolved on 21 July 2026 and requires implementation verification under V-11.
- Context: authorship and editing were defined, but it remained unclear whether a contribution survives loss of board access or deletion of the author’s account and who may remove somebody else’s sticky note.
- Decision: preserve a sticky note on its board when its author leaves, loses Participant access or deletes their account. After account deletion, replace the displayed author with **Deleted user**. The author may permanently delete the sticky note before deleting their account. On an active board, the Owner may delete any sticky note without editing another author’s text or separately deleting another author’s comment. Owner deletion uses the V-09 cascade, a minimal technical event log and the conditional daily digest. Authorised moderators and administrators can delete any board sticky note under D-24.
- Rationale: preserving a contribution protects the shared context developed on the board while account identity and access are removed.
- Verification: V-11 tests the Owner control, authorisation, V-09 cascade, technical log and digest inclusion. Moderator and administrator deletion rights remain aligned with D-24’s equal content-moderation scope and stricter safeguards.
- Boundary: deleting a board or its Owner’s account still deletes the complete board under D-21 and D-22. V-09 resolves ordinary deletion cascades and copy but still requires implementation and counter/result verification. V-06 resolves account-deletion treatment for retained contributions, Public sticky notes, hearts, dot votes, subscriptions and the maximum 30-day protected-backup period; implementation, backup-expiry testing and legal verification of required-record periods remain open.
- Affected docs: Product Constitution, Product Model, Product Playbook, Product Design Notes, Help Centre architecture, Collaboration, Private boards, account deletion, Privacy Policy, Terms and interface copy

### 2026-08-03 — Rename and expand the plan ladder

- Status: accepted; pricing, entitlements, migration and implementation remain open
- Context: **Free** and **Premium** do not express the StickyNotes.club membership metaphor, and a distinct professional tier is needed between the current paid plan and Chosen Few.
- Decision: use **Club Member → Club Host → Club Facilitator → Chosen Few** as the public plan order. Club Member replaces Free, Club Host replaces Premium, Club Facilitator is a new tier between Club Host and Chosen Few, and Chosen Few keeps its name.
- Rationale: the ladder moves from belonging, through bringing people together, to professional facilitation while using the club identity established by the domain name.
- Boundary: this decision establishes names and order only. It does not change D-13 or D-27 entitlements, set prices or define Club Facilitator limits and capabilities.
- Open work: decide the Club Facilitator entitlement and price; map upgrades and downgrades across four tiers; update plan identifiers and billing products safely; verify checkout, account state, paywalls and enforcement; then update marketing, interface and Help Centre copy together.
- Affected docs: Product Model, Product Playbook, Product Design Notes; after implementation, Product Constitution, Help Centre, marketing, interface, checkout and billing configuration

> **[DECISION D-29] Resolved on 3 August 2026; entitlement recorded on 21 August 2026** — The public plan ladder **Club Member → Club Host → Club Facilitator → Chosen Few** is live. Club Member succeeded Free and Club Host succeeded Premium without an entitlement change. Club Facilitator adds workshop mode, guests without an account up to the configured session limit and a higher owned-board allowance, at a higher price; Chosen Few includes workshop mode. See the entitlement table in the Product Model.

### 2026-08-21 — Ratify board duplication as ordinary board management

- Status: accepted
- Context: `POST /b/@slug/duplicate` had shipped while D-19 still stated that boards cannot be duplicated and that any duplication capability requires a new explicit decision. Under D-31 that is a gate, so the code needed ratification rather than transcription.
- Decision: duplication is ordinary board management. The owner may duplicate; no separate entitlement applies; the copy counts against the active-board allowance and passes the same gate as creating a board. The copy takes a **named list** of setup fields — description, layout, columns in order, background, workshop instruction, facilitator name, anonymity, voting enabled — and no content, participants, invitations or links. A duplicated workshop starts in *preparing*; a duplicate of an ordinary board stays ordinary. The suggested name adds **(copy)** and does not stack.
- Rationale: all three open points were already answered consistently by the implementation, and answered well. The whitelist is the part worth promoting from implementation detail to rule: a field added later is not copied unless someone adds it, so the failure mode is an incomplete copy rather than a leak. Routing the duplicate through the creation gate is what stops duplication from becoming the way around the board limit.
- Consequences: "keep this setup as my own template" is now a product capability whether or not it was designed as one, and that expectation is better acknowledged than denied. A Participant cannot duplicate a board they take part in, even without its content: the setup belongs to its owner. That is a boundary, not an omission.
- Affected docs: Product Model (v1.8, D-19), Product Playbook (v1.8), Product Design Notes

### 2026-08-21 — Describe the session as a state of a board

- Status: accepted
- Context: seven migrations and three services had introduced a complete session context — statuses, an input lock, a reveal mode, a timer, a lobby, spotlighting, guests, presence, anonymity, a result page — and the words *workshop*, *guest*, *timer*, *spotlight*, *lobby* and *QR* appeared in none of the four standing documents. Every rule about roles, rights and deletion had been written for a world with only Owner and Participant, so each of the other six conflicts was a symptom of this one.
- Decision: a workshop session is a state a private board can be in, not a second board type and not a separate object. One board, one address, one set of content. A session has three properties — status, input and reveal — and anything derivable from them is not stored.
- Rationale: a second board type would need its own permissions, sharing, deletion rules and place in every list, for a difference that lasts an afternoon. Keeping the session a state of the board is also why the result survives it.
- The distinctions worth having written down: **closed input is a pause in collecting, finished is the end** — a session spends much of its useful life with input closed and everything else open, because that is when the room discusses and votes. **The timer is a signal, not a lock**, or "may I write" gets two answers that diverge on the first pause. **Finishing freezes taking part but never moderation.** **Steering controls belong to the session bar, looking controls next to the content**, and only the facilitator gets a control that changes what the room sees. **Anonymity applies to the facilitator too.**
- Consequences: the Product Model gains a session context, a session lifecycle and four invariants; the Playbook gains a *Workshop rules* section; the Constitution's boundaries now say what a session is deliberately not, because leading with sessions invites comparison with facilitation suites. The owner is the facilitator and there is deliberately no separate facilitator role in this version.
- Also settled while writing this: two different things were called *archived* — a future whole-board archive and a workshop status on an ordinary active board. Copy must name the object.
- Raised, not resolved: board duplication has shipped while D-19 still forbids it. Recorded as C-12.
- Affected docs: Product Constitution (v1.5), Product Model (v1.7), Product Playbook (v1.7), Product Design Notes; Help Centre Architecture still to follow

### 2026-08-21 — Let a guest contribute fully inside a session, and nowhere else

- Status: accepted
- Context: D-23 stated that link access never grants comments, hearts, dot votes or Participant status. Workshop mode introduced `board_participants`, an identity layer that covers people without an account, and `actor_key`, which gives a guest exactly one heart and one vote per sticky note. Guests comment, vote and contribute today. The rights model had moved from *do you have an account* to *which actor are you on this board*, and the Product Model and Playbook had not followed.
- Decision: a **workshop link** is a third link type alongside View and Post. Inside the session a guest contributes on the same terms as a Participant — own sticky notes, arranging, comments, hearts and dot voting. Outside that one board a guest has nothing: no invitations, no access management, no board settings, no other board. Guest access is chosen when the link is created and never acquired by an existing link, and a workshop link always carries an expiry. Removing a guest ends access and keeps their contributions.
- Rationale: the boundary that matters is reach, not capability. A session in which half the room can only watch is not a session, and dot voting is the step that turns a wall of ideas into a shared priority — withholding it from the people who are actually in the room would remove the product's reason to exist. The old rule stays intact where it was aimed: View and Post links remain the weaker form of access.
- Consequences: a nickname is not an identity. A guest lives in a browser, nobody is verified, the link is the access, and clearing browser data produces a new guest. Never build a right on top of a nickname. Because the nickname is personal data the moment it hangs on content, it is separated from the contributions after a retention period and the work continues under a neutral name.
- Verified rather than assumed: the guest link always receives an expiry, the nightly cleanup does what the Privacy Policy promises, and the public documentation already described all of this correctly. This conflict lived only in the design set.
- Open: the Terms do not cover participation without an account. Recorded as V-12; the join screen now links to the Terms as well as the Privacy Policy, which is disclosure, not coverage.
- Affected docs: Product Model (v1.6), Product Playbook (v1.6), Product Design Notes (D-23, V-12), `boards/join.html`, Terms of Service after review

### 2026-08-21 — Record the Club Facilitator entitlement and close the D-29 gate

- Status: accepted
- Context: D-29 forbade publishing the plan ladder until Club Facilitator pricing and entitlements were decided and the migration verified. The names went live, migration `010_facilitator_tier.php` created the tier and the pricing page sells it at a higher price than Club Host, while no document recorded what the tier actually grants. A tier was therefore being sold on entitlements that existed only in code.
- Decision: record what the product grants as the official entitlement. Club Facilitator adds workshop mode on owned boards, participation by people without an account up to the configured session limit and a higher owned-board allowance; its daily publication allowance equals Club Host's; Chosen Few includes workshop mode. The board and participant numbers are settings with documented defaults rather than constants, and any copy stating them must read them from the product.
- Rationale: the tier is live, priced and working, and the three properties above are defensible rather than accidental. The gate has served its purpose; keeping it open would only mean that every pricing claim stays formally uncovered.
- Two properties confirmed deliberately, so they are not later read as oversights: **the equal publication allowance**, because a facilitation plan sells sessions and not volume on the worldwide wall, and the Playbook forbids volume carrying the story; and **workshop mode for Chosen Few**, because Chosen Few is sold as everything above it plus a celestial address, and removing a capability afterwards withdraws a promise.
- Consequences: D-13, D-27 and the Product Model entitlement table now describe four tiers. The stored role identifiers stay `user`, `premium`, `pro` and `chosen_few` — data, not labels. V-05 keeps the verification that genuinely remains, now across four tiers.
- Noticed while checking, not a conflict: the pricing page understates the product. A template comment still says the results page is "phase 4 and does not exist yet", while `/b/@slug/results` ships with ranking, print and Markdown export. Selling value you already deliver is the right direction to be wrong in, but it is worth correcting.
- Affected docs: Product Model (v1.5), Product Playbook (v1.5), Product Design Notes, pricing page, Help Centre plan page

### 2026-08-21 — Replace downgrade archiving with a selection of editable boards

- Status: accepted
- Context: D-13 promised that a downgrade lets the Owner choose which boards stay active, shows the rest before confirmation and archives them. Two problems. Archiving is still a future capability under V-02, so the promise could not be built. And the code does something else entirely: `BoardService::isOwnBoardWritable()` keeps the oldest N boards writable with `ORDER BY created_at ASC` and silently makes the rest read-only, with no selection and no warning.
- Decision: keep the selection step and drop the archiving. On downgrade the Owner picks which owned boards remain editable; the others stay visible and owned but read-only, and an upgrade restores editing on all of them. Warn before the downgrade completes, and state the read-only condition on the board itself.
- Rationale: the selection is the part that protects the user; archiving was the part that blocked the build. Letting the product pick by creation date is experienced as data loss even though nothing is lost, and a board that refuses input without saying why reads as a bug rather than a plan boundary.
- Consequences: a small build — one selection screen and a read-only state on the board — with no dependency on V-02. Until it exists, the documented promise is not kept; V-05 carries that as a known gap rather than an unnoticed one.
- Affected docs: Product Model, Product Playbook, Product Design Notes (D-13, V-05), Plans & subscriptions, downgrade and checkout copy

### 2026-08-21 — Split authority between the code and the documents

- Status: accepted
- Context: the design set had fallen behind the application on seven points, and the working assumption became "the code is leading". Governance ranked the five documents against each other but said nothing about the implementation, so the most common disagreement in practice had no rule at all.
- Decision: the implementation is authoritative for behaviour; the documents are authoritative for intent, meaning purpose, positioning, product boundaries, plan promises and release gates. A behaviour difference is a documentation defect. An intent difference is a product finding and needs a decision.
- Tiebreaker: ask what the document was doing. A passage that describes is behaviour; a passage that permits, forbids, promises or gates is intent, and sentences built on **do not**, **only**, **never**, **until** or a price almost always are. When it stays unclear, treat it as intent — a correction delayed by a day costs little, a promise revised without noticing costs trust.
- Rationale: an unrestricted "code is leading" repeals the Constitution without a decision and turns this register into a changelog. C-06 and C-07 are the evidence: a homepage edit and a shipped tier would otherwise have settled positioning and pricing on their own, and the compliance gates in V-06 and D-24 would tick themselves the moment code existed. The reverse rule is equally unusable: it would declare soft delete, guest voting and the Club Facilitator tier defects, though all three improve on what was written.
- Consequences: code that outruns intent is not reverted or blocked, because the same person builds and decides here and a rule that stops the work is ignored; it is recorded as a CONFLICT and settled before the next release touching that area. The resolutions of C-06, C-08, C-10 and C-11 were made on this rule before it existed and are hereby ratified. The known cost of this variant is that every difference needs a judgement; the tiebreaker exists to keep that judgement from landing on the desk each time.
- Rejected: authority by enumerated domain — a fixed list of protected subjects such as pricing, legal, safety and positioning. Easier to apply mechanically, but it protects only what the list happens to name and ages silently.
- Affected docs: Product Constitution (v1.4), Product Playbook, Product Design Notes

### 2026-08-21 — Lead with facilitated sessions without replacing the promise

- Status: accepted
- Context: the homepage, the pricing page and the frontpage proposal position StickyNotes.club as a tool for guided workshops, while the Constitution described an audience explicitly not served by team software and the Playbook pillars led with capture. The site had moved; the design set had not.
- Decision: facilitated sessions are the primary use and the lead commercial story. **A place where ideas can grow together** remains the canonical promise and tagline under D-01. Public surfaces may lead with *Run a focused workshop in minutes*.
- Rationale: a campaign headline and a product promise may be different sentences as long as they do not contradict each other, and a workshop is the sharpest form of ideas growing together. Replacing D-01 would force a re-framing of the wall, the private board and the entire Help Centre for no demonstrable gain.
- Consequences: *Who we serve* now opens with leading a session and joining one without an account. The Playbook pillars lead with **Get a room thinking together**. Two claims become load-bearing and must stay literally true: **one facilitator, no seat licences** and **no accounts or installs for participants**. New boundary: do not promise video, chat, an integration catalogue, an infinite canvas, framework templates or cross-session analytics — leading with sessions invites comparison with facilitation suites, and the answer is that this product is deliberately smaller.
- Open work: the Help Centre Architecture navigation still follows the capture-first order, and C-05 must land before the session context can be documented properly.
- Affected docs: Product Constitution (v1.3), Product Playbook (v1.4), Product Design Notes, Help Centre Architecture, marketing site

### 2026-08-21 — Give private-board sticky notes a restore window

- Status: accepted
- Context: migrations 013 and 014 introduced soft delete with an **Undo** for every private board while D-21 forbade promising Undo, trash or a recovery period. The documents described a product that no longer existed.
- Decision: layer deletion per object. A private-board sticky note leaves the board immediately and can be restored by the same person for a short window, then is purged. A Public sticky note, a comment and a board are deleted permanently at confirmation. Moderation deletion is always permanent.
- Rationale: a facilitator who removes the wrong sticky note mid-session needs a way back, and abusive content must genuinely disappear. One rule could not serve both.
- Consequences: the private-board confirmation dialog is replaced by an **Undo** after the fact; restore uses exactly the delete permission, so a participant cannot undo moderation and a facilitator can still correct his own slip. Copy states that a window exists, never its length. Checked and confirmed: neither the Terms nor the Privacy Policy promises anything about deleting an individual sticky note, so no policy change was required.
- Affected docs: Product Model, Product Playbook, Product Design Notes (D-21, V-09, V-11), `troubleshooting.md`, `collaboration.md`, `sticky-notes.md`

### 2026-08-21 — Show votes remaining rather than votes used

- Status: accepted
- Context: V-03, the Product Model and the Playbook prescribed **you have used 0 of 3 votes**; the product had already changed to votes remaining.
- Decision: the notice reports what remains. Vote controls dim when the allowance is spent, except on sticky notes the person has already voted on.
- Rationale: a participant needs to know how many decisions are still theirs to make. "Used 2 of 3" asks for arithmetic in the middle of a session, and being unable to withdraw a vote would leave someone stuck with their first picks.
- Affected docs: Product Model, Product Playbook, Product Design Notes (V-03)

## Research prompts

Use these prompts in interviews, feedback analysis or usability tests:

- Tell me about the last idea you wanted to capture before you forgot it.
- When does a thought become something you want to share?
- What makes an idea too private for a public wall?
- Show me how you currently turn a loose idea into a plan with other people.
- At what point does a board become hard to understand?
- Show me what warning you would need before deleting an account that owns private boards.
- Show me whether the email invitation and required sign-in make private-board access clear.
- Which interruption or notification would be genuinely useful during collaboration?
