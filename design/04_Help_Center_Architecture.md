# Help Centre Architecture

> Status: v1.2
> Role: information architecture, templates and governance for docs.stickynotes.club

## Purpose

The Help Centre helps users complete a goal, understand an important consequence and recover when something goes wrong. It also acts as a public record of behaviour users can rely on.

The Help Centre is not a roadmap. It describes verified, available behaviour only.

## Audience and top tasks

The primary audiences are:

- someone considering or starting with StickyNotes.club;
- a user sharing a public sticky note;
- a board owner setting up collaboration;
- a participant contributing to a board;
- an account holder managing security, privacy or payment;
- a user trying to solve a problem or contact support.

Their top tasks are:

1. Create and verify an account.
2. Create a draft and publish a first sticky note.
3. Create a private board.
4. Invite someone and control their access.
5. Organise a growing board.
6. Understand plans and limits.
7. Fix access, email or billing problems.
8. Delete content or an account safely.

## Navigation model

Navigation follows user goals and the product journey. Labels should match page titles and product language.

### Start here

- Home
- Getting started

### Share ideas

- Sticky notes

### Build ideas together

- Private boards
- Collaboration
- Organise your work

### Account and plans

- Manage your profile
- Plans & subscriptions
- Privacy & safety

### Community

- Community guidelines

### Help and support

- Frequently asked questions
- Troubleshooting
- Contact & support

This is the current single-level architecture. Add subpages when a page serves multiple distinct goals or becomes difficult to scan; do not add hierarchy merely to make the Help Centre look larger.

### Conceptual content placement

Do not add the proposed **Understanding StickyNotes.club** section or standalone pages whose only purpose is broad explanation, such as:

- Why sticky notes?
- Public vs Private
- Why collaboration?
- Why dot voting?

Place practical concepts beside the task they support: explain Public versus Private while creating or publishing sticky notes, and explain dot-voting rules within private-board collaboration. Put “Why sticky notes?” and the broader value of collaboration on the marketing site. Use short contextual guidance in the product when a user makes a visibility, invitation or voting choice.

> **[DECISION D-16] Resolved on 20 July 2026** — No separate Understanding section. Do not duplicate broad positioning in the Help Centre or create thin conceptual pages; link to one canonical task or marketing explanation instead.

## Current content inventory

| Page | Primary user question | Canonical permalink | Status |
| --- | --- | --- | --- |
| Home | Where should I start? | `/` | Exists; revise links |
| Getting started | How do I create and set up my account? | `/getting-started/` | Exists; verify deletion scope |
| Sticky notes | How do I create, publish and unpublish a sticky note? | `/sticky-notes/` | Exists; add and verify Draft/Public behaviour and external-copy warning |
| Private boards | How do I create and manage a private board? | `/private-boards/` | Exists; currently presents proposed archiving as an available feature |
| Collaboration | How do we work together on a board? | `/collaboration/` | Exists; needs concrete workflows |
| Organise your work | How do I keep a board understandable? | `/organise-your-work/` | Exists; canonical British-English permalink |
| Manage your profile | How do I update or remove my account information? | `/manage-your-profile/` | Exists; contains vague capability language |
| Plans & subscriptions | Which plan do I need and how do I manage it? | `/plans-and-subscriptions/` | Exists; add the approved board, invitation, collaboration and Public-publication entitlements; verify pricing, UTC reset, counters and downgrade behaviour |
| Privacy & safety | Who can see my content and how do I stay safe? | `/privacy-and-safety/` | Exists; document the D-24 privileged-access safeguards and remove private-board share-link claims |
| Community guidelines | What behaviour is expected? | `/community-guidelines/` | Exists |
| Frequently asked questions | What are the short answers to common questions? | `/faq/` | Exists; keep concise |
| Troubleshooting | How do I recover from a common problem? | `/troubleshooting/` | Exists; verify every recovery step |
| Contact & support | How do I get human help? | `/contact-and-support/` | Exists; “team” language may overstate capacity |

## Immediate architecture issues

### Resolved route corrections

Resolved on 20 July 2026:

- plan links now point to `/plans-and-subscriptions/`;
- organisation links now point to `/organise-your-work/`;
- repository history contains no matching old permalinks, so no redirects were required.

> **[ERROR E-01] Resolved** — Source links and repository history were verified. Reopen this item only if an external published route is discovered.

### Language and label decisions

Resolved on 20 July 2026:

- **Plans & subscriptions** is the canonical page and navigation label;
- British English is used in all prose and interface copy;
- permalinks also use British English;
- `/organise-your-work/` replaces `/organize-your-work/` without a compatibility redirect, by explicit early-development decision;
- the source file is `docs/organise-your-work.md`.

Board-role terminology is also resolved:

- **Owner** is the person who controls the board, invitations and participant access;
- **Participant** is a person who receives board access through an invitation;
- member, collaborator, Editor, Viewer and Commenter are not canonical role labels;
- Moderator and Admin are separate platform roles, not board roles.

