# Product Playbook

> Status: v1.2
> Role: practical rules for product, design, writing and release decisions

## Purpose

The Playbook translates the Product Constitution and Product Model into repeatable working practices. It should make small decisions faster and expose important uncertainty early.

## Review markers

Unresolved items use four markers throughout this design set:

- **ERROR** — a demonstrable mistake that can normally be corrected without a product decision;
- **CONFLICT** — two sources currently make incompatible claims;
- **DECISION** — an explicit product or editorial choice is needed;
- **VERIFY** — the documented claim must be checked against the product or operation.

Every marker has a stable ID and a checkbox in the Product Design Notes review register. When resolved, record the decision or evidence there first, update every affected document and then remove the inline marker.

## Working principles

- Start with a user problem, not a feature name.
- Separate observed facts from assumptions and proposals.
- Design the smallest complete outcome, not the smallest collection of controls.
- Make public/private visibility explicit.
- Use documentation as both specification and acceptance test.
- Record why a decision was made, especially when it is difficult to reverse.
- Let people capture first and add structure later.
- Treat a sticky note as the smallest meaningful unit and a board as context, not administration.

## Product workflow

### 1. Frame the problem

Write a short problem statement:

> [Person or situation] needs to [goal], because [reason]. Today, [evidence of the problem].

Also record:

- whose problem it is;
- where it occurs in the idea journey;
- whether it belongs to Public, Private or the transition between them;
- the evidence available;
- what remains assumed.

Do not use a proposed solution as the problem statement.

### 2. Define the outcome

Describe what the user should be able to accomplish and what a successful experience feels like.

Define one primary outcome and, where useful, guardrails such as:

- no increase in accidental public sharing;
- no extra setup before the first note;
- no content loss after a plan change;
- no new notification by default without a clear user benefit.

### 3. Map the behaviour

Before polishing screens, describe:

- entry point;
- happy path;
- empty, loading and error states;
- permissions and visibility;
- cancellation and undo;
- what happens to existing content;
- mobile and keyboard considerations;
- policy, billing or moderation implications.

Also state explicit non-goals for the first version. This prevents a small feature from silently becoming a new subsystem.

For destructive actions, specify confirmation, consequences and recovery before implementation.

### 4. Draft the Help Centre change

Write or update the relevant help content as if the behaviour already worked. If the workflow is difficult to explain simply, revise the behaviour.

The draft is a specification, not a promise. Do not publish it until the product has been verified.

### 5. Build and verify

Test the complete documented workflow, including access boundaries and failure states. Verify copy against the actual interface rather than expected implementation.

### 6. Release together

A product change and its necessary documentation should ship together. Update related policy or pricing pages when the change affects data, access, payment or user rights.

### 7. Learn and consolidate

After release:

- compare the result with the intended outcome;
- capture discoveries and support questions;
- record accepted or rejected decisions;
- promote repeated patterns into this Playbook or Product Model;
- remove documentation for behaviour that no longer exists.

## Evidence levels

Use these labels in Design Notes and proposals:

- **Current:** verified in the live or test product.
- **Documented:** described publicly but not yet re-verified.
- **Observed:** supported by user behaviour, feedback or support evidence.
- **Proposed:** a designed direction that has not shipped.
- **Open:** a question without an approved answer.

Public Help Centre pages may describe only **Current** behaviour. A documented claim that cannot be verified becomes a reconciliation task.

## Scope ladder

For each change, consider three levels:

1. **Essential:** the smallest version that solves the user problem safely.
2. **Useful next:** improvements justified by evidence after the essential version works.
3. **Later:** adjacent ideas kept out of the current release.

Avoid shipping a partial flow that creates a dead end. “Small” still includes the required empty, error, permission and cancellation states.

## UX rules

### Interaction

- Prefer recognition over recall.
- Give one screen or component one dominant next action.
- Put advanced options behind a clear, reversible step.
- Preserve the user’s work when an operation fails.
- Keep primary actions stable in placement and naming.
- Use familiar controls before inventing custom gestures.

### Public and private

- Show the audience before publishing or sharing.
- Before publishing, state that Public sticky notes and Instant Photos may be indexed by external search engines and used by external AI services, including for training, improvement, evaluation or operation. Do not offer a separate search-indexing or AI-use toggle.
- Never change content visibility silently.
- Let an author unpublish a Public sticky note by returning it to Draft. Explain that this removes it from the worldwide wall and intentional public discovery surfaces but cannot recall independent copies, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred.
- Keep a Public sticky note published without an automatic or author-selected expiry until the author returns it to Draft or deletes it, or authorised moderation removes it.
- Present a Public sticky note without the author’s name, username, profile picture, biography, links or contribution history. Show its publication date, country of origin, share count and heart count. Internal account attribution remains available for author controls and moderation while the account exists. After account deletion, remove that relationship, retain the Public sticky note and add the tape and accessible deleted-account state defined by V-06.
- Keep private-board access account-based and invitation-only. Do not expose or promise private-board share links, anonymous viewing or accountless contribution; sharing a Public sticky note is a separate Public action.
- Make board ownership and permission changes visible to affected users.
- Ask for confirmation when an action widens access or is difficult to reverse.
- Explain that Drafts and private boards are hidden from other ordinary users but remain accessible to authorised platform moderators and administrators.
- Permit privileged content access only when moderation, support, security or legal work genuinely requires it. Apply least privilege and record every privileged view and action in an audit trail.
- Allow moderators to hide, remove or restore content. Do not let them silently rewrite an author’s words; permit only a narrowly necessary, audited redaction such as removing exposed personal data from otherwise permitted content.
- Inform the affected author, and the Owner where board content is involved, of the action, scope, duration, reason and appeal route. A recorded safety or legal reason may temporarily delay notification.
- Give moderators and administrators the same content-moderation capabilities. Treat any additional administrator powers for system or account management as separate from content moderation.

