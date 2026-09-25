# GLOBAL BUILD / CI / COMPUTE POLICY

**Scope:** repositories owned by `Sharkecho`

**Purpose:** prevent accidental waste of private GitHub Actions quota, avoid unnecessary local heavy builds,
and route genuinely compute-heavy builds to appropriate free public GitHub-hosted standard runners.

---

## 1. Mandatory classification before creating CI/build files

Before creating or changing any of the following:

- `.github/workflows/*.yml`
- build scripts
- firmware / ROM / kernel workflows
- APK packaging workflows
- scheduled CI
- runner configuration
- build cache / artifact configuration

classify the workload first.

### Class A — lightweight control/software logic

Examples:

- Centore-Bridge / SmallBrain
- Country Bridge / Control Bridge
- Python control plane
- agent orchestration
- memory / state / policy / workflow logic
- ordinary unit/integration tests that do not require cloud compute

Default policy:

- **No automatic GitHub-hosted runner on push/PR unless there is a demonstrated need.**
- Prefer local incremental tests and affected regression only.
- Do not spend private-repository hosted-runner minutes just to duplicate local verification.
- Do not move these projects into the public build farm merely because public runners are free.

### Class B — heavy compilation/build

Examples:

- MT3000 / OpenWrt
- router firmware
- phone kernel
- Android ROM
- large APK builds
- SDK / toolchain builds
- cross-compilation
- firmware image generation

Default policy:

- Keep the real source/product repository private.
- Prefer a **public build-only repository** for workflows and non-sensitive build inputs when safe.
- Use GitHub standard hosted runners (`ubuntu-latest`, `windows-latest`) for public free compute.
- Build artifacts may be public only if they contain no private source, secrets, or sensitive configuration.

---

## 2. Cost rules

Without explicit owner approval:

- Do **not** enable paid GitHub Actions overage.
- Do **not** add paid Larger Runners.
- Do **not** add paid third-party cloud runners.
- Do **not** change a private source repository to public.
- Do **not** use Self-hosted Runner as a substitute for public cloud compute when the reason for cloud build is insufficient local performance.
- Do **not** start expensive full builds when an incremental/package-only build can satisfy the task.

Goal:

> Same verified result with the least time, least compute, least token use, lowest cost, and lowest risk.

---

## 3. Public build farm security boundary

A public build repository must not become a copy of a private source repository.

Allowed:

- workflow YAML
- build scripts
- public build configuration
- public patches intentionally approved for release
- dependency manifests
- reproducibility metadata
- hashes / manifests
- approved public binaries

Forbidden unless explicitly approved:

- private application/source tree
- private control algorithms
- credentials / tokens / keys
- private server/device configuration
- private evidence or raw execution logs
- personal paths/data
- secrets embedded in artifacts
- debug output that reveals private source/content

Public logs should expose only the minimum necessary build/verification information.

---

## 4. Trigger policy

Heavy public builds should normally use explicit/manual or trusted triggers.

Do not allow untrusted pull requests to obtain private credentials or private-source access.

For expensive builds:

- prefer `workflow_dispatch`;
- use concurrency controls;
- cancel superseded runs when safe;
- cache reusable toolchains/dependencies;
- use incremental/package-only builds before full firmware/ROM rebuilds.

---

## 5. Project examples

| Project type | Default compute policy |
| --- | --- |
| Centore-Bridge / SmallBrain | Local/incremental verification; no routine hosted cloud build |
| Country Bridge / Control Bridge | Local/incremental verification |
| MT3000 / OpenWrt | Public build-only repo + free standard GitHub-hosted runner |
| Phone kernel / ROM | Public build-only repo + free standard GitHub-hosted runner when safe |
| Android APK heavy build | Public build-only repo + free standard runner when safe |
| Small scripts/docs | No cloud build |

---

## 6. Agent rule

Any Agent, Codex, Copilot, Worker, automation, or human modifying a repository under this account must:

1. read the project-local `AGENTS.md` if present;
2. apply this global policy as the default;
3. classify the workload before changing CI/build infrastructure;
4. avoid automatic paid or quota-consuming compute unless explicitly approved;
5. preserve private source and secrets;
6. prefer incremental, reusable, cached, and parallel-safe execution;
7. stop and report `COMPUTE_POLICY_REVIEW_REQUIRED` if classification is unclear.

Project-local explicit rules override this document when they are stricter or more specific.
