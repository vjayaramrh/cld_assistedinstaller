# Pull Request Strategy - Revised for Triple-Beginners

**Context**: Supporting beginners to OpenShift Assisted Installer APIs, MCP, AND Ansible modules
**Approach**: Domain knowledge first, then tools, with progressive learning
**Goal**: Small, focused PRs that teach concepts step-by-step

---

## Overview: 7 PRs Instead of 1

Breaking down the original PR #1 into 7 focused PRs that build knowledge progressively:

```
Original PR #1 (17 files)
    ↓
Split into 7 PRs:

PR #1: Project Foundation (Structure + Config)          [Week 1]
PR #2: Domain Knowledge (What is Assisted Installer?)   [Week 1-2]
PR #3: API Exploration (Understanding the API)          [Week 2]
PR #4: MCP Introduction (Interactive Learning Tool)     [Week 3]
PR #5: Ansible Introduction (Automation Basics)         [Week 3-4]
PR #6: Development Workflows (Git, PR, Testing)         [Week 4]
PR #7: Project Planning (Requirements, Roadmap)         [Week 4-5]
```

**Total timeline**: 4-5 weeks with review cycles
**Average PR size**: 2-4 files, 10-20 minute reviews

---

## Detailed PR Breakdown

### PR #1: Project Foundation
**Branch**: `phase-1a-foundation`
**Size**: 7 files, ~26 lines
**Review time**: 10 minutes
**Learning focus**: Ansible collection structure

#### Files
```
.gitignore
ansible.cfg
galaxy.yml
plugins/modules/.gitkeep
plugins/module_utils/.gitkeep
examples/.gitkeep
tests/unit/.gitkeep
docs/.gitkeep
```

#### Commits (2)
1. `Add directory structure for Ansible collection`
2. `Add Ansible configuration files (ansible.cfg, galaxy.yml)`

#### What Beginners Learn
- ✅ Ansible collection directory structure
- ✅ Purpose of .gitkeep files
- ✅ Basic Ansible configuration
- ✅ Galaxy metadata

#### PR Description Template
```markdown
## Summary
Creates the foundational directory structure and minimal configuration for an Ansible collection.

## What This PR Does
- Establishes directory structure per Ansible collection standards
- Adds minimal ansible.cfg for local development
- Adds galaxy.yml with collection metadata

## For Complete Beginners
This PR shows what an Ansible collection looks like at its most basic level.

**Key concepts:**
- `plugins/modules/`: Where Ansible modules live
- `plugins/module_utils/`: Where shared utilities live
- `tests/`: Where tests go
- `examples/`: Where usage examples go

**Why .gitkeep files?**
Git doesn't track empty directories. .gitkeep files preserve the structure.

## Review Checklist
- [ ] Directory structure matches Ansible standards
- [ ] ansible.cfg has sensible defaults
- [ ] galaxy.yml metadata is correct
- [ ] .gitignore covers Python and Ansible artifacts

## Next PR
PR #2 will add domain knowledge documentation about OpenShift Assisted Installer.
```

#### Dependencies
None - this is the foundation

---

### PR #2: Domain Knowledge Documentation
**Branch**: `phase-1b-domain-knowledge`
**Size**: 4 files, ~400 lines
**Review time**: 15-20 minutes
**Learning focus**: Understanding OpenShift Assisted Installer

#### Files
```
docs/00_START_HERE.md
docs/01_ASSISTED_INSTALLER_CONCEPTS.md
docs/02_API_OVERVIEW.md
LICENSE
```

#### Commits (4)
1. `Add MIT License`
2. `Add START_HERE guide for complete beginners`
3. `Add Assisted Installer concepts documentation`
4. `Add API overview documentation`

#### What Beginners Learn
- ✅ What OpenShift Assisted Installer is
- ✅ Key domain concepts (clusters, hosts, infra-envs)
- ✅ Why this API exists
- ✅ High-level API structure
- ✅ Real-world use cases

#### Key Content

