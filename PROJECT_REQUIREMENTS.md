# Project Requirements & Objectives

This document summarizes the requirements and approach for building the cld_assistedinstaller project.

## Project Goal

Create an Ansible collection for the OpenShift Assisted Installer API that serves as a **comprehensive learning resource** for developers writing their first Ansible module.

## Primary Objectives

### 1. Educational Focus
**Requirement:** This project must be beginner-friendly and teach Ansible module development.

**Implementation:**
- Extensive documentation explaining the "why" not just the "what"
- Step-by-step walkthroughs for first-time module developers
- Visual diagrams and analogies to explain concepts
- Progressive complexity from simple to advanced
- Each commit serves as a learning opportunity

### 2. Proper Development Workflow
**Requirement:** Demonstrate professional GitHub workflow using Pull Requests.

**Implementation:**
- Each phase developed in a separate branch
- Pull Requests for all changes (not direct pushes to main)
- Small, focused commits with clear separation of concerns
- Commits organized to be individually reviewable
- Detailed commit messages explaining rationale

### 3. Modern Best Practices
**Requirement:** Use current (2026) best practices, not outdated approaches.

**Implementation:**
- Research best practices from official sources
- Use pytest (not unittest) for testing
- Use pytest-mock for clean mocking syntax
- Follow Ansible's official testing recommendations
- Reference official documentation extensively

### 4. Incremental Development
**Requirement:** Build in small, reviewable chunks.

**Implementation:**
- 10 phases, each as a separate Pull Request
- Each phase produces a working, testable deliverable
- Commits within each phase follow logical progression
- Beginners can review commits one-by-one to learn

## Technical Requirements

### Repository Details
- **Name:** cld_assistedinstaller
- **Location:** https://github.com/vjayaramrh/cld_assistedinstaller
- **Namespace:** vjayaramrh.cld_assistedinstaller
- **License:** MIT (permissive, beginner-friendly)

### API Source
- **API Documentation:** https://api.openshift.com/?urls.primaryName=assisted-service%20service
- **Base URL:** https://api.openshift.com/api/assisted-install/v2
- **Initial Module:** GET /v2/events endpoint

### Module Structure
- Follow Ansible collection best practices
- Directory structure: plugins/modules, plugins/module_utils, tests, docs, examples
- Configuration files: ansible.cfg, galaxy.yml, .gitignore, LICENSE

### Testing Approach
- Use pytest as test framework (modern approach)
- Use pytest-mock for mocking (not unittest.mock)
- Use ansible-test for sanity checks
- Unit tests in tests/unit/
- Test infrastructure comes in Phase 5

## Documentation Requirements

### For Beginners (Critical!)

1. **CONFIGURATION_FILES_EXPLAINED.md**
   - Explain why each config file is needed
   - What happens without each file
   - Use analogies for complex concepts
   - Provide examples

2. **TESTING_APPROACH.md**
   - Explain our modern testing strategy
   - Why we chose specific tools
   - References to official documentation
   - Modern patterns vs outdated approaches

3. **GIT_COMMIT_STRATEGY.md**
   - Why small, focused commits matter
   - Separation of concerns principle
   - How to review commits to learn
   - Commit message guidelines

4. **PULL_REQUEST_WORKFLOW.md**
   - How we use Pull Requests
   - Why PRs are important for learning
   - Step-by-step PR workflow
   - Review guidelines

5. **IMPLEMENTATION_PLAN.md**
   - Our phased approach
   - Reference links with "what you'll learn"
   - Technical decisions and rationale
   - Step-by-step strategy

6. **MODULE_DEVELOPMENT_WALKTHROUGH.md** (Future)
   - 10-step hands-on tutorial
   - Line-by-line code explanations
   - Common pitfalls and solutions

7. **BEGINNERS_GUIDE.md** (Future)
   - What is an Ansible module?
   - Key concepts glossary
   - Project structure explained
   - Prerequisites with learning links

### Code Documentation
- Inline comments explaining every section
- Educational comments for first-time developers
- Purpose of each import statement
- Logic explanations for complex code

## Phased Implementation Plan

### Phase 1: Repository Skeleton ✅ (Current PR #1)
- Directory structure
- Configuration files (ansible.cfg, galaxy.yml, .gitignore)
- LICENSE
- README
- Core documentation files
- **Status:** In Pull Request, ready for merge

### Phase 2: Module Utilities
- plugins/requirements.txt
- apiurl.py (simpler utility)
- apitoken.py (authentication logic)

### Phase 3: Core Events Module
- Full events.py implementation
- DOCUMENTATION, EXAMPLES, RETURN sections
- Educational inline comments

### Phase 4: Examples and Basic Documentation
- examples/events.yml with heavy comments
- examples/README.md
- docs/events_module_guide.md

### Phase 5: Testing Infrastructure
- tests/unit/test_events.py
- tests/unit/requirements.txt
- tests/run_tests.sh
- Comprehensive test suite

