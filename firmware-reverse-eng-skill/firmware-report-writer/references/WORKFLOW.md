# Firmware reverse-engineering workflow

This checklist is the operating sequence for the bundled skills. Keep the work read-only until dynamic testing or firmware modification is explicitly authorized.

## 1. Preserve provenance

- Record firmware filename, version, model/SKU, source, acquisition date, and SHA-256.
- Never overwrite the original input. Work from a copy or extracted view.
- Record the host OS, tool versions, and relevant cross-toolchain versions.
- Keep source-tree artifacts and deployed rootfs artifacts in separate evidence groups.

## 2. Establish the artifact map

- Identify the firmware container, partitions, filesystems, bootloader, kernel, rootfs, web files, httpd, CGI objects/archives, and shared libraries.
- Run `file` and relevant ELF inspection commands on each native artifact.
- Record architecture, endianness, ABI, stripped status, and whether each file is an object, executable, shared library, or archive.
- Hash binaries that may be compared; do not assume route or function parity when hashes differ.

## 3. Triage native code

- Use `mips-uclibc-static-triage` for symbols, imports, relocations, disassembly, wrappers, and execution models.
- Resolve external calls through relocation records or PLT/GOT linkage where possible.
- Mark names recovered from strings alone as candidates.
- Distinguish `shell-string`, `argv-based`, and `mixed/unclear` execution per call site.

## 4. Map web and CGI behavior

- Use `firmware-web-cgi-triage` to collect page references, JavaScript-generated routes, form actions, ASP/EJ references, and upload paths.
- Compare visible references against compiled route tables and handler linkage.
- Record hidden/candidate, visible-only, and rootfs-visible mismatches separately.
- Preserve auth gates, model/SKU conditionals, and reachability uncertainty.

## 5. Audit risk patterns

- Use `firmware-risk-pattern-audit` to search command execution, unsafe string handling, temporary files, path construction, upload/restore/upgrade, NVRAM, WPS, and suspicious CGI flows.
- For each candidate, record caller, input source, transformations, sink, artifact, offset/address, and confidence.
- Rank impact and confidence independently. Do not call a candidate exploitable without a supported source-to-sink path.

## 6. Validate selectively

- Propose dynamic tests, emulation, instrumentation, debugger breakpoints, route probes, or filesystem observation only after the static evidence is recorded.
- Isolate devices and avoid tests that alter persistent configuration unless explicitly approved.
- Record test commands, inputs, expected observations, actual observations, and cleanup.

## 7. Write and review the report

- Use `REPORT_TEMPLATE.md` and `firmware-report-writer`.
- Label every result `Confirmed`, `Candidate`, `Hypothesis`, or `Unknown`.
- Include exact artifact names, hashes, offsets/addresses, commands, and limitations.
- Run a final consistency check: every claim should point to evidence, and every uncertainty should remain visible.
