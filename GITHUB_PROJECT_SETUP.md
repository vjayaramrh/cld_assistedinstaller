# GitHub Projects Setup Guide

## Quick Start: Create Your First Project

### Step 1: Create Project via Web UI

1. Go to: https://github.com/vjayaramrh/cld_assistedinstaller/projects
2. Click "Link a project" → "New project"
3. Choose template: **Board** (simple Kanban)
4. Name: "Phase 1: Foundation & Learning Resources"
5. Click "Create"

### Step 2: Customize Columns

Default columns are usually:
- Todo
- In Progress
- Done

**Rename to be more descriptive**:
- 📋 Planned
- 🔨 Working On It
- 👀 In Review
- ✅ Completed

### Step 3: Add PR Tracking Tasks

Create draft issues for each PR:

```markdown
Title: PR #1: Project Foundation
Labels: phase-1, documentation, foundational
Description:
Create Ansible collection structure and basic configuration.

**Files**:
- Directory structure
- ansible.cfg
- galaxy.yml
- .gitignore

**Learning Objectives**:
- Understand Ansible collection structure
- Learn purpose of configuration files

**Depends On**: None (foundational)
**Blocks**: PR #2
```

Repeat for all 7 PRs.

### Step 4: Add Documentation Tasks

```markdown
Title: Write Domain Knowledge Documentation
Labels: phase-1, documentation, domain-knowledge
Description:
Create beginner-friendly docs explaining OpenShift Assisted Installer.

**Deliverables**:
- docs/00_START_HERE.md
- docs/01_ASSISTED_INSTALLER_CONCEPTS.md
- docs/02_API_OVERVIEW.md

**Learning Value**: Foundation for all future work
```

### Step 5: Add Learning Milestones

```markdown
Title: Build Mock MCP Server
Labels: phase-1, mcp, learning-tool
Description:
Create simple MCP server with mock data for safe API exploration.

**Why**: Lets beginners explore API without credentials
**Impact**: High - enables hands-on learning
```

## Recommended Project Views

### View 1: Current Sprint (Board)
**Filter**: `milestone:Phase-1 is:open`
**Sort**: By priority
**Purpose**: Day-to-day work tracking

### View 2: Learning Path (Table)
**Fields**:
- Title
- Status
- Learning Objective
- Dependencies
- Completed By

**Sort**: By dependency order
**Purpose**: See the learning progression

### View 3: PR Status (Board)
**Filter**: `label:pr-tracking`
**Columns**: Planned → Drafting → Review → Merged
**Purpose**: Track all 7 PRs at once

### View 4: Roadmap (Timeline)
**Show**: All phases
**Group By**: Phase
**Purpose**: Big picture view

## Labels to Create

### Priority Labels
- `priority: critical` - Blocking other work
- `priority: high` - Important for phase completion
- `priority: medium` - Nice to have
- `priority: low` - Future enhancement

### Type Labels
- `type: documentation` - Writing docs
- `type: code` - Writing code
- `type: testing` - Test coverage
- `type: infrastructure` - Project setup

### Phase Labels
- `phase-1: foundation` - Current phase
- `phase-2: utilities` - Next phase
- `phase-3: events-module` - Future

### Area Labels
- `area: domain-knowledge` - Assisted Installer concepts
- `area: mcp` - MCP server work
- `area: ansible` - Ansible module development
- `area: api` - API exploration

### Learning Labels
- `learning: beginner-friendly` - Great for newcomers
- `learning: hands-on` - Practical exercises
- `learning: conceptual` - Theory and concepts

### PR Labels
- `pr-tracking` - Tracks a specific PR
- `pr-1` through `pr-7` - Individual PR tracking

## Task Breakdown Example

### For PR #2 (Domain Knowledge)

**Parent Issue**: "PR #2: Domain Knowledge Documentation"

**Sub-tasks** (checkboxes or linked issues):
- [ ] Research Assisted Installer features
- [ ] Draft START_HERE guide
- [ ] Write ASSISTED_INSTALLER_CONCEPTS
- [ ] Write API_OVERVIEW
- [ ] Add LICENSE file
- [ ] Self-review all docs
- [ ] Request peer review
- [ ] Address feedback
- [ ] Merge PR

## Automation Ideas

### GitHub Actions Integration

```yaml
# .github/workflows/project-automation.yml
name: Update Project Board

on:
  pull_request:
    types: [opened, closed, reopened]
  issues:
    types: [opened, closed, reopened]

jobs:
  update-project:
    runs-on: ubuntu-latest
    steps:
      - name: Move PR to "In Review"
        if: github.event.pull_request.state == 'open'
        # Add to project automation

      - name: Move to "Done" when merged
        if: github.event.pull_request.merged == true
        # Update project status
```

### Auto-labeling PRs

```yaml
# .github/workflows/auto-label.yml
name: Auto Label PRs

on:
  pull_request:
    types: [opened]

jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - name: Label based on branch name
        # phase-1a-* → label: phase-1
        # phase-1b-* → label: phase-1, area: domain-knowledge
```

## Tracking Learning Progress

### Custom Fields in Project

Add these fields to track learning value:

1. **Learning Objective** (text)
   - What will beginners learn?

2. **Difficulty** (single select)
   - Beginner
   - Intermediate
   - Advanced

3. **Time Estimate** (number)
   - Hours to complete

4. **Prerequisites** (text)
   - What should you know first?

5. **Documentation Status** (single select)
   - Not Started
   - Draft
   - Review
   - Published

## Example Project Board Layout

