# Pull Request Workflow

This document explains how we use Pull Requests and why they're important.

## Why We Use Pull Requests

**For Beginners:**
- 📚 Learn proper GitHub workflow
- 👀 See how code reviews work
- 💬 Understand review conversations
- 🔄 Experience iterative improvement

**For Code Quality:**
- ✅ Review before merging
- ✅ Run automated checks
- ✅ Catch issues early
- ✅ Ensure standards are met

**For Collaboration:**
- 👥 Multiple reviewers can comment
- 💡 Knowledge sharing
- 📝 Document decisions
- 🤝 Team learns together

## Our PR Strategy

### Each Phase = One PR

- **Phase 1**: Repository skeleton (this PR!)
- **Phase 2**: Module utilities
- **Phase 3**: Events module
- ... and so on

### Why One PR Per Phase?
- ✅ Manageable size
- ✅ Clear scope
- ✅ Focused review
- ✅ Clean history

## PR Workflow

### Step 1: Create Branch
```bash
git checkout main
git pull origin main
git checkout -b phase-2-module-utilities
```

### Step 2: Make Commits
```bash
# Make changes
git add file.py
git commit -m "Add feature" -m "Explanation..."
```

### Step 3: Push Branch
```bash
git push -u origin phase-2-module-utilities
```

### Step 4: Create PR
```bash
gh pr create --title "Phase 2: Module utilities" --body "..."
```

### Step 5: Review Process
- Reviewers comment on code
- Author responds and makes changes
- Push additional commits if needed

### Step 6: Merge
```bash
gh pr merge --merge
```

**We use merge commits** to preserve detailed commit history for learning.

### Step 7: Clean Up
```bash
git checkout main
git pull origin main
git branch -d phase-2-module-utilities
```

## Review Guidelines

### For Reviewers
**Check:**
- ✅ Code follows patterns
- ✅ Good commit messages
- ✅ Clear documentation
- ✅ No security issues

**Be:**
- 👍 Constructive
- 💡 Helpful
- 📚 Educational
- 🤝 Respectful

### For Authors
**When receiving feedback:**
- Listen to concerns
- Ask clarifying questions
- Make requested changes
- Thank reviewers

## Benefits

**For This Project:**
- Each phase reviewed before merging
- Quality gate
- Conversations preserved

**For Beginners:**
- See real code review
- Learn from comments
- Practice collaboration

**For Portfolio:**
- Shows professional workflow
- Demonstrates collaboration
- Clean PR history

## Summary

**Key Takeaways:**
- 🎯 One PR per phase
- 📝 Clear PR descriptions
- 💬 Thoughtful reviews
- ✅ Merge when approved
- 📚 Great learning

This is how professional teams work!

## References

- [GitHub PR Docs](https://docs.github.com/en/pull-requests)
- [GitHub CLI](https://cli.github.com/manual/gh_pr)
- [Code Review Best Practices](https://google.github.io/eng-practices/review/)
