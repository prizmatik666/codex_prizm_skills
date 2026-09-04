# Bundle manifest

This manifest records the files that belong to the firmware skill backup.

| Path | Purpose |
|---|---|
| `README.md` | Fresh-user installation, included skills, and workflow |
| `MANIFEST.md` | Bundle inventory and provenance |
| `TOOLS.md` | External command-line dependencies and installation reference |
| `WORKFLOW.md` | End-to-end read-only analysis checklist |
| `CASE_LAYOUT.md` | Recommended artifact and evidence directory layout |
| `REPORT_TEMPLATE.md` | Reusable conservative firmware-analysis report template |
| `BUNDLE_VERSION` | Backup version and provenance marker |
| `firmware-report-writer/SKILL.md` | Report-writing instructions |
| `firmware-report-writer/agents/openai.yaml` | Codex display metadata and default prompt |
| `firmware-report-writer/references/` | Workflow, case-layout, report-template, and tools references |
| `firmware-risk-pattern-audit/SKILL.md` | Risk-pattern audit instructions |
| `firmware-risk-pattern-audit/agents/openai.yaml` | Codex display metadata and default prompt |
| `firmware-web-cgi-triage/SKILL.md` | Web/CGI route-triage instructions |
| `firmware-web-cgi-triage/agents/openai.yaml` | Codex display metadata and default prompt |
| `mips-uclibc-static-triage/SKILL.md` | MIPS/uClibc static-triage instructions |
| `mips-uclibc-static-triage/agents/openai.yaml` | Codex display metadata and default prompt |
| `mips-uclibc-static-triage/references/TOOLS.md` | MIPS/static-analysis dependency reference |
| `browser-crypto-protocol-reconstruction/SKILL.md` | Browser crypto and request-pipeline reconstruction |
| `browser-crypto-protocol-reconstruction/agents/openai.yaml` | Codex display metadata |
| `browser-crypto-protocol-reconstruction/references/analysis-checklist.md` | Browser crypto analysis worksheet |
| `embedded-auth-session-state-analysis/SKILL.md` | Native authentication/session-state tracing |
| `embedded-auth-session-state-analysis/agents/openai.yaml` | Codex display metadata |
| `embedded-protocol-reconstruction/SKILL.md` | Binary protocol and dispatch reconstruction |
| `embedded-protocol-reconstruction/agents/openai.yaml` | Codex display metadata |
| `firmware-differential-security-analysis/SKILL.md` | Cross-version security patch comparison |
| `firmware-differential-security-analysis/agents/openai.yaml` | Codex display metadata |
| `embedded-runtime-validation-safety/SKILL.md` | Bounded runtime validation guardrails |
| `embedded-runtime-validation-safety/agents/openai.yaml` | Codex display metadata |
| `tddp-control-plane-audit/SKILL.md` | Proprietary control-plane audit workflow |
| `tddp-control-plane-audit/agents/openai.yaml` | Codex display metadata |
| `embedded-config-state-provenance/SKILL.md` | Configuration/default/persistence provenance workflow |
| `embedded-config-state-provenance/agents/openai.yaml` | Codex display metadata |
| `firmware-xref-callgraph-reconstruction/SKILL.md` | Stripped-firmware XREF and indirect call-graph workflow |
| `firmware-xref-callgraph-reconstruction/agents/openai.yaml` | Codex display metadata |

The twelve skill directories are backups of the corresponding local Codex skills. Their `SKILL.md` and `agents/openai.yaml` files are copied verbatim from the installed skill definitions; the bundle documentation is maintained here.

## Operational assumptions

- The fresh user's Codex installation loads skills from `$HOME/.codex/skills` (or an equivalent configured skills directory).
- Firmware-analysis commands documented by the skills (`file`, `strings`, `nm`, `readelf`, `objdump`, `sha256sum`, and `rg`) are available on the analysis machine.
- The analyst supplies firmware/source/rootfs artifacts separately.
- Analysis is read-only by default; destructive or state-changing testing requires explicit authorization.
