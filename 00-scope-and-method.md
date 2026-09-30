# 00 — Scope and method

## What was inspected

On 2026-09-30 the public site was loaded in a desktop browser.

Observed:

- HTML document title `the department of fomo`
- Static assets under `/assets/gate/`, `/assets/room/`, `/assets/folder/`, `/assets/menu/`, `/assets/noticeboard/`
- Scripts:
  - `/js/config.js?v=public-dialogue-20260930`
  - `/js/api.js?v=985f7d3657cb`
  - `/js/address-format.js?v=a15faaa255ab`
  - `/js/notice-format.js?v=1661bb60deea`
  - `/js/app.js?v=public-dialogue-20260930`
- Stylesheet `/css/site.css?v=77fc3719229c`
- Unauthenticated JSON:
  - `GET /api/session`
  - `GET /api/public/notices`
  - `GET /api/public/scene-content`
- Response headers (Cloudflare, `noindex`, cache policy)
- Click-through of gate → hall → office → bell → clerk dialogue → `Sign in with X`
- Public X timeline of `@FomiesNFT`

`api.js` was read as shipped to the browser. That file is a map of every path the frontend is willing to call. It is not the server source.

## What was not done

- No X OAuth login, so the live task list, case UI, and engagement numbers for a real account were not seen.
- No Telegram connect.
- No `/admin` session.
- No contract read. The homepage does not publish a CA.
- No claim about the server language, database, or who operates the domain.
- No claim that 10k supply is on-chain. That number circulates in community copy and in the X article draft. The site bio/meta do not print it.

## How to read confidence

| Claim type | Confidence |
| --- | --- |
| A URL exists and returned a status we logged | High |
| A string exists in shipped JS | High |
| A user-facing sentence was photographed in the office scene | High |
| This endpoint really talks to the X API | Inferred from timeouts, error copy, and an official notice about X sign-in / task-check overload. High as product intent, not a packet capture of X. |
| Application totals on the noticeboard | Project-reported. Treat as marketing-grade telemetry. |
| Future mint, chain, allocation | Unknown. |

## License of these notes

Personal research. Quote with a link. Do not treat this repo as an official Fomies document.
