# Firmware reverse-engineering skill bundle

This directory is a portable backup of the custom firmware reverse-engineering skills. It is self-contained: each skill includes its Codex instructions and its `agents/openai.yaml` interface descriptor.

## Install for a fresh Codex

From the repository root, copy the four skill directories into the user's Codex skills directory:

```sh
mkdir -p "$HOME/.codex/skills"
cp -R dir/firmware-report-writer \
      dir/firmware-risk-pattern-audit \
      dir/firmware-web-cgi-triage \
      dir/mips-uclibc-static-triage \
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

## Typical workflow

1. Use `mips-uclibc-static-triage` to classify binaries and resolve symbols, relocations, and disassembly.
2. Use `firmware-web-cgi-triage` to build the source/rootfs web route map.
3. Use `firmware-risk-pattern-audit` to harvest and rank security-sensitive sinks and flows.
4. Use `firmware-report-writer` to produce the final evidence-backed report.

The skills are intentionally conservative. A string, symbol, or route candidate is not a confirmed reachable vulnerability without artifact linkage and visible data flow.

## Bundle contents

See [`MANIFEST.md`](MANIFEST.md) for the inventory and source provenance. No firmware samples or third-party binaries are included in this backup; analysis inputs remain separate from the skill definitions.