> **[DECISION D-07 / DECISION D-15 / DECISION D-23] Resolved on 20 July 2026; [ERROR E-02] source cleanup remains** — Apply these labels, British English, **Plans & subscriptions** and British-English permalinks consistently across interface copy, Help Centre pages and policies. Existing uses of members, collaborators, configurable permissions and private-board share links require removal or correction.

### Pages that overpromise detail

The Home page names invitations, private-board share links, comments, dot voting, layouts and filters, but the linked pages do not always explain how to perform those actions. D-23 confirms that private-board share links do not exist, so remove that claim. Comments, hearts and dot voting now have confirmed contexts; add verified workflows and rules or narrow the remaining promises.

Product filtering is bounded: private boards filter sticky notes by tags, while the worldwide wall filters Public sticky notes by country. Product search is unavailable and not planned. The search built into the Help Centre is separate and must not be used as evidence that the product itself supports search.

> **[DECISION D-09] Resolved on 20 July 2026** — Document **Filter by tag** for private boards and **Country** for the worldwide wall only after their exact controls and empty states are verified. Never refer to public boards; only individual Public sticky notes appear on the worldwide wall.

The Private boards guide should state that board creation contains a required **Name** field, an optional **Description** field and a template choice with **Blank** selected by default. It must not describe visibility, a central question or a desired result as creation fields; every board is private by definition. Document the five templates and their purpose: **Blank**, **Retro**, **Kanban**, **Week planner** and **Brainstorm**. Explain that Blank and Brainstorm use the same grid structure and can both later change to columns; only their default backgrounds and product framing differ. Retro, Kanban and Week planner start with columns. The Organise your work guide should explain reordering sticky notes within a row, moving sticky notes between columns, choosing from nine backgrounds, unrestricted current growth and the absence of board duplication. Do not describe the board as a freeform infinite canvas.

The Private boards guide should document **Last modified on YYYY/MM/DD** as a neutral date shown for each board in the board overview. Explain that it reflects the latest accepted visible change to the board, its content, organisation, collaboration or access. Merely opening or viewing a board does not change it. Do not describe an inactivity threshold, warning, reminder, email, activity feed, automatic reordering or automatic archival, restriction or deletion. The date is not an edit history and Q-06 adds no notification to the D-08 email model.

> **[QUESTION Q-06] Resolved on 22 July 2026; implementation verification required** — There is no indicator today. Publish the exact explanation only after verifying the creation value, included changes, excluded reads and failed edits, **YYYY/MM/DD** display, permissions and consistency with digest activity.

> **[VERIFY V-01] Resolved on 20 July 2026** — Document only **Name**, **Description** and template selection in the board-creation procedure.

> **[DECISION D-19] Resolved on 20 July 2026; [VERIFY V-08] resolved on 21 July 2026** — Document Blank and Brainstorm as structurally identical grid templates with different default backgrounds. Both can later change to columns. Retro, Kanban and Week planner start with columns.

The Organise your work guide must present sticky-note colours as expression and personalisation, not as product-defined status, priority or category. Use visible tags or labels whenever meaning matters, including any informal convention adopted within a board. Never require readers to distinguish meaning by colour alone.

> **[DECISION D-18] Resolved on 20 July 2026** — Do not document universal colour semantics. Colour remains expressive; explicit organisation belongs in tags or visible labels.

The same guide should explain that tags and due dates belong only to sticky notes on private boards. Tags are available only within their board and automatically become lower case. The Owner and every current Participant may create, rename and delete them; tags cannot be merged. Deleting a tag removes the label from affected sticky notes without deleting the sticky notes themselves. Private boards can filter sticky notes by tags.

Explain a due date as an optional visual attention signal. After it passes, the sticky note shows a red clock icon and the expired date. There is no due-date filter, reminder email or other due-date notification. Never put tags or due dates on a board, worldwide-wall Draft, Public sticky note or Instant Photo, and never describe a due date as assignment, task status or Public expiry.

> **[QUESTION Q-04] Resolved on 22 July 2026; implementation verification required** — Verify lower-case board-scoped tag behaviour, Owner and Participant management, absence of tag merging, label-only deletion, the expired-date treatment and the absence of due-date filtering and notifications before publishing exact procedures.

### Public hearts and the Wall of Love

A signed-in user’s heart on a Public sticky note is both the only public reaction and a favourite action. The sticky note appears on that user’s private **Wall of Love** while the public-heart relationship is active. Only that user can view the Wall. Private-board hearts never appear there.

Unhearting removes the entry from the user’s Wall of Love and subtracts one from the public heart count. Public → Draft, deletion and moderation removal clear every heart/favourite relationship; republishing does not restore them.

> **[DECISION D-10] Resolved; removal lifecycle added on 21 July 2026; [VERIFY V-10] implementation required** — Document the Wall of Love as user-only and add the heart’s dual meaning and removal rules to the Sticky notes guide and any Wall of Love guide. Public profile visibility is parked and must not be promised. Do not introduce pin or priority terminology.

