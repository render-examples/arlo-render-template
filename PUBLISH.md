# Publish handoff: arlo-render-template

Do **not** auto-run these unless explicitly asked. Order matters: the Deploy button URL only works after the repo exists **and** `is_template=true`.

## 1. Create and push under render-examples

```bash
cd /Users/ojusave/Desktop/Samples/render-templates/arlo-render-template
git init
git add .
git commit -m "$(cat <<'EOF'
Add Arlo Render gallery template (Zoom RTMS meeting assistant).

Package zoom/arlo as a multi-service Blueprint with projects/environments,
gallery README, and one-click template Deploy button wiring.
EOF
)"

gh repo create render-examples/arlo-render-template --public \
  --source=. --push \
  --description "Arlo Zoom Apps RTMS meeting assistant on Render (one-click template)"
```

## 2. Mark as GitHub template repository

```bash
gh api -X PATCH repos/render-examples/arlo-render-template -f is_template=true
gh api repos/render-examples/arlo-render-template --jq '{url:.html_url, is_template:.is_template}'
```

## 3. Patch Deploy button placeholder

Replace `<TEMPLATE_REPO_SLUG>` → `arlo-render-template` in `README.md`, commit, push.

Canonical Deploy URL:

```
https://render.com/deploy-template/api/github/start?template_repo=arlo-render-template
```

## 4. Optional smoke test

Click the Deploy button, fork into a personal account, Apply with real Zoom credentials (or expect backend crash-loop until Zoom secrets are set), confirm `backend` reaches Live and `/health` responds.

## 5. Gallery submission

Paste [`GALLERY-METADATA.json`](./GALLERY-METADATA.json) into the Render templates submission form. Hero/logo already under `assets/`.
