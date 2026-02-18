# Git Commit Strategy

This document explains how we organize our commits to make them easy to review and learn from.

## Why Small, Focused Commits Matter

### For Pull Request Reviews
- ✅ Easier to review one change at a time
- ✅ Reviewers can approve/reject specific parts
- ✅ Faster feedback cycles
- ✅ Easier to spot issues

### For Learning
- ✅ Each commit teaches one concept
- ✅ Clear progression from simple to complex
- ✅ Easy to understand what changed and why
- ✅ Can review commits one-by-one

### For Project History
- ✅ Clear history of how project evolved
- ✅ Easy to find when a feature was added
- ✅ Can revert specific changes if needed

## Separation of Concerns

Each commit should have a **single, clear purpose**.

### Good Examples ✅
- "Add directory structure"
- "Add Ansible configuration files"
- "Add LICENSE file"

### Bad Examples ❌
- "Add all files" - Too vague
- "Setup project and add docs" - Two things
- "WIP" - Unclear

## Our Commit Strategy for Phase 1

### Commit 1: Directory Structure
**Files:** Empty directories with .gitkeep
**Why first:** Foundation that everything builds on

### Commit 2: Ansible Configuration
**Files:** ansible.cfg, galaxy.yml
**Why together:** Both are Ansible-specific config

### Commit 3: Git Configuration
**Files:** .gitignore
**Why separate:** Git-specific, not Ansible

### Commit 4: License
**Files:** LICENSE
**Why separate:** Legal/licensing is distinct

### Commit 5: README
**Files:** README.md
**Why separate:** User-facing documentation

### Commit 6: Implementation Plan
**Files:** IMPLEMENTATION_PLAN.md
**Why separate:** Planning documentation

### Commits 7-9: Documentation
**Files:** Various docs/*.md files
**Why separate:** Each doc has different purpose

## Commit Message Format

```
<short summary (50 chars or less)>

<detailed explanation (72 chars per line)>
- Why this change is needed
- What it does
- How it helps beginners

<references if needed>
```

## How to Review Commits

### For Reviewers
1. Review commits in order
2. Check commit message explains "why"
3. Verify files match stated purpose
4. Approve or request changes per commit

### For Learners
```bash
# See all commits
git log --oneline

# Review specific commit
git show <commit-hash>

# See what changed
git diff <commit>^..<commit>
```

## Benefits

**For Pull Requests:**
- Small, focused changes easier to review
- Can discuss specific commits
- Easier to identify issues

**For Learning:**
- Progressive complexity
- Each commit is a lesson
- Clear narrative arc

**For Maintenance:**
- Easy to understand evolution
- Can cherry-pick specific commits
- Clear history for debugging

## Summary

✅ **Small commits** - One purpose each
✅ **Logical order** - Build from foundation up
✅ **Clear messages** - Explain what and why
✅ **Reviewable** - Easy to review one at a time
✅ **Learnable** - Each commit teaches something

This makes the project accessible to beginners!