### Public sticky-note metadata without an author profile

The Sticky notes guide must state that a Public sticky note shows a UTC-derived publication date in **YYYY/MM/DD** format, the user-selected account country copied at sticky-note creation, a completed-action share count and an active-heart count. The country is a stable snapshot and is never derived from IP. It does not show the author’s identity or a public-profile route. While the account exists, its relationship remains available internally for author controls and authorised moderation. After account deletion, the relationship and author controls are removed, the sticky note and metadata remain, and a small strip of tape at the top plus the accessible explanation **This sticky note remains after its author deleted their account.** communicate the state without adding identity.

Each successful **Copy link** or **Save as image** action adds one to the share count, including repeats; explain that it represents completed actions, not unique people or confirmed external distribution. Unhearting subtracts one. Public → Draft removes all public hearts/favourites and resets heart and share counts; republishing uses a new publication date, zero counts and no restored favourites. Deletion or moderation removal deletes the relationships and counters. Account deletion preserves the de-attributed note and aggregate metadata, removes heart relationships created by the deleted account and preserves other users’ hearts.

> **[DECISION D-10 / DECISION D-25] Resolved; [VERIFY V-10] implementation required** — Date format and country snapshot are confirmed. Verify share increments, repeats, unhearting, Public → Draft, republishing, deletion, moderation removal and account deletion end to end before publishing exact behavioural claims.

### Sticky-note and image content

The Sticky notes guide must distinguish the two worldwide-wall forms. A user publishes either a text sticky note or an **Instant Photo**, consisting of one uploaded image presented in a Polaroid-like frame with a caption. Both Public forms use the same Draft/Public lifecycle, publication allowance, metadata, hearts, sharing, moderation and deletion rules. The Private boards and Collaboration guides must describe only sticky notes; each private-board sticky note may contain one optional image, but an Instant Photo is not a separate board object.

State that images are the only accepted uploaded file category and each image is limited to **5 MB**. Do not document documents, audio, video, archives or general attachments. Sticky-note text and Instant Photo captions reject URLs, offer no clickable links or previews and expose no URL control. This Q-01 rule does not by itself change profile fields or private-board comments.

Explain that an image inherits the parent object’s audience, author, moderation and deletion lifecycle and is deleted with that object. Cover Draft/Public transitions, board permissions, image removal or replacement, rejected and interrupted uploads and the 5 MB validation error only after those paths have been implemented and verified.

The current alternative text **Instant Photo** is a generic type label rather than a useful image description. Do not make complete accessibility claims until the product has designed and tested accessible alternative-text capture, presentation and fallback. Exact accepted image formats and dimensions remain implementation details. The existing Instant Photo plan entitlement remains under D-13 and V-05.

> **[QUESTION Q-01] Content behaviour resolved on 22 July 2026; accessibility and implementation verification required** — Publish the two Public forms, single private-board form, image-only and 5 MB rules, URL prohibition and inherited lifecycle only when the product matches them. Keep the alternative-text deficiency visible as launch work.

### Publishing and persistent external copies

The Sticky notes guide should describe the complete immediate result: the Public sticky note appears on the worldwide wall, a calm success message is shown, and the author can view, share, edit or return it to Draft. Do not describe a celebration, confetti or “the world’s largest wall”.

A Public sticky note remains Public without an automatic or author-selected expiry until its author returns it to Draft or deletes it, or authorised moderation removes it. The Sticky notes guide must state this stable default without implying a countdown or scheduled disappearance.

The publishing flow and Sticky notes guide must state that every Public sticky note and Instant Photo may be crawled, indexed, cached and shown by external search engines. Their public text and images may also be processed or used by external AI services, including to train, improve, evaluate or operate AI systems. There is no separate search-indexing or AI-use opt-out. Keep this disclosure visible before **Publish**, not only in the Terms or Privacy Policy.

Drafts and private-board content must never be documented as available to public search or AI crawlers. Returning a Public object to Draft, deleting it or removing it through moderation stops StickyNotes.club from serving it publicly and removes it from current intentional discovery mechanisms. Explain that existing search results, caches, AI datasets, model training and other third-party uses cannot necessarily be identified, recalled or erased. A retained de-attributed Public object remains indexable and available for external AI use after account deletion until authorised moderation removes it.

> **[QUESTION Q-05] Resolved on 22 July 2026; implementation, policy and legal verification required** — Verify the Publish warning, public metadata, sitemap and crawler behaviour for text sticky notes and Instant Photos; verify removal from public routes after Return to Draft, deletion and moderation; and align the Terms and Privacy Policy. Do not promise control over prior search-engine or AI use.

Do not add a Help Centre workflow for copying, moving, referencing, creating a board from or adding a Public sticky note to a private board. No direct Public → Private transfer is planned. Viewing, sharing and saving an eligible Public sticky note as an image are independent actions; they do not create board membership, transfer ownership or add the author as a Participant.

