# reposplit
Document the new repo split

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

Based on scanning the directory structure of the three fat repos (`packages/`, `frontends/`, `libraries/`, `services/`, `shared/`), here's which existing entries from the Single repos list above look like they map to which source folders. Clusters with no obvious existing-name fit are left unassigned rather than guessing a new name.

### From `metabuilder`

| Existing name | Source paths |
| --- | --- |
| RepoForge | `frontends/repoforge`, `frontends/packagerepo`, `packages/package_manager`, `packages/package_validator`, `packages/github_tools` |
| SparkOS | `libraries/sparkos` |
| SDL3CPlusPlus | `frontends/gameengine`, `packages/arcade_lobby` |
| snippet-pastebin | `frontends/pastebin`, `packages/screenshot_analyzer` |
| docker-swarm-termina | `frontends/dockerterminal` |
| low-code-react-app-b | `packages/form_builder`, `css_designer`, `theme_editor`, `component_editor`, `schema_editor`, `ui_json_script_editor` |
| AutoMetabuilder | `frontends/nextjs` shell, `packages/admin*`, `ui_auth`, `ui_login`, `ui_permissions`, `role_editor`, `user_manager`, `audit_log`, `dashboard`, `nav_menu`, `ui_header/footer/home/intro/pages`, `notification_center`, `config_summary` |
| typthon | `scripts/python`, `scripts/*.py` |

**Unassigned:** `libraries/workflow` + `packages/workflow_editor` + `frontends/workflowui` + `packages/workflowui-*` (workflow engine); `libraries/components`, `icons`, `scss`, `hooks`, `types`, `redux`, `interfaces`, `schemas`, `translations` (M3 component library); `packages/codegen_studio`, `code_editor`, `nerd_mode_ide` (code-gen IDE); `packages/email_client`, `smtp_config`, `services/smtprelay` (email client); `packages/database_manager`, `dbal_core`, `dbal_demo`, `frontends/dbal`, `libraries/dbal` (DB admin); `libraries/cadquerywrapper`, `pcbgenerator`, `frontends/qt6` (CAD/PCB); `packages/media_center`, `stream_cast`, `services/media_daemon`, `services/radio`, `frontends/discjockey` (media/radio); `packages/forum_forge`, `social_hub`, `irc_webchat`; `frontends/caproverforge`; `packages/geocities-app`; `packages/api_tests`, `smoke_tests`, `testing`, `system_critical_flows`, `e2e/` (QA harness).

### From `next_extra_primary` ("Nextra") and `businessplanner` ("LaunchPad")

These two share an almost identical `services/` layout — LaunchPad appears to be built on the Nextra template plus its own strategy/business domains.

| Existing name | Source paths |
| --- | --- |
| nexus-command | `auth*`, `sso`, `users*`, `api-keys`, `audit`, `rate-limit`, `feature-flags`, `i18n`, `database`, `orm-models`, `migrate-service`, `migration-runner`, `job-queue`, `cron`, `infra*`, `platform-service`, `service-host`, `drogon-host`, `http-filters`, `manager-cli`, `portal`, `status-page`, `backup`, `object-store` |
| RevolutionaryWayToServeUpReactApps | `shared/` (components, hooks, icons, interfaces, redux, schemas, scss, storybook, theme, constants), `services/design-system` |
| strategy-execution-p (businessplanner only) | `hoshin`, `okr`, `pdca`, `pivot`, `decisions`, `weekly-review`, `scoping`, `kpi` |
| workforce-pay-bill-p (businessplanner only) | `financials`, `xero`, `zelt` |

**Unassigned:** `gamification*`, `badges`, `leaderboards`, `levels`, `streaks`, `xp`; `social*`, `comments*`, `blog`, `wiki`, `polls`, `gallery`; `ai-chat`, `ai-service`; `media-service`, `image`, `video`, `pdf`, `content-service`; `search*`, `elasticsearch`, `analytics*`, `api-documentation`; `notifications*`, `email`, `webhooks`, `imap-sync`; `ecommerce`, `commerce-service`; (businessplanner only) `gdpr`, `legal-team`, `market-research`, `risk-assessment`, `startup-types`, `accelerators`, `organisations`.

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