**docs/00_START_HERE.md**:
```markdown
# Start Here - Complete Beginner's Guide

## Who Is This For?
You're new to:
- OpenShift Assisted Installer
- REST APIs in general
- MCP (Model Context Protocol)
- Ansible module development

**That's okay!** This project is designed to teach you all of these.

## Learning Path
1. Read this file (you are here!)
2. Understand what Assisted Installer is (01_ASSISTED_INSTALLER_CONCEPTS.md)
3. Explore the API structure (02_API_OVERVIEW.md)
4. Make your first API call (coming in PR #3)
5. Use MCP for exploration (coming in PR #4)
6. Build your first Ansible module (coming in PR #5)

## Prerequisites
- Basic command line knowledge
- Basic understanding of APIs (we'll teach the details)
- Curiosity and willingness to learn!

## How to Learn
- Read docs in order
- Try examples as you go
- Document your questions
- Ask for help when stuck
```

**docs/01_ASSISTED_INSTALLER_CONCEPTS.md**:
```markdown
# OpenShift Assisted Installer - Core Concepts

## What Problem Does It Solve?
Installing OpenShift clusters (especially on bare metal or edge locations) can be complex.
Assisted Installer provides a guided workflow with:
- Web UI for interactive installations
- REST API for automation
- Support for bare metal, vSphere, and other platforms

## Key Concepts

### Cluster
A group of servers running OpenShift together.
- Has a unique ID
- Goes through installation stages
- Has associated hosts, events, and configuration

### Host
A physical or virtual machine that will be part of the cluster.
- Discovered via discovery ISO
- Validated for requirements
- Assigned roles (control plane, worker)

### Infrastructure Environment (infra-env)
The environment where hosts are discovered and configured.
- Contains discovery ISO configuration
- Network settings
- Host discovery parameters

### Events
Log entries tracking what's happening during installation.
- Different severity levels (info, warning, critical)
- Associated with clusters or hosts
- Crucial for troubleshooting

## Real-World Workflow
1. Create infrastructure environment
2. Generate discovery ISO
3. Boot hosts with ISO
4. Hosts register automatically
5. Configure cluster settings
6. Monitor events during installation
7. Cluster becomes ready

## Why Use the API?
- **Automation**: Integrate with CI/CD
- **Bulk operations**: Install multiple clusters
- **Custom workflows**: Build your own tools
- **Monitoring**: Track installation progress
- **Integration**: Connect with other systems

## Next Steps
Now that you know WHAT Assisted Installer is, let's explore the API structure.
→ Continue to 02_API_OVERVIEW.md
```

**docs/02_API_OVERVIEW.md**:
```markdown
# Assisted Installer API Overview

## Base URL
```
https://api.openshift.com/api/assisted-install/v2
```

## Authentication
Bearer token in Authorization header:
```bash
Authorization: Bearer YOUR_TOKEN_HERE
```

## Endpoint Categories

### 1. Clusters
Manage OpenShift clusters
- `GET /clusters` - List all clusters
- `GET /clusters/{id}` - Get cluster details
- `POST /clusters` - Create new cluster
- `PATCH /clusters/{id}` - Update cluster
- `DELETE /clusters/{id}` - Delete cluster

### 2. Events
Track installation progress and issues
- `GET /events` - List events with filters
- `GET /events/{id}` - Get specific event

**Common use**: Monitor installation progress, troubleshoot issues

### 3. Infrastructure Environments
Manage discovery environments
- `GET /infra-envs` - List environments
- `GET /infra-envs/{id}` - Get environment details
- `POST /infra-envs` - Create environment
- `PATCH /infra-envs/{id}` - Update environment

### 4. Hosts
Manage individual servers
- `GET /infra-envs/{id}/hosts` - List hosts in environment
- `GET /infra-envs/{id}/hosts/{host_id}` - Get host details
- `PATCH /infra-envs/{id}/hosts/{host_id}` - Update host

### 5. Manifests
Customize cluster configuration
- `GET /clusters/{id}/manifests` - List manifests
- `POST /clusters/{id}/manifests` - Add manifest

## Common Patterns

### Filtering
Many endpoints support query parameters:
```
GET /events?cluster_id=xxx&severity=critical&limit=50
```

### Pagination
Large result sets use offset/limit:
```
GET /clusters?offset=0&limit=20
GET /clusters?offset=20&limit=20  # Next page
```

### Error Responses
- `401 Unauthorized` - Invalid/expired token
- `404 Not Found` - Resource doesn't exist
- `400 Bad Request` - Invalid parameters
- `500 Internal Server Error` - API issue

## Safety Tips for Beginners

### Start with Read-Only
Practice with GET requests first:
- ✅ Safe: `GET /clusters`
- ✅ Safe: `GET /events`
- ⚠️  Caution: `POST /clusters` (creates resources)
- ⚠️  Caution: `DELETE /clusters/{id}` (destructive)

### Use Test Data
If possible, use a test/dev environment first.

### Understand Before Automating
Explore manually before building automation.

## Next Steps
In the next PR, we'll show you how to make your first API call.
```

