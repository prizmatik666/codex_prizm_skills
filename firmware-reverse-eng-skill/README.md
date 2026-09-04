# Firmware reverse-engineering skill bundle

This directory is a portable backup of the custom firmware reverse-engineering skills. It is self-contained: each skill includes its Codex instructions and its `agents/openai.yaml` interface descriptor, with companion references for repeatable analysis and reporting.

## What this package provides

The skills work as a coordinated analysis pipeline rather than a single-purpose scanner. Together they help an analyst:

- Identify firmware formats, architectures, filesystems, symbols, relocations, and disassembly targets.
- Connect web pages and browser-side transforms to HTTP/CGI handlers and native dispatch paths.
- Reconstruct packet framing, cryptographic boundaries, authentication state, configuration persistence, and indirect control flow.
- Find and rank dangerous sinks without overstating reachability or exploitability.
- Compare firmware versions, design bounded runtime checks, and preserve evidence for every conclusion.
- Produce a structured report that another analyst can reproduce and audit.

## Install for a fresh Codex

From the repository root, copy the twelve skill directories into the user's Codex skills directory:

```sh
mkdir -p "$HOME/.codex/skills"
cp -R firmware-reverse-eng-skill/firmware-report-writer \
      firmware-reverse-eng-skill/firmware-risk-pattern-audit \
      firmware-reverse-eng-skill/firmware-web-cgi-triage \
      firmware-reverse-eng-skill/mips-uclibc-static-triage \
      firmware-reverse-eng-skill/browser-crypto-protocol-reconstruction \
      firmware-reverse-eng-skill/embedded-auth-session-state-analysis \
      firmware-reverse-eng-skill/embedded-protocol-reconstruction \
      firmware-reverse-eng-skill/firmware-differential-security-analysis \
      firmware-reverse-eng-skill/embedded-runtime-validation-safety \
      firmware-reverse-eng-skill/tddp-control-plane-audit \
      firmware-reverse-eng-skill/embedded-config-state-provenance \
      firmware-reverse-eng-skill/firmware-xref-callgraph-reconstruction \
      "$HOME/.codex/skills/"
```

The skills are then available by name and are also automatically relevant when a task matches their descriptions. Restart or refresh the Codex session if the skill list is cached.

Before analysis, review [`TOOLS.md`](TOOLS.md) for the command-line dependencies and optional firmware tooling.

For a repeatable engagement, use [`WORKFLOW.md`](WORKFLOW.md), keep inputs in the layout described by [`CASE_LAYOUT.md`](CASE_LAYOUT.md), and start reports from [`REPORT_TEMPLATE.md`](REPORT_TEMPLATE.md).

## Included skills

- `firmware-report-writer` — turns reverse-engineering notes into conservative, auditable reports.
- `firmware-risk-pattern-audit` — triages risky command, file, string, upload, restore, NVRAM, and CGI patterns.
- `firmware-web-cgi-triage` — maps extracted web UI references to compiled CGI/httpd routes and identifies hidden or mismatched endpoints.
- `mips-uclibc-static-triage` — analyzes MIPS little-endian uClibc ELF artifacts, symbols, relocations, and execution models.
- `browser-crypto-protocol-reconstruction` — traces browser transforms, challenge-response, and encrypted request envelopes.
- `embedded-auth-session-state-analysis` — maps native login/session state, bindings, replacement, and expiry.
- `embedded-protocol-reconstruction` — reconstructs binary packet formats, protocol crypto, and dispatch tables.
- `firmware-differential-security-analysis` — isolates security-relevant changes across firmware versions.
- `embedded-runtime-validation-safety` — designs bounded, evidence-preserving runtime tests with safe defaults.
- `tddp-control-plane-audit` — reconstructs proprietary UDP/TCP control planes and authorization boundaries.
- `embedded-config-state-provenance` — traces factory, runtime, persistent, and reset configuration state.
- `firmware-xref-callgraph-reconstruction` — resolves stripped-binary XREFs, tables, callbacks, and source-to-sink paths.

## Reference materials

- [`TOOLS.md`](TOOLS.md) — required commands, package-install examples, MIPS-capable Binutils, and optional tooling.
- [`WORKFLOW.md`](WORKFLOW.md) — end-to-end evidence-first operating checklist.
- [`CASE_LAYOUT.md`](CASE_LAYOUT.md) — recommended separation of original inputs, extracted artifacts, evidence, tests, and reports.
- [`REPORT_TEMPLATE.md`](REPORT_TEMPLATE.md) — reusable report structure with endpoint, function, confidence, and risk tables.
- `firmware-report-writer/references/` — references installed alongside the report-writing skill.
- `mips-uclibc-static-triage/references/TOOLS.md` — dependency reference available alongside the MIPS skill.

## How to use the skills

Invoke a skill by name when the task is specialized, or let Codex select it from the skill description. Supply the firmware image, extracted rootfs, source tree, binaries, captures, or comparison images relevant to the task. Keep original inputs immutable and place generated output in a separate case directory.

Useful combinations include:

- Static native analysis: `mips-uclibc-static-triage` + `firmware-xref-callgraph-reconstruction`.
- Web management surface: `firmware-web-cgi-triage` + `browser-crypto-protocol-reconstruction` + `embedded-auth-session-state-analysis`.
- Protocol/control plane: `embedded-protocol-reconstruction` + `tddp-control-plane-audit`.
- Persistence/reset behavior: `embedded-config-state-provenance`.
- Security triage: `firmware-risk-pattern-audit` + `firmware-differential-security-analysis`.
- Live confirmation: `embedded-runtime-validation-safety`, after static analysis and explicit authorization.
- Final deliverable: `firmware-report-writer` with the supplied report template.

## Typical workflow

1. Preserve provenance: record device/version, scope, hashes, architecture, tool versions, and artifact boundaries.
2. Establish the layout: identify partitions, rootfs, web content, httpd/CGI artifacts, libraries, and source-tree counterparts.
3. Triage native code with `mips-uclibc-static-triage`; use `firmware-xref-callgraph-reconstruction` for stripped or indirect paths.
4. Map the web surface with `firmware-web-cgi-triage`; add browser crypto and auth/session skills when applicable.
5. Reconstruct protocol, configuration, or control-plane behavior with the specialized skills when present.
6. Audit sinks and compare versions using `firmware-risk-pattern-audit` and `firmware-differential-security-analysis`.
7. Apply `embedded-runtime-validation-safety` before any live validation, using the smallest authorized read-only test.
8. Produce the final evidence-backed report with `firmware-report-writer` and preserve commands, offsets, hashes, and unresolved questions.

The skills are intentionally conservative. A string, symbol, route, packet acceptance, or frontend transform is not proof of reachability, authentication, authorization, persistence, or exploitability without artifact linkage and visible data flow.

## Bundle contents

See [`MANIFEST.md`](MANIFEST.md) for the inventory and source provenance. No firmware samples or third-party binaries are included in this backup; analysis inputs remain separate from the skill definitions.
