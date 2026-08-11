# reposplit
Document the new repo split

## Strategy

Proper planning prevents piss poor performance. Keep it simple, stupid.

- **Fat repos are being phased out.** Investigation showed real, and in
  places diverging, code duplication between the fat repos and the
  standalone repos they were supposed to feed (e.g. `RepoForge`'s
  Android app source is byte-identical to `metabuilder/frontends/repoforge`,
  while other pairs like `SDL3CPlusPlus` vs `metabuilder/frontends/gameengine`
  have already forked apart). Rather than reconciling that drift, the plan
  is to move to lots of small, single-purpose repos and retire the fat
  repos once nothing of value is left in them.
- **No git history hacks.** Moving code out of a fat repo into its small
  repo is plain file copy/edit + a normal commit in the destination repo —
  no `git filter-repo`, `subtree split`, or other history-rewriting tools.
- **Dev-time merging.** Since day-to-day development benefits from having
  everything in one working tree, the plan is to build an argparse-based
  Python script that assembles the small repos into a combined dev
  workspace on demand (source of truth stays in each small repo; the
  workspace is just a local convenience view). Mechanism (symlinks vs.
  copy vs. git worktree/subtree) and where it reads the repo → mount-path
  mapping from (a dedicated config file vs. the tables below) are still
  open — TODO once decided.

### Fat Repos

- https://github.com/johndoe6345789/metabuilder
- https://github.com/johndoe6345789/next_extra_primary
- https://github.com/johndoe6345789/businessplanner

### Medium weight repos

- https://github.com/johndoe6345789/pyracms_core

### Single repos (these may need code merging in from fat ones)

- https://github.com/johndoe6345789/low-code-react-app-b
- https://github.com/johndoe6345789/SDL3CPlusPlus
- https://github.com/johndoe6345789/snippet-pastebin
- https://github.com/johndoe6345789/WizardMerge
- https://github.com/johndoe6345789/MetalOS
- https://github.com/johndoe6345789/winejs
- https://github.com/johndoe6345789/RevolutionaryWayToServeUpReactApps
- https://github.com/johndoe6345789/workforce-pay-bill-p
- https://github.com/johndoe6345789/strategy-execution-p
- https://github.com/johndoe6345789/docker-swarm-termina
- https://github.com/johndoe6345789/nexus-command
- https://github.com/johndoe6345789/RepoForge
- https://github.com/johndoe6345789/CaproverForge
- https://github.com/johndoe6345789/BlockWar
- https://github.com/johndoe6345789/AutoMetabuilder
- https://github.com/johndoe6345789/SparkOS
- https://github.com/johndoe6345789/typthon
- https://github.com/johndoe6345789/m3
- https://github.com/johndoe6345789/codegen_studio
- https://github.com/johndoe6345789/code_editor
- https://github.com/johndoe6345789/email_client
- https://github.com/johndoe6345789/dbal
- https://github.com/johndoe6345789/media_center
- https://github.com/johndoe6345789/geocities-app
- https://github.com/johndoe6345789/testing
- https://github.com/johndoe6345789/gamification
- https://github.com/johndoe6345789/social
- https://github.com/johndoe6345789/ai-chat
- https://github.com/johndoe6345789/content-service
- https://github.com/johndoe6345789/search
- https://github.com/johndoe6345789/analytics
- https://github.com/johndoe6345789/notifications
- https://github.com/johndoe6345789/ecommerce
- https://github.com/johndoe6345789/gdpr
- https://github.com/johndoe6345789/legal-team
- https://github.com/johndoe6345789/market-research
- https://github.com/johndoe6345789/risk-assessment
- https://github.com/johndoe6345789/startup-types
- https://github.com/johndoe6345789/accelerators
- https://github.com/johndoe6345789/organisations
- https://github.com/johndoe6345789/cli
- https://github.com/johndoe6345789/exploded-diagrams
- https://github.com/johndoe6345789/storybook
- https://github.com/johndoe6345789/dockerterminal-backend
- https://github.com/johndoe6345789/metabuilder-scripts
- https://github.com/johndoe6345789/design-system
- https://github.com/johndoe6345789/platform-core
- https://github.com/johndoe6345789/mojo
- https://github.com/johndoe6345789/packages
- https://github.com/johndoe6345789/object-store
- https://github.com/johndoe6345789/plugin-registry
- https://github.com/johndoe6345789/components
- https://github.com/johndoe6345789/hooks
- https://github.com/johndoe6345789/icons
- https://github.com/johndoe6345789/interfaces
- https://github.com/johndoe6345789/redux
- https://github.com/johndoe6345789/schemas
- https://github.com/johndoe6345789/scss
- https://github.com/johndoe6345789/translations
- https://github.com/johndoe6345789/types

