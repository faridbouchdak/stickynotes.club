# Product Model

> Status: v1.2
> Role: shared model of the current product
> Source of truth: implemented product behaviour, verified Help Centre content and current policies

## Product promise

**A place where ideas can grow together.**

This is the canonical tagline. The full sentence with “StickyNotes.club is” is reserved for ordinary prose where a complete grammatical sentence is needed.

The smallest useful object is a sticky note. The larger purpose is the progress an idea can make through sharing, discussion, organisation and collaboration.

## The idea journey

**Thought → Sticky note → Connections → Board → Collaboration → Decision or result**

This is the underlying growth model from the new notes. The shorter user-facing lifecycle remains:

**Capture → Share → Discuss → Organise → Collaborate → Execute**

Both are maps, not mandatory workflows. An idea may remain personal, stop after any step, skip steps, move backwards or be deliberately abandoned.

| Stage | User goal | Primary product support |
| --- | --- | --- |
| Capture | Preserve a thought quickly | Create a sticky note |
| Share | Make the thought visible to others | Worldwide wall or board access |
| Discuss | Add perspectives and context | Public interaction or board collaboration |
| Organise | Make relationships and priorities visible | Position, group, tag and date notes |
| Collaborate | Develop the idea with other people | Private boards, invitations and permissions |
| Execute | Turn a clearer idea into action | Due dates, decisions and links to the next workflow |

StickyNotes.club is strongest from capture through lightweight execution. It does not need to manage every downstream task.

### Growth phases

1. **Capture:** preserve an incomplete or fleeting thought without mandatory metadata.
2. **Explore:** add context, variants or related notes without forcing an early structure.
3. **Connect:** make relationships visible, possibly by bringing notes into a board.
4. **Collaborate:** help another person understand the context and contribute meaningfully.
5. **Make concrete:** record a choice, experiment, action or outcome without turning every note into a task.
6. **Complete or let go:** preserve useful context on its board or delete information that should not be retained.

> **[CONFLICT C-04 / DECISION D-02] Resolved on 20 July 2026** — Personal capture uses two existing models rather than a separate inbox: a Draft is hidden from other users, and a private board remains hidden from other ordinary users while its owner does not share it. Authorised platform moderators and administrators retain privileged access to all Drafts, boards and sticky notes.

## Product contexts

### Public: the worldwide wall

The public context exists to discover, inspire and start conversations.

Current characteristics:

- public sticky notes can be discovered by other people;
- Public sticky notes can be filtered by country;
- users need an account to create content;
- authors remain responsible for what they publish;
- Public sticky notes and Instant Photos may be shared, crawled, indexed, cached and shown by external search engines;
- their public text and images may be processed or used by external AI services, including to train, improve, evaluate or operate AI systems;
- users can interact with public notes through the controls available to their plan;
- inappropriate content can be reported and moderated.

The central expectation is reach: a public note is not confidential.

Country filtering is contextual browsing, not text search. There are no public boards.

#### Draft and Public statuses

A sticky note intended for the worldwide wall has two publication statuses:

- **Draft:** visible to its author and authorised platform moderators or administrators, but hidden from all other users and absent from the worldwide wall;
- **Public:** published on the worldwide wall and discoverable by other people.

Publishing is the deliberate transition from Draft to Public. The author can later unpublish a Public sticky note by returning it to Draft. Draft is a publication status, not a separate personal inbox or board type.

Public publication permits intentional external discovery and reuse: StickyNotes.club does not block search-engine indexing or external AI use of Public sticky notes and Instant Photos. There is no separate per-object search or AI opt-out. Before **Publish**, explain that the content can appear in search results and can be copied, cached or used by external AI services. The author remains responsible for having the right to publish the text and image and should not publish sensitive personal information or material they are not entitled to share.

A Public sticky note has no automatic or author-selected expiry. It remains Public until its author returns it to Draft or deletes it, or until authorised moderation removes it under the applicable rules. Returning it to Draft or deleting it stops StickyNotes.club from serving the public content and removes it from intentional indexing surfaces, but cannot recall independent copies, saved images, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred. A Public sticky note retained after account deletion remains public, indexable and available for external AI use until authorised moderation removes it.

After publication, the sticky note appears immediately on the worldwide wall and the author receives a calm success message. From the published sticky note, the author can immediately view, share, edit or return it to Draft. Publishing does not use confetti or another celebratory interruption.

> **[DECISION D-12] Resolved on 20 July 2026; disclosure expanded under Q-05 on 22 July 2026** — Use immediate publication, a simple success message and direct access to **View**, **Share**, **Edit** and **Return to Draft**. Do not use the unsupported “world’s largest wall” claim. Before publication, clearly state that the sticky note becomes public, may be indexed by search engines and may be used by external AI services. When returning it to Draft or deleting it, explain that this removes it from StickyNotes.club but cannot recall independent copies, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred. The Privacy Policy provides the full transparency explanation; the Terms state the contractual boundary.

> **[DECISION D-20] Resolved on 20 July 2026; account-deletion exception added on 21 July 2026** — Public sticky notes do not expire automatically and authors do not select an expiry date. Publication continues until deliberate author action or authorised moderation. If the account is deleted first, the sticky note remains after de-attribution under V-06 and can subsequently be removed only through authorised moderation.

> **[QUESTION Q-05] Resolved on 22 July 2026; implementation, policy and legal verification required** — Permit search-engine indexing and external AI use for every Public sticky note and Instant Photo, with no separate per-object opt-out. Keep Drafts and private-board content unavailable for public crawling. Verify the pre-publication warning, public-page metadata, sitemap and crawler configuration, removal from public surfaces after Draft, deletion or moderation, retained de-attributed Public content, and aligned Terms and Privacy Policy. Never promise recall from search engines, caches, AI datasets or models.