### Phase 6-8: Beginner Documentation (3 parts)
- BEGINNERS_GUIDE.md
- MODULE_DEVELOPMENT_WALKTHROUGH.md
- LEARNING_PATH.md
- QUICK_REFERENCE.md
- CONCEPTS.md
- TESTING_GUIDE.md

### Phase 9: Contribution and Polish
- CONTRIBUTING.md
- Update README with all links
- Visual diagrams in documentation

### Phase 10: GitHub Setup
- Verify repository is complete
- Final polish
- Project complete!

## Commit Strategy

### Each Commit Must:
1. Have a **single, clear purpose**
2. Include detailed commit message explaining "why"
3. Be independently reviewable
4. Follow separation of concerns
5. Build logically on previous commits

### Commit Message Format:
```
Short summary (50 chars max)

Detailed explanation (72 chars per line):
- Why this change is needed
- What it accomplishes
- How it helps beginners learn

References if applicable
```

### Example Commits from Phase 1:
- Add directory structure (foundation)
- Add Ansible configuration files (together - both Ansible-related)
- Add .gitignore (separate - Git-specific)
- Add LICENSE (separate - legal concern)
- Add README (separate - user-facing)
- Add documentation files (separate - each doc has different purpose)

## Learning Resources Strategy

### For Each Concept, Provide:
1. **Official documentation links**
   - Ansible docs
   - Python docs
   - pytest docs
   - GitHub docs

2. **"What you'll learn" descriptions**
   - Clear explanation of what each link teaches
   - Prerequisites noted
   - Relevance to our project

3. **Progressive learning path**
   - Start with basics
   - Build to advanced
   - Checkpoints to verify understanding

### Example Links Included:
- Ansible Module Development Guide
- Ansible Collection Structure
- Python Tutorial
- pytest Documentation
- Git Handbook
- REST API Tutorial

## Pull Request Workflow

### For Each Phase:
1. Create feature branch from main
2. Make focused commits
3. Push branch to GitHub
4. Create Pull Request with detailed description
5. Review process (can request changes)
6. Merge when approved (using merge commit, not squash)
7. Delete branch and return to main

### PR Template Elements:
- Summary of what phase accomplishes
- List of changes
- Commit breakdown
- Testing notes
- Documentation updates
- Guidance for reviewers
- Educational value for beginners

## Key Principles

### 1. Beginner-First Mindset
Every decision should consider: "Will a beginner understand this?"

### 2. Document the Why
Don't just show what was done - explain why it was done that way.

### 3. Professional Standards
Use the same workflows and tools professional teams use.

### 4. Learn from the Process
The development process itself is a teaching tool.

### 5. Modern, Not Outdated
Always use current best practices (2026 standards).

### 6. Small, Reviewable Changes
Each commit and PR should be digestible and understandable.

### 7. Comprehensive but Concise
Documentation should be thorough but scannable.

## Success Criteria

### For Beginners:
- ✅ Can understand project structure
- ✅ Can follow commit history to learn
- ✅ Can review PRs to see development process
- ✅ Have resources to learn prerequisite topics
- ✅ Can implement their own module following patterns

### For the Project:
- ✅ Working Ansible module for GET /v2/events
- ✅ Proper Ansible collection structure
- ✅ Modern testing infrastructure
- ✅ Comprehensive documentation
- ✅ Clean Git history with focused commits
- ✅ Professional PR workflow demonstrated

### For the Community:
- ✅ Reference implementation for beginners
- ✅ Demonstrates best practices
- ✅ Shows proper development workflow
- ✅ Provides learning resources
- ✅ Encourages contributions from first-timers

## Special Requests

### Configuration Files
Document **why** each configuration file is needed:
- ansible.cfg - why Ansible needs this
- galaxy.yml - what it's for and what happens without it
- .gitignore - why we ignore certain files
- LICENSE - why it matters legally

### Testing Approach
Research and use **best practices from the internet**, not just copying existing implementations:
- Search for 2026 Ansible testing best practices
- Use official Ansible documentation
- Reference pytest and modern testing tools
- Explain modern vs outdated approaches

### Small, Reviewable Chunks
Break work into commits that:
- Each have clear purpose
- Can be reviewed independently
- Tell a story of how project evolved
- Make good PR review material for beginners

### Pull Requests Over Direct Pushes
Use PR workflow to demonstrate:
- How professional teams work
- Code review process
- Iterative development
- Quality gates before merging

## Repository Philosophy

> "This is not just an Ansible collection - it's a comprehensive learning resource that teaches beginners how to write Ansible modules by demonstrating professional development practices through every commit, PR, and documentation file."

## Contact & Collaboration

- **Repository:** https://github.com/vjayaramrh/cld_assistedinstaller
- **Issues:** https://github.com/vjayaramrh/cld_assistedinstaller/issues
- **Owner:** Vishwanath Jayaraman (@vjayaramrh)

---

**Last Updated:** February 17, 2026
**Current Status:** Phase 1 (Repository Skeleton) in PR #1, ready for merge
