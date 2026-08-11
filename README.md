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
| AutoMetabuilder | `frontends/nextjs` shell, `packages/admin*`, `ui_auth`, `ui_login`, `ui_permissions`, `role_editor`, `user_manager`, `audit_log`, `dashboard`, `nav_menu`, `ui_header/footer/home/intro/pages`, `notification_center`, `config_summary`, `libraries/workflow`, `packages/workflow_editor`, `frontends/workflowui`, `packages/workflowui-*` |
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

**Done — clean copy, no conflict:**
- `caproverforge`, `frontends/packagerepo`, `libraries/pcbgenerator` were already byte-identical (or near-identical) to `CaproverForge`, `goodpackagerepo`, `pcbgenerator` — nothing to migrate, already in sync.
- `frontends/emailclient` added to `email_client`.
- `frontends/repoforge`'s `portal/` folder (the one piece not already in `RepoForge`) added to `RepoForge`.
- `frontends/cli`, `frontends/exploded-diagrams`, `frontends/storybook` — no existing match, created as new repos `cli`, `exploded-diagrams`, `storybook`.

**Needs a decision before touching — destination already has substantial, independently-evolved content that a blind copy would corrupt:**

| Source | Existing repo | Why it needs a decision |
| --- | --- | --- |
| `frontends/dockerterminal` | `docker-swarm-termina` | Diverged fork — different docs, CAPROVER deployment scripts, different file set |
| `frontends/gameengine` | `SDL3CPlusPlus` | Heavily diverged — destination is 508M vs 199M source, its own package/profile structure |
| `frontends/nextjs`, `frontends/workflowui` | `AutoMetabuilder` | Likely the wrong match entirely — `AutoMetabuilder`'s real README says it's "an AI-powered tool designed to integrate with the metabuilder SDLC workflow," not a platform/workflow-UI shell |
| `frontends/pastebin` | `snippet-pastebin` | Heavily diverged — destination is 65M vs 17M source, extensively built out on its own |
| `frontends/postgres` | `postgres` | Destination is a completely different, real Next.js/Drizzle app ("Postgres with Web UI"), not a Python dashboard |
| `frontends/qt6` | `CPlusPlusQT6Skel` (corrected from an earlier wrong `pcbgenerator` guess) | Diverged — same general idea (Qt6 skeleton) but different file structure on each side |

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
