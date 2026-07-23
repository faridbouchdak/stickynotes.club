# Product Constitution

> Status: v1.2
> Role: enduring product principles
> Review when: the product promise, audience or boundaries materially change

## Purpose

This document defines the principles that should remain true as StickyNotes.club grows. It is the highest-level product document: the Product Model, Playbook, interface and Help Centre should all be consistent with it.

The Constitution should change rarely. New feature ideas belong in the Design Notes until they have been tested and accepted.

## Core purpose

**Help ideas grow.**

StickyNotes.club helps people capture a thought before it disappears, share it when it can inspire others and give it a private place to develop when it needs attention or collaboration.

Not every idea needs to become a project. A thought may remain personal as a draft or on an unshared private board, be published briefly, grow into a plan or be deliberately abandoned. All of these are valid outcomes.

## Product promise

**A place where ideas can grow together.**

This is the canonical tagline. In ordinary prose, the complete sentence “StickyNotes.club is a place where ideas can grow together” may be used when grammatically necessary.

The product should make the first action feel effortless while leaving room for an idea to become clearer, richer and more useful over time.

## Who we serve

StickyNotes.club is for people who want to:

- quickly capture and share a thought;
- discover ideas from other people;
- brainstorm alone or with others;
- organise a growing collection of ideas;
- turn loose thoughts into a shared outcome.

It should work for an individual without feeling like team software and for a small group without requiring project-management training.

## Principles

### 1. Keep It Super Simple

The fastest path to a useful result should remain obvious.

- A user should be able to capture an idea before learning the system.
- Defaults should be safe and useful.
- Advanced controls should appear when they become relevant.
- Every new concept must earn the attention it asks from the user.

Simple does not mean limited. It means complexity is introduced deliberately and progressively.

Structure should follow the thought, not precede it. Creating a note should not require choosing a board, tag, deadline, participant or workflow.

### 2. Users think in goals, not features

Product language and navigation should describe what people want to achieve: share an idea, work together, organise a board or manage access.

We explain outcomes before controls and avoid exposing implementation details unless they help the user make a decision.

### 3. Public inspires. Private builds.

Public sticky notes help people share, discover and start conversations. Private boards help people collect, organise, collaborate, decide and act.

Publishing is deliberately open beyond StickyNotes.club. Public sticky notes and Instant Photos may be crawled, indexed, cached and shown by external search engines, and their public text and images may be processed or used by external artificial-intelligence services, including to train, improve, evaluate or operate AI systems. The interface must disclose this before publication. Drafts and private-board content remain excluded from this permission and from intentional public discovery.

A Public sticky note is presented without the author’s name, username, profile picture, biography or profile link. Its public context consists of the date it was published, its country of origin and its current share and heart counts. While the account exists, the service retains the private relationship needed for author controls and moderation. After account deletion, that relationship is removed and a small strip of tape at the top marks the retained Public sticky note, with an equivalent accessible explanation.

Store publication time in UTC and display its date consistently as **YYYY/MM/DD**. A sticky note copies the user-selected account country at creation and keeps that snapshot. Count each successfully completed **Copy link** and **Save as image** action, including repeats, as a share action rather than a unique person. Unhearting subtracts one. Returning a Public sticky note to Draft clears all public heart/favourite relationships and resets heart and share counts; republishing starts a new public lifecycle with a new publication date and zero counts. Account deletion is the exception: a retained de-attributed Public sticky note keeps its date, country and aggregate counts, apart from heart relationships removed with the deleted account.

Daily Public sticky-note allowances count only successful **Draft → Public** transitions, including republication after returning a sticky note to Draft. Creating or editing Drafts, creating or editing private-board sticky notes and editing an existing Public sticky note do not consume this allowance. Failed publication attempts never count. The allowance resets at **00:00:01 UTC** each day; user-facing copy should translate the remaining wait into the user’s local time.

These are not separate products. They are two contexts in the same journey of an idea. The boundary between them must always be clear so users understand who can see their content. This shared journey does not imply a product control for copying, moving or linking a Public sticky note to a private board; no such transition is planned. Within the private context, each sticky note belongs to exactly one board and never has simultaneous membership of multiple boards.

On the worldwide wall, a user publishes either a text sticky note or an **Instant Photo**: an image presented in a Polaroid-like frame with a caption. Both Public forms use the same Draft/Public lifecycle, publication allowance, metadata, hearts, sharing, moderation and deletion rules. On a private board, the only content object is a sticky note, which may contain one optional image; an Instant Photo is not a separate board object. Images inherit the object’s audience, ownership, moderation and deletion lifecycle, and each uploaded image is limited to **5 MB**. No other file type is accepted. Sticky-note text and Instant Photo captions reject URLs; the product provides no embedded links, link previews or URL attachments in these fields. The present generic alternative text **Instant Photo** is insufficient and must not be treated as an accessible description; alternative-text behaviour requires design and implementation before accessibility claims are final.

