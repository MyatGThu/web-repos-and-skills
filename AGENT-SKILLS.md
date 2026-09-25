# Agent Skills: Workflow and Engineering Skills

Skills that shape how an agent does the work itself (planning, scope discipline,
test-first practice, debugging, terse output) rather than skills about a specific stack.
Companion to [MOBILE-APP-STACK.md](./MOBILE-APP-STACK.md) (Vercel and Expo skills) and
[ECOMMERCE-STACK.md](./ECOMMERCE-STACK.md) (Shopify, Klaviyo, POD). Custom skills for
this business live in [`skills/`](./skills/).

**Last updated:** 2026-09-25.

## Adopted skills

| Skill (dir under `skills/`) | Source repo | Path in source | Commit | Licence (where stated) | Installs on skills.sh | Helps with |
|---|---|---|---|---|---|---|
| `find-skills` | [vercel-labs/skills](https://github.com/vercel-labs/skills) | `skills/find-skills` | `7407f38` | MIT (root LICENSE) | 3.5M | Searches the skills.sh registry (`npx skills find <query>`). Use for searching only: its own step 6 runs `npx skills add <pkg> -g -y` (global install, no confirmation), which bypasses this repo's vendor-and-verify rule. Treat an empty result as an outage, not an answer. |
| `karpathy-guidelines` | [forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills) (skills.sh lists it as `multica-ai/andrej-karpathy-skills`; the forrestchang URL redirects there) | `skills/karpathy-guidelines` | `2c60614` | MIT per frontmatter (no LICENSE file in source) | 37.9K | Think before coding, simplicity first, surgical changes, verify against success criteria. |
| `caveman` | [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) | `skills/caveman` | `2fd153c` | MIT (root LICENSE; `LICENSING.md` lists `skills/` as MIT, the engine dirs are BSL-1.1 and are not vendored) | 537K | Terse output to cut tokens. Vendored `SKILL.md` only, no plugin hooks, so it is opt-in (`/caveman`, "be brief", "less tokens") and stays on for the session once triggered. Its own boundaries keep code, commits, docs, PR text and customer-facing copy in normal prose. "Caveman" is a trademark: keep the vendored copy unchanged. Its README link to `../../README.md` does not resolve here. |
| `ponytail` | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) | `skills/ponytail` | `e3ba2aa` | MIT (root LICENSE) | 64.7K | "Laziest senior dev" solution ladder: reuse existing code, then stdlib, then native platform features, then already-installed deps; fix root causes. |
| `tdd` | [mattpocock/skills](https://github.com/mattpocock/skills) | `skills/engineering/tdd` | `c55ee46` | MIT (root LICENSE) | 961K | Test-first work; triggers only when the user asks for test-first or red-green-refactor. |
| `diagnosing-bugs` | [mattpocock/skills](https://github.com/mattpocock/skills) | `skills/engineering/diagnosing-bugs` | `c55ee46` | MIT (root LICENSE) | 660K | Diagnosis loop for hard bugs and performance regressions. |
| `research` | [mattpocock/skills](https://github.com/mattpocock/skills) | `skills/engineering/research` | `c55ee46` | MIT (root LICENSE) | 558K | Background agent researches primary sources and writes a cited Markdown file into the repo, which fits this repo's verified/unverified catalog rule. |

## Precedence when skills overlap

`karpathy-guidelines` and `ponytail` both push simplicity but conflict in three places.
`karpathy-guidelines` wins on:

- Asking vs assuming when a requirement is unclear: ask, do not assume.
- Scope: do not delete pre-existing dead code unasked.
- Tests: use the project's existing test framework.

`ponytail`'s solution ladder (reuse existing code, then stdlib, then native platform
features, then already-installed deps) still decides which solution to build once those
three points are settled.

`caveman` never applies to repo files, catalogs, commit messages, docs, PR text or
customer-facing copy. Terse mode is for the agent's own working output, not for anything
this repo publishes or anything a customer reads.

## Surveyed and not adopted

| Candidate | Why not |
|---|---|
| caveman-review | Same triggers as the vendored `code-review` skill (already in `skills/`, listed in MOBILE-APP-STACK.md); it changes output format only. |
| caveman-commit | Forces Conventional Commits, which this repo does not use, and drops AI attribution lines unless a user rule keeps them. |
| caveman-compress | Its Python scripts rewrite `CLAUDE.md` and memory files in place through the Anthropic API; out of scope for a catalog repo. |
| ponytail-review | Optional to adopt later: flags over-engineering only, and there is no application code in this repo yet. |
| ponytail-audit | One-off audit report format for application code; nothing to audit here yet. |
| obra/superpowers `test-driven-development` and `systematic-debugging` | Strong alternatives (236K and 270K installs). One skill per role is enough here; `mattpocock/skills` was chosen for both roles. |
| joellewis/finance_skills `lending` | 628 installs; narrow lending-only scope. |
| ailabs-393 `finance-manager` | Last commit 2025-11-11; stale. |
| NomaDamas `real-estate-search` | Korean data only. |

Nothing strong exists for housing and finance research. The method in
[HOUSING-FINANCE-RESEARCH.md](./HOUSING-FINANCE-RESEARCH.md) stands.