> **[DECISION D-20] Resolved on 20 July 2026** — Do not introduce expiry controls, countdowns or automatic unpublishing for Public sticky notes. Keep the publication lifetime predictable and controlled by deliberate action.

Keep public routes technically indexable and available to ordinary search and AI crawlers. Include eligible Public sticky notes and Instant Photos in public discovery mechanisms such as sitemaps and do not emit a `noindex` or product-level AI exclusion for them. Drafts, private-board content and removed Public content must never be exposed through those routes. After a Public object returns to Draft, is deleted or is removed through moderation, stop serving its content publicly and remove it from current discovery mechanisms; do not promise that third parties will erase prior copies or uses.

Publishing does not transfer ownership to StickyNotes.club. Instead, the user explicitly relinquishes ownership of the Public sticky note or Instant Photo. The Terms and Privacy Policy must transparently describe that consequence, public availability, crawler access, search indexing, caching and external AI use, and must define the necessary assurances and platform permissions. Require legal review before treating that wording as final, especially for images, personal data, third-party rights and use involving minors.

> **[QUESTION Q-05] Resolved on 22 July 2026; implementation, policy and legal verification required** — Test indexability, sitemap inclusion, crawler metadata and the Publish warning for both Public forms. Test removal from public routes and discovery mechanisms after Return to Draft, deletion and moderation. Confirm that de-attributed Public content retained after account deletion remains indexable. Align the Terms and Privacy Policy and avoid any promise that search or AI use can be recalled.

Store the Public publication timestamp in UTC and display the date as **YYYY/MM/DD**, for example **2026/07/21**. Copy the user-selected account country to the sticky note at creation and keep it as a stable snapshot; do not update it after an account-country change or derive it from the IP address.

> **[DECISION D-25] Resolved on 20 July 2026; metadata lifecycle added on 21 July 2026; implementation verification required** — Do not design a public author byline or profile route from a Public sticky note. Keep the Wall of Love private and public profile visibility parked. Use the approved date, country and counter rules and verify them under V-10.

### Safety reports and moderation

- Put **Report** on the relevant sticky note, comment or board. Offer **Spam or scam**, **Threats, harassment or hate**, **Privacy or personal data**, **Impersonation**, **Illegal or dangerous content**, **Sexual content or child safety**, **Copyright** through its separate route, and **Other** with an explanation.
- Confirm submission immediately with a case reference. Triage internally as **Emergency**, **High**, **Normal** or **Low**, but do not publish response-time promises until operational performance is verified.
- Require a human final decision. Automation may prioritise reports, identify obvious spam or apply a temporary protective limit, but cannot permanently remove content or exclude an account without human review.
- Choose proportionately among no action, warning, temporary visibility restriction, removal, temporary feature restriction, suspension for 24 hours, 7 days or 30 days, and permanent exclusion. Severe cases may skip lighter measures.
- A restriction disables only named capabilities. A suspension blocks account use and pauses invitations and contributions for its duration without deleting the account, board relationships or existing contributions. Permanent exclusion revokes platform access and pending invitations without running account deletion; existing contributions remain unless separately removed.
- Keep Owner removal of a Participant as the board-level access control. Do not introduce user-to-user blocking while the product has no direct messaging, following or visible Public-author profiles.
- Notify the affected author and, for board content, the Owner with the action, scope, duration, policy or legal ground, relevant facts, material automation and appeal route. Tell the reporter the outcome without disclosing another person’s private account information. Record and periodically review any safety or legal delay.
- Keep appeals free and available for six months. Use a different human reviewer where practicable and target a decision within fourteen days. Restore content or access where possible and send corrected notifications when an appeal succeeds.
- Retain only the reported content, necessary context, report, decision, reviewer, timestamps, action and appeal. Delete ordinary evidence six months after the final decision and serious or repeated-abuse evidence after twelve months; retain it longer only under a documented legal hold.
- Use invitation and publication rate limits, duplicate detection, account-verification friction and human review for spam. Rate limits may protect the service but must not automatically become a permanent sanction.
- Escalate imminent danger, child-safety material, credible threats and binding legal requests through a documented emergency path. Legally verify DSA applicability, evidence periods and reporting duties before launch.

> **[DECISION D-24] Behaviour resolved on 22 July 2026; implementation and legal verification required** — Verify reporting, triage, human decisions, measures, notifications, appeals, evidence expiry, least privilege, audit logging, spam controls and emergency escalation before documenting them as current behaviour.

### Destructive actions

- Use precise verbs: **Delete board**, not **Continue**.
- Explain what will be removed and who will be affected.
- Distinguish archive, remove access and permanent deletion.
- Do not promise Undo, trash, a recovery period or restoration for deleted sticky notes, comments or boards; deletion is immediately permanent after confirmation.
- Never use colour alone to communicate risk.

Use object-specific cascade rules and confirmations:

- Deleting a sticky note permanently deletes its comments, hearts and dot votes. Use **Delete this sticky note?** with **This permanently deletes the sticky note and all its comments, hearts and votes. This cannot be undone.** and actions **Cancel** / **Delete sticky note**.
- Deleting a comment deletes only that comment. Use **Delete this comment?** with **This permanently deletes the comment. This cannot be undone.** and actions **Cancel** / **Delete comment**.
- Deleting a board permanently deletes all its sticky notes, comments, hearts and dot votes and removes Participant access and pending invitations without deleting participant accounts. Use **Delete this board?** with **This permanently deletes the board and all its sticky notes, comments, hearts and votes. It also removes all participants and pending invitations. This cannot be undone.** and actions **Cancel** / **Delete board**.

