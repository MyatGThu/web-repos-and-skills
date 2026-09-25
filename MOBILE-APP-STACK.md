# Mobile App Stack: React Native skills from Vercel and Expo

Skills adopted for the planned **React-based mobile app** (one codebase, shipped to both
the Play Store and the App Store). Stack assumption: **Expo (React Native) with EAS Build**,
which is the standard way to ship a React codebase to both stores without maintaining two
native projects by hand.

**Last updated:** 2026-09-25. The nine Vercel skills and the eight Expo skills below were
cloned directly from GitHub and are vendored under `skills/` in this repo, so every entry is
verified (fetched, frontmatter parsed, directory name matches the declared `name:` field).

> **Discovery note.** On 2026-09-25 the `skills.sh` registry was reachable from this network
> and `npx skills find <query>` returned real results. That does not retire the fallback:
> still treat an empty result from that CLI on this network as an outage, not an answer, and
> confirm anything it surfaces against the source repo before relying on it.

## Adopted skills

### Vercel skills

| Skill (dir under `skills/`) | Source repo | Path in source | Commit | Licence | Helps you... |
|---|---|---|---|---|---|
| `vercel-react-native-skills` | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | `skills/react-native-skills` | `dd089a8` | MIT (frontmatter; repo has no LICENSE file) | RN and Expo best practices: a rules library covering list performance, native modals, Expo Image, Pressable, Reanimated derived values, monorepo native deps. The core skill for this build. |
| `vercel-react-best-practices` | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | `skills/react-best-practices` | `dd089a8` | MIT (frontmatter; repo has no LICENSE file) | React performance guidelines from Vercel engineering; applies to RN components as much as web. |
| `vercel-composition-patterns` | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | `skills/composition-patterns` | `dd089a8` | MIT (frontmatter; repo has no LICENSE file) | Component APIs that scale: compound components, render props, context, React 19 changes. |
| `writing-guidelines` | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | `skills/writing-guidelines` | `dd089a8` | MIT (frontmatter; repo has no LICENSE file) | Reviewing app copy and docs; in-app microcopy is most of a helper app's UX. |
| `ai-sdk` | [vercel-labs/open-agents](https://github.com/vercel-labs/open-agents) | `.agents/skills/ai-sdk` | `cf865e9` | MIT | Building AI features (the lease-decoder concept needs an LLM behind it). |
| `frontend-design` | [vercel-labs/open-agents](https://github.com/vercel-labs/open-agents) | `.agents/skills/frontend-design` | `cf865e9` | MIT | Distinctive, production-grade interface design; principles carry to native screens. |
| `web-animation-design` | [vercel-labs/open-agents](https://github.com/vercel-labs/open-agents) | `.agents/skills/web-animation-design` | `cf865e9` | MIT | Easing, duration, and reduced-motion judgement; maps to Reanimated and Moti. |
| `emil-design-eng` | [vercel-labs/open-agents](https://github.com/vercel-labs/open-agents) | `.agents/skills/emil-design-eng` | `cf865e9` | MIT | UI polish and the invisible details that make an app feel considered. |
| `code-review` | [vercel-labs/open-agents](https://github.com/vercel-labs/open-agents) | `.agents/skills/code-review` | `cf865e9` | MIT | Reviewing diffs and PRs during the app build. |

### Expo skills (official)

Source: [expo/skills](https://github.com/expo/skills), commit `efa52f0` (2026-09-24). Path
in source is `plugins/expo/skills/<name>`. Licence is MIT: the root LICENSE was copied into
each vendored dir, except `expo-animation`, which ships its own LICENSE (and its own
RECIPES.md) inside the source skill dir, so that copy was kept as-is instead of overwritten.
Note: the `eas-*` skills below describe paid EAS (Expo Application Services) usage, not free
local tooling.

| Skill (dir under `skills/`) | Installs on skills.sh | Size | Helps you... |
|---|---|---|---|
| `expo-router` | 19.2K | 84K | File-based navigation and routing; use when scaffolding and writing screens. |
| `expo-native-ui` | 21.5K | 92K | Native-feeling UI components and controls; use when scaffolding and writing screens. |
| `expo-data-fetching` | 18.8K | 52K | Data fetching and caching patterns for Expo apps; use when scaffolding and writing screens. |
| `expo-animation` | 8.2K | 56K | Motion and gesture animation (same body as emilkowalski's `animate-expo`, so do not also vendor that one). |
| `eas-app-stores` | 15.5K | 88K | `eas.json`, TestFlight and Play Store submission, store metadata. Unattended submit needs an App Store Connect API key. |
| `eas-workflows` | 14.9K | 36K | CI-style build, test and submit workflows on EAS. Ships `scripts/fetch.js`, which GETs the public workflow schema from `api.expo.dev`; no API key needed for that call. |
| `eas-update` | 4.3K | 28K | Over-the-air JS updates without a store resubmission. |
| `expo-upgrade` | 19K | 64K | Expo SDK version bumps and the migration steps that go with them. |

Not vendored: `expo-overview`, a router skill that points at 15 sibling skills, none
vendored here. Some vendored skills name unvendored siblings as see-also: `expo-ui`,
`eas-hosting`, `expo-brownfield`, `expo-dev-client`, `eas-update-insights`. Install the full
upstream set with `npx skills add expo/skills` if one of those is needed later.

**Relation to `vercel-react-native-skills`:** complementary, not overlapping. The Vercel
skill is performance and UI rules for React and React Native components; the Expo skills
above cover routing, native UI primitives, data fetching, and EAS build, submit, and OTA
update mechanics that the Vercel skill does not touch.

## Surveyed and not adopted

From the same two repos, with the reason each was left out:

| Skill | Why not |
|---|---|
| `react-view-transitions` | Web View Transition API only; React Native has no such API. |
| `deploy-to-vercel`, `vercel-cli-with-tokens`, `vercel-optimize` | Web hosting and Vercel billing; a store-distributed mobile app does not deploy this way. |
| `web-design-guidelines` | Audits DOM and CSS specifics that do not exist in RN; the design skills above cover the transferable part. |
| `baseline-ui` | Tailwind-specific checks; only relevant if the app adopts NativeWind, which is undecided. |
| `chat-sdk`, `agent-browser`, `workflow`, `deploy-open-harness`, `plan-mode`, `remove-demo-limits` | Platform bots, browser automation, and harness tooling; nothing to do with this build. |
| `callstackincubator/agent-skills` `react-native-best-practices` | Duplicates the Vercel RN rules already adopted above; 26.9K installs; the skill dir is 6.5M, mostly PNG assets. |
| `designed-by-ai` `design-mobile-apps` | Needs a `SLEEK_API_KEY`, an external paid dependency this repo does not want. |
| `anthropics/skills` `webapp-testing` | Web Playwright testing, not React Native. |

## How these fit the app build

1. **Scaffold and route** with `expo-router`, TypeScript, EAS Build profiles for both stores.
2. **Write screens** with `expo-native-ui` and `expo-data-fetching`, plus
   `vercel-react-native-skills` (lists, images, animations, modals) and
   `vercel-react-best-practices` for render discipline.
3. **Shape the component API** with `vercel-composition-patterns` before the screen count grows.
4. **Design pass** with `frontend-design`, `emil-design-eng`, and `web-animation-design`.
5. **AI features** (lease decoding, plain-language explanations) with `ai-sdk`.
6. **Build and submit** with `eas-workflows` and `eas-app-stores`; ship OTA fixes with
   `eas-update`; bump the SDK with `expo-upgrade`.
7. **Every PR** through `code-review`; every user-facing string through `writing-guidelines`;
   hard bugs and test-first work through `tdd` and `diagnosing-bugs`
   ([AGENT-SKILLS.md](./AGENT-SKILLS.md)).
