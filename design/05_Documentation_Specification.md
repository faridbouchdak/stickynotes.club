# Documentation Specification

> Status: v1  
> Purpose: Define the standards, philosophy and quality requirements for all StickyNotes.club documentation.

---

# 1. Purpose

Documentation is an essential part of StickyNotes.club.

It is not something that is written after a feature has been built.

Documentation is used to:

- help users;
- validate product design;
- define product behaviour;
- reduce support requests;
- support onboarding;
- provide reusable content for marketing;
- serve as a future knowledge base for AI assistants.

If a feature cannot be explained clearly, the product should be simplified before the documentation is expanded.

---

# 2. Documentation Philosophy

Documentation should always answer the user's question before explaining the product.

Users visit documentation because they want to accomplish something.

Therefore documentation is written around **goals**, not around **features**.

Good:

- Create a board
- Share an idea
- Organize your work

Avoid:

- Board management
- Sticky note functionality
- Tags & Due Dates

---

# 3. Core Principles

Every page should be:

- useful;
- calm;
- practical;
- easy to scan;
- easy to understand;
- technically correct;
- future maintainable.

Documentation should make StickyNotes.club feel simpler than it actually is.

---

# 4. Audience

Assume the reader:

- is curious;
- is not technical;
- wants to achieve something quickly;
- does not know the internal product structure.

Documentation should never require users to understand how the software is implemented.

---

# 5. Tone of Voice

The writing style should be:

- calm;
- friendly;
- practical;
- confident;
- human;
- concise.

Avoid:

- marketing hype;
- exaggerated enthusiasm;
- corporate language;
- unnecessary technical terminology;
- artificial urgency.

---

# 6. Information Architecture

Documentation is organised around user journeys.

Preferred navigation:

- Getting started
- Use StickyNotes.club
- Manage your account
- Community
- Need help

Never organise documentation around internal implementation or database structures.

Search complements navigation but never replaces it.

---

# 7. Standard Page Structure

Every Help Center page follows the same structure.

```text
Title

Introduction

What you'll learn

Main content

Good to know

Related guides
```

Each page should answer one primary question.

---

# 8. Writing Principles

Always:

- begin with the user's goal;
- explain why before how;
- explain outcomes before actions;
- use active voice;
- write short paragraphs;
- prefer verbs over nouns;
- avoid unnecessary repetition.

Prefer:

> Archive a board when you no longer actively use it.

Instead of:

> The archive functionality allows inactive boards to be hidden.

---

# 9. Product Truth

Documentation only describes implemented behaviour.

Never describe:

- planned features;
- prototypes;
- assumptions;
- possible future behaviour.

Future ideas belong in the Design Notes.

---

# 10. Terminology

Every concept has one preferred name.

Examples:

- note
- board
- private board
- public board
- archive
- delete
- profile

Avoid using multiple names for the same concept.

---

# 11. Related Guides

Every page should contain links to relevant pages.

No page should become a dead end.

Before publishing, verify:

- Which pages should link here?
- Which pages should this page link to?

---

# 12. Consistency

Consistency is more important than local optimisation.

Use the same:

- headings;
- wording;
- terminology;
- page structure;
- writing style;
- navigation patterns.

---

# 13. Documentation as Product Design

Documentation is an early validation tool.

The preferred workflow is:

```text
Design

↓

Write documentation

↓

Review documentation

↓

Build feature

↓

Test

↓

Improve both product and documentation
```

If documentation becomes difficult to write, reconsider the design.

---

# 14. Documentation Lifecycle

Every feature change requires:

1. Review the affected documentation.
2. Update related guides.
3. Check terminology.
4. Verify navigation.
5. Capture new insights in the Design Notes.
6. Update the Playbook if a reusable pattern emerges.

---

# 15. Quality Checklist

Before publishing a page verify:

- The user's goal is clear.
- The introduction explains why.
- Only one primary topic is covered.
- The page is easy to scan.
- Technical language is avoided.
- Related guides exist.
- Terminology is consistent.
- Public and Private behaviour is explained where relevant.
- The documentation reflects the implemented product.
- Links work.

---

# 16. Definition of Done

Documentation is considered complete when:

- it accurately reflects the product;
- it answers the user's question;
- it follows the standard structure;
- terminology is consistent;
- related guides have been added;
- navigation has been reviewed;
- another team member can understand it without additional explanation.

---

# 17. Anti-patterns

Avoid:

- describing UI before explaining the goal;
- documenting future behaviour;
- writing feature-first documentation;
- using technical implementation details;
- inconsistent terminology;
- duplicate explanations;
- orphan pages without incoming or outgoing links.

---

# 18. Golden Rule

Documentation should make StickyNotes.club feel easier to use than the software itself.

Great documentation is not the result of explaining complexity well.

It is the result of building software that does not require much explanation.