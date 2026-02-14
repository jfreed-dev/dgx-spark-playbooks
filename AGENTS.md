# Repository Guidelines

## Project Structure & Module Organization
- Playbooks live in `nvidia/<slug>/README.md`; use lowercase-kebab slugs that match the directory (for example `nvidia/open-webui/README.md`).
- Supporting scripts and configs belong in `nvidia/<slug>/assets/` (docker-compose files, helper scripts, frontend bundles). Keep executables minimal and document how to use them in the playbook README.
- Shared imagery goes in `src/images/`; link via relative paths instead of embedding binaries in Markdown.
- Do not commit downloaded models or build artifacts—reference upstream sources and download steps instead.

## Build, Test, and Development Commands
- This is a Markdown-first repo; there is no central build. Preview Markdown locally before opening a PR.
- Optional lint: `npx markdownlint-cli2 "**/*.md"` from the repo root if you have Node available.
- Validate compose files and scripts you add: `docker compose -f docker-compose.yml config` or `bash -n ./your-script.sh` within the relevant `assets/` folder.

## Coding Style & Naming Conventions
- Write concise, stepwise instructions with clear headings and a short table of contents that mirror existing playbooks.
- Use fenced code blocks with language hints (`bash`, `yaml`, `python`) and prefer copy/pasteable commands over prose.
- File and directory names stay lowercase-kebab; script names should describe the action (for example `model_download.sh`).
- Keep callouts consistent with existing docs, using blockquotes for `Note`, `Tip`, or `Warning`.

## Testing Guidelines
- Manually run new or changed commands on a DGX Spark (or closest equivalent) and note expected duration or risks.
- For docker-compose changes, run `docker compose config` and a quick `docker compose ps` to ensure services resolve; capture short verification steps in the README.
- If you add frontend assets under `assets/frontend`, run the package’s `npm test`/`npm run lint` when present; otherwise document the manual validation you performed.

## Commit & Pull Request Guidelines
- Follow Conventional Commits (`chore:`, `fix:`, `feat:`); keep subjects imperative and ≤72 characters (e.g., `chore: refresh vllm playbook`).
- PRs should list affected playbooks, summarize manual test steps, and link issues or requests. Include updated screenshots for UI-facing changes in `assets/` and reference them in the README.
- Avoid force-pushing after review; prefer follow-up commits labeled `fix:` or `chore:` for clarity.

## Security & Configuration Tips
- Never commit secrets, tokens, or downloaded model weights. Use placeholders like `YOUR_API_KEY` and point to external download steps.
- Keep scripts idempotent and non-destructive by default; gate destructive actions behind explicit flags or clear warnings.
