# Firmware reverse-engineering tools reference

The skills themselves are documentation and do not install software. Install the tools below on the analysis machine before using the bundle.

## Required command-line tools

These commands are used directly by the skill workflows:

| Command | Used for | Typical package |
|---|---|---|
| `rg` | Fast recursive source, web, and sink searches | `ripgrep` |
| `grep` | Portable fallback when `rg` is unavailable | `grep` / system package |
| `file` | Identifying firmware, ELF, object, archive, and shared-library formats | `file` |
| `strings` | Extracting printable strings and string offsets | `binutils` |
| `nm` | Inspecting symbols in objects and archives | `binutils` |
| `readelf` | Inspecting ELF headers, sections, symbols, and relocations | `binutils` |
| `objdump` | Disassembly and relocation-aware inspection | `binutils` |
| `sha256sum` | Hashing comparable binaries and artifacts | `coreutils` |
| POSIX shell | Running the documented command sequences | `bash` or another POSIX-compatible shell |

`grep` is a fallback, not an additional requirement if `rg` is installed. `strings`, `nm`, `readelf`, and `objdump` are normally supplied by the same GNU Binutils package.

## Example installation commands

Package names vary by distribution. These are reference commands for common systems; use the equivalent packages for the user's platform.

### Debian or Ubuntu

```sh
sudo apt update
sudo apt install ripgrep binutils file coreutils grep bash
```

### Fedora

```sh
sudo dnf install ripgrep binutils file coreutils grep bash
```

### Arch Linux

```sh
sudo pacman -S ripgrep binutils file coreutils grep bash
```

### macOS with Homebrew

```sh
brew install ripgrep binutils coreutils grep bash
```

macOS normally includes `file` and a BSD `strings`; Homebrew GNU packages may install versioned commands such as `gstrings`, `gnm`, `greadelf`, `gobjdump`, and `gsha256sum`. Prefer GNU Binutils when analyzing MIPS firmware, and check the installed command names with `command -v`.

## MIPS-specific considerations

The MIPS skill documents:

```sh
objdump -Dr -b elf32-little -m mips:isa32 artifact.o
```

The local `objdump` must support MIPS disassembly. If the host Binutils build does not, install a MIPS-capable cross-Binutils package supplied by the distribution, commonly named similar to `binutils-mipsel-linux-gnu`, or build/use a toolchain appropriate to the firmware's ABI. Verify with:

```sh
objdump -i | grep -i mips
```

For a cross-prefixed tool, substitute its command where appropriate, for example `mipsel-linux-gnu-objdump`.

## Optional tools for broader firmware work

These are not invoked by the skill definitions but are useful when following their recommended manual next steps:

| Tool | Typical use |
|---|---|
| `binwalk` | Firmware container and embedded-filesystem identification/extraction |
| `unsquashfs` / `mksquashfs` | SquashFS rootfs extraction and inspection |
| `7z` | Handling common firmware/archive containers |
| `qemu-mipsel` or `qemu-user-static` | User-mode execution experiments for compatible MIPS binaries |
| `gdb-multiarch` | Debugging and breakpoint-based validation across architectures |
| `strace` | Observing system calls during compatible dynamic tests |
| `radare2` or `Ghidra` | Interactive disassembly and reverse engineering |

Optional tools often require architecture, libc, kernel, device, or filesystem emulation setup. Their presence does not prove that a firmware binary can run safely or correctly.

## Compatibility checks

Run these before starting an analysis:

```sh
for tool in rg file strings nm readelf objdump sha256sum; do
  command -v "$tool" || echo "missing: $tool"
done
file --version 2>/dev/null || true
objdump --version 2>/dev/null | sed -n '1p' || true
```

On systems without `sha256sum`, use the platform equivalent. For example:

```sh
shasum -a 256 artifact
```

Keep the tool versions and exact commands in the analysis report appendix so results remain reproducible.