> **[CONFLICT C-01] Resolved on 20 July 2026** — Boards remain private and access-controlled. Public content consists of individual sticky notes on the worldwide wall. A board cannot be published or converted into a public board.

### Private: boards

The private context exists to brainstorm, organise, collaborate, decide and move an idea forward.

Current characteristics:

- a board has an owner;
- invited participants receive access through an invitation;
- every participant receives the same contribution rights; there is no separate Viewer, Editor or Commenter role;
- the owner manages invitations and participant access;
- board participants see the shared state of the board;
- a board can be permanently deleted;
- archiving the complete board is the one future lifecycle feature under consideration.

The central expectation is controlled access. “Private” does not prevent an authorised participant from copying information they can see.

An owner may keep a private board unshared. In that state, no other ordinary user has access and the board acts as a personal workspace for sticky notes. Authorised platform moderators and administrators retain privileged access. Inviting a participant adds access without making the board public.

### The boundary

Public sticky notes and private-board sticky notes are separate objects in separate visibility contexts. No built-in action to copy, move, reference, create a board from or add a Public sticky note to a private board is planned. Viewing, sharing or saving an eligible Public sticky note as an image does not transfer it into a board, change its ownership or make its author a board participant.

Any future cross-context workflow must be introduced through a new explicit product decision that defines visibility, attribution, consent, ownership, interactions and deletion behaviour before implementation.

## Core objects

### Account

An account represents a person’s access and identity.

It includes a verified email address, credentials, profile information, preferences and a plan. A user controls their profile and can delete their account. Account deletion must end future subscription renewal as part of the flow; any required billing records follow their separately documented retention rules.

### Profile

A profile contains account and identity information that may support account and collaborative contexts. Its name, username, profile picture, description and links do not accompany a Public sticky note on the worldwide wall.

Profile information is subordinate to the account: deleting the account removes the active profile, subject to documented retention and third-party copies.

### Sticky note

A sticky note is the smallest unit of expression in the product.

**Sticky note** is the canonical product term. Titles, navigation, buttons and formal definitions use the full term. “Note” may be used afterwards as shorthand when its meaning is unambiguous.

Depending on context, a sticky note may contain one optional image, have a colour, receive interactions and carry organisational metadata. On the worldwide wall, the user chooses between a text sticky note and a separate **Instant Photo** object: one image in a Polaroid-like frame with a caption. Both Public forms use the same Draft/Public lifecycle, publication allowance, metadata, hearts, sharing, moderation and deletion rules. On a private board, every contribution remains a sticky note with an optional image and never becomes an Instant Photo. Its author can edit it whether it is a Draft, appears publicly or is on a private board. Authorised platform moderators and administrators can view every object when D-24 permits privileged access and can hide, remove or restore it. They do not ordinarily rewrite an author’s words; only a narrowly necessary redaction, such as removing exposed personal data from otherwise permitted content, may change the text and must be audited.

Each uploaded image is limited to **5 MB**, inherits the parent object’s visibility, ownership, moderation and deletion lifecycle and is deleted with that object. Images are the only accepted uploaded file category; documents, audio, video, archives and other files are rejected. Sticky-note text and Instant Photo captions reject URLs and never generate clickable links or link previews. The current alternative text **Instant Photo** is only a generic type label, not an adequate description; accessible alternative-text capture and presentation remain an implementation requirement. Exact accepted image formats, dimensions, processing, failed-upload behaviour and alternative-text interface must be verified before the capability is documented as complete.

> **[CONFLICT C-02] Resolved on 20 July 2026; privileged-editing boundary refined under D-24 on 22 July 2026** — All sticky notes remain editable by their author. Board ownership or ordinary participation does not grant permission to rewrite another author’s note. Moderators and administrators may hide, remove or restore content and may alter text only for a narrowly necessary, audited redaction; they must not silently rewrite an author’s words.

Sticky notes and Instant Photos have no edit or version history. An accepted change to text, caption, colour, tags or due date overwrites the current stored value and leaves no earlier value available for viewing or restoration. Tags and due dates exist only in contexts that support those organisational fields; a due date is not a Public expiry date. Image replacement or removal and future alternative-text changes likewise update only the current object and do not create versions.

Autosave, locally preserved unsaved text and the V-04 conflict interface are transient reliability mechanisms. They do not expose a timeline or retain an earlier accepted server version after the conflict is resolved. D-24 audit records and report evidence remain purpose-limited operational records rather than an edit history and must not be offered as a version-restore source.

> **[QUESTION Q-02] Resolved on 22 July 2026; implementation verification required** — Do not build a history, revision list, compare view, previous-version viewer or restore-version action for sticky notes or Instant Photos. Verify that storage, APIs, interface and Help Centre reflect current-value-only editing without weakening autosave or conflict protection.

Colours are an expressive, personal and plan-related choice. They have no product-defined meaning and must not represent status, priority or category. Explicit organisation uses visible tags or labels. Users may form informal colour conventions within a board, but the product and documentation must never rely on colour alone to communicate meaning.

> **[DECISION D-18] Resolved on 20 July 2026** — Keep sticky-note colours expressive. Do not introduce product-wide colour semantics. Use visible tags or labels for explicit meaning and preserve accessibility without colour perception.

### Board

A board is an access-controlled workspace containing sticky notes arranged around a shared purpose.

A board has:

