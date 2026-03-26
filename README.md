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
- Create a ile Integrity Baseline
- Compare a directory agaisnt a baseline
- Export results to:
  - JSON
  - CSV
- Provide a summary-only output
- Quiet mode for automation
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

## Menu Modes

This tool provides two modes of operation:

### A) MENU MODE (default)
   - Activated when you run the script with NO arguments.
   - Allows checking a single file or an entire directory.
   - Uses your original ASCII-art interface.

To use Menu Mode, run the script without any arguments:
```bash
python FileChecker.py
```
You will see:
- ASCII banner
- Option to check a single file
- Option to check an entire directory
- Option to choose hashing algorithm
This tool is exactly like the previous version.

### B) ADVANCED CLI MODE
   - Activated when you run the script WITH arguments.
   - Enables full baseline creation, comparison, exporting,
     timestamp tracking, permission tracking, summary mode,
     and quiet mode.

To use the Advanced CLI Mode, you can run the script with arguments. 
To find which arguments you would like to use, youcan use -h / --help

```bash
python FileChecker.py --help
```

---

## Arguments


### BASELINE / COMPARE OPTIONS

--baseline DIR
    Create a baseline from the specified directory.

--compare BASELINE.json
    Compare a directory against an existing baseline file.

--dir DIR
    Directory to compare. If omitted, uses the baseline's
    original root directory.

---

### HASHING OPTIONS

--algo {md5, sha1, sha256, sha512}
    Hashing algorithm to use (default: sha256)

---

### OUTPUT OPTIONS

--out FILE
    Output path for baseline JSON when using --baseline.

--json-out FILE
    Write comparison results to a JSON file.

--csv-out FILE
    Write comparison results to a CSV file.

--summary
    Show only a summary of results.

--quiet
    Suppress detailed per-file output.

---

## Baseline Creation

A baseline is a JSON file containing:
- File hashes
- File sizes
- Modified time (mtime)
- Created time (ctime)
- Permissions (mode)
- Owner/group (uid/gid)
- Directory root
- Hashing algorithm used

Create a baseline:
```bash
    python file_integrity_checker.py \
        --baseline /path/to/dir \
        --algo sha256 \
        --out baseline.json
```

If --out is omitted, baseline.json is used automatically.

---

## Comparing Agaisnt a Baseline

Compare the current state of a directory to a baseline:
```bash
    python FileChecker.py \
      --compare baseline.json
```
Compare a different directory (not current dir):
```bash
    python FileChecker.py \
      --compare baseline.json \
      --dir /new/path/to/check
```

---

## Output Modes

A) FULL OUTPUT (default)
    Shows every file and its status.

B) SUMMARY MODE
```bash
python file_integrity_checker.py --compare baseline.json --summary
```
  Example summary:
      unchanged: 120
      modified: 3
      deleted: 1
      new: 2
      meta_changed: 1

C) QUIET MODE
```bash    
python file_integrity_checker.py --compare baseline.json --quiet
```
Only prints summary unless combined with --summary.

D) JSON EXPORT
```bash
python file_integrity_checker.py \
        --compare baseline.json \
        --json-out results.json
```

E) CSV EXPORT
```bash
python file_integrity_checker.py \
        --compare baseline.json \
        --csv-out results.csv
```

---

## Workflow

Step 1: Create a baseline
```bash
python file_integrity_checker.py --baseline /dir --out baseline.json
```

Step 2: Later, compare the directory
```bash
python file_integrity_checker.py --compare baseline.json
```

Step 3: Export results (optional)
```bash
python file_integrity_checker.py \
        --compare baseline.json \
        --json-out results.json \
        --csv-out results.csv
```

Step 4: Use summary mode for quick triage
```bash
python file_integrity_checker.py --compare baseline.json --summary
```

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

## Requirements

- Python 3.6+

No external libraries are required.

---

## Troubleshooting

Problem: "Directory does not exist"
Solution:
    Check your path and ensure it is correct.

Problem: "Baseline file not found"
Solution:
    Ensure the JSON file exists and is readable.

Problem: "Permission denied"
Solution:
    Run with appropriate permissions or exclude restricted folders.

Problem: "Ignored by pattern"
Solution:
    The file or folder matches IGNORE_PATTERNS.

---

## License

File Integrity Checker © 2026 by The-R34per is licensed under CC BY-SA 4.0. To view a copy of this license, visit https://creativecommons.org/licenses/by-sa/4.0/
