# Sharkecho · Global Repository Rules

> **GLOBAL BUILD / CI / COMPUTE POLICY**
>
> This account uses different compute strategies for different project types.
> Before creating or modifying any `.github/workflows/*.yml`, build script, CI job, firmware build,
> APK build, kernel/ROM build, or other compute-heavy automation, read:
>
> **[GLOBAL_BUILD_COMPUTE_POLICY.md](./GLOBAL_BUILD_COMPUTE_POLICY.md)**

## Core rule

### Local / control-plane projects — do NOT waste GitHub hosted compute

Projects such as:

- Centore-Bridge / SmallBrain
- Country Bridge / Control Bridge
- lightweight Python control logic
- orchestration / policy / memory / workflow code

normally **do not require cloud compilation**.

Rules:

- Do not add automatic GitHub-hosted CI merely because CI is available.
- Do not consume private-repository Actions minutes for routine push/PR verification unless explicitly required.
- Prefer local incremental tests / affected regression only.
- Do not add paid or larger runners without explicit approval.

### Heavy build projects — use public free standard GitHub-hosted runners

Projects such as:

- MT3000 / OpenWrt firmware
- phone kernel / ROM
- large Android APK builds
- SDK / cross-compilation / firmware image builds

should preferentially use a **PUBLIC build-only repository** with standard GitHub-hosted runners when the build can be safely separated from private source.

Rules:

- Keep product/source repositories private unless explicitly approved otherwise.
- Public builder repositories contain build workflows/scripts/config only, not private product source.
- Use standard runners such as `ubuntu-latest` / `windows-latest`.
- Do not use paid Larger Runners without explicit approval.
- Never expose secrets, private source, private evidence, credentials, or sensitive logs in public Actions output/artifacts.

## Priority

1. Project-local `AGENTS.md` / explicit project policy has highest priority.
2. This account-level policy is the default when a project has no more specific rule.
3. If unsure whether a workload belongs on GitHub-hosted compute, **do not start the workflow**; mark it for review.