For Public sticky-note deletion, also explain that independent copies, saved images, screenshots, search results, caches, AI datasets, model training and other external uses cannot be recalled. Omit dependent-object wording only in contexts where those objects cannot exist. V-09 must test the cascade, corrected controls and resulting counters before the implementation is treated as complete.

Account deletion remains the separate V-06 lifecycle: every owned board is permanently deleted; sticky notes and comments on boards owned by somebody else remain under **Deleted user**; Drafts, personal hearts and the Wall of Love are removed; dot-vote totals lose the account relationship; Public sticky notes remain after de-attribution; and future subscription renewal ends. Deleted data may remain in protected technical backups for no more than 30 days, without ordinary product access or user-facing recovery. Separately required billing, tax or legal records use the applicable legally verified period and contain as little product content as practicable.

For every retained Public sticky note, place a small strip of tape at the top and provide the accessible explanation **This sticky note remains after its author deleted their account.** Keep the publication date, country of origin, share count and heart count, but remove the internal account relationship and all author controls. Do not describe the tape as decorative only or rely on it without accessible text. Authorised moderation remains available.

The account-deletion confirmation must identify owned boards that will be permanently deleted and explain the different treatment of Drafts, contributions on other Owners’ boards and retained Public sticky notes. It must also state that retained Public content remains indexable and available for external AI use and that independent copies, saved images, screenshots, search results, caches, AI datasets, model training and other external uses cannot be recalled. Test subscription non-renewal and deletion from protected backups within 30 days before publishing a complete deletion promise. Do not publish exact billing, tax or legal-record periods until they have been legally verified.

> **[DECISION D-21] Partly resolved on 20 July 2026; [VERIFY V-09] cascade and copy approved on 21 July 2026; technical-backup period resolved on 22 July 2026** — Sticky-note, comment and board deletion has no Undo or recovery period and becomes final immediately after confirmation. Protected technical backups expire within 30 days and cannot be used as a product recovery path. V-09 remains open for deletion implementation and counter verification; V-06 must verify backup expiry and separately required records.

Individual sticky notes do not have **Completed** or **Archived** states. The only future archive feature under consideration applies to a complete private board, including its sticky notes, comments, hearts and dot votes. Only the Owner or an authorised platform moderator or administrator may archive, restore or permanently delete it.

If implemented, keep an archived board visible but read-only for its Owner and existing Participants. Preserve all board content and interactions, allow the Owner to revoke existing access, cancel pending invitations, prevent new invitations and stop routine activity and daily-digest notifications. Retain the archive indefinitely until it is restored or permanently deleted. Restoration reactivates the board for its remaining Participants; cancelled invitations remain cancelled. Necessary privileged moderation continues under D-24, and permanent deletion remains immediate and irreversible under D-21.

> **[VERIFY V-02] Resolved on 20 July 2026** — Use this archive lifecycle when the feature is designed and implemented. Do not present board archiving as an existing capability until it has shipped. Private-board share links do not exist.

### Calmness

- Notifications are off or minimal unless their value is clear.
- Avoid streaks, artificial urgency and engagement pressure.
- Use badges only for information that needs attention.
- Keep empty states helpful but brief.
- Celebrate real progress without interrupting the next action.

### Collaboration

Design collaboration as four optional layers rather than one all-or-nothing feature:

1. **See:** understand the idea, existing context, participants and decisions.
2. **Respond:** on a private board, ask a question or add feedback through a comment, place a heart or participate in dot voting. On the worldwide wall, the only response is a heart from a signed-in user.
3. **Contribute:** create notes and edit one’s own notes within granted permissions. Administrative moderation is a separate capability.
4. **Decide:** record what was chosen, completed or rejected.

An email invitation should make the board name, inviter, required account, 14-day expiry and granted Participant capability clear. The recipient signs in or creates an account before access begins. Declining grants no access and appears as **Declined** to the Owner without a separate Owner email. A new Participant should be able to understand the board without asking for a separate briefing. The Owner can later revoke access; revocation is immediate and sends the former Participant an immediate email.

When Participant access ends, preserve that person’s existing sticky notes on the board. If the person deletes their account, retain those sticky notes on boards owned by somebody else and replace their displayed author with **Deleted user**. Explain before account deletion that the author can permanently delete their sticky notes first.

On an active board, allow the Owner to permanently delete any sticky note, including a Participant’s, without granting permission to edit another author’s text or separately delete another author’s comment. Use the V-09 warning and cascade. Log actor, board, sticky note, author, time and cascade outcome without retaining the deleted content body. Include the event in the affected author’s conditional daily digest while they still have access; do not send an immediate deletion email. Moderator and administrator deletion remains governed by D-24’s stricter audit and notification rules.

Comments are supporting discussion, not sticky notes. They do not use Draft/Public statuses. Do not introduce public comments or public dot voting without a new product decision.

A Participant may post a comment and delete their own comment. Do not offer or document comment editing. Moderator and administrator actions remain privileged controls under D-24.

Treat a private-board heart as a personal toggle. The first click changes the light heart to red and increases the displayed count by one; the next click changes it back to light and decreases the count by one. Do not connect private-board hearts to the Wall of Love.

For dot voting, only the Owner starts and closes a round. Let the Owner choose **1**, **3**, **5** or **10** dots per Participant and preselect **3**. A Participant may place at most one dot on each sticky note and may withdraw a vote while the round is active. Keep results hidden until the Owner closes the round.