#### PR Description Template
```markdown
## Summary
Introduces domain knowledge documentation for complete beginners to OpenShift Assisted Installer.

## What This PR Does
- Adds navigation guide for learners (START_HERE)
- Explains Assisted Installer concepts and use cases
- Provides API overview and endpoint reference
- Adds MIT License

## Why This PR Comes Before Code
Before learning MCP or Ansible, beginners need to understand:
- What problem we're solving
- What the domain concepts are
- How the API is structured

This documentation provides that foundation.

## For Reviewers
Focus on:
- Is the content beginner-friendly?
- Are explanations clear and accurate?
- Are there confusing sections?
- What questions do you still have?

## For Beginners
Read the docs in this order:
1. `docs/00_START_HERE.md`
2. `docs/01_ASSISTED_INSTALLER_CONCEPTS.md`
3. `docs/02_API_OVERVIEW.md`

Take your time. Understanding the domain is more important than rushing to code.

## Next PR
PR #3 will add hands-on API exploration guides.
```

#### Dependencies
- PR #1 merged (need docs/ directory)

---

### PR #3: API Exploration Guide
**Branch**: `phase-1c-api-exploration`
**Size**: 3 files, ~350 lines
**Review time**: 15 minutes
**Learning focus**: Making actual API calls

#### Files
```
docs/03_YOUR_FIRST_API_CALL.md
docs/04_UNDERSTANDING_RESPONSES.md
docs/05_COMMON_API_PATTERNS.md
```

#### Commits (3)
1. `Add hands-on guide for first API call`
2. `Add guide for understanding API responses`
3. `Add common API patterns documentation`

#### What Beginners Learn
- ✅ How to get an API token
- ✅ Making curl requests
- ✅ Reading JSON responses
- ✅ Common API patterns (filtering, pagination)
- ✅ Troubleshooting API errors

#### Key Content

**docs/03_YOUR_FIRST_API_CALL.md**:
```markdown
# Your First API Call - Hands-On Tutorial

## Prerequisites
- You've read 01_ASSISTED_INSTALLER_CONCEPTS.md
- You've read 02_API_OVERVIEW.md
- You have a Red Hat account (free to create)

## Step 1: Get an API Token

### Option A: Using Offline Token (Recommended for Learning)
1. Go to https://console.redhat.com/openshift/token
2. Copy your offline token
3. Set environment variable:
   ```bash
   export AI_OFFLINE_TOKEN="your-token-here"
   ```

### Option B: Using API Token
1. Get API token from Red Hat console
2. Set environment variable:
   ```bash
   export AI_API_TOKEN="your-token-here"
   ```

## Step 2: Make Your First Call

Let's list all clusters (safest first call):

```bash
curl -s -H "Authorization: Bearer $AI_API_TOKEN" \
  https://api.openshift.com/api/assisted-install/v2/clusters | jq
```

**What's happening:**
- `-s`: Silent mode (no progress bar)
- `-H`: Add Authorization header
- `| jq`: Pretty-print JSON (install jq if needed)

## Step 3: Understand the Response

You'll see something like:
```json
[
  {
    "id": "12345678-1234-1234-1234-123456789012",
    "name": "my-cluster",
    "status": "ready",
    "created_at": "2026-03-18T10:00:00Z",
    ...
  }
]
```

**This is an array** of cluster objects.
- Empty array `[]` means no clusters
- Each object has an `id`, `name`, `status`, etc.

## Step 4: Get Details of One Cluster

If you have a cluster, get its details:
```bash
CLUSTER_ID="your-cluster-id-here"
curl -s -H "Authorization: Bearer $AI_API_TOKEN" \
  "https://api.openshift.com/api/assisted-install/v2/clusters/$CLUSTER_ID" | jq
```

You'll see MUCH more detail about that specific cluster.

## Step 5: List Events

Events are great for learning because:
- Read-only (safe!)
- Show what's happening
- Useful for troubleshooting

```bash
curl -s -H "Authorization: Bearer $AI_API_TOKEN" \
  "https://api.openshift.com/api/assisted-install/v2/events" | jq