### Auxillery repos to support the other ones

- https://github.com/johndoe6345789/DeployButton
- https://github.com/johndoe6345789/jenkins
- https://github.com/johndoe6345789/codingstandards
- https://github.com/johndoe6345789/dashy

## Suggested Micro-Repo Names

Based on scanning the directory structure of the three fat repos (`packages/`, `frontends/`, `libraries/`, `services/`, `shared/`), here's which existing entries from the Single repos list above look like they map to which source folders. Where nothing existing fits, the proposed name is just the literal name of the source folder — no invented branding.

### From `metabuilder`

| Existing name | Source paths |
| --- | --- |
| RepoForge | `frontends/repoforge` *(confirmed byte-identical Android app source — not the package registry, see `goodpackagerepo` below)* |
| goodpackagerepo | `frontends/packagerepo` *(confirmed byte-identical, already in sync)*, `packages/package_manager`, `packages/package_validator`, `packages/github_tools` *(not yet migrated)* |
| SparkOS | `libraries/sparkos` |
| SDL3CPlusPlus | `frontends/gameengine`, `packages/arcade_lobby` |
| snippet-pastebin | `frontends/pastebin`, `packages/screenshot_analyzer` |
| docker-swarm-termina | `frontends/dockerterminal` |
| low-code-react-app-b | `packages/form_builder`, `css_designer`, `theme_editor`, `component_editor`, `schema_editor`, `ui_json_script_editor` |
| AutoMetabuilder | `libraries/workflow`, `packages/workflow_editor`, `frontends/workflowui` *(now the whole app, 2026-08-11 — see note below)*, `packages/workflowui-*` |
| typthon | `scripts/python`, `scripts/*.py` |
| cadquerywrapper | `libraries/cadquerywrapper` |
| pcbgenerator | `libraries/pcbgenerator` *(confirmed near-identical, already in sync)* |
| CaproverForge | `frontends/caproverforge` *(confirmed byte-identical, already in sync)* |
| pyracms_forum | `packages/forum_forge`, `social_hub`, `irc_webchat` |

No existing name fit these, so the proposed name is just the literal name of the source folder itself. **Created and populated 2026-08-11** — each was pushed to GitHub with the listed source paths copied in as-is.

| Repo (now created) | Source paths |
| --- | --- |
| `m3` | `libraries/components`, `icons`, `scss`, `hooks`, `types`, `redux`, `interfaces`, `schemas`, `translations` |
| `codegen_studio` | `packages/codegen_studio`, `frontends/codegen` |
| `code_editor` | `packages/code_editor`, `nerd_mode_ide` |
| `email_client` | `packages/email_client`, `smtp_config`, `services/smtprelay`, `frontends/emailclient` *(added 2026-08-11)* |
| `dbal` | `packages/database_manager`, `dbal_core`, `dbal_demo`, `frontends/dbal`, `libraries/dbal` |
| `media_center` | `packages/media_center`, `stream_cast`, `services/media_daemon`, `services/radio`, `frontends/discjockey` |
| `geocities-app` | `packages/geocities-app` |
| `testing` | `packages/api_tests`, `smoke_tests`, `testing`, `system_critical_flows`, `e2e/` |
| `cli` | `frontends/cli` *(created 2026-08-11)* |
| `exploded-diagrams` | `frontends/exploded-diagrams` *(created 2026-08-11)* |
| `storybook` | `frontends/storybook` *(created 2026-08-11)* |

