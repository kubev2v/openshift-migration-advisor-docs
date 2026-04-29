---
title: "release notes v0.11.0"
linkTitle: "release notes v0.11.0"
weight: 2
---

# Migration Planner — combined release notes — `0.11.0`

## Release overview

Across the Migration Planner repositories, new and enhanced capabilities include implement deep inspection flow with VM selection, VDDK/credentials modal, and results column (#297) and Add the option to configure the columns that users wants to see in the VMs table (#310). Repository-specific summaries and commit lists provide additional detail.

Generated from GitHub compare (previous tag → target tag).

## [kubev2v/migration-planner](https://github.com/kubev2v/migration-planner)

- **Compare:** `v0.10.0` → `v0.11.0`
- **Commits:** 31

### Summary

This release emphasizes new and expanded behavior around Update github.com/google/pprof digest to 545e8a4, docs: Include necessary dependencies, and feat: Implement the account endpoint. Additional scope includes Update golang.org/x/exp digest to 746e56f, test: Log the error if it occurs, and docs: fix typos in permissions doc.


### Commits

- `6e9b713` ECOPROJECT-4320 | fix: remove residual constraint created by gorm auto migrate
- `ce0d76d` ECOPROJECT-4320 | fix: remove obsolete name_org_id index
- `a499bd7` NO-JIRA | ci: Bump Active Release Branch to release-0.11
- `495d5b0` Update module github.com/duckdb/duckdb-go-bindings/linux-arm64 to v0.1.24
- `093140d` Update module github.com/duckdb/duckdb-go-bindings/linux-amd64 to v0.1.24
- `78fe7cc` Update module github.com/duckdb/duckdb-go-bindings/windows-amd64 to v0.1.24
- `b7e6a4c` Update github.com/google/pprof digest to 545e8a4
- `4c224c0` NO-JIRA | docs: Include necessary dependencies
- `fa4e0ff` NO-JIRA | feat: Implement the account endpoint
- `fd58915` NO-JIRA | fix: fix migration order
- `e578e60` ECOPROJECT-4339 | fix: handled invalid schema error
- `d6c3029` Update module github.com/go-ini/ini to v1.67.1
- `5095fe1` Update golang.org/x/exp digest to 746e56f
- `047ca5c` Update golang.org/x/exp digest to 746e56f
- `4b186d2` ECOPROJECT-4341 | fix: The vmx is not supporting old versions of vSphere
- `3a680e9` NO-JIRA | test: Log the error if it occurs
- `04f396f` NO-JIRA | docs: fix typos in permissions doc
- `52ef075` NO-JIRA | chore: Add dependabot to validation skip list and chore commit type
- `35046ef` NO-JIRA | feat: Agent-UI repository changes have been detected.
- `a3b9ac8` Build(deps): Bump go.opentelemetry.io/otel/sdk from 1.40.0 to 1.43.0
- `c5f26c9` ECOPROJECT-4284 | feat: [BE] integrate with the Deep inspector's lib
- `783d8b3` ECOPROJECT-4356 | feat: flex params additions
- `66d6b0e` NO-JIRA | test: revert agent to be without deep inspector packages installed
- `52e0dc1` Revert "NO-JIRA | test: revert agent to be without deep inspector packages in…"
- `fce5c74` NO-JIRA | fix: image size overflow
- `fd217e9` ECOPROJECT-4389 | fix: apply over-commit ratios in cluster sizing recommendations
- `e5724fc` NO-JIRA | feat: Agent-UI repository changes have been detected.
- `18961b4` NO-JIRA | feat: Agent repository changes have been detected.
- `0180e8d` NO-JIRA | fix: removing size header
- `0f84f1d` Revert "NO-JIRA | fix: removing size header"
- `53f7dcb` NO-JIRA | fix: revert agent to be without deep inspector packages installed

## [kubev2v/migration-planner-ui-app](https://github.com/kubev2v/migration-planner-ui-app)

- **Compare:** `v0.10.0` → `v0.11.0`
- **Commits:** 20

### Summary

This release emphasizes new and expanded behavior around | feat: add feature-flagged partner management section, | feat: add new status in Agent version column in environments table (#559), and | feat: implement complexity by Disk&OS. Additional scope includes chore: update planner-sdk to latest version that includes changes related with time estimation (#570), | feat: redesign Migration Time Estimation tab, and | refactor: extract the functions formatting the duration in the same place with some basic tests.

- **PRs referenced:** [#559](https://github.com/kubev2v/migration-planner-ui-app/pull/559), [#560](https://github.com/kubev2v/migration-planner-ui-app/pull/560), [#562](https://github.com/kubev2v/migration-planner-ui-app/pull/562), [#565](https://github.com/kubev2v/migration-planner-ui-app/pull/565), [#570](https://github.com/kubev2v/migration-planner-ui-app/pull/570)

### Commits

- `feb971c` NO-JIRA | ci: Bump Active Release Branch to release-0.11
- `759f694` ECOPROJECT-4342 | fix: prevent Renovate from upgrading to compromised axios version
- `0a25ca8` NO-JIRA | fix: solving security-scan issue (#560)
- `6b417b3` ECOPROJECT-4318 | fix: keep RVTools modal inputs disabled until report opens
- `2e32791` ECOPROJECT-4327 | fix: solving issues with stale data in rvTools form (#562)
- `05ec8d6` ECOPROJECT-4325 | feat: add feature-flagged partner management section
- `6f132dd` NO-JIRA | fix: Use stub data on production to display partners features
- `756c8e9` ECOPROJECT-4148 | fix: surface backend validation errors and prevent stale error display in assessment creation
- `927c72b` ECOPROJECT-4148 | fix: extrac duplicted isNameError function into ErrorParse.ts file and replace in the files that are using this code
- `6f1dc7b` ECOPROJECT-4307 | fix: align height for each assumption card in Migration time estimation modal (#565)
- `69a615d` NO-JIRA | fix: differentiate aria labels on proxy fields help buttons
- `f03b8db` NO-JIRA | fix: rename InfastructureOverview to InfrastructureOverview
- `e626338` ECOPROJECT-4304 | feat: add new status in Agent version column in environments table (#559)
- `d419663` ECOPROJECT-4244 | feat: implement complexity by Disk&OS
- `1eb6920` ECOPROJECT-4304 | fix: change 'Downloading OVA' to 'Download pending' to better understanding
- `f16cc32` NO-JIRA | fix: solving security-scan errors
- `f02a040` NO-JIRA | chore: update planner-sdk to latest version that includes changes related with time estimation (#570)
- `05d68c3` ECOPROJECT-4354 | feat: redesign Migration Time Estimation tab
- `2eddbb1` ECOPROJECT-4354 | refactor: extract the functions formatting the duration in the same place with some basic tests
- `6c2a494` ECOPROJECT-4354 | refactor: fixing bugs with pluralization in time duraction

## [kubev2v/assisted-migration-agent](https://github.com/kubev2v/assisted-migration-agent)

- **Compare (assisted-migration-agent, via migration-planner `agent-v2` submodule):** [`0754f12` → `0754f12`](https://github.com/kubev2v/assisted-migration-agent/compare/0754f129bb3907262835f83186d0f651e1b2ea23...0754f129bb3907262835f83186d0f651e1b2ea23) ([migration-planner](https://github.com/kubev2v/migration-planner) tags `v0.10.0` → `v0.11.0`)
- **Commits:** 0

### Summary

This range does not show clear feature-style work in commit subjects alone. See dependency updates, the commit list, and merged PRs for fixes, upgrades, and docs.


_No commits in range (or compare empty)._

## [kubev2v/migration-planner-agent-ui](https://github.com/kubev2v/migration-planner-agent-ui)

- **Compare:** `v0.8.0` → `v0.11.0`
- **Commits:** 15

### Summary

This release emphasizes new and expanded behavior around refactor: Replace local agent-client with published npm package (#296), implement deep inspection flow with VM selection, VDDK/credentials modal, and results column (#297), and Add the option to configure the columns that users wants to see in the VMs table (#310). Further detail is in the commit list below.

- **PRs referenced:** [#291](https://github.com/kubev2v/migration-planner-agent-ui/pull/291), [#296](https://github.com/kubev2v/migration-planner-agent-ui/pull/296), [#297](https://github.com/kubev2v/migration-planner-agent-ui/pull/297), [#298](https://github.com/kubev2v/migration-planner-agent-ui/pull/298), [#299](https://github.com/kubev2v/migration-planner-agent-ui/pull/299), [#301](https://github.com/kubev2v/migration-planner-agent-ui/pull/301), [#302](https://github.com/kubev2v/migration-planner-agent-ui/pull/302), [#303](https://github.com/kubev2v/migration-planner-agent-ui/pull/303), [#304](https://github.com/kubev2v/migration-planner-agent-ui/pull/304), [#305](https://github.com/kubev2v/migration-planner-agent-ui/pull/305), [#306](https://github.com/kubev2v/migration-planner-agent-ui/pull/306), [#307](https://github.com/kubev2v/migration-planner-agent-ui/pull/307), [#308](https://github.com/kubev2v/migration-planner-agent-ui/pull/308), [#309](https://github.com/kubev2v/migration-planner-agent-ui/pull/309), [#310](https://github.com/kubev2v/migration-planner-agent-ui/pull/310)

### Commits

- `89df0c2` refactor: Replace local agent-client with published npm package (#296)
- `089f46e` chore(deps): update dependency vite to v8 (#291)
- `ea70985` feat: implement deep inspection flow with VM selection, VDDK/credentials modal, and results column (#297)
- `181955a` fix: solving issues with inventory downloading (#302)
- `1415d07` chore(deps): update registry.access.redhat.com/ubi9/nginx-124 docker digest to 5f74c82 (#298)
- `12c9c49` chore(deps): update registry.access.redhat.com/ubi9/nodejs-24-minimal docker digest to 4a92f2e (#299)
- `589e028` chore(deps): update dependency node to v24 (#301)
- `7048aa2` chore(deps): update dependency @types/node to v25.5.2 (#303)
- `c1f3a3d` chore(deps): update dependency minimatch to v10.2.5 (#304)
- `48d4abb` chore(deps): update dependency typescript to v6 (#305)
- `e66b27f` chore(deps): update dorny/paths-filter action to v4 (#306)
- `f7c2532` chore(deps): Bump lodash from 4.17.23 to 4.18.1 (#307)
- `531fee6` chore(deps-dev): Bump vite from 8.0.3 to 8.0.5 (#308)
- `c9a2071` feat: Add the option to configure the columns that users wants to see in the VMs table (#310)
- `3f554f7` fix: ECOPROJECT-4145 - align overlapping elements and content not aligned (#309)
