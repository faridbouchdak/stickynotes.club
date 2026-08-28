# Shared image system, prompts and verified sources

Checked on 27 August 2026.

## Brand system

### Colours found in the current Help Centre styles

- Purple: #E0B0FF
- Dark purple/link: #7652A8
- Pink: #FF7EB9
- Yellow: #FFF740
- Mint: #98FB98
- Ink: #1F2937
- Muted text: #4B5563
- Soft background: #FFF9FC

Use white space and one dominant pastel. Do not turn every image into a multicolour collage.

### Typography

Use a clear system sans-serif. If text is added after generation, prefer Inter, Arial or a comparable high-legibility sans-serif. Never rely on generated lettering.

### Accessibility

- The post copy must make sense without the image.
- Put essential on-image wording in the caption and alt text.
- Keep text contrast at least 4.5:1 for ordinary text.
- Do not communicate categories through colour alone.
- Add alt text manually on every platform that supports it.

## Master first-post concept

**Creative idea:** “The room is quiet; the work is not finished.”

Show the moment immediately after a small professional workshop: a facilitator at a table, a wall with real paper sticky notes in the background, a laptop nearby, calm late-afternoon light and a sense of useful work rather than chaos. The image supports the founder story; it does not depict a product feature.

### Master generation prompt

> Editorial documentary photograph of the quiet moment immediately after a small professional workshop. One adult independent facilitator, seen naturally from the side rather than posing, sits at a light wooden table reviewing a few handwritten paper sticky notes. In the softly blurred background is a workshop wall with a modest number of pastel sticky notes arranged in emerging groups. An open laptop is present but its screen is turned slightly away and contains no legible interface or text. Calm late-afternoon daylight, credible European co-working room, human and practical, understated rather than glossy, generous negative space, subtle brand palette of pastel purple #E0B0FF, pink #FF7EB9, yellow #FFF740 and mint #98FB98 with dark charcoal #1F2937. Photorealistic, editorial, natural skin texture, realistic hands, no staged smiles. No logos, no readable writing, no invented software interface, no floating notes, no exaggerated mess, no corporate stock-photo poses, no gradients, no 3D render.

Generate once at high resolution, then crop per channel. Add any copy and the real StickyNotes.club mark afterwards in a design tool, not inside the generation prompt.

## Production masters

1. **Feed master:** 1080 x 1350 px, 4:5, sRGB JPEG quality 85-92.
2. **Status/Story master:** 1080 x 1920 px, 9:16, sRGB JPEG quality 85-92.
3. **Link preview:** 1200 x 630 px, 1.91:1.
4. **Product proof:** real screenshot at native resolution; blur or replace private/customer content before export.

## Platform specifications and operational choices

| Platform | Recommended first-post asset | Verified boundary or reason |
| --- | --- | --- |
| LinkedIn | 1080 x 1350, 4:5, JPEG under 5 MB | LinkedIn accepts ratios from 3:1 through 4:5, recommends 1080 px width and allows 5 MB photo uploads |
| Facebook | 1080 x 1350, 4:5 | Operational cross-platform recommendation; preview in the Facebook composer because Meta surfaces vary |
| Instagram | 1080 x 1350, 4:5 feed; 1080 x 1920 Story | Instagram currently preserves supported feed ratios through 3:4, but 4:5 remains the safer shared feed master |
| WhatsApp Status | 1080 x 1920, 9:16 | WhatsApp Status supports photo/video sequences that disappear after 24 hours; keep key content away from UI edges |
| X | 1200 x 1500, 4:5, JPEG under 5 MB | Single images from 2:1 through 3:4 display in full; 4:5 fits that range |
| Reddit | No image for the first community post | Community post types and rules vary; text is the appropriate first contribution here |
| Bluesky | 1200 x 1500, 4:5, compressed below 1,000,000 bytes | Up to four images; each image currently limited to 1,000,000 bytes and can have alt text |
| Mastodon | 1200 x 1500, 4:5 | Mastodon.social follows the documented default of up to four images; limits remain instance-configurable |
| WIP.co | Real 1600 x 1000 screenshot or no image | WIP is a completed-work changelog. A genuine artefact is more appropriate than generated campaign art |

## Safe areas

- Feed master: keep faces, hands and any later-added words inside the central 864 x 1080 px.
- Status master: keep key content inside y=250-1650 px; the top and bottom are UI-risk areas.
- Link preview: keep essential content inside the central 1000 x 500 px.
- Never place the logo against an edge; allow at least 6% padding.

## Product screenshot rules

- Use only current, verified UI.
- Create a dedicated demo board with fictional neutral content.
- Do not show personal data, customer names, participant names, private links or live QR codes.
- Show one behaviour per image.
- If a screenshot contains important wording, repeat it in the caption or alt text.
- Do not retouch the interface into a capability the product does not have.

## Verified sources

### StickyNotes.club

- Product: https://stickynotes.club/
- Run a workshop: https://docs.stickynotes.club/run-a-workshop/
- Join a workshop: https://docs.stickynotes.club/join-a-workshop/
- Plans and subscriptions: https://docs.stickynotes.club/plans-and-subscriptions/
- Live collaboration: https://docs.stickynotes.club/live-collaboration/

### Platform sources

- LinkedIn photo requirements: https://www.linkedin.com/help/linkedin/answer/a527229/sharing-photos-or-videos
- X posts and 280-character standard: https://help.x.com/en/using-x/how-to-post
- X photo ratios and file limits: https://help.x.com/en/using-x/posting-gifs-and-pictures
- X image descriptions: https://help.x.com/en/using-x/write-image-descriptions
- Instagram image resolution help: https://help.instagram.com/1631821640426723
- WhatsApp Status: https://faq.whatsapp.com/643144237275579/
- Reddit community settings: https://support.reddithelp.com/hc/en-us/articles/15484546290068-Community-settings
- Reddit organic playbook: https://redditinc.com/hubfs/Reddit%20Inc/Content/Reddit%20Pros%20organic%20playbook.pdf
- Bluesky post schema: https://github.com/bluesky-social/atproto/blob/main/lexicons/app/bsky/feed/post.json
- Bluesky image posting: https://docs.bsky.app/blog/create-post
- Mastodon posting: https://docs.joinmastodon.org/user/posting/
- Mastodon instance-specific limits: https://docs.joinmastodon.org/entities/Instance/
- WIP.co help: https://wip.co/help

## Uncertainty

- Facebook does not publish one durable organic-feed dimension that is best across every personal-profile surface. The 4:5 recommendation is an operational choice, not a hard platform limit.
- WIP.co's current help page explains the completed-todo format but does not publish a precise ideal image dimension. Use a genuine readable screenshot and inspect the composer preview.
- Reddit community rules can change at any time. The proposed communities must be checked again on the day of posting.