- a name and owner;
- an optional description;
- invited participants;
- sticky notes in a grid or column layout;
- one of nine selectable backgrounds;
- optional organisation of its sticky notes through tags and due dates;
- an active or deleted state today, with a future archived state under consideration.

A board is both a collection and a lightweight workspace: it groups related notes while giving participants enough shared context to understand what is happening. It should not require a formal project description, workflow or setup.

The board overview shows **Last modified on YYYY/MM/DD** for each board. Board creation establishes the initial value. Update it after every accepted user-visible mutation to board content, organisation, collaboration, access or settings, including changes to board details or layout; sticky notes, their images, tags and due dates; comments and mentions; hearts and dot voting; and invitations or Participant access. Viewing or opening a board, a failed or unsaved attempt, background maintenance, backup activity and privileged access without a user-visible change do not update it.

This is a neutral last-change date, not an inactivity status. Do not calculate or display an inactive threshold, send inactivity email, notification or reminder, automatically reorder boards by recency, or automatically archive, restrict or delete a board because time has passed. The indicator appears in the board overview only and creates no history or activity feed.

> **[QUESTION Q-06] Resolved on 22 July 2026; implementation verification required** — Add the board-overview date and verify its initial value, every included mutation, excluded reads and failures, **YYYY/MM/DD** presentation, access filtering and relationship with D-08 digest activity. Confirm that it creates no inactivity label, notification, automated lifecycle action or event history.

> **[VERIFY V-01] Resolved on 20 July 2026** — Board creation contains a required **Name** field, an optional **Description** field and a template choice with **Blank** selected by default. There is no visibility choice, central-question field or desired-result field. Every board is private by definition.

Board creation offers five starting templates:

| Template | Description | Starting structure |
| --- | --- | --- |
| **Blank** | An empty board, arrange it however you like | Default selection; grid that can later be changed to columns |
| **Retro** | Went well / To improve / Actions — great with dot-voting | Columns |
| **Kanban** | To do / Doing / Done | Columns |
| **Week planner** | A column for every weekday | Columns |
| **Brainstorm** | Open grid for collecting ideas, vote on the best ones later | Grid; structurally identical to Blank, with a different default background, and can later be changed to columns |

Sticky notes can be reordered within their current row and, in column layouts, moved between columns. Boards cannot be duplicated. They currently have no product-defined spatial or content limit and grow as material is added; this is structured growth, not a freeform unlimited canvas.

Blank and Brainstorm have identical structural behaviour. Their different names, descriptions and default backgrounds provide different starting moods, but neither adds columns or different board capabilities.

> **[DECISION D-19] Resolved on 20 July 2026; Brainstorm layout verified on 21 July 2026** — Use the existing template-based grid/column model, nine selectable backgrounds, no board duplication and unrestricted current growth. Blank and Brainstorm both start as grids and can later change to columns; only their default backgrounds and framing differ. Any future limit or duplication capability requires a new explicit decision.

### Deletion of sticky notes, comments and boards

Deletion is immediately permanent. There is no Undo control, trash, recovery period or restore flow for a sticky note, comment or board.

- Deleting a sticky note also permanently deletes every comment, heart and dot vote attached to it.
- Deleting a comment deletes only that comment.
- Deleting a board permanently deletes all its sticky notes, comments, hearts and dot votes. It removes Participant access and pending invitations but does not delete participant accounts.

Use the following canonical confirmations:

- **Sticky note:** heading **Delete this sticky note?**; body **This permanently deletes the sticky note and all its comments, hearts and votes. This cannot be undone.**; actions **Cancel** and **Delete sticky note**.
- **Comment:** heading **Delete this comment?**; body **This permanently deletes the comment. This cannot be undone.**; actions **Cancel** and **Delete comment**.
- **Board:** heading **Delete this board?**; body **This permanently deletes the board and all its sticky notes, comments, hearts and votes. It also removes all participants and pending invitations. This cannot be undone.**; actions **Cancel** and **Delete board**.

For a Public sticky note, also show the existing warning that deletion from StickyNotes.club cannot recall independent copies, saved images, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred. Dependent phrases should be omitted only when that context cannot contain the named objects.

> **[DECISION D-21] Partly resolved on 20 July 2026; cascade and copy resolved on 21 July 2026; account-deletion behaviour resolved on 21 July 2026; technical-backup period resolved on 22 July 2026** — Immediate permanence, ordinary deletion cascades, canonical object-specific confirmations and a maximum 30-day protected-backup period are resolved. V-09 must verify deletion implementation and counter updates. V-06 must verify backup expiry; the separate legal or billing-record periods remain open pending legal review.

### Membership and access

Access connects a person to a board. There are two board roles:

- **Owner:** creates and remains responsible for the board, invites and removes participants, may delete any sticky note on the active board without editing another author’s text, and may delete the board. Once whole-board archiving exists, the owner may also archive it. Each board has exactly one Owner and ownership cannot be transferred.
- **Participant:** receives access through an invitation and can view the complete board, create sticky notes, edit and delete their own sticky notes, and add or delete their own comments. A participant can also place hearts and use dot voting.

There are no separate Viewer, Editor or Commenter board roles. Invitation always grants participation rather than read-only access. An Owner does not hand off an owned board: deleting the Owner’s account permanently deletes every board that account owns.

Private-board access is granted only through an email invitation. The recipient must sign in to an existing account or create an account before becoming a Participant. An invitation expires after 14 days. Declining it grants no access and leaves the invitation marked **Declined** for the Owner without sending a separate email. There are no private-board share links, anonymous visitors or accountless viewing, comments, hearts, dot votes or sticky-note contributions. The Owner can revoke a Participant’s access; revocation takes effect immediately and sends the former Participant an immediate email.