Do not offer or document voting-round reset or reopening. After the Owner closes a round, show a voting-round icon and vote count on each sticky note that received at least one vote. Starting a new round immediately and permanently makes the previous round and its results unavailable; there is no replacement warning or recoverable voting history.

Display the active-round notice above the sticky notes. Its used-vote and allowance values update for the Participant, while the default initial state reads:

> Voting is open — you have used 0 of 3 votes. Votes stay hidden until the round is closed.

After closure, show the latest results and place this notice above the sticky notes, substituting the actual closing date:

> Showing the results of the last voting round (closed 2026/07/20).

### Real-time collaboration and saving

Treat real-time behaviour as a quality requirement for existing private-board collaboration, not as a separate roadmap feature. Synchronise accepted sticky-note creation, editing, deletion and movement, comments, hearts, votes and voting-round state changes to other active Participants without requiring a refresh. Autosave editable sticky-note text and show a visible saving, saved or failed state.

Never discard unsaved text after a connection or server failure. Preserve it locally and provide a safe retry path. When editable text has changed on the server, keep the local version and show a conflict instead of silently using last-write-wins. Let the server determine the accepted state of hearts, votes and position changes and correct any optimistic display when necessary. Constant presence indicators are optional; content protection is mandatory.

> **[VERIFY V-04] Requirement approved on 21 July 2026; implementation unverified** — The capability is reported as probably not implemented. Verify it across separate sessions, connection loss, failed requests, simultaneous author/moderator editing and permission loss. Do not promise real-time collaboration in interface or Help Centre copy until it passes.

Do not provide edit history for sticky notes or Instant Photos. After an accepted edit, text, caption, colour, tags and due date are current values only; no earlier value can be viewed, compared or restored. Tags and due dates apply only where supported and a due date must never be described as a Public expiry. Image replacement or removal and future alternative-text changes also update only the current object.

Keep this boundary separate from reliability and accountability. Autosave, preserved unsaved text and conflict handling protect work in progress but do not retain an accepted version timeline. Moderation audit logs and report evidence serve D-24 and must not be exposed as revision history or used as a routine restore source.

> **[QUESTION Q-02] Resolved on 22 July 2026; implementation verification required** — Remove or avoid history, revision, compare and restore-version controls and claims. Test current-value overwrite alongside V-04 saving, failure and conflict behaviour.

> **[DECISION D-07] Resolved on 20 July 2026; Owner deletion boundary added on 21 July 2026** — Use only **Owner** and **Participant** as board roles. The Owner invites and removes Participants, manages and may delete the board and, on an active board, may delete any sticky note without editing another author’s text or separately deleting another author’s comment; once whole-board archiving exists, the Owner may archive it. Every invited Participant can view and contribute, including creating sticky notes, editing and deleting their own sticky notes, adding and deleting their own comments, placing hearts and using dot voting. There are no separate Viewer, Editor or Commenter roles. Authorised platform moderators and administrators remain separate platform roles.

Keep exactly one non-transferable Owner per board. Ownership cannot be handed to a Participant or reassigned by a moderator or administrator. The Owner remains involved throughout the development of the board’s idea. Deleting the Owner’s account permanently deletes every board that account owns, including its sticky notes and participant access; the account-deletion warning must state this before confirmation.

> **[DECISION D-22] Resolved on 20 July 2026** — Do not design ownership transfer, co-ownership or owner succession. Verify the owned-board deletion warning and cascade under V-06.

> **[DECISION D-26] Resolved on 21 July 2026; [VERIFY V-11] implementation required** — Preserve a former Participant’s board sticky notes and use **Deleted user** after their account is deleted. The author may delete them beforehand. The Owner may delete any sticky note on an active owned board under the limits above; authorised moderators and administrators may delete under D-24. Verify Owner controls, V-09 cascade, technical logging and digest inclusion end to end.

> **[DECISION D-23] Resolved on 20 July 2026; invitation lifecycle completed under D-08 on 21 July 2026** — Email invitation plus sign-in or account creation is the only private-board entry path. Do not design anonymous access, accountless participation or private-board share links. Invitations expire after 14 days; declined invitations grant no access; access revocation is immediate and triggers an email to the former Participant.

### Activity and notifications

Use email only; do not introduce an in-product activity inbox. Send an immediate email when someone is invited to a private board, when their Participant access is later revoked and when a current Participant is explicitly mentioned. A mention may name one or more current Participants; send each mentioned person their own notification. Do not email the Owner when an invitation is declined; show **Declined** in invitation management. A scheduled daily job sends at most one activity digest to a recipient, and only when at least one private board they can still access has changed since the previous digest.

In the board overview, show one neutral recency line per board: **Last modified on YYYY/MM/DD**. Set it when the board is created and update it only after an accepted user-visible change to board content, organisation, collaboration, access or settings. This includes board detail and layout changes; sticky-note creation, editing, deletion and movement; image, tag and due-date changes; comments and mentions; hearts and dot-voting changes; and invitation or Participant-access changes.

Do not update the date when somebody merely opens or views the board, when an edit fails or remains unsaved, or because of background maintenance, backups or privileged access without a user-visible mutation. Do not expose the underlying events as an activity feed or edit history.

Do not derive an **Inactive** state or threshold from the date. Send no inactivity email, notification or reminder, show no warning or urgency treatment, do not automatically reorder boards by this date, and never archive, restrict or delete a board automatically because it has not changed. Existing D-08 emails and the conditional daily digest remain event-driven; Q-06 adds no email.

> **[QUESTION Q-06] Resolved on 22 July 2026; implementation verification required** — Verify date updates for the included event set and exclusions, **YYYY/MM/DD** display in the board overview, access control, preserved board ordering and consistency with D-08. Confirm that no inactivity state, notification, history or automated lifecycle consequence is introduced.

