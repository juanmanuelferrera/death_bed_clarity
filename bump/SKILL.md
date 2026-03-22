---
name: bump
description: Use when releasing a new version of Kavya - fully autonomous build, version bump, README update, commit, push, and GitHub release with DMG attached. Zero human intervention required.
---

# Bump — Kavya Release

Fully autonomous release pipeline. Run everything without stopping for confirmation.

## Execution Flow

Run all steps sequentially without asking the user. Decide everything autonomously.

### 1. Determine Version

```bash
git log $(git describe --tags --abbrev=0)..HEAD --oneline
```

| Change type | Bump |
|-------------|------|
| New major feature, UI overhaul, breaking change | MINOR (0.X.0) |
| Bug fixes, small improvements, tweaks | PATCH (0.0.X) |

Decide the version yourself based on the commits. Do NOT ask the user.

### 2. Update Version in All 5 Places

Use the Edit tool on each — no manual confirmation:

1. `package.json` — `"version": "X.Y.Z"`
2. `src-tauri/tauri.conf.json` — `"version": "X.Y.Z"`
3. `src-tauri/tauri.conf.json` — `"title": "Kavya X.Y.Z"` (window title in app.windows[0])
4. `src-tauri/Cargo.toml` — `version = "X.Y.Z"`
5. `README.md` — badge `version-X.Y.Z-blue`

### 3. Update README Content

Add any new features/fixes to the appropriate sections. Update the roadmap checklist if items were completed. Match existing formatting style exactly.

### 4. Build

```bash
npm run tauri build
```

Timeout: 10 minutes. Output:
- `src-tauri/target/release/bundle/macos/Kavya.app`
- `src-tauri/target/release/bundle/dmg/Kavya_X.Y.Z_aarch64.dmg`

### 5. Commit and Push

Stage all changed files including `Cargo.lock`, commit, and push in one chained command:

```bash
git add package.json src-tauri/tauri.conf.json src-tauri/Cargo.toml src-tauri/Cargo.lock README.md && git commit -m "vX.Y.Z: Brief description" && git push origin main
```

Commit message style: `v0.14.0: Feature name, other feature`

### 6. Create GitHub Release

```bash
gh release create vX.Y.Z \
  --title "Kavya vX.Y.Z — Short Title" \
  --notes "$(cat <<'EOF'
## What's New

- **Feature** — description

## Download

Download the DMG, open it, drag Kavya to Applications.
Requires macOS and [Claude Code](https://claude.ai/code) for CLI chat mode.
EOF
)" \
  src-tauri/target/release/bundle/dmg/Kavya_*_aarch64.dmg
```

### 7. Update Website & Deploy (kavya-app.com)

Update the website repo at `~/.emacs.d/git_projects/web_kavya/`:

1. **`blog.html`** (DevLog page) — Add a new `<article class="blog-entry">` at the top of `<section class="blog-feed"><div>`, before the previous version's entry. Include date, version title, and 2-3 paragraphs describing what's new.

2. **`features.html`** — Add any new features as `<div class="feature-item">` entries in the appropriate `<details>` accordion section. Update the `<span class="acc-count">` number to match.

3. Commit and push to deploy:
```bash
cd ~/.emacs.d/git_projects/web_kavya && git add blog.html features.html && git commit -m "vX.Y.Z: Blog entry + features update" && git push
```

Pushing deploys the site automatically via Cloudflare Pages. No manual deploy step needed.

### 8. Confirm and Open

```bash
gh release view vX.Y.Z --web
```

This opens the release page in the browser automatically. Done.