Revoking or otherwise ending a Participant’s access does not remove that person’s existing sticky notes from the board. If the Participant later deletes their account, those sticky notes remain on boards owned by somebody else and their displayed author becomes **Deleted user**. The author can avoid this persistence by deleting their sticky notes before account deletion.

On an active board, the Owner can permanently delete any sticky note, including one written by a Participant, but cannot edit another author’s text or separately delete another author’s comment. Deleting the sticky note invokes the V-09 warning and removes its comments, hearts and dot votes. Record the Owner, board, sticky note, author, time and cascade outcome in a technical event log without retaining the deleted content body. Include the deletion event in the affected author’s conditional daily digest while that author still has board access; do not send an immediate email. Authorised moderators and administrators can also delete any board sticky note under the stricter D-24 audit and notification safeguards.

> **[DECISION D-07] Resolved on 20 July 2026** — Use only **Owner** and **Participant** as board roles. Authorised platform moderators and administrators remain platform roles, not board roles.

> **[DECISION D-22] Resolved on 20 July 2026** — A board has exactly one non-transferable Owner. Neither a Participant nor a moderator or administrator can receive ownership through transfer. Owner-account deletion deletes all boards owned by that account and therefore all content and access attached to those boards.

> **[DECISION D-23] Resolved on 20 July 2026** — Require an account for all private-board access and participation. Use email invitations only; do not create or document private-board share links or accountless roles. Public sticky-note sharing remains a separate Public action.

### Interaction

Interactions depend on context:

- **Worldwide wall:** a signed-in user can place a heart on a Public sticky note. The heart is both the only public response and a favourite action: the sticky note appears on that user’s **Wall of Love** while the heart remains active.
- **Private board:** an invited participant can comment under a sticky note, place a heart and vote through dot voting.

Comments are ordinary comments, not sticky notes. They do not use Draft/Public statuses and remain visually and conceptually subordinate to their sticky note.

> **[DECISION D-03] Resolved on 20 July 2026** — Public interaction is limited to hearts from signed-in users. A public heart also saves the Public sticky note as a favourite on the user’s Wall of Love. Invited private-board participants can comment, place hearts and use dot voting. Comments are not linked sticky notes, and private-board hearts do not add sticky notes to the Wall of Love.

A Participant can post a comment and delete their own comment, but comments cannot be edited after posting. Moderator and administrator controls remain separate privileged actions under D-24.

A private-board heart is toggled per Participant. On the first click, the light heart turns red and the displayed heart count increases by one. On the next click, the red heart returns to its light state and the count decreases by one. A private-board heart does not add the sticky note to the Wall of Love.

The Owner starts and closes a dot-voting round and chooses an allowance of **1**, **3**, **5** or **10** dots per Participant; **3** is selected by default. Each Participant can place at most one dot on any one sticky note. A vote can be withdrawn while the round remains active. Results remain hidden until the Owner closes the round.

There is no dot-voting reset rule, reset action or reopening. After closure, every sticky note that received at least one vote shows a voting-round icon with its vote count. The board also identifies the latest round and its closing date. Starting a new round immediately and permanently makes the previous round and its results unavailable; the product shows no replacement warning and keeps no accessible voting-round history.

While a round is active, the interface displays this notice above the sticky notes, with the numbers reflecting the Participant’s current usage and the Owner-selected allowance:

> Voting is open — you have used 0 of 3 votes. Votes stay hidden until the round is closed.

After closure, the interface displays the latest results with this notice above the sticky notes, using the round’s actual closing date:

> Showing the results of the last voting round (closed 2026/07/20).

A user viewing a Public sticky note has two sharing actions:

- **Copy link** places the sticky note’s direct link on the clipboard for use in any external channel.
- **Save as image** generates an image that can be stored locally and used independently, including on social media.

Neither sharing action creates another product object, moves the sticky note to a board or changes ownership. Increase the share count by one after each successfully completed **Copy link** or **Save as image** action. Repeat actions count again; the value represents completed product share actions, not unique people or confirmed external distribution.

### Real-time collaboration and saving

Real-time collaboration is an important implementation requirement for the existing private-board model, not a separate candidate feature. It is reported as probably not implemented today and must not be presented as current until V-04 passes.

The intended behaviour is:

- accepted creation, editing, deletion and movement of private-board sticky notes, plus comments, hearts, votes and voting-round state changes, synchronise to other active Participants without a page refresh;
- editable sticky-note text autosaves and exposes a visible saving, saved or failed state;
- a connection or server failure preserves unsaved local text and offers a safe retry path;
- when the server version of editable text has changed, the product preserves the local version and shows a conflict instead of silently applying last-write-wins;
- hearts, votes and position changes use the server-accepted state as authoritative and correct any optimistic local display when necessary.

The exact retry mechanism, conflict-resolution interface and status copy remain implementation details. Constant presence indicators are not required; protecting content matters more than showing continuous activity.

> **[VERIFY V-04] Requirement approved on 21 July 2026; implementation unverified** — Test each behaviour above across two browsers or sessions, connection loss, failed requests, simultaneous author/moderator editing and permission loss. Until those tests pass, remove or qualify claims that changes are visible in real time.

### Tag and due date

A tag groups related sticky notes within one private board; one sticky note can have multiple tags. Tags are board-scoped and automatically converted to lower case, so differently capitalised forms resolve to the same tag on that board. The Owner and every current Participant may create, rename and delete tags under their ordinary board rights. Tags cannot be merged. Deleting a tag removes that label from every sticky note that uses it without deleting any sticky note.