Aggregate routine board changes into that daily message. Do not send separate immediate emails for comments, hearts, dot votes or individual edits unless the recipient is explicitly mentioned, and do not use reminders or engagement prompts. Filter every digest and mention email using the recipient’s access at send time so removed Participants do not receive private-board information.

> **[DECISION D-08] Resolved on 21 July 2026; mention email added under Q-03 on 22 July 2026** — Invitations expire after 14 days. Declining grants no access, appears to the Owner as **Declined** and sends no separate Owner email. Access revocation takes effect immediately and sends the former Participant an immediate email. An explicit mention sends an immediate email to each named current Participant. The daily digest remains conditional and limited to one per day. Verify mention entry points, duplicate handling, digest duplication, access filtering, delivery failures and applicable preferences and unsubscribe or transactional-email treatment before making operational promises.

### Mention, not assignment

Do not provide an assignee, responsible-person, assignment-acceptance, reassignment or assigned-to-me filter. A private-board contribution may instead mention one or more current board Participants. Mentioning draws attention and triggers an immediate email to each named person; it does not change authorship, ownership, board access, edit or deletion rights, due date or responsibility. Public sticky notes and Instant Photos do not support mentions.

> **[QUESTION Q-03] Resolved on 22 July 2026; implementation verification required** — Verify mention entry locations, one and multiple recipients, current-Participant selection, revoked access, duplicate mentions, email delivery, preference treatment and whether the same event also appears in the daily digest. Never document a mention as assignment.

### Accessibility

- All essential actions must work without colour perception.
- Keep sticky-note colours expressive rather than semantic. Use visible tags or labels for status, priority, category or any board-specific convention; never require a user to infer meaning from colour alone.
- Interactive elements need clear labels and visible focus.
- Text and controls need sufficient contrast and target size.
- Keyboard order should follow the visual and task order.

> **[DECISION D-18] Resolved on 20 July 2026** — Do not introduce product-defined colour meanings. Colour remains personalisation; explicit organisation belongs in tags or visible labels.
- Motion should not be required to understand a change.
- Error messages should identify the problem and a next step.

## Content and terminology

### Canonical terms

Use these consistently:

- **sticky note** for the core content object;
- **worldwide wall** for the public discovery context;
- **private board** or **board** for an access-controlled workspace;
- **board owner** for the person controlling a board;
- **participant** for a person who has accepted an invitation to a board;
- **plan** for Free, Premium or Chosen Few;
- **subscription** for a recurring paid agreement.

**Sticky note** is mandatory in titles, navigation, buttons, first mentions and formal definitions. **Note** is allowed only as a natural shorthand after the object is clear. Do not use **post**, **card**, **item** or **content** as interchangeable product names.

Use **Plans & subscriptions** and `/plans-and-subscriptions/` as the canonical Help Centre title and permalink. Do not introduce alternative page labels for the same subject.

### Writing rules

- Start with the user’s goal or situation.
- Explain the outcome before the steps.
- Use short sentences and concrete verbs.
- Address the user as “you”.
- Prefer active voice.
- Name the interface control exactly as shown.
- Do not promise behaviour that has not been verified.
- Avoid hype, filler and claims such as “easy” when the workflow can demonstrate it instead.
- State limits, prices and consequences plainly.

### Interface copy

- Button labels describe the action: **Create board**, **Send invitation**, **Delete note**.
- Confirmation headings name the consequence: **Delete this board?**
- Success messages confirm the result and disappear without blocking work.
- Error messages follow: what happened, why if known, and what the user can do next.

After a meaningful action, confirmation copy may reinforce progress, but it must remain truthful and calm. Publishing places the sticky note immediately on the worldwide wall and shows a simple success message. The author can then directly **View**, **Share**, **Edit** or **Return to Draft**. Do not use confetti, a blocking celebration or engagement pressure.

Use layered transparency for external copies, search indexing, caches and AI use:

1. Before **Publish**, state that the sticky note will be public and may be copied or indexed by others.
2. At **Return to Draft** and public-note deletion, state that the action removes the sticky note from StickyNotes.club and current intentional discovery mechanisms but cannot recall independent copies, screenshots, search results, caches, AI datasets, model training or other external uses that already occurred.
3. Use the Privacy Policy for the full explanation of public-data visibility, third-party indexing and caching.
4. Use the Terms for the contractual boundary and limits of removal from third-party systems.

> **[DECISION D-12] Resolved on 20 July 2026** — Immediate publication, calm success feedback and direct next actions. Do not use “the world’s largest wall” or other unsupported reach claims. Verify the exact interface copy against the implemented controls.

## Help Centre rules

- One primary question or goal per page.
- Do not create a separate **Understanding StickyNotes.club** section. Keep necessary concepts beside the practical task they explain.
- Put product positioning and broad “why” narratives on the marketing site; use brief contextual guidance in the interface when a user makes a relevant choice.
- Treat **readable in under two minutes** as a soft target for ordinary guides, not a hard limit.
- Never remove necessary privacy, billing, deletion, access, safety or troubleshooting information to meet a reading-time target.
- Split a long page only when it contains genuinely separate user goals, not merely to reduce its word count.
- Keep existing permalinks stable unless a redirect is added and verified.
- Use the standard page structure where it helps; do not add empty template sections.
- Link to the next likely task, not every remotely related page.
- Keep plan details in one canonical page and link to it elsewhere.
- Check navigation labels, page titles and in-page links as part of every update.
- Write in the selected language variant consistently; current product documentation uses English with some mixed US/UK spelling that should be normalised.

