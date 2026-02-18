# cld_assistedinstaller

Ansible collection for the OpenShift Assisted Installer API - designed for beginners learning Ansible module development.

## 🎓 For First-Time Ansible Module Developers

**New to Ansible modules?** You're in the right place! This repository is specifically designed to help you learn.

### Start Here:
1. 📖 **[IMPLEMENTATION_PLAN.md](IMPLEMENTATION_PLAN.md)** - Understand our approach and planning process
2. 📁 **[docs/CONFIGURATION_FILES_EXPLAINED.md](docs/CONFIGURATION_FILES_EXPLAINED.md)** - Why each config file is needed
3. 📚 **[docs/BEGINNERS_GUIDE.md](docs/BEGINNERS_GUIDE.md)** - Introduction to Ansible modules
4. 🛠️ **[docs/MODULE_DEVELOPMENT_WALKTHROUGH.md](docs/MODULE_DEVELOPMENT_WALKTHROUGH.md)** - Step-by-step implementation tutorial
5. 📋 **[docs/LEARNING_PATH.md](docs/LEARNING_PATH.md)** - Guided learning sequence

### Quick Reference:
- 📝 **[docs/QUICK_REFERENCE.md](docs/QUICK_REFERENCE.md)** - Commands and common tasks

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

## Acknowledgments

This project was created as a learning resource for Ansible module development.
