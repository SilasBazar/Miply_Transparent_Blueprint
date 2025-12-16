# MIPLY - Transparent Blueprint

This repo contains a static HTML prototype and a minimal Tailwind-based build pipeline to produce a deployable site for GitHub Pages.

## Quick start

1. Install dependencies:
   ```bash
   npm ci
   ```
   Note (Windows PowerShell): if you see a policy error ("running scripts is disabled"), either run the command in Git Bash/CMD or update PowerShell execution policy for the current user:
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
   ```
2. Build the site (compiles SCSS and generates Tailwind CSS):
   ```bash
   npm run build
   ```
3. For local development, compile SCSS and watch for changes in a separate terminal:
   ```bash
   npm run watch:scss
   ```
   And in another terminal run Tailwind watch to regenerate the dist CSS when `src/css/main.css` changes:
   ```bash
   npm run watch:css
   ```
4. Preview the site by opening `dist/index.html` in a browser after building (the `index.html` file is copied from `src/pages/`).

## Notes
- SCSS partials live in `assets/scss/` and are compiled to `src/css/main.css` before Tailwind processes it into `dist/assets/css/main.css`.
- The GitHub Action `Build and Deploy` runs `npm run build` and deploys `dist/` to the `gh-pages` branch automatically on push to `main`.
- The page uses a small runtime include loader to pull `/includes/header.html` and `/includes/footer.html` at runtime; the workflow copies `src/includes/` into `dist/includes/` so the includes load on GitHub Pages.
- If you prefer a Jekyll-based flow (native GH Pages), we can switch to that and add a small build step for Tailwind in CI.