> **[DECISION D-14] Resolved on 20 July 2026** — The two-minute target is a soft guideline for focus. Accuracy, consequences and task completion take precedence over reading time.

> **[DECISION D-16] Resolved on 20 July 2026** — No separate Understanding section. Help Centre concept content must support a concrete task, marketing explains the wider value, and the product provides concise context at the point of choice.

## Plan and paywall rules

- Let people understand the value before presenting a paywall.
- Explain the exact limit reached and the available next step.
- Do not hide existing user content when a plan changes without prior explanation.
- Show price, tax treatment, billing interval and renewal behaviour before purchase.
- Make cancellation available through the account or customer portal.
- Treat entitlements as product rules that require the same documentation and testing as other behaviour.

Free includes one active, editable owned private board and full participation on boards to which the user is invited. Premium includes up to five active, editable owned private boards; Chosen Few includes unlimited active owned private boards. Archived owned boards and joined boards do not consume the active-board allowance.

Only Premium and Chosen Few Owners can send private-board invitations. Free users can receive invitations and participate fully. Comments, private-board hearts, dot voting and private-board sticky-note tags and due dates are available on all plans.

Lead paid-plan explanations with the ability to initiate and scale private collaboration. Use higher publication and board volume and additional personalisation as supporting value, not the main story. The concise tier narrative is **Free is for capturing and joining. Premium is for bringing people together around your own ideas. Chosen Few is for people who want no practical plan-level volume limits.** Always pair this narrative with the exact entitlement table where a person is choosing or purchasing a plan.

Do not frame Free as intentionally frustrating, suggest that Free Participants collaborate less fully after joining, or imply that Chosen Few removes safety, content, file, technical or other non-plan boundaries.

> **[QUESTION Q-07] Resolved on 22 July 2026; content and commercial verification required** — Audit marketing, pricing, paywalls, checkout and onboarding for the collaboration-first value story. Preserve the D-13 and D-27 entitlements and verify that supporting volume, organisation and personalisation claims are accurate.

Count only a successful **Draft → Public** transition against the daily sticky-note allowance, including republication after a sticky note has returned to Draft. Do not count creating or editing Drafts, creating or editing private-board sticky notes, editing an existing Public sticky note or failed publication attempts. When the limit is reached, disable only publication, explain what happened and preserve the rest of the product. State that publication becomes available again at **00:00:01 UTC on the next day** and show the wait in the user’s local time. Do not delete, hide or invalidate existing work.

Treat a downgrade as a deliberate reduction in functionality. When the new plan’s active-board allowance is lower than the number of active boards the user owns, require the Owner to select which allowed number remain active: one for Free or up to five for Premium. Before confirmation, show the selected active boards and every other owned board that will be archived; do not complete the downgrade until the selection fits. Archive the listed excess boards with the Owner’s authorisation. Preserve them indefinitely as read-only under V-02; do not delete them, and do not count them towards the active allowance. Block restoration when it would exceed that allowance and offer an upgrade or a way to create capacity.

> **[DECISION D-13] Resolved on 22 July 2026** — The Free, Premium and Chosen Few entitlements, **00:00:01 UTC** reset, successful-publication counter scope, treatment of republication and exclusion of failed attempts are approved. Do not enable the downgrade path until V-02 archiving and the V-05 entitlement flow are implemented and tested.

## Functional guardrails

### Boards and layouts

Board creation requires a **Name**, allows an optional **Description** and presents a template choice with **Blank** selected by default. Do not introduce or document a visibility choice, central-question field or desired-result field: every board is private by definition.

The template choice offers **Blank**, **Retro**, **Kanban**, **Week planner** or **Brainstorm**, with **Blank** selected by default. Blank and Brainstorm use the same grid structure and can later change to columns; they differ only in default background and product framing. Retro, Kanban and Week planner start with columns.

> **[VERIFY V-01] Resolved on 20 July 2026** — Keep the board-creation workflow and its Help Centre instructions limited to **Name**, **Description** and template selection.

Users can reorder sticky notes within their current row and move them between columns where columns exist. A board offers nine backgrounds, cannot be duplicated and currently grows without a product-defined spatial or content limit. Describe this as a structured grid/column workspace, not as a freeform unlimited canvas.

> **[DECISION D-19] Resolved on 20 July 2026; [VERIFY V-08] resolved on 21 July 2026** — Preserve the current layouts, movement, backgrounds, absence of duplication and unrestricted growth. Document Blank and Brainstorm as structurally identical grids with different default backgrounds; both can later change to columns.

### Search

Product search is unavailable and not planned. Do not show or promise text-search fields for Public sticky notes, Drafts, boards or comments.

Filtering remains deliberately scoped: private boards can filter sticky notes by tags, and the worldwide wall can filter Public sticky notes by country. Label these controls by their filter, such as **Filter by tag** or **Country**, rather than **Search**. Help Centre search is a separate documentation capability.

> **[DECISION D-09] Resolved on 20 July 2026** — No product search. Keep only tag filtering on private boards and country filtering for Public sticky notes on the worldwide wall.

### Tags and dates

Tags are optional aids for finding and grouping sticky notes on a private board, not substitutes for permissions, status or board structure. Scope each tag to one board and convert its text to lower case automatically so capitalisation does not create duplicates. The Owner and every current Participant may create, rename and delete tags using their ordinary board rights; there is no separate tag-management role and tags cannot be merged. Deleting a tag removes only that label from every affected sticky note and never deletes a sticky note. Keep tags flat and avoid hierarchies until repeated user needs justify them.

A private-board sticky note may have one optional due date. When it has passed, show a red clock icon and the expired date on the sticky note. Do not provide due-date filtering, reminder email or another notification. The due date is a visual attention signal only; it creates no task, assignment or expiry lifecycle.

