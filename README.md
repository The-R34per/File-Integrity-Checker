## File Integrity Checker

A lightweight Python tool for generating cryptographic hashes of files and directories.  
Supports multiple hashing algorithms, single‑file checks, directory‑wide scans, and ignore patterns to skip unnecessary or noisy files.

---

## Features

- Check the integrity of a single file or an entire directory
- Supports multiple hashing algorithms:
  - MD5
  - SHA1
  - SHA256
  - SHA512
- Ignore patterns to skip:
  - Cache folders
  - Temporary files
  - Logs
  - Virtual environments
  - Git metadata
  - Node modules
- No external dependencies — pure Python

---

## How It Works

The tool computes a cryptographic hash for each file using the selected algorithm.  
Hashes can be used to:

- Detect tampering  
- Verify file integrity  
- Monitor changes over time  
- Validate downloaded files  

Ignore patterns prevent hashing files that naturally change often (logs, caches, etc.).

---

## Ignore Patterns

The following patterns are skipped automatically:

- pycache
- *.log
- *.tmp
- .git
- venv
- node_modules

These prevent false positives and reduce noise during scans.

---

## Usage

Run the script:

```bash
python FileChecker.py
```

You will be prompted to:

1. Choose between:
   - Single file check
   - Directory check

2. Select a hashing algorithm:
   - MD5
   - SHA1
   - SHA256
   - SHA512

3. Enter the file or directory path.

The tool will output the hash for each processed file.

---

## Example Output:

```bash
File: /path/to/example.txt
SHA256 Hash: 3a7bd3e2360a3d...

File: /path/to/project/main.py
SHA512 Hash: 91f2c9b1a4d0...
```

---

## Requirements

- Python 3.6+

No external libraries are required.

---

## License

File Integrity Checker © 2026 by The-R34per is licensed under CC BY-SA 4.0. To view a copy of this license, visit https://creativecommons.org/licenses/by-sa/4.0/
