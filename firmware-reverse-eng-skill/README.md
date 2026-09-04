# Firmware reverse-engineering skill bundle

This directory is a portable backup of the custom firmware reverse-engineering skills. It is self-contained: each skill includes its Codex instructions and its `agents/openai.yaml` interface descriptor.

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

## Typical workflow

1. Use `mips-uclibc-static-triage` to classify binaries and resolve symbols, relocations, and disassembly.
2. Use `firmware-web-cgi-triage` to build the source/rootfs web route map.
3. Use `firmware-risk-pattern-audit` to harvest and rank security-sensitive sinks and flows.
4. Use `firmware-report-writer` to produce the final evidence-backed report.
5. Apply `embedded-runtime-validation-safety` before any live validation.
6. Use `tddp-control-plane-audit`, `embedded-config-state-provenance`, and `firmware-xref-callgraph-reconstruction` when those specialized boundaries are present.

The skills are intentionally conservative. A string, symbol, or route candidate is not a confirmed reachable vulnerability without artifact linkage and visible data flow.

## Bundle contents

See [`MANIFEST.md`](MANIFEST.md) for the inventory and source provenance. No firmware samples or third-party binaries are included in this backup; analysis inputs remain separate from the skill definitions.