Do not place tags or due dates on a board, worldwide-wall Draft, Public sticky note or Instant Photo. Do not confuse a due date with D-20 Public-content expiry, which does not exist.

> **[QUESTION Q-04] Resolved on 22 July 2026; implementation verification required** — Test lower-case deduplication within and separation between boards, tag creation, renaming and deletion by Owners and Participants, the absence of merging, preservation of sticky notes after tag deletion, due-date display before and after expiry, and the absence of due-date filtering and notifications.

### Favourite, pin and priority

Favourite already exists through the public heart. When a signed-in user hearts a Public sticky note, that sticky note appears on their private **Wall of Love** and the heart count increases by one. Unhearting removes it from that user’s Wall and subtracts one. Only that user can view the Wall. The heart remains the visible public reaction while also supporting personal retrieval. Private-board hearts do not affect the Wall of Love.

Returning a Public sticky note to Draft, deleting it or removing it through moderation removes all its public heart/favourite relationships. Public → Draft also resets the heart and share counts. Republishing starts with a new publication date, zero counts and no restored Wall of Love entries.

Pin and priority solve different potential problems—shared prominence and required attention—but neither exists or is planned. Do not use either term for hearts, tags, due dates or layout position.

> **[DECISION D-10] Resolved on 20 July 2026; removal lifecycle resolved on 21 July 2026** — Treat an active public heart as the favourite relationship powering a user-only Wall of Love. Public profile visibility is parked rather than planned. Apply the reset and removal rules above and verify their implementation under V-10.

### Images and URLs

On the worldwide wall, let a user create either a text sticky note or an **Instant Photo** consisting of one image in a Polaroid-like frame plus a caption. Apply the same Draft/Public lifecycle, publication allowance, metadata, hearts, sharing, moderation and deletion rules to both Public forms. On private boards, create only sticky notes, each with one optional image. Do not expose an Instant Photo as a separate private-board object.

Accept images only and reject documents, audio, video, archives and every other uploaded file category. Limit each image to **5 MB** and show a clear validation error before submission when the limit or file-category rule fails. The image inherits the object’s audience, author, moderation and deletion lifecycle and is deleted with it.

Reject URLs in sticky-note text and Instant Photo captions. Do not turn URL-like strings into clickable links or previews and do not expose a URL or general-attachment control. This rule does not silently redefine profile fields or private-board comments, which are outside Q-01.

The current alternative text **Instant Photo** identifies only the object type and is not an adequate image description. Treat the accessible alternative-text input, display and fallback as unresolved implementation work. Verify accepted image formats, dimensions, processing, upload failure and removal, lifecycle transitions and alternative-text behaviour before publishing complete accessibility or file-support claims.

> **[QUESTION Q-01] Content behaviour resolved on 22 July 2026; accessibility and implementation verification required** — Apply the two Public forms, the single private-board form, image-only and 5 MB rules, URL prohibition and inherited lifecycle above. Plan availability remains governed by D-13 and V-05 rather than Q-01.

### Export and handoff

An eligible individual sticky note can be saved as an image. **Save as image** is not available for Drafts and must not be shown or promised in that state. Treat it as a note-level action, not as a general export system. Preserve the sticky note’s visual identity and make it clear that the resulting file is an independent local copy governed by the person who saves or shares it.

On a Public sticky note, present two sharing actions: **Copy link**, which places the direct link on the clipboard for pasting into any external channel, and **Save as image**, which generates an independent image suitable for storage or social media. Increase the share count by one after every successful completion of either action, including repeats. Describe the count as completed share actions, not unique people or confirmed external shares. Do not imply direct posting to a social network.

On account deletion, retained de-attributed Public sticky notes keep their publication date, creation-country snapshot and aggregate share and heart counts. Remove heart relationships created by the deleted account and adjust the affected counts; preserve other users’ hearts and Wall of Love entries for the retained Public sticky note.

Bulk, board-level and structured export do not exist and are not planned. Do not promise printable boards, Markdown, JSON, CSV, PDF or similar content exports.

A person can still contact StickyNotes.club by email to exercise applicable privacy rights, including access to or portability of personal data. Handle that request through the documented privacy process. Do not describe it as a board-export tool or imply that every shared object will be returned in a reusable product format.

> **[DECISION D-11] Resolved on 20 July 2026** — Support only saving an eligible individual sticky note as an image; exclude Drafts. Do not provide or promise bulk, board-level or structured export. Keep privacy access and portability requests available by email and conceptually separate from product functionality. Verify image format, dimensions, resolution, filename, included attribution or metadata and availability for Public and private-board sticky notes.

## Onboarding rules

The first experience should prove the promise quickly:

1. create a note;
2. understand where it is and who can see it;
3. find it again;
4. see how related notes may come together;
5. understand that collaboration can be added later.

Do not require extensive profile completion, board design or workflow choices before first value.

> **[DECISION D-06] Resolved on 20 July 2026** — A sticky note created for the worldwide wall starts as a **Draft**, hidden from other ordinary users, and becomes visible to them only after deliberate publication as **Public**. A sticky note created on a private board inherits that board’s ordinary-user access; an unshared board is hidden from other ordinary users. Authorised platform moderators and administrators retain privileged access to all Drafts, boards and sticky notes. No separate personal inbox is required.

## Measuring value

Prefer signals that an idea progressed or remained useful:

- a person returns to create another note;
- a note is found again;
- related notes are brought together;
- an invited person contributes meaningfully;
- a board reaches a deliberate result or, once the future feature exists, is archived;
- users finish core tasks without support.