```

## Common Errors

### 401 Unauthorized
```json
{"error": "Unauthorized"}
```
**Fix**: Check your token is valid and not expired

### 404 Not Found
```json
{"error": "Cluster not found"}
```
**Fix**: Verify the cluster ID exists

### Empty Results
```json
[]
```
**Not an error!** Just means no resources found.

## Practice Exercises

1. List all your clusters
2. Get details of one cluster (if you have any)
3. List all events
4. List events for a specific cluster
5. Try an invalid cluster ID (see the error)

## Troubleshooting

### jq not installed?
```bash
# macOS
brew install jq

# Linux
sudo apt install jq  # or yum install jq
```

### Token expired?
Get a new token from console.redhat.com/openshift/token

### Don't have any clusters?
That's fine! The learning continues with mock data in the next PRs.

## Next Steps
Now that you've made real API calls, let's learn to read the responses in detail.
→ Continue to 04_UNDERSTANDING_RESPONSES.md
```

#### PR Description Template
```markdown
## Summary
Adds hands-on guides for making actual API calls and understanding responses.

## What This PR Does
- Step-by-step first API call tutorial
- Guide to understanding JSON responses
- Common API patterns (filtering, pagination, errors)

## Why This Matters
Theory is great, but hands-on practice builds real understanding. These guides let beginners:
- Make actual API calls
- See real responses
- Build muscle memory
- Gain confidence

## For Reviewers
Try the tutorials yourself!
- Are the steps clear?
- Did you encounter any issues?
- What could be clearer?

## For Beginners
You'll need:
- curl (usually pre-installed)
- jq (for pretty JSON)
- A Red Hat account (free)

Work through the guides at your own pace.

## Next PR
PR #4 will introduce MCP as an easier way to explore the API.
```

#### Dependencies
- PR #2 merged (references domain docs)

---

### PR #4: MCP Introduction & Mock Server
**Branch**: `phase-1d-mcp-introduction`
**Size**: 3 files, ~500 lines
**Review time**: 20 minutes
**Learning focus**: Using MCP for API exploration

#### Files
```
docs/06_MCP_INTRODUCTION.md
docs/07_MOCK_API_SERVER.md
examples/mcp-mock-server/README.md
```

#### Commits (3)
1. `Add MCP introduction for beginners`
2. `Add mock API server documentation`
3. `Add example MCP server structure`

#### What Beginners Learn
- ✅ What MCP is and why it's useful
- ✅ How MCP makes API exploration easier
- ✅ Setting up an MCP server
- ✅ Using mock data for safe learning
- ✅ Comparing manual curl vs MCP tools

#### Key Content

**docs/06_MCP_INTRODUCTION.md**:
```markdown
# Introduction to Model Context Protocol (MCP)

## What is MCP?

MCP (Model Context Protocol) lets AI assistants like Claude interact with external tools and data sources.

**In plain English**: Instead of you typing curl commands, you can ask Claude to interact with APIs for you.

## Why MCP for This Project?

### Without MCP
```bash
# You type this every time:
curl -s -H "Authorization: Bearer $AI_API_TOKEN" \
  "https://api.openshift.com/api/assisted-install/v2/events?severity=critical" | jq
```

### With MCP
```
# You just ask:
"Show me critical events for cluster xyz"
```

Claude uses the MCP server to make the API call for you!

## Key Concepts

### MCP Server
A program that:
- Connects to an API (like Assisted Installer API)
- Provides "tools" Claude can call
- Handles authentication
- Returns results

### MCP Tools
Functions the MCP server exposes:
- `list_events` - Get cluster events
- `get_cluster` - Get cluster details
- `list_clusters` - List all clusters

### MCP Resources
Documents or data the server provides:
- Documentation
- Configuration
- Reference data

## Benefits for Beginners

### 1. Explore Without Memorizing Commands
Don't remember the exact curl syntax? Just ask Claude.

### 2. Learn the API Interactively
```
"What events does cluster X have?"
"Show me only critical events"
"What happened in the last hour?"
```

### 3. Safe Practice with Mock Data
Use a mock MCP server to practice without:
- Needing API credentials
- Affecting real systems
- Network connectivity

### 4. Understand Before Building
Explore the API through MCP BEFORE writing Ansible modules.

## How It Works

```
You: "Show me events for cluster X"
  ↓
Claude Code: Calls MCP server tool list_events
  ↓
MCP Server: Makes API request to Assisted Installer
  ↓
API: Returns JSON data
  ↓
MCP Server: Formats response
  ↓
