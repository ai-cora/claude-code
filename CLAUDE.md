# Claude Code Contributions

This repository contains bug reports, patches, and tools for [Claude Code](https://github.com/anthropics/claude-code).

## Creating Issues

See [docs/issues/creating.md](docs/issues/creating.md) for the full guide on creating and organizing issues.

## Issue Directory Structure

Each issue should be in its own directory under `issues/`:

```
issues/
└── issue-name/
    ├── README.md      # Quick overview and file index
    ├── ISSUE.md       # Full issue text (copy/paste ready)
    ├── minimal-repro.sh    # Minimal reproduction script
    └── ...            # Supporting files (screenshots, test harnesses, etc.)
```

## Markdown Conventions

- **Line breaks**: Use two trailing spaces at the end of a line to create a line break (for adjacent lines that should render separately)