Do not optimise raw note counts, daily sessions, notification clicks, time in product or reaction volume as ends in themselves. StickyNotes.club should help people progress, not hold their attention.

## Priority order

When planning work, prefer:

1. trust and data preservation;
2. fast capture and retrieval;
3. understandable notes and boards;
4. privacy and access;
5. lightweight collaboration;
6. completion, archiving and cleanup;
7. discovery and public distribution;
8. deeper organisation and automation.

A visible feature does not automatically outrank reliability or clarity work.

## Marketing and positioning

Marketing should explain the human outcome rather than count features. The core story is that ideas often disappear, become scattered or are forced into a heavy system too early; StickyNotes.club lets people begin small and add structure or collaboration when it becomes useful.

The canonical product promise and tagline is:

> **A place where ideas can grow together.**

Use “StickyNotes.club is a place where ideas can grow together” only when a complete grammatical sentence is needed in ordinary prose.

Use these narrative pillars where they are true:

- **Capture before it disappears.**
- **Give ideas room to grow.**
- **Bring related thoughts together.**
- **Grow ideas together.**
- **Keep control of what is public.**

For commercial positioning, make **Grow ideas together** the lead paid-value pillar. Free supports capturing and full participation on invited boards; Premium unlocks bringing people into owned boards; Chosen Few serves people who need no plan-level publication or active-board limits. Volume, organisation and personalisation provide evidence and differentiation underneath that collaboration story rather than competing with it.

Prefer “Capture ideas before they’re forgotten” over “Create sticky notes”, and “Give every project its own place to think” over “Private boards”. Support claims with recognisable situations such as a writer collecting angles, friends planning a trip or a neighbourhood initiative organising suggestions.

Do not position the product as a heavy company platform or promise public boards. Boards are private and access-controlled; public distribution happens through individual sticky notes on the worldwide wall. Private-board content preserves ownership and attribution. Public content follows the explicit relinquishment, anonymous presentation and limited internal-control relationship defined in D-28.

Do not promise or design a direct Public → Private transfer. There is no planned action to copy, move, reference, create a board from or add a Public sticky note to a private board. Viewing, sharing and saving an eligible sticky note as an image are separate actions and must not be described as board transfer or collaboration.

Treat a private-board sticky note as belonging to exactly one board. Do not design or document simultaneous membership of multiple boards. If similar text is captured separately on another board, it is a distinct sticky note with its own author, interactions and lifecycle.

The homepage should answer within a few seconds:

1. What is StickyNotes.club?
2. What can I do here?
3. Where do I start?

Onboarding is part of marketing when it proves the promise without demanding profile completion or system configuration first.

## Review checklist

### Product review

- Does this solve the stated problem?
- Does it fit the Constitution and Product Model?
- Are visibility, ownership and permissions clear?
- Is the essential version complete?
- Are edge cases and content migration defined?
- Is success measurable without optimising for noise?

### Content review

- Does terminology match the interface?
- Is the first paragraph useful on its own?
- Are actions and consequences unambiguous?
- Are all claims verified?
- Do links and permalinks work?
- Are pricing, privacy and policy implications reflected elsewhere?

### Release review

- Happy path tested.
- Empty, loading, error and permission states tested.
- Mobile and keyboard path checked.
- Analytics, logs or support signals defined only where needed.
- Help Centre updated and reviewed.
- Terms, Privacy Policy and plan information updated if affected.
- Design Notes updated with the decision and remaining questions.
- GitHub Pages build on `main` completed successfully in GitHub Actions.
- `https://docs.stickynotes.club` serves the release over valid HTTPS.
- Changed permalinks, redirects, internal links and the 404 path were checked explicitly.

The canonical Help Centre source is `/docs` on `main` in `faridbouchdak/stickynotes.club`. GitHub Pages deploys it automatically to `https://docs.stickynotes.club`, and failed builds are visible in GitHub Actions. Fly.io does not participate in documentation deployment. Cloudflare provides the domain and network layer but does not deploy the site.

> **[VERIFY V-07] Partly resolved on 21 July 2026** — Repository, source directory, branch, GitHub Pages deployment, automatic publishing, Actions failure visibility, canonical host and HTTPS are confirmed. Still verify preview behaviour, British-English permalinks, intentional absence or presence of redirects, internal links, the production 404 path, cache behaviour and rollback.

## Decision record template

Use this in Product Design Notes for decisions worth preserving:

```markdown
### YYYY-MM-DD — Decision title

- Status: proposed | accepted | reversed
- Context: what problem or constraint prompted this?
- Decision: what will we do?
- Rationale: why this option?
- Consequences: what becomes easier, harder or out of scope?
- Evidence needed: how will we know whether to keep it?
- Affected docs: links or filenames
```

## Feature concept template

```markdown
# Feature: [name]

## User problem

For [person] who [situation], [problem] causes [consequence].

## Desired outcome

The person can [result] without [current obstacle].

## Core scenario

1. ...
2. ...
3. ...

## Minimum valuable version

- ...

## Not in this version

- ...

## Visibility and rights

- Who can see this?
- Who can change this?
- What happens when it is shared or moved?

## Lifecycle and exceptions

- How is it created, changed and deleted, and does the proposed whole-board archive lifecycle apply?
- What can fail, and how is work preserved?

## Documentation impact

- Canonical page:
- Related pages:
- Terminology or policy changes:

## Valuable signal

Which behaviour would show that the problem is genuinely better?
```

## Definition of done

A product change is done when:

- the intended user outcome works;
- important access, error and destructive states are safe;
- interface and documentation use the same language;
- related Help Centre, pricing and policy content is current;
- the documented workflow has been tested;
- remaining uncertainty is recorded rather than hidden.