### 4. Trust users by default

Users own the content they create or share inside private boards and should remain in control of it. Publishing to the worldwide wall is a deliberate exception: by publishing a sticky note or Instant Photo, the user explicitly relinquishes ownership of that Public content. The worldwide wall shows no name, profile or public contribution history; its only origin information is the stored country snapshot. Publication date, share count and heart count may also appear. While the account exists, a private internal relationship remains only for author controls and authorised moderation. It is not public attribution and does not preserve ownership after publication.

- Privacy and access must be understandable before sharing.
- The ownership consequence of publishing must be clear before **Publish**.
- Editing, deletion and account controls should be easy to find.
- Deleting a sticky note, comment or private board is immediately permanent after confirmation; the warning must name what disappears and state that it cannot be undone. Sticky-note deletion also removes its comments, hearts and dot votes. Comment deletion removes only that comment. Board deletion removes all board content and interactions and revokes Participant access and pending invitations without deleting participant accounts.
- Public sticky notes remain available without an automatic expiry until their author returns them to Draft or deletes them, subject to proportionate moderation.
- Public sticky notes and Instant Photos may be indexed by search engines and used by external AI services; explain this before publication and never imply that later unpublishing can recall data already copied, cached, indexed or incorporated into an external system.
- Product limits and prices should be stated plainly.
- Moderation should be proportionate, explainable and open to correction through a free appeal.
- We collect and retain only what is needed to operate the service.

Trust also requires honest communication about limits: “private” means access-controlled, not impossible for an authorised participant to copy. Drafts and private boards are hidden from other ordinary users, but authorised platform moderators and administrators retain privileged access when moderation, support, security or legal work genuinely requires it. This access must be disclosed, limited to the minimum necessary and recorded in an audit trail. Moderators may hide, remove or restore content; they must not silently rewrite an author’s words. A narrowly necessary redaction, such as removing exposed personal data while preserving otherwise permitted content, is the only content-editing exception and must be attributed in the audit trail.

Reporting must be accessible from the relevant sticky note, comment or board and return an immediate receipt and case reference. A human makes final moderation decisions. Measures range from no action and a warning through visibility or feature restrictions to temporary suspension or permanent exclusion, according to severity and repetition. Existing contributions do not disappear merely because an account is restricted, suspended or excluded; content removal is a separate decision. The affected author and, for board content, the Owner receive a clear reason, scope, duration and appeal route unless a recorded safety or legal reason temporarily delays notification. Ordinary cases retain only necessary evidence for six months after the final decision; serious or repeated abuse may be retained for twelve months, with longer retention only under a documented legal hold. Appeals remain available without charge for six months and should be reviewed by a different person where practicable.

### 5. Calm software beats noisy software

StickyNotes.club should help people think, not compete for their attention.

- Notifications should be useful, controllable and restrained.
- Empty space and clear hierarchy are productive.
- Urgency should be reserved for genuinely urgent information.
- Engagement metrics must not become the product’s purpose.

### 6. Documentation is part of the product

If behaviour cannot be explained clearly, it is probably not clear enough in the product.

Documentation is written alongside product decisions, reflects implemented behaviour and forms part of acceptance testing. Help content should enable a user to succeed without needing support.

The canonical Help Centre is published from `/docs` on `main` in `faridbouchdak/stickynotes.club` through GitHub Pages at `https://docs.stickynotes.club`. Publishing is automatic, build failures are visible in GitHub Actions and HTTPS is required. Fly.io does not deploy the Help Centre; Cloudflare’s domain and network role is separate from deployment.

### 7. Consistency beats cleverness

Familiar patterns, stable language and predictable behaviour reduce the effort needed to use the product.

Use the same term for the same concept everywhere. Reuse established interaction patterns unless a new pattern solves a demonstrated problem substantially better.

### 8. Let structure emerge

Users should not need to know what an idea will become before they capture it.

- Notes may start incomplete or uncertain.
- Relationships, boards and collaboration appear when useful.
- Completion and deliberate abandonment are both valid outcomes.
- The product should support small steps instead of imposing a complete process.

### 9. Sticky notes carry ideas. Boards give context.

A sticky note is the smallest meaningful product object: a self-contained thought that can be found, connected, shared, retained or removed according to its context. After the object has been established clearly, “note” may be used as a natural shorthand.

A board brings related notes together around a topic, question, plan or collaboration. It should create context and visibility, not bureaucracy. New functionality should strengthen the movement of ideas rather than overshadow notes with system administration.

Every board has one non-transferable Owner. Keeping that person involved preserves continuity while the idea develops. Deleting the Owner’s account also permanently deletes every board they own, so this consequence must be explicit before account deletion.

