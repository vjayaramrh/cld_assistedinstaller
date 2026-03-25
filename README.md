# cld_assistedinstaller

[![AI Assisted](https://img.shields.io/badge/AI-Assisted_by_Claude-5A67D8?style=flat-square&logo=anthropic)](AI_ASSISTED_DEVELOPMENT.md)
[![Community Driven](https://img.shields.io/badge/Community-Driven-green?style=flat-square)](CONTRIBUTING.md)
[![Beginner Friendly](https://img.shields.io/badge/Beginner-Friendly-orange?style=flat-square)](docs/00_START_HERE.md)

Ansible collection for the OpenShift Assisted Installer API - designed for beginners learning Ansible module development.

---

## 🚀 Join Us: Community-Driven Learning Project!

**This is YOUR chance to contribute to open source!** We're building an Ansible collection together as a community, learning and growing as we go.

### 🎯 Perfect For You If:
- ✅ New to open source contributions
- ✅ Learning OpenShift Assisted Installer
- ✅ Want to understand MCP (Model Context Protocol)
- ✅ Interested in Ansible module development
- ✅ Want to be part of a supportive learning community
- ✅ Ready to learn by doing!

### 🌟 Why Join This Project?

**Learn Together:**
- Beginner-friendly tasks available NOW
- Learn from other contributors
- Pair programming opportunities
- Your questions help create better documentation

**Make Real Impact:**
- Your code will help others automate OpenShift deployments
- Documentation you write teaches future learners
- Every contribution matters - big or small!

**Celebrate Success:**
- Public recognition for contributors
- Your name in the project
- Portfolio-worthy contributions
- Learn professional development practices

### 🚧 Current Phase: Foundation & Learning Resources

We're restructuring to make contributing EASY:
- 7 focused PRs instead of 1 massive PR
- Clear, bite-sized tasks
- Multiple contribution opportunities
- Something for every skill level

**Track Progress:**
- [PR_STRATEGY_REVISED.md](PR_STRATEGY_REVISED.md) - Complete plan
- GitHub Project board (setting up now!) - Task tracking
- New PRs created progressively over 4-5 weeks

### 🤝 How to Get Involved

**Right Now:**
1. ⭐ Star this repository
2. 👀 Watch for updates
3. 💬 Join discussions in Issues
4. 📖 Read [PR_STRATEGY_REVISED.md](PR_STRATEGY_REVISED.md)
5. 🎉 Get ready to contribute!

**Coming Soon:**
- "Good first issue" labels
- Contributor guide
- Community discussion channel
- Contribution recognition system

**Want to help shape this project?** Comment on issues, share ideas, or just say hi! We're building this together.

---

## 🎓 For First-Time Ansible Module Developers

**New to Ansible modules?** You're in the right place! This repository is specifically designed to help you learn.

### Start Here (Available Now):
1. 📖 **[PROJECT_REQUIREMENTS.md](PROJECT_REQUIREMENTS.md)** - Project goals and requirements
2. 📖 **[IMPLEMENTATION_PLAN.md](IMPLEMENTATION_PLAN.md)** - Our phased approach
3. 📁 **[docs/CONFIGURATION_FILES_EXPLAINED.md](docs/CONFIGURATION_FILES_EXPLAINED.md)** - Why each config file is needed
4. 🔧 **[docs/GIT_COMMIT_STRATEGY.md](docs/GIT_COMMIT_STRATEGY.md)** - How we organize commits
5. 🔄 **[docs/PULL_REQUEST_WORKFLOW.md](docs/PULL_REQUEST_WORKFLOW.md)** - How we use Pull Requests
6. 🧪 **[docs/TESTING_APPROACH.md](docs/TESTING_APPROACH.md)** - Modern testing strategy

### Coming in Future Phases:
- 📚 docs/BEGINNERS_GUIDE.md - Introduction to Ansible modules (Phase 6)
- 🛠️ docs/MODULE_DEVELOPMENT_WALKTHROUGH.md - Step-by-step tutorial (Phase 7)
- 📋 docs/LEARNING_PATH.md - Guided learning sequence (Phase 7)
- 📝 docs/QUICK_REFERENCE.md - Commands cheat sheet (Phase 6)

## Overview

This collection provides Ansible modules for interacting with the OpenShift Assisted Installer API. Currently includes:

- **events** - Retrieve cluster events

## Prerequisites

- Python 3.6 or higher
- Ansible 2.9 or higher
- Red Hat account with console.redhat.com access
- Offline token from https://console.redhat.com/openshift/token

## Installation

```bash
# Clone the repository
git clone https://github.com/vjayaramrh/cld_assistedinstaller.git
cd cld_assistedinstaller

# Install Python dependencies
pip install -r plugins/requirements.txt

# Set up authentication (choose one)
export AI_OFFLINE_TOKEN="your-offline-token-here"
# OR
export AI_API_TOKEN="your-api-token-here"
```

### Getting Your Offline Token

1. Visit https://console.redhat.com/openshift/token
2. Log in with your Red Hat account
3. Click "Load token"
4. Copy the offline token
5. Export it: `export AI_OFFLINE_TOKEN="your-token"`

## Quick Start

```yaml
---
- name: Get cluster events
  hosts: localhost
  tasks:
    - name: List all events
      events:
      register: result

    - name: Display events
      debug:
        var: result.cluster_events
```

Run the playbook:
```bash
ansible-playbook examples/events.yml
```

## Documentation

### For Beginners
- [IMPLEMENTATION_PLAN.md](IMPLEMENTATION_PLAN.md) - How we planned and built this project
- [CONFIGURATION_FILES_EXPLAINED.md](docs/CONFIGURATION_FILES_EXPLAINED.md) - Why each config file exists
- [PULL_REQUEST_WORKFLOW.md](docs/PULL_REQUEST_WORKFLOW.md) - How we use Pull Requests
- [GIT_COMMIT_STRATEGY.md](docs/GIT_COMMIT_STRATEGY.md) - How we organize commits

### Technical Documentation
- [TESTING_APPROACH.md](docs/TESTING_APPROACH.md) - Modern testing strategy

## License

MIT License - see [LICENSE](LICENSE) for details.

## Support

- 📖 Check the [documentation](docs/)
- 🐛 Report issues: https://github.com/vjayaramrh/cld_assistedinstaller/issues

## 🤖 AI-Assisted Development

**This project is being built with assistance from Claude (Anthropic's AI assistant).**

We're transparent about this because:
- ✅ Modern development increasingly uses AI tools
- ✅ You can use Claude too - it's a learning accelerator!
- ✅ AI helps explain concepts, generate documentation, and review code
- ✅ We want to show how AI and humans collaborate effectively

**What Claude helps with:**
- Structuring documentation for beginners
- Explaining complex concepts simply
- Reviewing code for best practices
- Suggesting contribution opportunities
- Generating example code and tests

**What humans contribute:**
- Domain expertise and real-world experience
- Creative problem-solving
- Community building and mentorship
- Critical thinking and decision-making
- Testing and validation

**Want to use Claude for your contributions?** We encourage it! Claude can help you:
- Understand unfamiliar concepts
- Write clearer documentation
- Debug code issues
- Learn new technologies
- Generate test cases

See [AI_ASSISTED_DEVELOPMENT.md](AI_ASSISTED_DEVELOPMENT.md) for tips on using AI effectively.

---

## Acknowledgments

This project was created as a learning resource for Ansible module development, built collaboratively by the community with AI assistance.
