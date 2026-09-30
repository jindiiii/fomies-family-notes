# 07 — CMS and admin

`GET /api/public/scene-content` returns `vent`, `idle`, `office` with `{handle}` / `{case}` / `{alias}` tokens. Admin twins draft/validate/publish office and scene packs.

`GET /api/public/notices` returns `{ announcements }` with paper style, label, text, unix `published_at`, optional links, and a mobile image variant.

Observed 2026-09-30: bathroom memo, 52,934 / 43,202 / 9,732 split, weekend notice, morale classified, bell-127 complaint, 100k-views-in-6h traffic report linking the Gud luck post, X sign-in + task-check overload, applications-open notice.

Inbox + mark-read and interactions save/delete exist. `/api/admin/availability` matches `loginEnabled` on session. Public DOM also contains Test controls / Exit test mode strings; treat as preview overlay, not a public cheat menu.
