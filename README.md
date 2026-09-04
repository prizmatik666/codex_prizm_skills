# codex_prizm_skills

Portable backups of custom Codex skills, including a complete firmware reverse-engineering toolkit.

## Firmware reverse-engineering package

The [`firmware-reverse-eng-skill/`](firmware-reverse-eng-skill/) package contains 12 coordinated Codex skills for moving from raw firmware evidence to a conservative, reproducible security report.

It covers:

- Binary and native-code analysis for MIPS/uClibc firmware
- Web UI, CGI, route-table, XREF, and call-graph reconstruction
- Browser cryptography, authentication/session state, and configuration provenance
- Embedded protocol and TDDP/control-plane reconstruction
- Risk-pattern triage and firmware-version differential analysis
- Safe runtime validation with bounded, read-only defaults
- Evidence-backed reporting, templates, dependency guidance, and case organization

The package is useful for analysts who need to preserve provenance, connect source/rootfs/web/native artifacts, separate confirmed evidence from hypotheses, and identify the smallest safe next validation step.

See [`firmware-reverse-eng-skill/README.md`](firmware-reverse-eng-skill/README.md) for the complete inventory, installation instructions, usage guidance, and workflow.
