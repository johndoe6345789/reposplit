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
- https://github.com/johndoe6345789/BlockWar
- https://github.com/johndoe6345789/AutoMetabuilder
- https://github.com/johndoe6345789/SparkOS
- https://github.com/johndoe6345789/typthon

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
| RepoForge | `frontends/repoforge`, `frontends/packagerepo`, `packages/package_manager`, `packages/package_validator`, `packages/github_tools` |
| SparkOS | `libraries/sparkos` |
| SDL3CPlusPlus | `frontends/gameengine`, `packages/arcade_lobby` |
| snippet-pastebin | `frontends/pastebin`, `packages/screenshot_analyzer` |
| docker-swarm-termina | `frontends/dockerterminal` |
| low-code-react-app-b | `packages/form_builder`, `css_designer`, `theme_editor`, `component_editor`, `schema_editor`, `ui_json_script_editor` |
| AutoMetabuilder | `frontends/nextjs` shell, `packages/admin*`, `ui_auth`, `ui_login`, `ui_permissions`, `role_editor`, `user_manager`, `audit_log`, `dashboard`, `nav_menu`, `ui_header/footer/home/intro/pages`, `notification_center`, `config_summary`, `libraries/workflow`, `packages/workflow_editor`, `frontends/workflowui`, `packages/workflowui-*` |
| typthon | `scripts/python`, `scripts/*.py` |

No existing name fit these, so the proposed name is just the literal name of the source folder itself:

| Proposed name (new repo) | Source paths |
| --- | --- |
| `m3` | `libraries/components`, `icons`, `scss`, `hooks`, `types`, `redux`, `interfaces`, `schemas`, `translations` |
| `codegen_studio` | `packages/codegen_studio`, `frontends/codegen` |
| `code_editor` | `packages/code_editor`, `nerd_mode_ide` |
| `email_client` | `packages/email_client`, `smtp_config`, `services/smtprelay` |
| `dbal` | `packages/database_manager`, `dbal_core`, `dbal_demo`, `frontends/dbal`, `libraries/dbal` |
| `cadquerywrapper` | `libraries/cadquerywrapper` |
| `pcbgenerator` | `libraries/pcbgenerator`, `frontends/qt6` |
| `media_center` | `packages/media_center`, `stream_cast`, `services/media_daemon`, `services/radio`, `frontends/discjockey` |
| `forum_forge` | `packages/forum_forge`, `social_hub`, `irc_webchat` |
| `caproverforge` | `frontends/caproverforge` |
| `geocities-app` | `packages/geocities-app` |
| `testing` | `packages/api_tests`, `smoke_tests`, `testing`, `system_critical_flows`, `e2e/` |

### From `next_extra_primary` ("Nextra") and `businessplanner` ("LaunchPad")

These two share an almost identical `services/` layout — LaunchPad appears to be built on the Nextra template plus its own strategy/business domains.

| Existing name | Source paths |
| --- | --- |
| nexus-command | `auth*`, `sso`, `users*`, `api-keys`, `audit`, `rate-limit`, `feature-flags`, `i18n`, `database`, `orm-models`, `migrate-service`, `migration-runner`, `job-queue`, `cron`, `infra*`, `platform-service`, `service-host`, `drogon-host`, `http-filters`, `manager-cli`, `portal`, `status-page`, `backup`, `object-store` |
| RevolutionaryWayToServeUpReactApps | `shared/` (components, hooks, icons, interfaces, redux, schemas, scss, storybook, theme, constants), `services/design-system` |
| strategy-execution-p (businessplanner only) | `hoshin`, `okr`, `pdca`, `pivot`, `decisions`, `weekly-review`, `scoping`, `kpi` |
| workforce-pay-bill-p (businessplanner only) | `financials`, `xero`, `zelt` |
| pyracms_core *(medium-weight repo, not a Single repo)* | `blog`, `wiki`, `comments*`, `polls`, `gallery` |

No existing name fit these either — same rule, proposed name is just the literal source folder name:

| Proposed name (new repo) | Source paths |
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
