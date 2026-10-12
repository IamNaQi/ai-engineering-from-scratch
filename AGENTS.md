## Cursor Cloud specific instructions

This repository is a lesson curriculum plus the static site in `site/`. Nothing has to stay running for the curriculum checks to pass. There is no database and no product Docker stack (the compose file under `phases/00-setup-and-tooling/07-docker-for-ai/code/` is lesson material).

- Lesson code that imports third-party packages must run with `.venv/bin/python`. The venv is created from `requirements.txt`. PyTorch here is the CPU wheel (`torch` version ends in `+cpu`). `phases/00-setup-and-tooling/01-dev-environment/code/verify.py` reports CUDA as failed; that check is optional and the script still exits 0 when the core checks pass.
- Stdlib contributor checks (`scripts/audit_lessons.py`, `scripts/build_catalog.py`, `scripts/check_readme_counts.py`, `scripts/lesson_run.py`) run with system `python3`. Commands and flags are documented in those scripts and in `.github/workflows/curriculum.yml`.
- `scripts/lesson_run.py --execute` stops each lesson after 10 seconds. `phases/01-math-foundations/10-dimensionality-reduction` exceeds that timeout even when scikit-learn is installed. That is a timeout, not a missing dependency.
- Preview the site with `python3 -m http.server 8080 -d site`. Avoid `node site/build.js` unless you are editing `README.md`, `ROADMAP.md`, or `glossary/terms.md` (see `CONTRIBUTING.md`). A rebuild currently rewrites lesson `lang` fields in `site/data.js`, not only the timestamp, so do not commit that diff unless the source tables actually changed.
- Phase 19 TypeScript capstones are separate npm packages under `phases/19-capstone-projects/*/code/ts/` and have no lockfile. Run `npm install` and `npm test` inside the package you are working on. They are not part of the root dependency refresh.
- `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` are only needed for lessons that call a provider. Audits, the site, and the Phase 1 scripts do not need them.
