# Rahul Saka — Personal Portfolio & 21-Tool Developer Workbench

Target GitHub Pages URL: https://itsrahul-saka.github.io/
GitHub Repository: https://github.com/itsrahul-saka/itsrahul-saka.github.io

## What's Inside This Package

- `index.html` — Complete, standalone, single-file static website with all HTML, CSS, JavaScript, all 21 interactive tools (12 Developer Engineering tools + 9 CSE Student Lab tools), light/dark theme persistence, and the exact `rahul-kitten.webp` artwork embedded as a Base64 data URI.
- `README.md` — Deployment and customization instructions.

## How to Upload to GitHub Pages from Android (Single-File Upload)

Because `index.html` embeds its styles, scripts, and the `rahul-kitten.webp` artwork directly inside a single file, you can deploy or update the entire site from an Android phone browser without Git CLI or Node.js:

1. Open Chrome or Firefox on your Android phone and sign in to GitHub: https://github.com/itsrahul-saka/itsrahul-saka.github.io
2. Tap the **+** (Add file) menu near the top of the repository file list and select **Upload files**.
3. Select the standalone `index.html` file from your phone's Downloads folder.
4. Scroll down to **Commit changes**, enter a short commit message (for example, `Deploy portfolio and 21-tool workbench`), choose **Commit directly to the main branch**, and tap **Commit changes**.
5. In repository **Settings -> Pages**, ensure **Source** is set to **Deploy from a branch** (`main` / `/ (root)`). Within 1–2 minutes, your live site will be available at https://itsrahul-saka.github.io/.

## How to Customize Placeholders

Open `index.html` in VS Code or any text editor:
- Search for `SITE_CONFIG` or `[Editable Placeholder` in `index.html` to update the Featured Projects cards or add an optional contact link when ready.