A private-board sticky note may have one optional due date. After it passes, the sticky note shows a red clock icon together with the expired date. Due dates cannot be filtered and remain visual only: they send no reminder email or other notification. A due date does not make the sticky note a task, create an assignment or determine the lifetime of the sticky note. Do not introduce separate deadline, reminder, scheduled and event dates until evidence shows that users need the distinction.

Tags and due dates belong only to sticky notes on private boards. A board itself, a worldwide-wall Draft, a Public sticky note and an Instant Photo cannot have them.

> **[QUESTION Q-04] Resolved on 22 July 2026; implementation verification required** — Verify board-scoped lower-case tag deduplication, ordinary Owner and Participant management, absence of tag merging, label-only deletion, sticky-note-only due dates, the expired-date treatment and the absence of due-date filtering and notifications.

## Parked concepts, not current objects or roadmap items

The source notes describe possibilities that are not established current behaviour. They remain outside the product model and are not under consideration for the current roadmap:

- **Product search:** text-based discovery across public, personal or board content. This does not currently exist and is not planned.
- **In-product activity:** a screen or inbox of relevant changes. This remains parked; the daily email digest defined by D-08 is part of the current notification model, not an in-product activity feature.
- **Pin:** a board-level way to keep shared content prominent.
- **Priority:** a signal that something needs attention; it is not automatically the same as favourite or pin.
- **Image content:** one uploaded image of no more than 5 MB inside a private-board sticky note, or the image inside a worldwide-wall Instant Photo. It inherits the parent object’s access and lifecycle.
- **Bulk or structured product export:** a printable board, Markdown or structured export of product content. This does not exist and is not planned. An individual sticky note can be saved as an image.

> **[DECISION D-04] Resolved for the current roadmap on 20 July 2026; image-content boundary clarified by Q-01 on 22 July 2026** — Search, an in-product activity screen, pins, priority, general attachments and bulk, board-level or structured export are parked. Q-01’s single supported image is content inside the defined sticky-note or Instant Photo object, not a general attachment system. URLs, link previews and other file types remain absent. Saving one sticky note as an image already exists under D-11, and favourite behaviour already exists through public hearts and the Wall of Love under D-10. The D-08 daily email digest is part of the current notification model, not a separate future feature. Archiving a complete private board is the only future feature currently under consideration.

> **[DECISION D-11] Resolved on 20 July 2026** — A user can save one eligible sticky note as an image; **Save as image** is not available while a worldwide-wall sticky note is a Draft. There is no bulk, board-level or structured product export and none is planned. A person may still request access to or portability of their personal data through the privacy process by email. That legal/privacy process is not a product export feature and must not be presented as one.

### Wall of Love

Every user has a private **Wall of Love** containing the Public sticky notes to which that user has given an active heart. In this context, a heart acts as both appreciation and a favourite. Only the user can view their Wall of Love. Private-board hearts never add content to it.

Unhearting removes the relationship, removes the sticky note from that user’s Wall of Love and subtracts one from the public heart count. Returning the sticky note to Draft, deleting it or removing it through moderation removes every public heart/favourite relationship. Republishing after Draft does not restore old favourites.

> **[DECISION D-10] Resolved on 20 July 2026; removal lifecycle resolved on 21 July 2026** — Favourite is an existing public-heart behaviour and the Wall of Love is visible only to its user. Pin and priority do not exist and are not planned. Showing the Wall of Love on a future profile is parked, not planned. Use the removal and reset rules above and verify their implementation under V-10.

> **[DECISION D-09] Resolved on 20 July 2026** — Product search is unavailable and not planned. Private boards can filter sticky notes by tags. The worldwide wall can filter Public sticky notes by country. These scoped filters must not be described as search or as public-board filtering.

### Email notifications

The current notification model uses email only. A private-board invitation, a later revocation of Participant access and an explicit mention each create an immediate email. A mention may name one or more current Participants on that board; send each mentioned person their own notification without treating the mention as an assignment. Declining an invitation does not email the Owner; the Owner sees **Declined** in invitation management. A scheduled daily job sends at most one activity digest to a recipient and only when at least one private board they can still access has changed since the previous digest. The digest is the routine notification mechanism; there is no in-product activity inbox and no immediate email for individual comments, hearts, dot votes or routine edits unless the recipient is explicitly mentioned.

> **[DECISION D-08] Resolved on 21 July 2026; mention email added under Q-03 on 22 July 2026** — Invitations expire after 14 days. Declining grants no access, is shown to the Owner as **Declined** and sends no separate Owner email. Access revocation takes effect immediately and sends the former Participant an immediate email. Explicit mentions send immediate email to each named current Participant. A scheduled job sends at most one conditional activity digest per day. Verify mention entry points, duplicate handling, access-at-send filtering, scheduling, aggregation, delivery failures and applicable email-preference and unsubscribe or transactional-email treatment before documenting operational details.

### Mention, not assignment

A sticky note has an author but no assignee, responsible person or assignment lifecycle. Private-board content may mention one or more people who currently participate on that board. A mention is an attention signal and immediate email trigger only. It never changes the mentioned person’s board access, authorship, edit or deletion rights, due date, ownership or responsibility. Public sticky notes and Instant Photos have no mention or assignment feature.

> **[QUESTION Q-03] Resolved on 22 July 2026; implementation verification required** — Do not build assignment, assignee filtering, acceptance, reassignment or completion responsibility. Verify one- and multi-person mentions, current-Participant selection, permission loss, duplicates, email delivery and the relationship with the daily digest.

