# Scarborough Beach Surf School — rebuild working repo

Working files for the surfschool.com rebuild: a fast static homepage prototype, the full website evaluation (as a live page + Word doc), the rebuild scope, and the local-LLM build prompt.

## What's in here

| File / folder | What it is | Live URL (once Pages is on) |
|---|---|---|
| `index.html` | Fast static homepage prototype (keeps the real TuriTop booking widget) | `https://USERNAME.github.io/REPO/` |
| `evaluation/index.html` | The full evaluation & rebuild scope, rendered as a styled web page | `https://USERNAME.github.io/REPO/evaluation/` |
| `Surf-School-Evaluation.docx` | Same evaluation as a Word document (for printing / the meeting) | downloadable from the repo |
| `Surf-School-Evaluation.md` | Evaluation in Markdown (renders in the GitHub repo view) | — |
| `REBUILD-SPEC.md` | Short technical scope note | — |
| `qwen-prompt.md` | Self-contained prompt to rebuild the homepage on a local model (Qwen 2.5) | — |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is (no Jekyll processing) | — |

> Replace `USERNAME` and `REPO` above with your GitHub username and repository name.

## Publish it (one-time, ~2 minutes)

From this folder, in Terminal:

```bash
git init
git add .
git commit -m "Surf school rebuild: homepage prototype + evaluation"
git branch -M main
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

Then turn on GitHub Pages (this is a settings click only you can make):

1. On GitHub, open the repo → **Settings** → **Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: **main**, folder: **/(root)**. Save.
4. Wait ~1 minute, then your live URLs above will work.

## Pushing changes from now on

Edit any file, then:

```bash
git add .
git commit -m "describe the change"
git push
```

Pages redeploys automatically within a minute or so.

## Notes

- The homepage pulls its photos and the TuriTop booking widget straight from the web, so the live page looks and books exactly like the real thing.
- The booking widget uses the existing TuriTop account (`data-company="S559"`), so no booking/payment migration is involved.
- To regenerate `evaluation/index.html` after editing the Markdown: `pandoc Surf-School-Evaluation.md -s -o evaluation/index.html` (add your styling header as preferred).
