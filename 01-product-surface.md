# 01 — Product surface

The site is a two-scene office, not a landing page with sections.

## Document chrome

- `<title>the department of fomo</title>`
- `meta name="robots" content="noindex,nofollow,noarchive"`
- Matching `x-robots-tag` on responses
- Description: `fomies whitelist. ring the bell, take a number, answer three questions. the clerk is watching.`
- OG image: `/assets/gate/OG.webp`

They are not trying to rank in Google. Traffic is supposed to come from X.

## Scene 0 — intro

Blurred hall, centered wordmark, one button: **Enter the department**.

## Scene 1 — hall

Hand-painted corridor. Mapped hit regions in `CFG.art` (see [02](./02-frontend-stack.md)):

- WC door
- Public notice frame
- Wooden door labelled `DEPARTMENT OF FOMO`
- Fire cabinet
- Elevator with yellow caution tape and `OUT OF ORDER`
- Floor sign `CAUTION / THIN FLOOR`
- Floor vent
- Volume control in the lower left after you are inside

The elevator is decoration. The wooden door is the real entrance.

## Scene 2 — office

This is the product.

Visible props that are also UI:

| Prop | Role |
| --- | --- |
| Service bell | Starts the clerk state machine |
| Clerk (suit, red tie, square pupils) | Dialogue + login |
| Folder / paper tray | Application file |
| Clipboard / task tray | Social tasks |
| Cork noticeboard | CMS-backed announcements |
| Staff portraits | Gallery |
| Social icons | X / Telegram |
| Nameplate `INTAKE OFFICER / DEPT. OF FOMO` | Flavour |
| `EXIT` scratch on the desk | Back to hall |
| Volume slider | Audio |

Mobile gets a separate tray and a menu (`menu-tasks`, `menu-noticeboard`, `menu-gallery`) because pixel hitboxes are hostile to thumbs. `CFG.artPortrait` offsets the bell and the menu to the safe edges.

## Dialogue is the nav

Unauthenticated path observed 2026-09-30:

1. Ring bell → `Good. Someone's here.` → **Hello**
2. Branch. One roll: `It's getting busy in here. More files every day. And some of them have started leaving.` with A/B/C
3. Choosing `I've never been here.` → `Everyone says that. From this side of the desk you all look the same.`
4. `Anyway. The window's open, if you've got business here.`
5. `Applications are open. Qualifications are questionable.`
6. `Connect your X and I'll start the paperwork. One file per account. Allegedly.`
7. Primary: **Sign in with X**
8. Secondary: **Who else works here?**
9. Footnote: `authorize only on x.com. no X password is entered here.`

Idle / repeat-bell lines are not hardcoded only in `app.js`. Many come from `GET /api/public/scene-content` (`idle`, `vent`, `office` keys) so the team can retune the clerk without a frontend release.

Examples from that payload:

- `every ring is going in your file.`
- `this is why the last clerk left.`
- `one active file per account. it keeps the department honest. allegedly.`
- `we'll call you {handle} unless you object. your legal name is unnecessary. your online personality will do.`
- `case {case} is filed. that folder is yours now. the committee is occupied. nothing will happen fast.`

## Design language

Google fonts loaded:

- Chewy — wordmark / display
- Nunito 700/800/900 — UI
- Courier Prime — file / form / department paperwork

Palette: yellow CTA, dusty blue walls, cork, brass plate. Closer to a 2010 office flash game than to a neon mint template.

## What this is for

The surface is doing three jobs at once:

1. Make the whitelist feel like an appointment, not a form.
2. Slow people down before OAuth.
3. Give later review a personality label and a case number instead of a spreadsheet row.