### Plan and entitlement

A plan determines usage limits and access to paid capabilities. Current public plan names are Free, Premium and Chosen Few.

| Capability | Free | Premium | Chosen Few |
| --- | --- | --- | --- |
| Sticky notes per day | 2 | 12 | Unlimited |
| Active, editable owned private boards | 1 | 5 | Unlimited |
| Send private-board invitations | No | Yes | Yes |
| Receive invitations and participate | Yes | Yes | Yes |
| Private-board comments, hearts and dot voting | Yes | Yes | Yes |
| Private-board sticky-note tags and due dates | Yes | Yes | Yes |

Board limits count active, editable boards the user owns, not archived owned boards or boards they join as a Participant. A Free user can therefore keep one owned board active and participate fully on invited boards, but cannot invite another person to their own board. Initiating board collaboration is a Premium or Chosen Few entitlement.

The primary paid-value story is private collaboration, expressed through this tier narrative:

- **Free is for capturing and joining.** A Free user can publish within the Free allowance, keep one owned private board active and participate fully on boards they are invited to.
- **Premium is for bringing people together around your own ideas.** Sending invitations and initiating collaboration on owned boards is the central upgrade value; greater publication and board volume and additional personalisation support it.
- **Chosen Few is for people who want no practical plan-level volume limits.** It removes the daily Public-publication and active-owned-board limits while retaining the same product, safety, content and technical boundaries.

Do not sell Premium primarily as paying to escape a deliberately frustrating Free limit. Do not suggest that Free users receive reduced participation rights after they join a board. Feature comparisons, paywalls and checkout must continue to state the exact D-13 and D-27 entitlements; positioning does not alter them.

> **[QUESTION Q-07] Resolved on 22 July 2026; content and commercial verification required** — Use private collaboration as the primary paid-value story and volume, organisation and personalisation as supporting reasons. Apply the tier narrative above across marketing, pricing, paywalls, checkout and onboarding without changing entitlements or overstating Chosen Few as exempt from non-plan limits.

The daily sticky-note allowance counts only successful **Draft → Public** transitions, including republication after a sticky note has returned to Draft. Creating or editing Drafts, creating or editing private-board sticky notes and editing an existing Public sticky note do not count. Failed publication attempts never count. When the limit is reached, block only publication and preserve all existing content and other available actions. Publication becomes available again at **00:00:01 UTC on the next day**; show the remaining wait or reset moment in the user’s local time.

The product should treat plan rules as entitlements attached to an account, not as separate user types. A downgrade is a deliberate choice to reduce functionality. Moving to Free leaves one owned board active and editable; moving to Premium leaves up to five; Chosen Few has no active-board limit. Before confirmation, the Owner selects which allowed number of owned boards remain active and sees the others listed for archival. The downgrade cannot complete until the selection fits the new allowance. The listed excess boards are then archived automatically with the Owner’s authorisation and remain owned, preserved and read-only under V-02. They do not count towards the active-board allowance. Restoration is blocked when it would exceed the current allowance; the Owner must first create capacity or upgrade. No content is deleted solely because a paid plan ends.

> **[DECISION D-13] Resolved on 22 July 2026** — The entitlement matrix and Owner-selected automatic archival of owned boards above a downgraded active-board allowance are approved. Daily Public publication limits reset at **00:00:01 UTC** and count only successful **Draft → Public** transitions, including republication; other creation and editing actions and failed attempts do not count. **[VERIFY V-05]** must compare all limits and entitlements with the application and checkout and confirm the dependency on V-02 archiving.

### Public identity

A Public sticky note does not display an author name, username, profile picture, biography, external link, profile link or contribution history. It displays:

- the date on which it was published;
- its country of origin;
- its current share count; and
- its current heart count.

The publication timestamp is stored in UTC and the date is displayed as **YYYY/MM/DD**, for example **2026/07/21**. The country is the user-selected account country copied to the sticky note at creation. It is a stable snapshot and does not change when the account country later changes; do not infer it from the IP address.

Returning a Public sticky note to Draft removes all public heart/favourite relationships and resets both counts to zero. Republishing sets a new publication timestamp and date, starts both counts at zero and does not restore old Wall of Love entries. The creation-country snapshot remains unchanged. Final sticky-note deletion or moderation removal deletes the relationships and counters with the sticky note.

If the author deletes their account, the Public sticky note remains after its internal account relationship is removed. A small strip of tape at the top marks this state, accompanied by the accessible explanation **This sticky note remains after its author deleted their account.** This status does not add an identity or profile route. The sticky note no longer has author controls and can be changed or removed only through authorised moderation.

The platform retains the relationship with the author’s account so the author can edit, return the sticky note to Draft or delete it and authorised moderation can act. This internal attribution is not public attribution. There is no current public profile or contribution-history route from a Public sticky note, and the Wall of Love remains visible only to its user.

> **[DECISION D-25] Resolved on 20 July 2026; account-deletion indicator and metadata lifecycle added on 21 July 2026; implementation verification required** — Keep Public sticky notes free of author profile fields and show the UTC-derived **YYYY/MM/DD** publication date, creation-country snapshot, completed-action share count and active-heart count. A retained Public sticky note from a deleted account additionally shows the tape treatment and accessible deleted-account explanation and keeps these metadata values, except for heart relationships removed with the account. Public profile visibility remains parked rather than planned. Verify the complete implementation under V-10.

## Relationships