Claude Code: Shows you the results
```

## MCP vs Direct API Calls

| Aspect | Direct curl | MCP |
|--------|------------|-----|
| Ease | Remember syntax | Natural language |
| Auth | Manage tokens | Configured once |
| Formatting | Manual jq | Auto-formatted |
| Learning | Steeper curve | Gentler intro |
| Flexibility | Full control | Guided experience |

**Best practice**: Learn both! Use MCP for exploration, understand the underlying curl.

## Next Steps
Let's set up a mock MCP server for safe practice.
→ Continue to 07_MOCK_API_SERVER.md
```

**docs/07_MOCK_API_SERVER.md**:
```markdown
# Mock API Server - Safe Learning Environment

## Why Mock Data?

### For Complete Beginners
- ✅ No API credentials needed
- ✅ No risk of affecting real systems
- ✅ Works offline
- ✅ Consistent, predictable responses
- ✅ Learn at your own pace

### For Developers
- ✅ Test code without API access
- ✅ Simulate error scenarios
- ✅ Fast iteration
- ✅ CI/CD testing

## What's Included

A simple MCP server that returns mock data for:
- Cluster information
- Events
- Infrastructure environments
- Hosts

**Note**: This is a learning tool, not connected to real API.

## Setup (Coming in Future PR)

We'll build this together! For now, understand the concept.

## Example Usage

Once set up, you can ask:
```
"Show me sample cluster events"
"What does a cluster object look like?"
"Give me an example of a critical error"
"Show me the structure of an infrastructure environment"
```

## Learning Workflow

```
Step 1: Use mock MCP server
   ↓
Step 2: Understand API responses
   ↓
Step 3: Design Ansible module
   ↓
Step 4: Test module with mock data
   ↓
Step 5: Test module with real API
```

## Mock Data Structure

Mock responses are based on real API responses, with:
- Realistic field names
- Proper data types
- Example values
- Error scenarios

## Transition to Real API

When ready:
1. Get API token
2. Switch MCP server to use real API
3. Same questions, real data!

## Next Steps
After learning MCP concepts, we'll move to Ansible module development.
```

#### PR Description Template
```markdown
## Summary
Introduces Model Context Protocol (MCP) as an interactive learning tool for API exploration.

## What This PR Does
- Explains what MCP is for complete beginners
- Shows how MCP simplifies API exploration
- Documents mock API server concept
- Provides foundation for hands-on MCP learning

## Why MCP for Beginners?
MCP bridges the gap between:
- Manual API calls (curl commands)
- Automated tools (Ansible modules)

It provides an interactive middle ground perfect for learning.

## Educational Value
- Natural language API exploration
- Safe practice with mock data
- Understand API before automating
- Smooth transition to Ansible modules

## For Reviewers
Focus on:
- Is MCP explained clearly for non-technical people?
- Are the benefits clear?
- Does this make sense before introducing Ansible?

## Next PR
PR #5 will introduce Ansible module development concepts.
```

#### Dependencies
- PR #3 merged (references API exploration)

---

### PR #5: Ansible Module Introduction
**Branch**: `phase-1e-ansible-introduction`
**Size**: 3 files, ~450 lines
**Review time**: 20 minutes
**Learning focus**: Ansible module basics

#### Files
```
docs/08_ANSIBLE_MODULE_BASICS.md
docs/09_YOUR_FIRST_MODULE.md
docs/10_MCP_TO_ANSIBLE_BRIDGE.md
```

#### Commits (3)
1. `Add Ansible module basics documentation`
2. `Add first module tutorial`
3. `Add MCP-to-Ansible conceptual bridge`

#### What Beginners Learn
- ✅ What Ansible modules are
- ✅ How they work
- ✅ Module structure and patterns
- ✅ Connection between MCP tools and Ansible modules
- ✅ When to use Ansible vs MCP

#### Key Content

**docs/10_MCP_TO_ANSIBLE_BRIDGE.md**:
```markdown
# From MCP Tools to Ansible Modules

## The Connection

You've learned:
1. The Assisted Installer API (domain knowledge)
2. How to call APIs manually (curl)
3. How to explore APIs with MCP (interactive)

Now: How to automate with Ansible modules

## Same Operation, Different Interfaces

### Via curl (Manual)
```bash
curl -H "Authorization: Bearer $TOKEN" \
  "https://api.openshift.com/.../events?severity=critical"
