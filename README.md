# fomies.family technical notes

Personal research notes on the public website [fomies.family](https://fomies.family/) and the X account [@FomiesNFT](https://x.com/FomiesNFT).

This repo is the **technical appendix**. The opinion piece lives on X. If you only want the call / the vibe / why the account looks professional, read the article. If you want how the site is actually built, stay here.

- Author: [金迪](https://x.com/Jindi1996) (`@Jindi1996`) / GitHub [`jindiiii`](https://github.com/jindiiii)
- Observed: 2026-09-30 (HKT)
- Subject site: `https://fomies.family/`
- **Not affiliated** with Fomies. Not an audit. Not financial advice.
- **DYOR.**

## Contents

| File | What it covers |
| --- | --- |
| [00-scope-and-method.md](./00-scope-and-method.md) | How this was observed, what was *not* done |
| [01-product-surface.md](./01-product-surface.md) | Gate / hall / office, hitboxes, copy |
| [02-frontend-stack.md](./02-frontend-stack.md) | Scripts, fonts, canvas config, Cloudflare |
| [03-auth-session.md](./03-auth-session.md) | X OAuth2, CSRF, one-file-per-account |
| [04-tasks-and-engagement.md](./04-tasks-and-engagement.md) | Why the social tasks are server-checked |
| [05-api-map.md](./05-api-map.md) | Every `/api/*` path the public JS calls |
| [06-application-and-interview.md](./06-application-and-interview.md) | Case files, interview tree, wallet field |
| [07-cms-and-admin.md](./07-cms-and-admin.md) | Notices, scene dialogue, `/admin` |
| [08-timeline-and-numbers.md](./08-timeline-and-numbers.md) | X timeline + self-reported application counts |
| [09-lookalikes.md](./09-lookalikes.md) | Names that are easy to mix up |
| [x-article-corrections.md](./x-article-corrections.md) | Fact-check of the X article draft |

## One-line take

This is not a Galxe/Zealy checkbox page with a mint button. It is a custom scene engine (3840×1800 art + hit regions) in front of a sessioned API: X OAuth2, Telegram connect/confirm, `/api/tasks/check`, an interview state machine, and a CMS for clerk lines and the noticeboard.

That is interesting. It is not a guarantee of a fair whitelist, a real mint, or a secondary market.

## Official surfaces (as of 2026-09-30)

- Site: https://fomies.family/
- X: https://x.com/FomiesNFT
- Login is `POST /auth/x/start` → `https://x.com/i/oauth2/authorize`. The site itself says: authorize only on x.com; no X password is entered here.

If a page asks you to send funds, sign an unlimited approval, or type an X password into fomies.family, it is not this site.