- A person has one account and one profile.
- An account has one active plan at a time.
- A person authors sticky notes.
- A board has exactly one non-transferable owner and may have multiple participants.
- A board contains multiple sticky notes; each private-board sticky note belongs to exactly one board.
- A private-board sticky note may have multiple board-scoped tags and one optional due date; boards and Public content have neither.
- An invitation connects a person to a board as a participant.
- A mention connects one private-board contribution to one or more current board Participants for attention and an immediate notification email; it creates no assignment, ownership or permission.
- A public heart relates a signed-in person to a Public sticky note and places that note on the person’s Wall of Love while the relationship remains active.
- Private-board comments, hearts and dot votes relate invited participants to board sticky notes.

A sticky note cannot gain board membership through the worldwide wall: a Public sticky note is not copied, moved or referenced into a private board. A sticky note created inside a private board belongs to that board only and cannot simultaneously belong to another board.

## Lifecycles

### Sticky note

**Created → Active → Enriched → Connected**
**Any retained state → Deleted**

These are conceptual states, not necessarily visible status labels.

- **Created:** the thought has been captured.
- **Active:** the note is available in its chosen context.
- **Enriched:** context, media, tags, dates or discussion have been added.
- **Connected:** the note is related to other ideas or people.
- **Deleted:** after confirmation, it is removed permanently without Undo or a user-facing recovery period; protected technical backup copies expire within 30 days under D-21.

An individual sticky note has no dedicated **Completed** or **Archived** system status. Completion may describe the meaning or outcome of a note, but is not a product state. Archiving applies only to the proposed whole-board feature below.

For publication on the worldwide wall, the explicit status path is:

**Draft ⇄ Public**

Drafts are hidden from other ordinary users but remain accessible to authorised platform moderators and administrators. Public sticky notes are visible on the worldwide wall without automatic expiry and may be indexed or used by external AI services. Unpublishing returns a Public sticky note to Draft and removes it from the worldwide wall and current intentional discovery mechanisms; independent copies, saved images, screenshots, search results, caches, AI datasets, model training or other external uses may remain outside StickyNotes.club.

> **[DECISION D-05] Resolved on 20 July 2026** — Do not introduce **Completed** or **Archived** states for individual sticky notes. The only future archive feature under consideration applies to an entire private board, including all of its sticky notes, comments, hearts and dot votes.

### Board

**Created → Active → Shared**
**Any retained state → Deleted**

- A newly created board is private to its initial access set.
- It becomes shared when other people receive access.
- Completion may describe the team’s outcome, but is not a system status.
- After the warning and confirmation, deletion is immediately permanent without Undo or a user-facing recovery period. The board’s sticky notes, comments, hearts and dot votes are deleted; Participant access and pending invitations are removed without deleting participant accounts. V-09 verifies the implementation.

#### Proposed future extension: archive a private board

Archiving is not treated as a current capability. The sole future lifecycle feature under consideration is archiving an entire private board as one unit, including every sticky note, comment, heart and dot vote it contains. Only the Owner or an authorised platform moderator or administrator may archive, restore or permanently delete it.

An archived board is read-only for its Owner and Participants. Existing Participants retain viewing access, although the Owner can still revoke that access. Pending invitations are cancelled, no new invitations can be sent and cancelled invitations do not revive automatically after restoration. Sticky notes, comments, hearts and dot votes remain intact, but ordinary users cannot create, edit, delete, comment, heart or vote while the board is archived. Necessary moderator or administrator actions remain available under D-24.

Archived boards generate no routine activity or daily-digest notifications. They are retained indefinitely until an authorised restoration or permanent deletion. Restoration returns the preserved board and its remaining Participants to the active collaboration rules; permanent deletion remains immediate and irreversible under D-21.

> **[VERIFY V-02] Resolved on 20 July 2026** — Use the read-only, access, invitation, interaction, notification, restoration and indefinite-retention rules above if whole-board archiving is implemented. The current Help Centre must still remove archive instructions until the feature actually ships.

### Moderation case

**Reported → Triaged → Under review → Decided → Appealed or Closed**

A report targets a specific sticky note, comment or board and uses one of these reasons: spam or scam; threats, harassment or hate; privacy or exposed personal data; impersonation; illegal or dangerous content; sexual content or child safety; copyright through its separate route; or another reason with an explanation. Submission returns an immediate receipt and case reference. Internal urgency is **Emergency**, **High**, **Normal** or **Low**; these are operational targets rather than public response-time promises until performance is verified.

A human makes every final decision. Automation may prioritise reports, detect obvious spam or apply a temporary protective limit, but cannot permanently remove content or exclude an account without human review. Available outcomes are no action, warning, temporary visibility restriction, removal, temporary feature restriction, account suspension for 24 hours, 7 days or 30 days, and permanent exclusion. Severe cases may skip lighter measures. Moderators may hide, remove or restore content but do not ordinarily rewrite it; only a narrowly necessary, audited redaction may alter otherwise permitted content.

A restriction disables only named capabilities, such as publishing, interactions or invitations. A suspension blocks account use for its duration and pauses invitation acceptance and contribution without deleting the account, board relationship or existing contributions. Permanent exclusion revokes platform access and pending invitations but does not run the V-06 account-deletion cascade; existing contributions remain unless separately removed. Owner removal of a Participant remains a board-level access action. No separate user-to-user blocking feature is planned while the product has no direct messaging, following or visible Public-author profiles.

The affected author and, for board content, the Owner receive a clear statement of the action, scope, duration, policy or legal ground, relevant facts, any material use of automation and the appeal route. The reporter receives the outcome without another person’s private account information. A recorded safety or legal reason may delay a notification, which must then be reviewed periodically. Appeals are free and available for six months; a different human reviewer handles them where practicable, with a fourteen-day internal resolution target. An overturned decision restores content or access where possible and triggers corrected notifications.

