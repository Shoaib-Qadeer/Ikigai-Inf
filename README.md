# Inferred Ikigai prototype (v0.1.0)

Three short games plus a multiple-choice check that build an explainable
work-interest and working-style profile for students aged 18+.
All scoring is deterministic and runs in the browser. AI is optional and
only adds a reflection coach.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The whole app: games, self-report, scoring rules, student report, evidence report |
| `api/health.js` | Lets the app detect that AI calls can go through this server |
| `api/ai.js` | Forwards AI requests to an OpenAI-compatible API, so the key never sits in browser code |

The scoring rules live in the `<script id="core">` block of `index.html`.
They are pure functions with no randomness: the same answers always give the
same scores. The design & scoring specification document describes every rule.

## Deploy on Vercel

1. Create a new GitHub repository and add these files.
2. On vercel.com, choose **Add New → Project** and import the repository.
   No build settings are needed: framework preset "Other", no build command.
3. Optional, for AI mode with your own key: in **Settings → Environment
   Variables** add `OPENAI_API_KEY`. Without it, each student can paste their
   own key in AI mode and it is forwarded per request.
4. Optional: `AI_BASE_URL` for another OpenAI-compatible provider, and
   `AI_ALLOWED_MODELS` (comma-separated) to limit which models can be used.

Or from a terminal: `npm i -g vercel`, then `vercel` in this folder.

## Run locally

`npx vercel dev` runs the page and the API routes together.
Opening `index.html` directly works too, but AI mode then calls the
provider straight from the browser.

## What is stored

Nothing on the server. Session data lives in the browser tab until the
student copies or downloads it. Before collecting data from other students,
add consent forms and get your program's ethics review.