> **[DECISION D-17] Resolved on 20 July 2026** — Keep Public and Private connected in the product explanation, but do not imply that a cross-context transfer control exists or is planned. Reopen this only through a new explicit product decision.

Describe a private-board sticky note as belonging to exactly one board. Do not document simultaneous multi-board membership. Similar material captured separately on another board is a distinct sticky note with its own author, interactions and lifecycle.

Use three documentation layers for external copies, search indexing, caches and AI use:

1. Contextual interface copy before **Publish** and at **Return to Draft** or deletion.
2. A concise explanation in the Sticky notes and Privacy & safety guides.
3. Full transparency in the Privacy Policy, with the contractual removal boundary in the Terms.

> **[DECISION D-12] Resolved / verification required** — Verify the exact success message, action labels and warning placement in the product. The public guides must explain that returning to Draft removes the sticky note from the worldwide wall and current intentional discovery surfaces but cannot recall independent copies, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred.

> **[DECISION D-20] Resolved on 20 July 2026** — Document no automatic expiry and no author-selected expiry date. Keep account-deletion and the maximum 30-day protected technical-backup period linked to the separate D-21 rules; ordinary content deletion has no recovery period.

### Immediate and permanent content deletion

The Sticky notes, Collaboration and Private boards guides must state that deletion of a sticky note, comment or board becomes permanent immediately after confirmation. There is no Undo, trash, recovery period or restore flow.

Document these approved cascades and confirmations:

- Sticky note: delete its comments, hearts and dot votes; use **Delete this sticky note?**, **This permanently deletes the sticky note and all its comments, hearts and votes. This cannot be undone.**, **Cancel** and **Delete sticky note**.
- Comment: delete only that comment; use **Delete this comment?**, **This permanently deletes the comment. This cannot be undone.**, **Cancel** and **Delete comment**.
- Board: delete all sticky notes, comments, hearts and dot votes and remove Participant access and pending invitations without deleting participant accounts; use **Delete this board?**, **This permanently deletes the board and all its sticky notes, comments, hearts and votes. It also removes all participants and pending invitations. This cannot be undone.**, **Cancel** and **Delete board**.

For a Public sticky note, also explain that independent copies, saved images, screenshots, search results, caches, AI datasets, model training and other external uses cannot be recalled.

> **[DECISION D-21] Partly resolved on 20 July 2026; [VERIFY V-09] cascade and copy approved on 21 July 2026; account-deletion behaviour resolved on 21 July 2026; technical-backup period resolved on 22 July 2026** — Publish the ordinary cascades and object-specific confirmation model only after V-09 verifies the implementation and counter/result updates. V-04 separately governs cross-session visibility. For account deletion, use V-06: protected backup copies expire within 30 days without ordinary product access or recovery; separately required record periods remain pending legal verification.

### One non-transferable board Owner

The Private boards and account-deletion guides must state that every board has exactly one Owner and that ownership cannot be transferred to a Participant or reassigned by a moderator or administrator. This preserves the Owner’s involvement while the idea develops.

Deleting the Owner’s account permanently deletes every board that account owns, including the board content and participant access attached to it. The account-deletion flow must show this consequence before confirmation and should identify the affected boards clearly. Do not promise a successor Owner or recovery path.

> **[DECISION D-22] Resolved on 20 July 2026; V-06 implementation verification required** — Verify the warning and owned-board deletion cascade. V-06 preserves sticky notes and comments on other Owners’ boards under **Deleted user**, retains de-attributed Public sticky notes with the tape and accessible state, removes personal hearts and preserves only anonymous dot-vote totals. Protected backup copies expire within 30 days; required billing, tax or legal-record periods remain pending legal verification.

The account-deletion guide and confirmation must distinguish every outcome: owned boards and Drafts are permanently deleted; sticky notes and comments on other Owners’ boards remain under **Deleted user**; Public sticky notes remain without an account relationship or author controls, receive the tape and accessible explanation, and remain indexable and available for external AI use; personal heart relationships and the private Wall of Love are removed; dot-vote totals remain only without the account relationship; and future subscription renewal ends. Explain that deleted data may remain in protected technical backups for no more than 30 days, without ordinary product access or a user-facing recovery path, and that separately required billing, tax or legal records may use a legally mandated period while containing as little product content as practicable. Explain that independent copies, saved images, screenshots, search results, caches, AI datasets, model training and other external uses cannot be recalled. Do not publish exact required-record periods until they have been legally verified or promise complete backend erasure before backup expiry has been tested.

### Invitation-only, account-based board access

The Private boards, Collaboration and Privacy & safety guides must state that access starts with an email invitation. The recipient signs in or creates an account before becoming a Participant. There are no anonymous visitors, guest roles, accountless contributions or private-board share links.

Document that an invitation expires after 14 days, that declining grants no access and appears as **Declined** to the Owner without a separate Owner email, and that revoking Participant access takes effect immediately and sends the former Participant an immediate email. Sharing a Public sticky note remains a separate action and must not be presented as private-board access.

