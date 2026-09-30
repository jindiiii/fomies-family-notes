# 03 — Auth and session

## Session before login

`GET /api/session` without a cookie (2026-09-30):

```json
{
  "user": null,
  "draft": null,
  "campaign": { "id": "department", "status": "open" },
  "loginEnabled": true,
  "loginUnavailableReason": null
}
```

`campaign.status` is the switch the clerk copy keys off (`open` / `closed` / `not_open` in `app.js`).

## How X login starts

Shipped client references:

- `POST /auth/x/start` — GET on that path returns **405** with `Allow: POST`
- Redirect target pattern: `https://x.com/i/oauth2/authorize`
- Logout: `/auth/logout`

Hash errors the intro screen understands:

- `#identity`
- `#login_cancelled`
- `#login_expired`
- `#login_unavailable`
- `#login_paused`

Human copy next to those codes (from `app.js`):

| Code | Shown to the user |
| --- | --- |
| `login_unavailable` | x sign-in is unavailable. please try again later. |
| `login_paused` | new x sign-ins are paused for this preview… |
| `login_expired` | that sign-in expired. start a new sign-in. |
| `login_cancelled` | x sign-in was cancelled. no account was connected. |
| `sign_in_required` | your session ended. please sign in again. |
| `csrf_rejected` | your session changed. refresh your connection before retrying. |
| `limit_reached` | too many attempts. wait a little before trying again. |

The footnote under the button is doing real work: they do not want a password form on their origin.

## One file per account

Repeated in clerk lines and in the login prompt:

> Connect your X and I'll start the paperwork. One file per account. Allegedly.

Alias rules in the same error table: `2–20 letters or numbers, with spaces, dots, apostrophes, hyphens or underscores.` Legal name is explicitly not required.

## What this buys them

1. A stable identity that is painful to mass-produce compared with typing an @handle.
2. A handle they can later scan for `#Fomies` / `@FomiesNFT` (see [04](./04-tasks-and-engagement.md)).
3. A reason to rate-limit and pause sign-in when X or their own box falls over — which they already admitted on the noticeboard.

## What this does not buy them

OAuth does not prove a human. It proves an X account completed an official authorize screen. Aged farm accounts still exist. The extra cost is real; it is not infinite.
