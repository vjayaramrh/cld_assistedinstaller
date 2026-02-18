# Configuration Files Explained

This document explains why each configuration file in the repository is needed and what it does.

## ansible.cfg

**Location:** `ansible.cfg` (repository root)

### What is it?
Ansible's configuration file that tells Ansible how to behave and where to find important files.

### Why do we need it?
Without this file, Ansible wouldn't know where to find our custom modules! By default, Ansible only looks for modules in its own installation directory.

### What's inside?
```ini
[defaults]
library = plugins/modules
module_utils = plugins/module_utils
```

- `library` - Tells Ansible: "Look in plugins/modules for custom modules"
- `module_utils` - Tells Ansible: "Look in plugins/module_utils for shared utilities"

### For beginners:
Think of ansible.cfg as a **map** that tells Ansible where everything is located in our project.

---

## galaxy.yml

**Location:** `galaxy.yml` (repository root)

### What is it?
Metadata file for an Ansible collection - like a business card for your collection.

### Why do we need it?
- Identifies the collection (namespace.name)
- Enables publishing to Ansible Galaxy
- Tracks version information
- Provides documentation links

### What's inside?
- **namespace + name**: Forms `vjayaramrh.cld_assistedinstaller`
- **version**: Semantic versioning (1.0.0)
- **authors**: Credits
- **license**: MIT (permissive)
- **repository**: GitHub URL

### For beginners:
This is how others will find and install your collection:
```bash
ansible-galaxy collection install vjayaramrh.cld_assistedinstaller
```

---

## .gitignore

**Location:** `.gitignore` (repository root)

### What is it?
Tells Git which files and directories to ignore - they won't be tracked or committed.

### Why do we need it?
Keeps the repository clean by ignoring:
- Python cache files (*.pyc, __pycache__)
- Ansible retry files (*.retry)
- Test artifacts (.pytest_cache)
- IDE settings (.vscode, .idea)
- OS files (.DS_Store)

### For beginners:
Think of .gitignore as a **filter** that keeps your repository clean by ignoring temporary and personal files.

---

## LICENSE

**Location:** `LICENSE` (repository root)

### What is it?
Legal terms under which others can use, modify, and distribute your code.

### Why MIT License?
- ✅ Permissive (others can do almost anything)
- ✅ Simple to understand
- ✅ Popular and well-recognized
- ✅ Commercial-friendly
- ✅ Just requires attribution

### What happens without it?
❌ Legally, no one can use your code (even if it's public on GitHub)

### For beginners:
The MIT License is like saying: "Use this code however you want, just remember where it came from, and we're not responsible if something goes wrong."

---

## Summary

| File | Purpose | What happens without it? |
|------|---------|--------------------------|
| **ansible.cfg** | Tells Ansible where modules are | Can't find custom modules |
| **galaxy.yml** | Collection metadata | Can't publish/distribute properly |
| **.gitignore** | Keeps repo clean | Cluttered with temp files |
| **LICENSE** | Legal permission | Unusable by others |

## References

- **ansible.cfg**: https://docs.ansible.com/ansible/latest/reference_appendices/config.html
- **galaxy.yml**: https://docs.ansible.com/ansible/latest/dev_guide/collections_galaxy_meta.html
- **Git ignore**: https://git-scm.com/docs/gitignore
- **Licenses**: https://choosealicense.com/