### From `next_extra_primary` ("Nextra") and `businessplanner` ("LaunchPad")

These two share an almost identical `services/` layout — LaunchPad appears to be built on the Nextra template plus its own strategy/business domains.

| Existing name | Source paths |
| --- | --- |
| nexus-command | `auth*`, `sso`, `users*`, `api-keys`, `audit`, `rate-limit`, `feature-flags`, `i18n`, `database`, `orm-models`, `migrate-service`, `migration-runner`, `job-queue`, `cron`, `infra*`, `platform-service`, `service-host`, `drogon-host`, `http-filters`, `manager-cli`, `portal`, `status-page`, `backup`, `object-store` |
| RevolutionaryWayToServeUpReactApps | `shared/` (components, hooks, icons, interfaces, redux, schemas, scss, storybook, theme, constants), `services/design-system` |
| strategy-execution-p (businessplanner only) | `hoshin`, `okr`, `pdca`, `pivot`, `decisions`, `weekly-review`, `scoping`, `kpi` |
| workforce-pay-bill-p (businessplanner only) | `financials`, `xero`, `zelt` |
| pyracms_core *(medium-weight repo, not a Single repo)* | `wiki`, `comments*`, `polls` |
| pyracms_gallery | `gallery` |
| pyracms_article | `blog` |

No existing name fit these either. **Created and populated 2026-08-11**, sourced from `next_extra_primary` except the businessplanner-only rows, which came from `businessplanner`:

| Repo (now created) | Source paths |
| --- | --- |
| `gamification` | `gamification*`, `badges`, `leaderboards`, `levels`, `streaks`, `xp` |
| `social` | `social*` |
| `ai-chat` | `ai-chat`, `ai-service` |
| `content-service` | `media-service`, `image`, `video`, `pdf`, `content-service` |
| `search` | `search*`, `elasticsearch` |
| `analytics` | `analytics*`, `api-documentation` |
| `notifications` | `notifications*`, `email`, `webhooks`, `imap-sync` |
| `ecommerce` | `ecommerce`, `commerce-service` |
| `gdpr` *(businessplanner only)* | `gdpr` |
| `legal-team` *(businessplanner only)* | `legal-team` |
| `market-research` *(businessplanner only)* | `market-research` |
| `risk-assessment` *(businessplanner only)* | `risk-assessment` |
| `startup-types` *(businessplanner only)* | `startup-types` |
| `accelerators` *(businessplanner only)* | `accelerators` |
| `organisations` *(businessplanner only)* | `organisations` |

`BlockWar`, `WizardMerge`, `MetalOS`, and `winejs` didn't obviously map to any source folder in these three repos.

## Migration Status — `metabuilder/frontends/`

First pass at actually migrating code (not just mapping names) from `metabuilder/frontends/*`, 2026-08-11.

**Trimmed 2026-08-11.** Every folder below has a confirmed destination, so `metabuilder/frontends/` now only contains `cli`, `nextjs`, and `qt6` — kept because metabuilder actively uses them as part of its own multi-frontend showcase. Everything else was removed from the fat repo.

**Done — clean copy, no conflict:**
- `caproverforge`, `frontends/packagerepo`, `libraries/pcbgenerator` were already byte-identical (or near-identical) to `CaproverForge`, `goodpackagerepo`, `pcbgenerator` — nothing to migrate, already in sync.
- `frontends/emailclient` added to `email_client`.
- `frontends/repoforge`'s `portal/` folder (the one piece not already in `RepoForge`) added to `RepoForge`.
- `frontends/cli`, `frontends/exploded-diagrams`, `frontends/storybook` — no existing match, created as new repos `cli`, `exploded-diagrams`, `storybook`.

**Resolved 2026-08-11 — merged newer into older.** For every diverged pair, `metabuilder`'s copy had the more recent commit date (as recent as Aug 10) vs. the standalone repos (dating back to Jan/Jul). Did an overlay merge: metabuilder's files overwrite matching paths, new files get added, nothing unique to the destination repo was deleted.