> **[DECISION D-23] Resolved on 20 July 2026** — Remove private-board share-link claims from Help Centre pages and policies. Do not document accountless viewing, commenting, voting or contribution.

### Sticky notes after a Participant leaves or deletes their account

The Collaboration and account-deletion guides must explain that ending Participant access does not remove that person’s existing sticky notes or comments. If the person deletes their account, those contributions remain on boards owned by somebody else and their displayed author becomes **Deleted user**. Before account deletion, explain that the author may permanently delete these contributions themselves. Authorised moderators and administrators retain their D-24 moderation powers.

On an active board, the Owner can permanently delete any sticky note, including one written by a Participant, but cannot edit another author’s text or separately delete another author’s comment. The Sticky notes and Collaboration guides must use the V-09 warning and explain that comments, hearts and dot votes disappear with the sticky note. The deletion is technically logged without retaining the deleted content body and appears in the affected author’s conditional daily digest while that author still has access; there is no immediate deletion email.

> **[DECISION D-26] Resolved on 21 July 2026; [VERIFY V-11] implementation required** — Verify Owner-only board scope, controls, authorisation, V-09 cascade, minimal technical log and digest inclusion before publishing the workflow. Moderator and administrator deletion remains subject to D-24’s stricter privileged logging and notification safeguards.

> **[VERIFY V-03] Resolved on 20 July 2026** — Public response is limited to hearts from signed-in users. A Public sticky note can be shared through **Copy link**, which places its direct link on the clipboard, or **Save as image**, which generates an independent image suitable for storage or social media. Invited private-board Participants can post and delete their own comments but cannot edit them. A private-board heart is a personal toggle: the first click changes the light heart to red and adds one to the displayed count; the next click changes it back to light and subtracts one. Only the Owner starts and closes a voting round and chooses 1, 3, 5 or 10 dots per Participant, with 3 selected by default. A Participant may place at most one dot per sticky note, withdraw a vote while the round is active and see results only after the Owner closes the round. There is no reset or reopening. Document the active notice as **Voting is open — you have used 0 of 3 votes. Votes stay hidden until the round is closed.** and the latest-results notice as **Showing the results of the last voting round (closed 2026/07/20).**, substituting the current values and actual closing date. Each voted-on sticky note displays a voting-round icon and count. Starting a new round permanently makes the previous round and results unavailable without a warning. Digest presentation remains under D-08 and V-10 separately tracks the share counter.

> **[VERIFY V-04] Requirement approved on 21 July 2026; implementation action required** — Real-time collaboration is reported as probably not implemented. Do not claim that changes appear immediately until testing confirms synchronisation without refresh for sticky-note creation, editing, deletion and movement, comments, hearts, votes and voting-round state. When implemented, document autosave and visible saving, saved and failed states; preservation and safe retry of unsaved text after failures; conflict handling that retains the local version instead of silently applying last-write-wins; and server-authoritative heart, vote and position state. Verify separate sessions, connection loss, failed requests, simultaneous author/moderator editing and permission loss before publishing the workflow.

### No edit history

The Sticky notes and Collaboration guides must not describe a version history, revision list, comparison view or restore-version action. Sticky notes and Instant Photos retain only the currently accepted state. An accepted change to text, caption, colour, tags or due date replaces the previous value. Image replacement or removal and future alternative-text changes likewise create no stored version.

Explain tags and due dates only where those organisational fields are supported. A due date is not a Public expiry date; D-20 continues to prohibit automatic and author-selected Public expiry. Keep autosave, preserved unsaved text and conflict handling under V-04: they protect work in progress but do not create an accepted-version timeline. Do not expose D-24 audit records or report evidence as edit history or a routine restoration path.

> **[QUESTION Q-02] Resolved on 22 July 2026; implementation verification required** — Verify current-value overwrite across storage, APIs and interface while preserving V-04 saving, retry and conflict protection. Publish no edit-history or version-restoration claims.

### Email-only notification model

The Help Centre should describe four private-board email flows: an immediate invitation email, an immediate access-revocation email to the former Participant, an immediate mention email to each explicitly named current Participant and a conditional daily activity digest. A declined invitation is shown to the Owner as **Declined** without an email. A scheduled job sends at most one digest to a recipient per day and only when a board they can still access has changed since the previous digest. There is no in-product activity inbox and no immediate email for each comment, heart, dot vote or edit unless the recipient is explicitly mentioned.

> **[DECISION D-08] Resolved on 21 July 2026; mention email added under Q-03 on 22 July 2026 / operational verification required** — Document the 14-day invitation expiry, **Declined** status without Owner email, immediate revocation and revocation email, immediate mention email, and conditional once-daily digest. Verify mention entry points, duplicate handling, mention/digest duplication, scheduling, aggregation, access filtering, delivery failures and applicable preferences and unsubscribe or transactional-email treatment before documenting settings or exact delivery times.

### Mentions without assignment