```
┌─────────────┬──────────────┬─────────────┬──────────┐
│  📋 Planned │ 🔨 In Progress│ 👀 In Review│ ✅ Done │
├─────────────┼──────────────┼─────────────┼──────────┤
│ PR #3: API  │ PR #2: Domain│             │ PR #1:   │
│ Exploration │ Knowledge    │             │Foundation│
│             │              │             │          │
│ PR #4: MCP  │ Mock Data    │             │ LICENSE  │
│ Intro       │ Fixtures     │             │ file     │
│             │              │             │          │
│ PR #5:      │              │             │          │
│ Ansible     │              │             │          │
└─────────────┴──────────────┴─────────────┴──────────┘
```

## Benefits for This Project

### For You (Project Owner)
- ✅ Track 7 PRs systematically
- ✅ Manage dependencies visually
- ✅ See bottlenecks quickly
- ✅ Plan upcoming work
- ✅ Show progress to stakeholders

### For Beginners Following Along
- ✅ See the learning path clearly
- ✅ Know what's coming next
- ✅ Track their own progress
- ✅ Find specific learning resources
- ✅ Understand project status

### For Contributors
- ✅ Find tasks to help with
- ✅ Avoid duplicate work
- ✅ See priorities
- ✅ Understand context

### For Reviewers
- ✅ See what needs review
- ✅ Understand PR dependencies
- ✅ Prioritize review work
- ✅ Track feedback incorporation

## Alternative: GitHub Milestones

If Projects feels too complex, start simpler with **Milestones**:

### Create Milestone: "Phase 1: Foundation"
- Due date: 5 weeks from now
- Description: Complete repository skeleton and learning resources
- Link all 7 PR issues to this milestone

**Pros**:
- Simpler than Projects
- Built into GitHub
- Shows % complete

**Cons**:
- Less visual
- No Kanban board
- Fewer customization options

## Recommended Approach for Beginners

### Start Simple, Grow Complex

**Week 1**: Use GitHub Milestones
- Create "Phase 1" milestone
- Add 7 issues (one per PR)
- Track completion %

**Week 2-3**: Add Basic Project Board
- Convert to Project
- Use simple Kanban (3 columns)
- Link existing issues

**Week 4+**: Enhance as Needed
- Add custom fields
- Create multiple views
- Add automation

**Principle**: Don't over-engineer from day 1. Add complexity as you discover needs.

## Sample Issues to Create Now

### Issue #1: PR #1 - Project Foundation
```markdown
**Type**: PR Tracking
**Phase**: Phase 1
**Priority**: Critical (blocks all others)

**Description**:
Create the foundational Ansible collection structure.

**Deliverables**:
- [ ] Directory structure with .gitkeep files
- [ ] ansible.cfg
- [ ] galaxy.yml
- [ ] .gitignore

**Learning Objectives**:
- Understand Ansible collection layout
- Learn configuration file purposes

**Dependencies**: None
**Blocks**: PR #2, PR #3, PR #4, PR #5, PR #6, PR #7

**Estimated Time**: 2-3 hours
**Review Time**: 10 minutes
```

### Issue #2: PR #2 - Domain Knowledge
```markdown
**Type**: PR Tracking, Documentation
**Phase**: Phase 1
**Priority**: High

**Description**:
Create beginner-friendly documentation explaining OpenShift Assisted Installer.

**Deliverables**:
- [ ] docs/00_START_HERE.md
- [ ] docs/01_ASSISTED_INSTALLER_CONCEPTS.md
- [ ] docs/02_API_OVERVIEW.md
- [ ] LICENSE

**Learning Objectives**:
- Understand what Assisted Installer is
- Learn key domain concepts
- Grasp API architecture

**Dependencies**: PR #1 (need docs/ directory)
**Blocks**: PR #3

**Estimated Time**: 1 day
**Review Time**: 15-20 minutes
```

Continue for all 7 PRs...

## Quick Commands

### Create Issues via CLI (if gh supports it)
```bash
# Create issue for PR #1
gh issue create \
  --title "PR #1: Project Foundation" \
  --label "phase-1,pr-tracking,priority:critical" \
  --milestone "Phase 1: Foundation" \
  --body-file .github/ISSUE_TEMPLATES/pr-tracking.md

# List all phase-1 issues
gh issue list --label phase-1

# Check milestone progress
gh issue list --milestone "Phase 1: Foundation"
```

## Next Steps

1. **Create the Project** (5 minutes)
   - Go to repository Projects tab
   - Click "New project"
   - Choose "Board" template

2. **Create 7 Issues** (20 minutes)
   - One for each PR
   - Use template above
   - Add appropriate labels

3. **Add to Project Board** (5 minutes)
   - Drag issues to "Planned" column
   - Set up dependencies

4. **Share with Community** (2 minutes)
   - Update README with project board link
   - Invite collaborators if any

**Total setup time**: ~30-40 minutes for complete setup

## Tips for Success

### Keep It Updated
- Move cards when status changes
- Close issues when PRs merge
- Add notes and comments
- Celebrate completions! 🎉

### Make It Visible
- Link from README
- Reference in PR descriptions
- Share in commit messages
- Update in team meetings

### Use It for Learning
- Track "aha moments"
- Document blockers
- Note common questions
- Share resources

### Iterate
- Start simple
- Add features as needed
- Get feedback from users
- Adjust based on reality

## Conclusion

**Yes, GitHub Projects would be extremely useful** for this project because:

1. ✅ Visualizes the 7-PR progression
2. ✅ Tracks dependencies clearly
3. ✅ Shows learning path for beginners
4. ✅ Manages complexity
5. ✅ Demonstrates professional practices
6. ✅ Helps YOU stay organized
7. ✅ Teaches project management alongside coding

**Recommendation**: Set it up now, before submitting PR #1. Then each PR can reference the project board, showing beginners how professional teams track work.
