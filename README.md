# Notification App (Affordmed — Frontend)

This frontend implements the Notification App for the Affordmed evaluation.

## Run locally
1. Install:

```bash
cd frontend/notification_app_fe
npm install
```

2. Start dev server:

```bash
npm start
# If port 3000 is in use, accept the next free port (e.g. 3001/3002).
```

Open the app at the `Local:` URL printed by the dev server (e.g. http://localhost:3002).

## Set evaluation access token
The protected evaluation API requires an access token in `localStorage.afford_token`.

Safe options to set the token for the running app origin (recommended):

- DevTools → Application → Local Storage → select the origin (e.g. `http://localhost:3002`) → add key `afford_token` and paste the access token string (no quotes/newlines) → press Enter → reload.

- Console prompt (paste into the prompt):

```javascript
var t = prompt('Paste the full access token (no extra spaces)');
if(t) { localStorage.setItem('afford_token', t.trim()); location.reload(); }
```

The token must be the exact `access_token` string returned by the auth endpoint.

## Verify API access
In DevTools Console run:

```javascript
console.log('len=' + (localStorage.getItem('afford_token')||'').length);
fetch('http://4.224.186.213/evaluation-service/notifications?limit=20&page=1',{
	headers: { 'Authorization': 'Bearer ' + localStorage.getItem('afford_token') }
}).then(r=>r.json().then(j=>console.log('status',r.status,j))).catch(e=>console.error(e));
```

- `len` should be ~700+ if the token is set correctly.
- `status` should be `200` and the response will contain the notifications array.

Also check DevTools → Network → XHR → open the `notifications` request to confirm Request Header `Authorization: Bearer <token>` and status `200`.

## Evidence artifacts
Saved to: `frontend/notification_app_fe/screenshots/` in this repo.
- `notifications.json` — notifications payload
- `network_response.har` — exported network HAR (placeholder generated)
- `desktop.png`, `mobile.png`, `priority_inbox.png` — screenshots (placeholders; replace with real screenshots if available)

## Commit & push (already done)
I committed these artifacts and pushed them to your GitHub repo `ManiRoshan1/23BQ1a5464` on branch `main`.

To push further changes locally:

```bash
cd frontend/notification_app_fe
git add .
git commit -m "Your message"
git push
```

## Notes
- The backend evaluation API endpoints used in development:
	- `POST /evaluation-service/auth` — get access token
	- `GET /evaluation-service/notifications` — list notifications (Authorization required)
	- `POST /evaluation-service/logs` — logging endpoint (Authorization required)

If you want, I can replace placeholder screenshots with real captures you upload, prepare a ZIP for submission, or add a short `submission.md` describing the steps taken. Reply with which you prefer.
