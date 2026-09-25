# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

This is the **skills and libraries repo** for the Amara Bay build (companion to
`myatgthu/lastone`; both repos work on `main`).
It contains no application code: only curated catalogs (`LIBRARIES.md`,
`ECOMMERCE-STACK.md`, `HOUSING-FINANCE-RESEARCH.md`, `MOBILE-APP-STACK.md`,
`AGENT-SKILLS.md`) and adopted and custom Claude skills under `skills/*/SKILL.md`.

Rules that matter here:

- **Skill format**: each skill is `skills/<name>/SKILL.md` with YAML frontmatter
  (`name` matching the directory, non-empty `description`). Quote any description
  containing a colon; the frontmatter must parse with a standard YAML parser.
- **Vendored skills**: copy the upstream skill dir verbatim (keep upstream em-dashes;
  the em-dash rule below applies only to our own text). Copy the source LICENSE into the
  vendored dir when it has none of its own. Record the repo, path, commit, and licence in
  the matching catalog.
- **Skill precedence**: see [AGENT-SKILLS.md](./AGENT-SKILLS.md) ("Precedence when skills
  overlap"): `karpathy-guidelines` wins over `ponytail` on asking, scope, and tests;
  `caveman` never applies to repo files or customer-facing copy.
- **Expansion policy (owner instruction)**: never rely only on existing skills. When a
  capability is missing, research the ecosystem first (the gap analysis in
  ECOMMERCE-STACK.md shows the method), adopt an external skill if one genuinely
  covers it, and build here only for real gaps. Re-survey at each build phase.
- **Catalog hygiene**: entries marked with a check were fetched and verified; unmarked
  entries came from search. Keep that distinction honest. `LIBRARIES.md` is refreshed
  by a scheduled job; do not hand-edit it in bulk.
- **Cross-references**: skills point into `lastone/docs/*` by path (the specs live
  there, the operating procedure lives here). Keep both sides working when renaming.
- **Never use em-dashes** in anything new (owner instruction, 2026-08-24). One logical
  change per commit. **All work on `main`** (owner decision 2026-08-25). Push with
  `git push -u origin main`, retrying network failures up to 4 times with 2s/4s/8s/16s
  backoff.
