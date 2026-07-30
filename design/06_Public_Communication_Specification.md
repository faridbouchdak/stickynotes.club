# Public Communication Specification

> Status: v1  
> Purpose: Define the standards, boundaries and quality requirements for public StickyNotes.club communication.

---

# 1. Purpose

Public communication explains what people can do with StickyNotes.club and why a product change matters to them.

It includes:

- milestone announcements;
- release messages;
- social posts;
- public sticky notes from StickyNotes.club;
- product-update emails;
- website announcements; and
- launch or availability messages.

Public communication is not a substitute for product documentation. It creates understanding and interest, then links to the canonical Help Centre guide when someone needs details.

---

# 2. Relationship to other sources

Public communication must follow the established product truth.

Use this order of authority:

1. **Product Constitution** — enduring principles and boundaries.
2. **Product Model** — current product behaviour and terminology.
3. **Product Playbook** — reusable product and writing rules.
4. **Product Design Notes** — verification status and unresolved questions.
5. **Help Centre** — canonical public explanation of verified behaviour.
6. **Documentation Specification** — writing and quality standards.
7. **Public Communication Specification** — how verified facts are presented publicly.

When sources disagree, do not publish the claim until the conflict is resolved in the design documents.

---

# 3. Communication philosophy

Lead with what changes for the person using the product.

The feature is evidence. The outcome is the message.

Prefer:

> Work together without losing your flow.

Instead of:

> We implemented polling, autosave and conflict detection.

Public communication should make the product feel useful and understandable without exaggerating it.

---

# 4. Core principles

Every public message should be:

- true;
- useful;
- calm;
- human;
- concise;
- specific;
- understandable without technical knowledge; and
- consistent with the product and Help Centre.

Excitement may mark a real milestone. It must not replace substance.

---

# 5. Audience

Assume the reader:

- may not know StickyNotes.club yet;
- may know the product but not the feature;
- is scanning quickly;
- wants to understand why the update matters;
- does not know internal product or technical language; and
- may rely on the message when deciding whether to use or trust the product.

Write so that the message remains clear when seen outside its original context.

---

# 6. Product truth and verification

Only communicate behaviour that is implemented, available and sufficiently verified.

Before publication, confirm:

- the behaviour exists in the current product;
- the relevant verification item is resolved;
- the claim applies to the named audience, plan and context;
- important limitations are not hidden;
- the Help Centre agrees with the message; and
- the message does not imply a planned capability is already available.

Do not announce a development commit, completed code or internal test result as a public product release unless the behaviour is available to its intended users.

Use explicit labels such as **coming soon**, **in development** or **experimental** only when communicating future work is intentional. Never phrase future behaviour as current fact.

---

# 7. Standard message structure

Use the smallest structure that communicates the milestone clearly:

```text
Milestone

User outcome

Verified behaviour

Optional next step
```

For a short public sticky note or social post:

1. Mark the milestone in one short line.
2. State the main user benefit.
3. Support it with no more than three concrete behaviours.

Example:

> Real-time collaboration is live! 🎉
>
> Work together without losing your flow.
>
> Private boards now stay up to date automatically. Your text saves as you type, and simultaneous edits are handled without silently losing anyone's words.

---

# 8. Lead with outcomes

Describe the value before the mechanism.

Good outcomes include:

- stay focused;
- work together;
- keep ideas safe;
- understand who can see something;
- make a decision;
- recover from a problem; and
- finish a task with fewer interruptions.

Avoid presenting internal work as the user benefit:

- database migrations;
- endpoints;
- frameworks;
- polling intervals;
- refactors;
- implementation phases; and
- test-harness details.

Technical detail belongs in development notes unless it materially affects a user's decision or recovery path.

---

# 9. Tone of voice

The writing style should be:

- calm;
- friendly;
- practical;
- confident;
- optimistic;
- human; and
- concise.

Avoid:

- hype without evidence;
- superlatives such as **revolutionary**, **perfect** or **game-changing**;
- artificial urgency;
- corporate language;
- exaggerated promises;
- defensive explanations; and
- language that makes unfinished work sound complete.

Use **we** sparingly. Prefer the reader's experience over a description of what StickyNotes.club built.

---

# 10. Milestones and celebration

A milestone message may be more celebratory than Help Centre copy.

Celebration is appropriate when:

- a meaningful capability becomes available;
- an important reliability or safety improvement is verified;
- a clear product boundary is completed; or
- users can now achieve a previously unavailable goal.

Keep celebration proportional. One exclamation mark or emoji is usually enough for a short announcement.

Do not manufacture a milestone from routine maintenance that has no meaningful user outcome.

---

# 11. Terminology and language

Use canonical product terms consistently, including:

- sticky note;
- Draft;
- Public;
- worldwide wall;
- private board;
- Owner;
- Participant;
- View link; and
- Post link.

Use British English in public communication.

Do not introduce a new public label to make a message sound more exciting. Common search or conversational synonyms may appear only when they do not blur the product meaning.

---

# 12. Claims and precision

