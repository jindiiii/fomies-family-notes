# 05 — API map

Extracted from shipped `/js/api.js` on 2026-09-30.

## Applicant surface

`/api/session`, `/api/alias`, `POST /auth/x/start`, `/auth/logout`, `/api/tasks`, `POST /api/tasks/check`, `POST /api/telegram/connect`, `POST /api/telegram/confirm`, `/api/interview` plus start/restart/advance/answer/edit-written, `/api/application` plus submit/addresses/review, `/api/case`, `POST /api/clerk/arrival`, `/api/engagement`, `POST /api/engagement/refresh`, `/api/referrals`, `POST /api/scene/step`, `/api/public/notices`, `/api/public/scene-content`.

Unauthenticated `GET /api/tasks` and `GET /api/application` returned 401.

## Admin surface (401 without a grant)

`/admin` itself is 401, not 404. The same JS file knows: access/grants/search, availability, capabilities, cases + reset + export, content draft/import/publish/validate, inbox + mark-read, interactions, notice-assets, notices, office-content, scene-content, tasks + history + telegram-test, test-controls.

Implications: dialogue and notices are CMS-publishable; cases can be exported; someone is expected to read an inbox; test-controls exist behind auth.

Writes send `X-CSRF-Token`. Fetch uses `redirect: error`.
