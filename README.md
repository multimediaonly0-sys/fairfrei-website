# Fair&Frei Café — Website + Decap CMS

## What's in here
- `index.html` — the single-page site. It reads text from `content/site.json` at load time, so editing that file (via Decap or by hand) updates the live page with no rebuild step.
- `content/site.json` — all editable text.
- `images/uploads/` — where uploaded photos land.
- `admin/index.html` + `admin/config.yml` — the Decap CMS editing screen, at `yoursite.com/admin`.

## 1. Push to GitHub
Create a new **public** repo, push all these files to the `main` branch, then in
**Settings → Pages**, set source to `main` / root. Your site will be live at
`https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`.

## 2. Set up login for the CMS (the one extra step GitHub Pages needs)
GitHub Pages can't run server code, but Decap's GitHub login needs a tiny server
to complete the OAuth handshake. The standard fix: deploy a **free** open-source
OAuth proxy (one click, no cost) and point Decap at it.

1. Create a GitHub OAuth App: **github.com/settings/developers → New OAuth App**
   - Homepage URL: your GitHub Pages URL
   - Authorization callback URL: `https://YOUR-PROXY-URL/callback`
2. Deploy the proxy — easiest option is Vercel's one-click deploy of
   `vencax/netlify-cms-github-oauth-provider` (works despite the old "netlify-cms" name;
   it's the same Decap CMS project). Set its `OAUTH_CLIENT_ID` and
   `OAUTH_CLIENT_SECRET` env vars from step 1.
3. In `admin/config.yml`, replace:
   - `repo:` with `your-username/your-repo-name`
   - `base_url:` with your deployed proxy's URL
4. Commit and push.

## 3. Edit content
Go to `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/admin/`, log in with the
GitHub account that has write access to the repo, and edit away — text and photos,
no code.

## 4. Give your friend (the non-technical editor) access
Add them as a **Collaborator** on the GitHub repo (Settings → Collaborators).
They'll log into `/admin` with their own GitHub account — no separate password
system to manage.

## Notes
- The hero photo currently points at a placeholder path
  (`/images/uploads/bowl-placeholder.jpg`) — upload the real bowl photo from
  your flyer via the CMS's image field and it'll replace it automatically.
- The map at the bottom is a live embed for "Wengen 15, 87534 Oberstaufen" —
  double-check it pins the right building before launch.