```

### Via MCP (Interactive)
```
Ask Claude: "Show me critical events"
MCP tool: list_events(severity="critical")
```

### Via Ansible (Automated)
```yaml
- name: Get critical events
  events_info:
    severity: critical
    api_token: "{{ token }}"
  register: result
```

**Same API call, three ways!**

## Conceptual Mapping

| MCP Tool | Ansible Module |
|----------|----------------|
| Tool name | Module name |
| Input parameters | Module arguments |
| Tool handler code | Module main() function |
| Return data | module.exit_json() |
| Error handling | module.fail_json() |
| Tool description | DOCUMENTATION string |

## When to Use Each

### Use MCP when:
- ✅ Exploring the API
- ✅ One-off queries
- ✅ Learning API structure
- ✅ Testing ideas quickly

### Use Ansible when:
- ✅ Repeatable automation
- ✅ Complex workflows
- ✅ Infrastructure as code
- ✅ Team collaboration
- ✅ CI/CD integration

## Learning Progression

```
Week 1-2: Understand the API (domain + manual calls)
   ↓
Week 3: Explore with MCP (interactive learning)
   ↓
Week 4: Build Ansible modules (automation)
   ↓
Week 5+: Combine all three (full toolkit)
```

## Building Both

In this project, we'll create:
1. MCP server for exploration
2. Ansible modules for automation

You'll see how similar they are under the hood!

## Key Insight

> Both MCP tools and Ansible modules are structured interfaces to APIs.
> Learn one, understand both.
```

#### PR Description Template
```markdown
## Summary
Introduces Ansible module development concepts and bridges to MCP understanding.

## What This PR Does
- Explains Ansible modules for beginners
- Provides first module tutorial
- Shows connection between MCP tools and Ansible modules
- Clarifies when to use each approach

## Educational Flow
By now, beginners have:
1. ✅ Understood the domain (Assisted Installer)
2. ✅ Made manual API calls (curl)
3. ✅ Explored with MCP (interactive)
4. ✅ Ready to automate with Ansible (this PR)

## Key Teaching Point
MCP tools and Ansible modules are similar concepts - both create structured interfaces to APIs.

## For Reviewers
- Are the parallels clear?
- Does this connect previous learning?
- Is the progression logical?

## Next PR
PR #6 will add development workflow documentation (Git, PRs, testing).
```

#### Dependencies
- PR #4 merged (references MCP concepts)

---

### PR #6: Development Workflows
**Branch**: `phase-1f-workflows`
**Size**: 3 files, ~400 lines
**Review time**: 15 minutes
**Learning focus**: Professional development practices

#### Files
```
docs/GIT_COMMIT_STRATEGY.md
docs/PULL_REQUEST_WORKFLOW.md
docs/TESTING_APPROACH.md
```

#### Commits (3)
1. `Add git commit strategy documentation`
2. `Add pull request workflow documentation`
3. `Add testing approach documentation`

#### What Beginners Learn
- ✅ Git commit best practices
- ✅ Pull request workflow
- ✅ Code review guidelines
- ✅ Modern testing approaches
- ✅ CI/CD concepts

#### PR Description Template
```markdown
## Summary
Documents professional development workflows (Git, PRs, testing).

## What This PR Does
- Git commit best practices
- Pull request workflow and etiquette
- Testing strategies for modules
- Development lifecycle

## Why After Technical Content?
Beginners now know:
- What we're building (domain + tools)
- How to build it (MCP + Ansible)

Now: Professional practices for building it well.

## For Reviewers
This PR demonstrates the workflows it documents!
- Small, focused commits ✅
- Clear PR description ✅
- Reviewable size ✅

## Next PR
PR #7 will add project requirements and roadmap planning.
```

#### Dependencies
- PR #5 merged (assumes knowledge of what we're building)

---

### PR #7: Project Planning & Roadmap
**Branch**: `phase-1g-planning`
**Size**: 4 files, ~900 lines
**Review time**: 25-30 minutes
**Learning focus**: Project planning and API coverage

#### Files
```
README.md
IMPLEMENTATION_PLAN.md
PROJECT_REQUIREMENTS.md
FULL_API_COVERAGE_PLAN.md
```

#### Commits (4)
1. `Add comprehensive README`
2. `Add implementation plan summary`
3. `Add project requirements documentation`
4. `Add full API coverage expansion plan`

