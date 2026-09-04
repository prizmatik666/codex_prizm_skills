# Recommended analysis case layout

Use a separate case directory for each firmware version or device. Keep the original evidence immutable and put generated results elsewhere.

```text
case-name/
├── README.md                 # scope, device/version, authorization, case notes
├── inputs/
│   ├── original/             # immutable firmware/source inputs
│   └── hashes.sha256         # hashes of original inputs
├── extracted/
│   ├── firmware/             # unpacked partitions/containers
│   └── rootfs/               # extracted root filesystem, including www/
├── source/                   # source tree, if available; keep separate from rootfs
├── binaries/                # selected httpd, CGI, ELF, object, and archive files
├── evidence/
│   ├── strings/
│   ├── symbols/
│   ├── relocations/
│   ├── disassembly/
│   └── route-maps/
├── tests/                    # explicitly authorized dynamic-test inputs/results
└── reports/                 # reports and addenda
```

Recommended case README fields:

- Device, model/SKU, firmware version, and region
- Acquisition source and date
- Authorization/scope and test restrictions
- Input hashes and extraction tool versions
- Architecture, endianness, ABI, and suspected libc
- Differences between source and deployed rootfs artifacts
