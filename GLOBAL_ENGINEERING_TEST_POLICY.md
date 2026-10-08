# GLOBAL ENGINEERING TEST POLICY V1
Scope: all Sharkecho-developed repositories and AI coding Agents
Status: ACTIVE | Approved: 2026-10-08

Canonical detailed implementation guide: `Sharkecho/CodingOS-AgentCanvas/docs/codingos/GLOBAL_TEST_QUALITY_GATES_V1.md`.
This global policy applies to CodingOS/OpenHands, DPC, AI Translator, LiveBrain, LiveOS, MT3000 and all subsequent coding projects, subject to stricter local SSOT rules.

Every change must have bounded acceptance criteria, risk classification, test selection, executed verification evidence, immutable source revision and rollback. Do not represent a source commit or mock test as production verification. Use smallest affected tests first, then boundary-specific integration, reliability, security and release tests. Reuse existing suites; avoid unnecessary repeat and full builds. Simultaneously execute independent tests only when safe; dependent Gates remain serial. Keep private code, secrets, audio, production credentials and raw logs off the public farm.

Adopt a unified catalogue of 18 categories: static/type/lint; unit; boundary/property; API/ABI/FFI contract; module integration; user-black-box; E2E; affected regression; fault recovery; concurrency; load/stress; soak/leak; performance/cost; SAST/SCA/auth/privacy; fuzzing; clean build/deployment; staging/canary/rollback; production smoke/monitoring.

Adopt G0 task/impact/risk plan; G1 module; G2 integration and black-box; G3 reliability/performance/security; G4 release and staging; G5 authorized production smoke. Not every change runs all 18; a test matrix is chosen based on risk, affected boundaries and stage. High-risk AI model/Agent operations additionally require real-model inference, prompt/tool injection and tool-permission validation, data isolation, deterministic fallback and model accuracy tests.

States: NOT_STARTED, RUNNING, PASS, FAIL, BLOCKED, NOT_VERIFIED, WAIVED. No evidence -> NOT_VERIFIED. WAIVED requires accountable owner, expiry, reason and explicit approval. Production and safety critical bypasses cannot be autonomously waived. Source SHA, environment, actual commands, result and run/artifact URL (where non-sensitive) are mandatory for PASS.

Execution ownership: CodingOS/OpenHands Agent Server/SDK executes tests in target workspaces; Canvas displays Gate evidence and task progress; Public-Build-Farm supplies isolated compute where secure and economically justified; each target repository remains the source authority. Changes to frontend-only code do not magically implement SDK execution or enforcement.

The global build/compute policy remains in force. If conflict exists, the stricter security or project-local rule wins.
