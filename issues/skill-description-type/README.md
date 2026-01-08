# Skill Description Type Validation Bug

**GitHub Issue**: https://github.com/anthropics/claude-code/issues/XXX
**Status**: Draft
**Severity**: High (CLI unusable)

## Summary

Claude Code crashes with `TypeError: X.description.split is not a function` when a skill's YAML frontmatter has a `description` field that is an array instead of a string.

## Quick Reproduction

```bash
# Creates temp project with bad skill, launches claude, cleans up
d=$(mktemp -d) && mkdir -p "$d/.claude/skills/bad"
echo -e "---\nname: bad\ndescription: [array]\n---\n# Bad" > "$d/.claude/skills/bad/SKILL.md"
cd "$d" && claude; rm -rf "$d"
# Then type / to trigger crash
```

## Files

| File | Description |
|------|-------------|
| [ISSUE.md](ISSUE.md) | Full GitHub issue text |
| [test-harness.sh](test-harness.sh) | Interactive test with cleanup |
| [minimal-repro.sh](minimal-repro.sh) | Minimal 3-line reproduction |
| [suggested-fix.md](suggested-fix.md) | Analysis and fix suggestions |

## Root Cause

Line 3061 in `cli.js` calls `.split(" ")` on description without type checking:

```javascript
descriptionKey: X.description.split(" ").map(...)
```

YAML parses `[text]` as an array, not a string with brackets.

## Suggested Fix

Add Zod validation when loading skill frontmatter:

```javascript
const skillFrontmatterSchema = z.object({
  name: z.string(),
  description: z.string(),  // Validates type
  // ...
});
```