Private boards support personal Participant access and controlled link access. Participant access starts with an email invitation whose recipient must sign in or create an account. An invitation expires after 14 days. Declining it grants no access and leaves a **Declined** status visible to the Owner without sending the Owner a separate email. If the Owner later revokes Participant access, the former Participant receives an immediate email. An Owner whose plan includes initiating collaboration may also create a **View link** that shows a read-only version of the board to anyone with the link, without requiring an account, or a **Post link** that additionally lets a signed-in StickyNotes.club user on any plan add sticky notes. Link access does not make somebody a Participant or grant comments, hearts, dot votes or board-management rights. Link creation is paid and Owner-only; an Owner must remain able to revoke an existing link at any time, including after a downgrade, to disable access through it.

Routine private-board activity is communicated calmly through at most one daily email digest and only when an accessible board has changed. Invitations, access revocation and an explicit mention are the immediate ordinary collaboration emails; individual edits, comments, hearts and dot votes do not otherwise trigger separate messages.

The board overview gives calm orientation through **Last modified on YYYY/MM/DD**. The date changes only after an accepted content, organisation, collaboration, access or board-setting change; merely opening or viewing a board does not count. Do not label a board inactive, warn or email because time has passed, and never archive, restrict or delete a board automatically for inactivity.

Sticky notes cannot be assigned to an Owner or Participant and never acquire an assignee or responsible-person field. A private-board author may instead mention one or more people who are current Participants on that board. Each mentioned Participant receives a notification email. A mention draws attention only: it does not change authorship, ownership, access, editing or deletion rights, due dates or responsibility. Exact mention entry locations, duplicate handling, access checks and email operation require verification.

Creating a private board requires a **Name**, allows an optional **Description** and presents a template choice with **Blank** selected by default. Visibility, a central question and a desired result are not separate creation fields; the board is private by definition.

Private-board comments can be posted and deleted by their author but cannot be edited. A private-board heart is a personal toggle: the first click changes the light heart to red and adds one to the displayed count; the next click changes it back to light and subtracts one. The Owner starts and closes each dot-voting round and selects an allowance of 1, 3, 5 or 10 dots per Participant; the default is 3. A Participant can place no more than one dot on a sticky note, can withdraw a vote while the round is active and sees the results only after the Owner closes the round. Closed-round results appear directly on every sticky note that received a vote, using a voting-round icon and count. There is no voting-round reset, reopening or replacement warning. Only the latest closed round remains available; starting a new round permanently makes the previous round and its results unavailable. Notices above the sticky notes explain the active or closed state.

Private-board collaboration must eventually synchronise accepted changes without requiring a page refresh and autosave editable sticky-note text. The interface must make saving, success and failure visible, preserve unsaved text through connection or server failures and provide a safe retry path. A simultaneous text change must never silently overwrite local work: preserve the local version and show a conflict. Hearts, votes and position changes use the server’s accepted state as authoritative. Until this behaviour is implemented and verified, do not promise real-time collaboration.

StickyNotes.club keeps no edit or version history for sticky notes or Instant Photos. An accepted edit to text, caption, colour, tags or a due date replaces the current value; no earlier value remains available to view or restore. Tags and due dates apply only where those organisational fields are supported and never create a Public expiry. Autosave, temporary preservation of unsaved local text and conflict handling protect the current edit but do not create stored versions. Moderation audit records and report evidence are separate and must not become a user-facing content history.

A Public sticky note can be shared by copying its link to the clipboard or by saving a generated image for independent use, including on social media. Neither action creates a private-board copy or changes the sticky note’s ownership.

If whole-board archiving is introduced, it preserves the complete private board indefinitely as a read-only record until restoration or permanent deletion. Existing Participants retain viewing access, while new invitations, contributions and activity digests stop. Only the Owner or an authorised platform moderator or administrator may archive, restore or permanently delete it. The Owner may still revoke existing Participant access, and necessary privileged moderation remains available under the platform safeguards.

A subscription downgrade is a deliberate acceptance of reduced functionality, never permission to delete content. Free permits one active, editable private board owned by the user; Premium permits five; Chosen Few permits unlimited active owned boards. Before confirming a downgrade that exceeds the new allowance, the Owner chooses which permitted number of boards remain active and sees every other owned board identified for archival. The downgrade cannot complete until that selection fits the new allowance. Excess owned boards are then archived with the Owner’s authorisation and remain owned, preserved and read-only under the archive rules. An archived board can be restored only when doing so stays within the current active-board allowance or after an upgrade.