Retain only the reported content, necessary context, report, decision, reviewer, timestamps, action and appeal. Delete ordinary case evidence six months after the final decision and serious or repeated-abuse evidence after twelve months. Retain it longer only under a documented legal hold. Every privileged view and action is audited. The DSA applicability, public policy wording, evidence periods and emergency reporting duties require legal verification before launch.

> **[DECISION D-24] Behaviour resolved on 22 July 2026; implementation and legal verification required** — Implement and test reporting, human review, proportional measures, notifications, appeals, evidence expiry, least-privilege access, audit logging, spam controls and emergency escalation before publishing current-capability claims.

### Account

**Registered → Email pending → Active → Restricted or suspended → Deleted**

Restriction and suspension are exceptional safety, legal or payment states. Account deletion:

- removes the active profile, credentials, preferences, Drafts, the private Wall of Love and every public or private heart relationship created by the account;
- ends future subscription renewal, while separately required billing records may follow a documented retention rule;
- permanently deletes every board the account owns, including its sticky notes, comments, hearts, dot votes, Participants and invitations;
- preserves the account’s sticky notes and comments on boards owned by somebody else under **Deleted user**;
- removes the account relationship from its dot votes while preserving only anonymous aggregate totals;
- preserves its Public sticky notes on the worldwide wall after irreversibly removing the internal account relationship;
- adds a small strip of tape at the top of each retained Public sticky note and exposes the accessible explanation **This sticky note remains after its author deleted their account.**;
- leaves those Public sticky notes without author controls and subject only to authorised moderation; and
- cannot recall independent copies, saved images, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred.

Protected technical backups may retain deleted data for no more than 30 days after deletion, without ordinary product access or a user-facing recovery path. The data must age out through the backup cycle by the end of that period. Any separately required billing, tax or legal records follow their applicable retention period, must contain as little product content as practicable and remain subject to legal verification. These rules must be aligned with the Privacy Policy, Terms, infrastructure and processors.

> **[VERIFY V-06] Account deletion — behaviour resolved on 21 July 2026; 30-day technical-backup period resolved on 22 July 2026; implementation and legal-record verification required** — Verify the warning and every effect above, including owned-board cascade, **Deleted user** contributions, Draft removal, retained and de-attributed Public sticky notes, tape and accessible state, heart and Wall of Love removal, anonymous dot-vote totals, subscription non-renewal, lack of product recovery and deletion from protected backups within 30 days. Verify any required billing, tax or legal-record periods before finalising the lifecycle and public policies.

### Subscription

**Free → Paid → Renewing → Cancelled → Free/restricted**

Cancellation stops future renewal. Paid capabilities normally remain available until the end of the paid period. Content above the next plan’s limits may become restricted or read-only rather than being deleted.

## Ownership and control rules

- Users retain ownership of the content they create or upload.
- Authors can edit their own public and board sticky notes using available controls.
- Board owners control invitations, participant access and the board itself, including deletion of any sticky note on an active board.
- Authors can delete their own board sticky notes and comments. Other Participants cannot edit or delete another author’s sticky note or comment. Board ownership never grants editing rights or separate deletion rights over another author’s comment; it grants the defined sticky-note deletion exception and its V-09 cascade.
- Authorised moderators and administrators can hide, remove or restore any board sticky note under D-24. They may alter its text only for a narrowly necessary, audited redaction.
- Authorised platform moderators and administrators can view all boards and sticky notes, including Drafts and notes on private boards, only when moderation, support, security or legal work genuinely requires it. Access is limited to the minimum necessary and every privileged view and action is recorded. Moderators and administrators have the same content-moderation capabilities; administrators may additionally hold separate system and account-management capabilities. D-24 governs reports, measures, notifications, appeals and evidence retention.
- The service may restrict content or access for safety, legal, security or payment reasons as described in the Terms.
- Deletion from the active product cannot remove independent copies or caches held by third parties.

## Product invariants

These statements should remain true across interfaces:

1. A user can understand whether an action is public or access-controlled before completing it.
2. Capturing a first idea does not require configuring an organisational system.
3. A board’s owner can see and manage who has access.
4. Destructive actions clearly state their effect and permanence.
5. A paid plan ending does not by itself delete user content.
6. The same objects and actions use the same names across product, billing, policies and Help Centre.
7. The canonical Help Centre is automatically published by GitHub Pages from `/docs` on `main` to `https://docs.stickynotes.club`; Fly.io and Cloudflare are not alternative documentation deployment paths.

## Known uncertainties

The following items are referenced inconsistently or without enough implementation detail and must be verified before this model is treated as final:

- privileged comment-moderation controls and implementation of the resolved V-09 confirmation copy and deletion cascades; ordinary comments cannot be edited, their authors can delete them, and comments are covered by the daily board digest rather than immediate email;
- implementation and launch verification for the proposed whole-board archive feature; its intended restore, access, interaction, notification and retention rules are resolved under V-02;
- the warning and implementation of the resolved V-06 account-deletion lifecycle, including expiry from protected backups within 30 days, plus legal verification of any required billing, tax or legal-record periods;
- which organisational features belong to each plan.
- the removal lifecycle of the private Wall of Love; pin, priority and bulk, board-level or structured export are confirmed absent and not planned;
- the practical limits, formatting and display locations of board descriptions; central-question fields, multiple owners and public boards are confirmed absent;
- the exact interface copy used for the resolved post-publish success message and actions.

These questions are tracked in the Product Design Notes.