The Collaboration and Sticky notes guides must state that sticky notes cannot be assigned and never have an assignee or responsible person. Private-board content may instead mention one or more current board Participants. Each named person receives an immediate email. A mention draws attention only; it does not change the author, Owner, permissions, edit or deletion rights, due date or responsibility. Public sticky notes and Instant Photos do not support mentions.

Document only the mention entry locations verified in the product. Test one and multiple recipients, duplicate mentions, edits that add or remove a mention, access revoked before sending, email delivery, preferences, accessible controls and whether the event also appears in the daily digest. Never use **Assign**, **Assigned to**, **Responsible** or task-management language for this feature.

> **[QUESTION Q-03] Resolved on 22 July 2026; implementation verification required** — Publish mentions as an attention and email feature, not an assignment system. Do not document assignee filters, acceptance, reassignment or responsibility.

### Sticky-note images, product export and privacy requests

An eligible individual sticky note can be saved as an image, but **Save as image** is not available for Drafts. On a Public sticky note, the Sticky notes guide should document the two sharing actions: **Copy link** places the direct link on the clipboard for use in an external channel, while **Save as image** generates an independent local copy suitable for storage or social media. A successful completion of either action increments the share count. Do not promise direct social-network posting. Verify image format, dimensions, resolution, filename, attribution or metadata and availability for private-board sticky notes.

StickyNotes.club does not provide or plan bulk, board-level or structured export. Do not document printable-board, Markdown, JSON, CSV, PDF or similar export workflows.

A person can contact StickyNotes.club by email to exercise applicable privacy rights to access or portability of personal data. The Privacy & safety and Contact & support pages should link to the canonical Privacy Policy and explain the request route without calling it a product export or promising that every shared object is returned in a reusable format.

> **[DECISION D-11] Resolved on 20 July 2026** — Document the single-note image action, keep broader product export absent and keep privacy requests available by email. Do not present these three paths as interchangeable.

### Plan entitlements and daily limits

The Plans & subscriptions page needs a scannable comparison table with the following product rules:

| Capability | Free | Premium | Chosen Few |
| --- | --- | --- | --- |
| Sticky notes per day | 2 | 12 | Unlimited |
| Active, editable owned private boards | 1 | 5 | Unlimited |
| Send private-board invitations | No | Yes | Yes |
| Receive invitations and participate | Yes | Yes | Yes |
| Comments, private-board hearts and dot voting | Yes | Yes | Yes |
| Mention current board Participants | Yes | Yes | Yes |
| Private-board sticky-note tags and due dates | Yes | Yes | Yes |

State that archived owned boards and joined boards do not consume the active-board allowance. The daily sticky-note limit applies only to successful **Draft → Public** transitions, including republication. Creating or editing Drafts, creating or editing private-board sticky notes, editing an existing Public sticky note and failed publication attempts do not count. When the limit is reached, explain that publication is unavailable until **00:00:01 UTC on the next day**, expressed for the user in local time.

Lead the Plans & subscriptions page with private collaboration as the primary paid value while keeping the Help Centre factual rather than promotional. The supporting tier summary is **Free is for capturing and joining. Premium is for bringing people together around your own ideas. Chosen Few is for people who want no practical plan-level volume limits.** Follow it immediately with the exact comparison table and explanations above.

Make clear that Free Participants retain full collaboration rights on boards they join, Premium primarily unlocks sending invitations and initiating collaboration on owned boards, and Chosen Few removes the documented plan-level publication and active-board limits only. Present higher volume, organisation and personalisation as supporting differences. Do not imply that payment removes safety, content, file or technical boundaries or alter D-13 and D-27 through marketing shorthand.

> **[QUESTION Q-07] Resolved on 22 July 2026; content and commercial verification required** — Align the Plans & subscriptions guide with the collaboration-first value hierarchy and verify all supporting claims against the product, pricing and checkout. Keep broad emotional positioning on the marketing site under D-16.

> **[DECISION D-13] Resolved on 22 July 2026 / [DECISION D-27] Resolved and refined on 21 July 2026 / [VERIFY V-05] required** — Apply the successful-publication counter and UTC reset above. A deliberate downgrade to Free requires the Owner to select 1 active, editable owned board; a downgrade to Premium requires a selection of up to 5. Before confirmation, list the selected active boards and every other owned board that will be archived, and refuse to continue until the selection fits the new allowance. Automatically archive the listed excess boards with the Owner’s authorisation and preserve them read-only under V-02. Do not count archived or joined boards towards the active allowance, and block restoration when the allowance is full. Verify counters, archival, checkout and later upgrade behaviour before enabling or documenting the flow. Never describe the downgrade as deleting content.

### Future board archiving described as current

`docs/private-boards.md` currently says that a user can archive a board, and `docs/organise-your-work.md` advises archiving completed work. Whole-board archiving is only a proposed future feature. Until it ships, remove both current-capability claims.