A sticky note contributed to somebody else’s board remains part of that board when its author leaves, loses access or deletes their account. After account deletion, the author is shown as **Deleted user**. The author may permanently delete the sticky note before deleting their account. On an active board, the Owner may permanently delete any sticky note to manage the board but may never edit another author’s text or separately delete another author’s comment. Owner deletion uses the full V-09 warning and cascade, is technically logged and appears in the affected author’s daily digest while they still have access. Authorised moderator and administrator removal remains subject to the stricter D-24 safeguards.

Account deletion removes the profile, credentials, preferences, Drafts, personal heart relationships and private Wall of Love, and ends future subscription renewal. Every owned board is permanently deleted with its content and access. Sticky notes and comments contributed to somebody else’s board remain under **Deleted user**. Public sticky notes remain on the worldwide wall after their account relationship is removed; the tape treatment and accessible text **This sticky note remains after its author deleted their account.** communicate that state without adding identity. These retained Public sticky notes no longer have author controls, remain indexable and available for external AI use, and remain subject to authorised moderation. Dot-vote totals may remain only without a relationship to the deleted account. Deleted data may persist in protected technical backups for no more than 30 days, without ordinary product access or a user-facing recovery path, before ageing out through the backup cycle. Separately required billing or administrative records may be retained for the applicable legal period, contain as little product content as practicable and require legal verification before the Privacy Policy and Terms are finalised. Independent copies, saved images, screenshots, search results, caches, AI datasets, model training and other external uses cannot be recalled.

Boards use understandable grid or column structures rather than a freeform infinite canvas. Blank and Brainstorm use the same grid structure and can later change to columns; they differ only in their default background and product framing. Retro, Kanban and Week planner start with columns. People remain free to reorder sticky notes and adapt the layout where supported. Decorative backgrounds must not carry meaning or reduce readability.

Sticky-note colours support expression and personalisation, not product-defined status, priority or category. Whenever meaning matters, communicate it with visible text, a tag or a label and never through colour alone.

Tags and due dates organise only sticky notes on private boards, never a board itself or Public content. They remain lightweight, optional aids: tags group notes within one board and a due date provides a visual attention signal without creating an assignment, reminder or notification.

## Product boundaries

StickyNotes.club is not intended to become:

- full project-management software;
- a long-form document editor;
- a social network optimised for reach or engagement;
- an enterprise knowledge base;
- an unlimited-canvas digital whiteboard;
- a replacement for chat or video meetings.

It sits between personal thinking and lightweight collaboration. It may connect to adjacent workflows, but should not absorb all of them.

## Decision hierarchy

When principles appear to compete, use this order:

1. Protect people, their privacy and their content.
2. Preserve the core purpose and the public/private boundary.
3. Help the user complete their goal with minimal effort.
4. Keep behaviour consistent and explainable.
5. Optimise growth, conversion or operational efficiency.

Commercial value matters, but it must not weaken safety, clarity or user control.

Private collaboration is the primary paid-value story. Free lets a person capture ideas, keep one owned private board active and participate fully when invited. Premium primarily enables that person to bring others into their own boards. Chosen Few removes plan-level publication and active-board limits for people who need more room. Higher volume and additional personalisation support this story; they must not replace it with a feature-count or artificial-scarcity message.

KISS applies beyond the interface. Product scope, navigation, language, documentation, onboarding, technical architecture and marketing should all carry only the complexity their purpose requires.

## Decision checklist

Before approving a meaningful product change, ask:

- Which user problem does this solve?
- How does it help an idea grow?
- Does it belong in the public or private context, or bridge the two?
- Is visibility and ownership clear?
- What is the simplest useful version?
- Can a first-time user understand it without instruction?
- Can it be explained in a short Help Centre section?
- Does it introduce pressure, noise or unnecessary configuration?
- Does it reuse established language and patterns?
- What evidence would tell us whether it worked?

If the answers are unclear, the idea remains a hypothesis rather than a product decision.

## Signs that we are drifting

Reconsider a change when:

- users must configure the system before capturing an idea;
- the difference between public and private becomes ambiguous;
- more notifications are used to manufacture engagement;
- pricing or limits are hard to understand;
- several names exist for the same concept;
- Help Centre copy relies on “may”, “depending on” or vague promises;
- a feature primarily imitates a larger product category rather than solving a StickyNotes.club problem.

## Governance

- The Constitution is the source for enduring principles.
- The Product Model defines current concepts, states and boundaries.
- The Playbook translates both into repeatable working rules.
- Design Notes hold evidence, open questions, proposals and decisions.
- The Help Centre describes only behaviour users can rely on today.

Material changes to this document should include a version change and a short rationale in the Design Notes.

## Resolved decision

> **[DECISION D-01] Resolved on 20 July 2026** — Use **A place where ideas can grow together.** as the official product promise and tagline. Use the full sentence with “StickyNotes.club is” only when normal prose requires it.
