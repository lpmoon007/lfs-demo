# LFS demo — deploy folder

Static page + one serverless function. Deploy this folder to Vercel as its own project.

```
index.html        the demo page (self-contained: styles, transcripts, fallback answers)
api/coach.js      the live LFS Coach endpoint — holds the case file and the system prompt
vercel.json       function timeout + no-cache on /api
```

## Required

Vercel → Project → Settings → Environment Variables:

| Name | Value | Environments |
|---|---|---|
| `ANTHROPIC_API_KEY` | `sk-ant-...` | Production, Preview, Development |

Optional: `LFS_MODEL` (default `claude-sonnet-4-5`), `LFS_MAX_TURNS` (default `14`).

## Build settings

Framework preset **Other**. Build command **empty**. Output directory **empty**.
No `package.json` and no dependencies — `api/coach.js` uses built-in `fetch`.

## Analytics

Already configured in `index.html`: GA4 `G-M0Q17HCKMM`, Clarity `xp6res7ssv`.

## Behavior if the key is missing

The page still works. `api/coach.js` returns 503, the coach badge flips to **demo mode**, and the
authored fallback answers are served. Nothing errors visibly — but the coach is the point, so
check the badge says **live** after deploying.