| Source | Existing repo | metabuilder last touched | destination last touched (pre-merge) |
| --- | --- | --- | --- |
| `frontends/dockerterminal` | `docker-swarm-termina` | 2026-08-07 | 2026-07-21 |
| `frontends/gameengine` | `SDL3CPlusPlus` | 2026-06-25 | 2026-01-16 |
| `frontends/pastebin` | `snippet-pastebin` | 2026-08-08 | 2026-01-21 |
| `frontends/postgres` | `postgres` | 2026-08-08 | 2026-01-16 |
| `frontends/qt6` | `CPlusPlusQT6Skel` (corrected from an earlier wrong `pcbgenerator` guess) | 2026-08-03 | 2026-07-21 |

**Resolved 2026-08-11:**
- `frontends/workflowui` → is now `AutoMetabuilder`'s app (confirmed: workflow UI *is* the same product as AutoMetabuilder's AI-powered SDLC workflow tool). First attempt overlay-copied it onto the repo root, colliding with the existing `backend/`+`frontend/` app (two parallel apps, two `package.json`s). Reverted with `git revert`, redid it, then went further: only one app should exist, so the old `backend/`+`frontend/` was removed entirely and workflowui's content promoted to the repo root as the sole app.
- `frontends/nextjs` → **stays in `metabuilder`**, not migrated — it's the actual MetaBuilder platform UI itself, along with the admin/auth/dashboard packages it renders (`packages/admin*`, `ui_auth`, `ui_login`, `ui_permissions`, `role_editor`, `user_manager`, `audit_log`, `dashboard`, `nav_menu`, `ui_header/footer/home/intro/pages`, `notification_center`, `config_summary`).

**Audited all 6 merges for the same "two apps" problem (2026-08-11).** Checking beyond the top level (matching entry points, build configs) found it wasn't isolated to AutoMetabuilder:
- `SDL3CPlusPlus`, `postgres`, `snippet-pastebin` — clean. Only one entry point / build config each; the small additions (`postgres.py`, `pastebin.py`) are legitimate same-app management scripts, not a second app.
- `CPlusPlusQT6Skel` — **had it too.** The merge interleaved metabuilder's `src/*.cpp` files into the same `src/` folder as the original skeleton's own `main.cpp`/`greeter.*`/`qml_curses_frontend.*`/`qml_parser.*`, and the new `CMakeLists.txt` only built the metabuilder side — orphaning the original's files and their tests. Reverted, removed the old skeleton's implementation and its now-dead tests, kept metabuilder's version as the sole app (kept non-conflicting tooling like `python/`, `third_party/`, `dev_tool.py`).
- `docker-swarm-termina` — **partially had it.** `frontend/` was a clean same-app merge (kept). `backend/` was not: metabuilder's `dockerterminal` backend is C++/Drogon, while this repo's real backend is a substantial, tested Python app (17 test files — auth, websockets, docker client, etc.). Unlike the other two, discarding a working tested implementation isn't a call to make unilaterally, so `backend/` was reverted out of `docker-swarm-termina`. Since `metabuilder/frontends/` needed trimming and this C++ backend had nowhere else to go, it now has its own repo: **`dockerterminal-backend`**.

## Migration Status — `packages/`, `libraries/`, `services/` cleanup pass

Before trimming `frontends/`, checked the remaining "Existing name" matches from the tables above that had never actually been migrated (only proposed). Several turned out to be wrong matches entirely, and most of the plausible ones already have *newer* content than the fat repo — so nothing was merged into them:

