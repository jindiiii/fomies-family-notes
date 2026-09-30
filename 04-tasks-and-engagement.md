# 04 — Tasks and engagement

This is the part that is actually different from a fake quest board.

## Client task types

`app.js` builds labels and outbound URLs from `task.type`:

| type | Label logic | Outbound |
| --- | --- | --- |
| follow | follow @handle | `https://x.com/i/user/{id}` |
| like | like the post | `https://x.com/i/web/status/{id}` |
| repost / quote / reply | matching verb | same status URL |
| post | post on x | `https://x.com/compose/post` |
| telegram_join | join Telegram | `task.targetUrl` (must be `https://t.me`) |
| telegram_boost | boost Telegram — {rewardPoints} points | `https://t.me/boost/{handle}` |

`withLike` composes strings like `like and quote`. Hashtag / mention chips are first-class.

## Check path

`API.checkTask(payload)` → `POST /api/tasks/check` with a **45 second** client timeout.
`GET /api/tasks` is 401 when logged out.

Telegram is two calls: `POST /api/telegram/connect` then `POST /api/telegram/confirm`.

Admin companions (auth required): task list, `/:id/history`, `telegram-test`. History existing at all is the opposite of storing a boolean the user toggled.

## Why this is real in product terms

A fake board: open tweet, tick done, store `clicked_at`.
This board: X session required, check POST may run almost a minute, Telegram is connect-then-confirm, and the noticeboard already published an incident where **X sign-ins and task checks hit their limits at the same time**.

That incident only happens if check traffic hits an upstream or a worker queue.

## Engagement record

After login the file UI can render form ER-1. Client copy: counts recent public X posts that use `#Fomies` or mention `@FomiesNFT`.

Wired fields: posts scanned / matching, original / replies / quotes, views, likes / replies / reposts / quotes received, `points.total`, `points.newViews`. Partial view coverage appends `+`.

`GET /api/engagement` and `POST /api/engagement/refresh` (30s). Refresh is gated by `nextRefreshAt`.

This rewards people who actually talk about the project. It also rewards bought replies. It is a filter, not a moral sorting hat.

## Referrals

`GET /api/referrals`. Public links already seen: `https://fomies.family/?ref=<hex>`.