> **[DECISION D-05 / VERIFY V-02] Resolved design; not yet available** — When implemented, explain that archiving preserves the entire private board, including sticky notes, comments, hearts and dot votes, indefinitely. The board remains visible but read-only for the Owner and existing Participants; the Owner can revoke access, pending invitations are cancelled, new invitations and routine activity or daily-digest notifications stop, and cancelled invitations do not revive after restoration. Only the Owner or an authorised platform moderator or administrator may archive, restore or permanently delete it. Necessary privileged moderation remains available under D-24. Private-board share links do not exist under D-23.

### Infrastructure and cross-site consistency

The documentation repository and branch are locally confirmed as `faridbouchdak/stickynotes.club` on `main`; the Jekyll site is configured under `/docs` for `https://docs.stickynotes.club`. GitHub Pages automatically publishes changes from `main`, failed builds are visible in GitHub Actions and the live host uses valid HTTPS. Fly.io does not deploy the documentation. Cloudflare provides the domain and network layer but no deployment.

> **[ERROR E-03] Resolved on 20 July 2026** — Fly.io hosts the application, database and stored content in Amsterdam. Cloudflare provides the domain’s DNS, network delivery and security. Hetzner is no longer used, and the About page now agrees with the Privacy Policy.

## Page types

### Task guide

Answers “How do I do this?” Use numbered steps and state prerequisites and results.

Examples: create a board, invite a participant, cancel a subscription.

### Concept guide

Answers “How does this work?” Explain the mental model, choices and consequences.

Examples: public versus private, permissions, plan limits.

### Troubleshooting guide

Answers “Why is this not working?” Start with the symptom, then provide the safest likely fixes from simplest to most involved.

### Reference page

Provides details users need to compare or verify.

Examples: plan comparison, supported limits or permission matrix.

A page may combine a short concept introduction with task sections, but should still have one primary question.

> **[DECISION D-14] Resolved on 20 July 2026** — Treat “readable in under two minutes” as a soft target for ordinary guides. Accuracy, necessary consequences and successful task completion take priority for billing, deletion, privacy, access, safety and troubleshooting. Split a page only when it contains distinct user goals; never remove essential information merely to shorten it.

## Standard page pattern

Use only the sections that help answer the page’s primary question.

1. **Front matter** — layout, unique title, navigation order and stable permalink.
2. **Title** — matches navigation and search language.
3. **Introduction** — names the user goal and expected outcome in two or three sentences.
4. **What you’ll learn** — optional for longer pages; list concrete outcomes.
5. **Main task or explanation** — meaningful headings, prerequisites and numbered steps where order matters.
6. **Result and consequences** — what changes, who can see it and whether it can be undone.
7. **Good to know** — only useful limits, cautions or adjacent choices; do not repeat the page.
8. **Related guides** — two to four likely next tasks.

Horizontal rules may separate major sections, but should not substitute for information hierarchy.

## Writing and formatting rules

- Lead with the outcome, then explain the action.
- Use one idea per paragraph.
- Prefer concrete verbs and exact interface labels.
- Use numbered lists for sequences and bullets for choices.
- Put interface labels in bold.
- Use sentence case for headings.
- Avoid “simply”, “easy”, “just” and promotional claims.
- Explain irreversible or access-changing consequences before the action.
- Do not use “depending on your account” when an exact plan or permission rule can be named.
- Do not describe the company as a team when support is provided by one person unless that presentation is intentional.
- Use **A place where ideas can grow together.** as the canonical tagline. Use the full sentence with “StickyNotes.club is” only when ordinary prose requires a complete sentence.

> **[CONFLICT C-03] Resolved on 20 July 2026** — **Sticky note** is the canonical term in titles, navigation, buttons, first mentions and formal definitions. **Note** may be used as shorthand afterwards when unambiguous. Search copy may include note, post or idea as discovery synonyms, but these are not product labels.

## Search and discoverability

- Put the words users are likely to search for in the title or first paragraph.
- Include common synonyms naturally: cancel subscription, stop renewal, delete account.
- Use one canonical page for each fact and link to it rather than duplicating volatile details.
- Keep pricing, plan limits and role permissions in structured comparison sections where they are easy to scan.
- Add redirects when a published permalink changes.

Recommended search synonyms to consider in page metadata or copy:

| Canonical term | Likely searches |
| --- | --- |
| Sticky note | note, post, idea |
| Private board | board, workspace, project |
| Participant | member, collaborator, teammate |
| Plans & subscriptions | pricing, billing, upgrade, cancel |
| Account deletion | remove account, close account, erase data |

## Linking rules

- Link descriptive text, not “click here”.
- Link to the primary page for a concept.
- Prefer relative site permalinks for Help Centre pages.
- Check every internal link before publication.
- Related guides should reflect the user’s likely next question.
- Policy links must resolve correctly from both the main site and docs subdomain; absolute URLs may be safer when the sites publish separately.

## Documentation workflow

### Before implementation