#### What Beginners Learn
- ✅ Project documentation structure
- ✅ Requirements gathering
- ✅ Long-term planning
- ✅ API coverage strategy
- ✅ Realistic timelines

#### PR Description Template
```markdown
## Summary
Adds project-level documentation: README, requirements, implementation plan, and API coverage roadmap.

## What This PR Does
- Comprehensive README with navigation
- Implementation plan summary
- Detailed project requirements
- Full API coverage plan (all endpoints)

## Why Last?
Now that beginners understand:
- The domain (Assisted Installer)
- The tools (MCP + Ansible)
- The workflows (Git, PRs, testing)

They can understand the big-picture planning.

## Completing Phase 1
This PR completes Phase 1 (Repository Skeleton).
All 7 PRs together establish the foundation for building modules.

## For Reviewers
Big picture questions:
- Is the plan realistic?
- Are requirements clear?
- Is API coverage comprehensive?
- Ready to start building?

## Next Phase
After this PR: Phase 2 begins (Module utilities and first modules)
```

#### Dependencies
- PR #6 merged (references workflows in planning)

---

## Summary Comparison

### Original Approach (1 PR)
```
PR #1: Everything
- 17 files
- Mix of config, docs, planning
- 60+ minute review
- Hard to focus
```

### New Approach (7 PRs)
```
PR #1: Foundation (structure)           → 10 min review
PR #2: Domain knowledge                 → 15 min review
PR #3: API exploration                  → 15 min review
PR #4: MCP introduction                 → 20 min review
PR #5: Ansible introduction             → 20 min review
PR #6: Development workflows            → 15 min review
PR #7: Planning & roadmap               → 30 min review
------------------------------------------------------------
Total: Same content, 7 focused sessions  → ~125 min total
```

## Learning Progression

```
PR #1: "Here's what an Ansible collection looks like"
   ↓
PR #2: "Here's what Assisted Installer does"
   ↓
PR #3: "Here's how to call the API"
   ↓
PR #4: "Here's an easier way to explore (MCP)"
   ↓
PR #5: "Here's how to automate (Ansible)"
   ↓
PR #6: "Here's how to work professionally"
   ↓
PR #7: "Here's the complete plan"
```

## Timeline

| Week | PRs | Focus |
|------|-----|-------|
| 1 | #1, #2 | Foundation + Domain Knowledge |
| 2 | #3, #4 | API Exploration + MCP |
| 3 | #5, #6 | Ansible + Workflows |
| 4-5 | #7 | Planning + Review Cycles |

**Flexible**: Can accelerate if reviews are fast.

## Benefits

### For Triple-Beginners
- ✅ Domain knowledge first (what is Assisted Installer?)
- ✅ Manual exploration (understand the API)
- ✅ Interactive tools (MCP for learning)
- ✅ Automation (Ansible for production)
- ✅ Best practices (workflows)
- ✅ Big picture (planning)

### For Reviewers
- ✅ Smaller, focused reviews
- ✅ Clear scope per PR
- ✅ Logical progression
- ✅ Can review different PRs concurrently

### For Project Quality
- ✅ Incremental validation
- ✅ Better documentation
- ✅ Clear git history
- ✅ Foundation for future phases

## Success Metrics

After all 7 PRs, beginners should be able to:
- [ ] Explain what Assisted Installer is
- [ ] Make API calls manually
- [ ] Use MCP for exploration
- [ ] Understand Ansible module structure
- [ ] See connections between MCP and Ansible
- [ ] Follow professional workflows
- [ ] Understand the project roadmap
- [ ] Ready to build their first module

## Next Steps

1. **Close current PR #1**
   ```bash
   gh pr close 1 --comment "Splitting into 7 focused PRs for better learning progression"
   ```

2. **Create PR #1 (Foundation)**
   - Cherry-pick relevant commits
   - Use PR template
   - Submit for review

3. **After each merge**
   - Create next PR from updated main
   - Continue progression

4. **Document learnings**
   - What worked well?
   - What was confusing?
   - Update docs based on feedback

---

## Recommendation

**Proceed with 7-PR strategy** because:
1. ✅ Optimized for triple-beginners (domain + MCP + Ansible)
2. ✅ Domain knowledge before tools
3. ✅ Progressive complexity
4. ✅ Clear learning objectives per PR
5. ✅ Manageable review sessions
6. ✅ Better documentation quality
7. ✅ Sets pattern for future phases

**Start with**: PR #1 (Foundation) - smallest, safest, establishes the structure.
