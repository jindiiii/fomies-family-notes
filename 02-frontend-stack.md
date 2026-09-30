# 02 — Frontend stack

## What it is not

No React / Next / Vue bundle in the script list. No RainbowKit, Privy, wagmi, or SIWE strings in `app.js`. Wallet connection is not the homepage CTA.

This is vanilla JS: five IIFEs plus Cloudflare Insights.

```
/js/config.js          canvas + closed-window copy
/js/api.js             fetch wrapper + endpoint map
/js/address-format.js  address encode/decode + policy
/js/notice-format.js   noticeboard paper layout
/js/app.js             ~162 KB scene + dialogue + forms
```

`app.js` cache-buster on the day of observation: `public-dialogue-20260930`. They version the dialogue pack independently of the API helper.

## Canvas model

`config.js` starts with a 3840×1800 canvas and per-prop hitboxes (`bathroom`, `door`, `elevator`, `bell`, `folder`, `board`, `gallery`). Portrait mode offsets the bell and menu to the safe edges.

Interaction is "is this click inside a rectangle on the painting", not "is this an anchor in a flex column".

Room plate also carries a closure window (`responseUntil: 2026-09-28T20:00:00+04:00`), which matches the X beat where applications were paused on Sunday.

## Networking helper (`api.js`)

- `credentials: same-origin`, `cache: no-store`, `redirect: error`
- JSON only; wrong content-type → `access_expired`
- CSRF from `/api/session` or `/api/alias`, sent as `X-CSRF-Token` on writes
- Timeouts: default 12s; engagement refresh 30s; `/api/tasks/check` 45s

45s on task check is the tell. A local checkbox does not need 45 seconds.

## Hosting / headers

Cloudflare, HTML `private, no-store`, `referrer-policy: no-referrer`, `x-robots-tag: noindex,nofollow,noarchive`, HTTP/3.

## Address module

`address-format.js` is a real encoder/decoder (alphabet, checksum, destinations, policy). Community replies mention a Solana address field that rejects bad paste. That is an application field, not proof of the mint chain.

## Comparison (short)

Usual mint site: Next + Tailwind cards, connect wallet first, copy in the repo, index for ads.
This site: painted scene + hitboxes, connect X last, copy in a CMS, explicit noindex.