1. Identify the user question and canonical page.
2. Draft the expected workflow and consequences.
3. Flag facts that need product, policy or billing confirmation.

### During implementation

1. Match interface terminology to the draft.
2. Capture empty, error, permission and destructive states.
3. Update screenshots only when they materially reduce confusion; prefer durable text.

### Before publication

1. Test every documented step in the current product.
2. Verify plan, role, platform and region differences.
3. Check headings, navigation, links and redirects.
4. Review related Privacy Policy, Terms and pricing claims.
5. Remove future-facing or unverified language.

### After publication

1. Monitor support questions and failed searches.
2. Correct unclear wording at the canonical source.
3. Review pages affected by each product release.
4. Schedule periodic checks for pricing, providers, retention periods and legal contact details.

### Reuse without duplication

The long-term goal is to maintain product knowledge once and reuse it for:

- the Help Centre;
- website FAQs;
- onboarding messages;
- in-product help;
- support replies and a possible AI assistant;
- tutorials.

The canonical source must remain identifiable. Reuse through links, structured content or generation; do not create independent copies that silently drift.

## Technical publishing baseline

- Repository: `faridbouchdak/stickynotes.club`
- Branch: `main`
- Documentation source: `/docs`
- Generator/theme: Jekyll with Just the Docs
- Canonical docs host: `https://docs.stickynotes.club`
- Search: enabled through the current Just the Docs configuration

> **[VERIFY V-07] Partly resolved on 21 July 2026** — GitHub Pages is the confirmed deployment path, not Fly.io or Cloudflare. Automatic publication from `main`, Actions failure visibility, the canonical host and HTTPS are working. Local configuration confirms `/docs/CNAME` as `docs.stickynotes.club`, `_config.yml` as `https://docs.stickynotes.club` and Just the Docs as the theme. Still verify preview behaviour, British-English permalinks, intentional redirect absence or presence, internal links, the production 404 path, cache behaviour and rollback before treating the operational baseline as complete.

## Documentation acceptance checklist

- The page answers one primary user question.
- Behaviour has been verified in the product.
- Visibility, permissions and destructive consequences are explicit.
- Interface labels match exactly.
- Plan and price claims match checkout and entitlements.
- Internal and cross-site links work.
- Related pages do not contradict the change.
- Front matter and permalink are correct.
- The page works on a narrow screen and remains scannable.
- No roadmap item is presented as currently available.

## Recommended next content pass

1. Fix canonical links and navigation labels across all pages.
2. Audit every capability named on the Home page.
3. Replace vague profile and permission language with verified rules.
4. Expand Collaboration into concrete invitation, access and contribution tasks.
5. Document what happens when a board, note, account or subscription is deleted or cancelled.
6. Align infrastructure and provider statements across About, Privacy Policy and Help Centre.
7. Add automated link checking to the publication workflow.
8. Keep conceptual explanations with their relevant tasks and broad positioning on the main site; do not add an Understanding section.
9. Resolve note/sticky-note terminology and the English spelling convention.
10. Reconcile About and Privacy Policy infrastructure claims.
11. Add a reporting flow from each eligible sticky note, comment and board with **Spam or scam**, **Threats, harassment or hate**, **Privacy or personal data**, **Impersonation**, **Illegal or dangerous content**, **Sexual content or child safety**, **Copyright** through its separate route, and **Other** with an explanation. Return an immediate receipt and case reference, and explain the result without disclosing another person’s private account information.
12. Explain that authorised moderators and administrators may access Drafts, private boards and sticky notes only for genuine moderation, support, security or legal work, using least privilege and audited access. They may hide, remove or restore content but may alter an author’s words only for a narrowly necessary, audited redaction.
13. Document the proportional action ladder, the effect of restrictions, suspension and permanent exclusion, and that existing contributions remain unless separately removed. Do not document a user-to-user block control; Owners remove board access and users report policy or safety problems.
14. Explain the decision notice and free six-month appeal, including scope, duration, reason, material automation and restoration after a successful appeal. State that safety or law may temporarily delay notification.
15. Keep evidence periods, emergency escalation and exact response times out of current-capability copy until implementation and legal verification are complete. The intended rules are six months for ordinary cases, twelve months for serious or repeated abuse and longer only under a documented legal hold.

> **[DECISION D-24] Behaviour resolved on 22 July 2026; implementation and legal verification required** — Moderators and administrators use the same content-moderation capabilities; broader administrator system or account-management powers remain separate. The approved workflow covers report reasons and receipt, human final review, proportional measures, no separate user blocking, restriction and suspension effects, notifications, six-month appeals, evidence expiry, spam controls and emergency escalation. Publish these as current behaviour only after end-to-end testing and legal review.

## Success signals

The Help Centre is working when:

- users can choose the right guide from its title and description;
- a task can be completed without contacting support;
- support questions reveal genuinely new situations rather than missing basic instructions;
- product, Help Centre, pricing and policy language agree;
- documentation changes ship with product changes;
- broken links and unverified claims are caught before publication.