- **Confirmed already in sync, no action needed:** `cadquerywrapper` ← `libraries/cadquerywrapper`, `SparkOS` ← `libraries/sparkos` (both byte-identical).
- **Wrong matches — not the same product, don't merge:** `typthon` (it's a CPython interpreter fork, not a home for `scripts/python`), `nexus-command` (a React "Atomic Component Framework," not backend auth/infra services), `RevolutionaryWayToServeUpReactApps` (a codegen/project-generation tool, not a shared UI kit).
- **Destination is newer than the fat repo — nothing to merge in:** `workforce-pay-bill-p`, `strategy-execution-p`, `pyracms_core`, `pyracms_gallery`, `pyracms_article` (all 2 weeks–2.5 months newer than their `businessplanner`/`next_extra_primary` counterparts). `low-code-react-app-b` is only hours newer and its `packages/` don't structurally match `form_builder`/`css_designer`/etc. anyway.
- **Not yet checked:** `packages/package_manager`, `package_validator`, `github_tools` → `goodpackagerepo`.

These weren't touched — no clean "newer wins" case to act on, and the wrong matches need real destinations decided separately rather than forced.

## Migration Status — `metabuilder/libraries/` (2026-08-11)

Following the same "wrong match → new repo" rule applied to `frontends/`:

- **New repos created** for content with no real existing match: `mojo` (Mojo language compiler/tooling), `metabuilder-scripts` (replaces the wrong `typthon` match), `design-system` (replaces the wrong `RevolutionaryWayToServeUpReactApps` match — this is `next_extra_primary/shared/` + `services/design-system`), `platform-core` (replaces the wrong `nexus-command` match — `next_extra_primary/services/{auth,sso,users,api-keys,audit,rate-limit,feature-flags,i18n,database,orm-models,migrate-service,migration-runner,job-queue,cron,infra,platform-service,service-host,drogon-host,http-filters,manager-cli,portal,status-page,backup,object-store}`).
- **Merged into existing repos:** `libraries/qml` → `CPlusPlusQT6Skel` (its QML component library). `libraries/workflow` + `packages/workflow_editor` → `AutoMetabuilder` (previously only *mapped* to it in the tables above, never actually copied — fixed now).
- **`metabuilder/libraries/` emptied entirely** — every one of its 16 folders now has a confirmed home (the rest were already-synced matches: `cadquerywrapper`, `components`→`m3`'s split repos, `dbal`, `pcbgenerator`, `sparkos`, etc.)

## Migration Status — `metabuilder/packages/` (2026-08-11)

Bundled the remaining 68 packages (everything not already migrated to `codegen_studio`, `code_editor`, `email_client`, `dbal`, `media_center`, `geocities-app`, `testing`, or `AutoMetabuilder`) into one new repo, **`packages`**, rather than splitting each into its own repo — a deliberate simpler pass here rather than atomizing further.

**`metabuilder/packages/` is now empty.** One open dependency risk worth noting: the admin/auth/dashboard packages (`admin`, `ui_auth`, `ui_login`, `ui_permissions`, `role_editor`, `user_manager`, `audit_log`, `dashboard`, `nav_menu`, `ui_header/footer/home/intro/pages`, `notification_center`, `config_summary`) moved out with this batch even though `frontends/nextjs` — which renders them — stays in `metabuilder`. That coupling may need reconciling (e.g. nextjs pulling them back in as a dependency) rather than being a clean split.

## Migration Status — `metabuilder/services/` (2026-08-11)

`media_daemon` and `radio` were already migrated to `media_center`; `smtprelay` was already migrated to `email_client`. `object-store` and `plugin-registry` had no clear existing match (a `storage-*` repo family exists but wasn't confirmed to align — one candidate is completely empty, others unverified), so each got its own new repo rather than guessing. **`metabuilder/services/` is now empty.**

`metabuilder` now only has `frontends/{cli,nextjs,qt6}` left from its original domains — everything else has been split out.

## Progress Tracking

Tracks the actual split work: which fat repo (source) is feeding which single repo (destination), and where that migration stands.

<!--
TODO: fill in the real source -> destination pairs and current status below.
Only you know which fat repo's code is landing in which single repo, and
how far along each one is — that mapping isn't recoverable from the repo
list above. Suggested status values: Not started / In progress / Done.
-->

| Source (fat repo) | Destination (single repo) | Status |
| --- | --- | --- |
| metabuilder | TODO | Not started |
| next_extra_primary | TODO | Not started |
| businessplanner | TODO | Not started |