Use the narrowest accurate claim.

Prefer:

> Changes usually appear within a few seconds.

Instead of:

> Every change appears instantly.

Avoid absolute words such as **always**, **never**, **instant**, **unlimited**, **secure** and **private** unless the complete statement is supported by the product model and verified behaviour.

A memorable phrase must not be more certain than the evidence behind it.

---

# 13. Limitations and consequences

Do not hide a limitation that would materially change how someone understands the announcement.

Include the limitation in the message when it affects:

- access;
- privacy;
- ownership;
- deletion;
- payment or plan availability;
- data preservation;
- safety; or
- whether the user can complete the stated goal.

Link to the canonical Help Centre guide when the full explanation would make the public message too long.

Minor operational details do not need to appear in the announcement when the Help Centre explains them and omitting them does not mislead the reader.

---

# 14. Calls to action

Use a call to action only when there is a useful next step.

Good:

- Open your private board.
- Read how live collaboration works.
- Create your first sticky note.

Avoid:

- vague engagement requests;
- pressure to act immediately;
- more than one primary action; and
- links that do not directly support the message.

The destination must exist and match the promise in the call to action.

---

# 15. Channel adaptation

Keep the product truth unchanged across channels. Adapt only the length, framing and amount of context.

### Public sticky note

- one milestone;
- one user outcome;
- one short explanation;
- no dependency on a link for basic understanding.

### Social post

- understandable when shared without surrounding context;
- one optional Help Centre or product link;
- hashtags only when they improve discovery;
- no repeated slogan, headline and feature list saying the same thing.

### Product-update email

- outcome-led subject line;
- short introduction;
- clear explanation of what changed;
- relevant limitation or prerequisite;
- one primary action.

### Website announcement

- durable language rather than momentary hype;
- enough context for a first-time visitor;
- link to the canonical Help Centre guide.

---

# 16. Accessibility and inclusion

Public communication must remain understandable without relying on:

- an image;
- colour;
- an emoji;
- specialist knowledge; or
- cultural references that exclude part of the audience.

When an image contains important text, repeat that meaning in the accompanying copy or accessible alternative text.

Place an emoji after meaningful words, not in place of them. Avoid multiple decorative emoji that interrupt reading.

---

# 17. Privacy, safety and trust

Never include personal, private-board or customer information in public communication without a clear and valid reason and the required consent.

Do not use private content as an example merely because it is available internally.

Do not imply that:

- private content is public;
- public content can be recalled from external copies;
- a technical safeguard removes every risk;
- payment removes safety or policy boundaries; or
- StickyNotes.club guarantees outcomes controlled by third parties.

Trust claims must be factual, bounded and consistent with the Privacy Policy, Terms of Service and Help Centre.

---

# 18. Consistency and reuse

Use one canonical explanation for each product fact.

Public communication may simplify that explanation but must not create a competing version of the product truth.

Reuse:

- canonical terminology;
- verified interface labels;
- the Help Centre's explanation of consequences;
- established tagline and value language; and
- approved milestone copy when repeating the same announcement.

Update or retire older public messages when they materially misrepresent the current product and remain under StickyNotes.club's control.

---

# 19. Publication workflow

For every public product message:

1. Identify the user outcome.
2. Identify the verified product change supporting it.
3. Check the relevant Design Notes item.
4. Check the current Help Centre explanation.
5. Draft the shortest complete message.
6. Remove technical detail that does not help the audience.
7. Check terminology, limitations and tone.
8. Verify every link and call to action.
9. Review the final message in the channel where it will appear.
10. Publish only when the product and supporting documentation are available.

---

# 20. Quality checklist

Before publishing, verify:

- The milestone is real and available.
- The user outcome is clear.
- Every product claim is implemented and verified.
- The message is understandable without technical knowledge.
- The tone is calm, human and proportionate.
- Canonical terminology and British English are used.
- No important access, privacy, plan or safety limitation is hidden.
- The message does not promise instant, perfect or unlimited behaviour without evidence.
- Celebration supports rather than replaces the message.
- The call to action is useful and works.
- The Help Centre contains the necessary detail.
- The message remains accurate outside its original context.

---

# 21. Definition of done

Public communication is ready when:

- it truthfully describes an available product outcome;
- it is consistent with the design documents and Help Centre;
- it is concise enough for its channel;
- it includes the context needed to avoid a misleading impression;
- terminology, links and interface labels are correct; and
- a reader can understand what changed and why it matters without additional explanation.

---

# 22. Anti-patterns

Avoid:

- announcing implementation rather than availability;
- leading with technical architecture;
- listing every changed component;
- copying Help Centre paragraphs into a short announcement;
- describing planned behaviour as live;
- hiding a material limitation;
- using excitement to make a small change seem larger;
- making an absolute claim from a best-effort behaviour;
- introducing non-canonical product names;
- repeating the same idea in the headline, subheading and body; and
- adding a call to action that does not help the reader continue.

---

# 23. Golden rule

Say what people can now do, why it matters and only what StickyNotes.club can truthfully support.
