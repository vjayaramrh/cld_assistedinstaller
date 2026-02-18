# Full API Coverage Plan

This document outlines the plan to create Ansible modules for **all** OpenShift Assisted Installer REST API endpoints.

## Overview

Based on the OpenShift Assisted Installer API, we need modules for multiple resource types. This expands from our initial single module (events) to a comprehensive collection covering the entire API surface.

## API Resources (Based on Reference Implementation)

From the existing implementation and API documentation, the main resources are:

### 1. **Clusters** (Core Resource)
Operations on OpenShift clusters

### 2. **Infrastructure Environments (infra-envs)**
ISO images and infrastructure setup

### 3. **Hosts**
Individual machines/nodes in clusters

### 4. **Events**
Cluster and infrastructure event logs

### 5. **Manifests**
Kubernetes manifests for clusters

### 6. **Operators**
Cluster operators and their configuration

### 7. **OpenShift Versions**
Available OpenShift versions and features

### 8. **Support Levels**
Platform support levels and architectures

### 9. **Domains**
DNS domains for clusters

## Module Development Strategy

### Phase Groups

Instead of building all modules at once, we organize into **module groups** where each group is a separate PR:

#### **Foundation Phase (Current)**
- **Phase 1**: Repository skeleton ✅
- **Phase 2**: Module utilities (apiurl, apitoken)
- **Phase 3**: First module (events - read-only, simplest)

#### **Read-Only Modules Phase** (Learn patterns first)
These modules only retrieve data (GET operations) - easier for beginners:

- **Phase 4**: openshift_versions module
  - GET /v2/openshift-versions
  - Query available OpenShift versions
  - Similar complexity to events

- **Phase 5**: support_levels module
  - GET /v2/support-levels/architectures
  - GET /v2/support-levels/features
  - Query support information

- **Phase 6**: supported_operators module
  - GET /v2/supported-operators
  - List available operators

#### **Complex Read Modules Phase**
Still GET-only but with more parameters:

- **Phase 7**: clusters module (read operations)
  - GET /v2/clusters (list)
  - GET /v2/clusters/{cluster_id} (get details)
  - Multiple query parameters
  - Pagination support

- **Phase 8**: infra_envs module (read operations)
  - GET /v2/infra-envs (list)
  - GET /v2/infra-envs/{infra_env_id} (get details)
  - Complex filtering options

- **Phase 9**: hosts module (read operations)
  - GET /v2/infra-envs/{infra_env_id}/hosts
  - GET /v2/clusters/{cluster_id}/hosts
  - Host inventory and status

#### **Write Operations Phase** (CRUD)
Modules that create, update, delete resources:

- **Phase 10**: clusters module (full CRUD)
  - POST /v2/clusters (create)
  - PATCH /v2/clusters/{cluster_id} (update)
  - DELETE /v2/clusters/{cluster_id} (delete)
  - Idempotency handling
  - State management (present/absent)

- **Phase 11**: infra_envs module (full CRUD)
  - POST /v2/infra-envs (create)
  - PATCH /v2/infra-envs/{infra_env_id} (update)
  - DELETE /v2/infra-envs/{infra_env_id} (delete)
  - Complex parameter validation

- **Phase 12**: hosts module (management operations)
  - POST operations for host binding
  - PATCH for host configuration
  - State transitions

#### **Advanced Operations Phase**
Specialized operations and workflows:

- **Phase 13**: manifests module
  - GET /v2/clusters/{cluster_id}/manifests
  - POST /v2/clusters/{cluster_id}/manifests
  - DELETE /v2/clusters/{cluster_id}/manifests
  - File upload/download handling

- **Phase 14**: cluster_actions module
  - POST /v2/clusters/{cluster_id}/actions/install
  - POST /v2/clusters/{cluster_id}/actions/reset
  - POST /v2/clusters/{cluster_id}/actions/cancel
  - Workflow operations

- **Phase 15**: infra_env_actions module
  - Download ISO operations
  - Image regeneration
  - Complex workflows

#### **Testing & Integration Phase**

- **Phase 16**: Integration tests
  - End-to-end workflows
  - Test against real API (with test clusters)
  - Playbook examples

- **Phase 17**: Advanced testing
  - Molecule tests
  - CI/CD with GitHub Actions
  - Ansible sanity tests for all modules

#### **Documentation Phase**

- **Phase 18**: Complete beginner guides
  - BEGINNERS_GUIDE.md
  - MODULE_DEVELOPMENT_WALKTHROUGH.md
  - LEARNING_PATH.md
  - QUICK_REFERENCE.md

- **Phase 19**: Module-specific guides
  - Guide for each module
  - Complex workflow examples
  - Troubleshooting guides

- **Phase 20**: Final polish
  - CONTRIBUTING.md
  - Update all README files
  - Collection packaging for Galaxy

## Module Structure Pattern

Each module follows this pattern (learned from events module):

```python
# 1. DOCUMENTATION - YAML describing module
# 2. EXAMPLES - Usage examples
# 3. RETURN - Return value documentation
# 4. Imports
# 5. Module logic
# 6. Main function
```

## Module Complexity Levels

### Level 1: Read-Only Simple (events, openshift_versions, supported_operators)
- Only GET operations
- Simple parameters
- No state management
- Always changed=False

### Level 2: Read-Only Complex (clusters list, infra_envs list)
- GET operations with complex filtering
- Pagination
- Multiple query parameters
- Still no state changes

### Level 3: CRUD Simple (clusters, infra_envs basic operations)
- Create, Read, Update, Delete
- State parameter (present/absent)
- Idempotency required
- Changed flag management

### Level 4: CRUD Complex (hosts with binding, manifests)
- Complex parameter validation
- File handling
- Multiple related operations
- State transitions

### Level 5: Workflows (cluster actions, multi-step operations)
- Orchestrate multiple API calls
- Wait for state changes
- Error recovery
- Complex error handling

## Estimated Timeline

### If Building Alone
- **Phases 1-3** (Foundation): 2-3 weeks ✅ (Phase 1 in PR)
- **Phases 4-6** (Read-only simple): 2 weeks
- **Phases 7-9** (Read-only complex): 3 weeks
- **Phases 10-12** (CRUD operations): 4 weeks
- **Phases 13-15** (Advanced operations): 3 weeks
- **Phases 16-17** (Testing): 2 weeks
- **Phases 18-20** (Documentation & polish): 2 weeks

**Total: ~18-20 weeks (4-5 months)**

### If Building with Team (2-3 developers)
- Parallel module development after Phase 3
- Multiple modules per sprint
- **Total: ~10-12 weeks (2.5-3 months)**

## Module Priority

### Must-Have (Core functionality)
1. ✅ events (in progress)
2. clusters (full CRUD)
3. infra_envs (full CRUD)
4. hosts
5. cluster_actions

### Should-Have (Important features)
6. manifests
7. openshift_versions
8. support_levels
9. supported_operators

### Nice-to-Have (Advanced features)
10. domains
11. Additional operators modules
12. Advanced workflow modules

## Learning Progression

The phased approach teaches progressively:

1. **Phases 1-3**: Basic module structure (current)
2. **Phases 4-6**: Pattern repetition with variation
3. **Phases 7-9**: Complex parameters and filtering
4. **Phases 10-12**: State management and idempotency
5. **Phases 13-15**: Advanced patterns
6. **Phases 16-20**: Professional practices (testing, docs)

## Repository Structure at Completion

```
cld_assistedinstaller/
├── plugins/
│   ├── modules/
│   │   ├── events.py
│   │   ├── clusters.py
│   │   ├── infra_envs.py
│   │   ├── hosts.py
│   │   ├── manifests.py
│   │   ├── cluster_actions.py
│   │   ├── infra_env_actions.py
│   │   ├── openshift_versions.py
│   │   ├── support_levels.py
│   │   ├── supported_operators.py
│   │   └── ... (additional modules)
│   ├── module_utils/
│   │   ├── apitoken.py
│   │   ├── apiurl.py
│   │   ├── common.py (shared functions)
│   │   └── validators.py (parameter validation)
│   └── requirements.txt
├── tests/
│   ├── unit/
│   │   ├── test_events.py
│   │   ├── test_clusters.py
│   │   ├── test_infra_envs.py
│   │   └── ... (one per module)
│   ├── integration/
│   │   └── targets/
│   │       ├── events/
│   │       ├── clusters/
│   │       └── ... (integration test suites)
│   └── run_tests.sh
├── docs/
│   ├── BEGINNERS_GUIDE.md
│   ├── modules/
│   │   ├── events.md
│   │   ├── clusters.md
│   │   ├── infra_envs.md
│   │   └── ... (one per module)
│   └── workflows/
│       ├── create_cluster.md
│       ├── deploy_host.md
│       └── ... (workflow guides)
└── examples/
    ├── events.yml
    ├── clusters.yml
    ├── workflows/
    │   ├── full_cluster_deployment.yml
    │   └── ... (complex examples)
    └── README.md
```

## Benefits of Phased Approach

### For Beginners
- ✅ Learn progressively (simple → complex)
- ✅ Master patterns before complexity
- ✅ Each module builds on previous learning
- ✅ Can contribute at their skill level

### For Project
- ✅ Incremental value delivery
- ✅ Early modules usable before completion
- ✅ Pattern consistency across modules
- ✅ Quality maintained throughout

### For Reviewers
- ✅ Small, focused PRs per module
- ✅ Can review independently
- ✅ Clear scope per phase
- ✅ Easy to spot issues early

## Module Reusability

As we build more modules, we extract common patterns:

### Shared Utilities (module_utils/)

**common.py:**
- handle_api_error(response, module)
- build_query_params(params, param_list)
- check_required_params(module, required)

**validators.py:**
- validate_uuid(value)
- validate_ssh_key(value)
- validate_ip_address(value)

**pagination.py:**
- handle_pagination(url, headers, params)

### Module Templates

Create templates for each complexity level:
- read_only_simple_template.py
- crud_module_template.py
- workflow_module_template.py

## Success Criteria for Full Coverage

### Code Quality
- ✅ All modules follow same pattern
- ✅ Comprehensive test coverage (>80%)
- ✅ Passes ansible-test sanity
- ✅ Documented with examples

### Documentation
- ✅ Guide for each module
- ✅ Workflow examples
- ✅ Troubleshooting guides
- ✅ Beginner-friendly throughout

### Usability
- ✅ Can deploy full cluster via playbooks
- ✅ Idempotent operations
- ✅ Clear error messages
- ✅ Comprehensive examples

### Community
- ✅ Published to Ansible Galaxy
- ✅ Active issue tracking
- ✅ Contribution guidelines
- ✅ Maintainer documentation

## Next Steps

1. **Complete Phase 1-3** (events module) - Learn the basics
2. **Decide on priority modules** - Which APIs are most important?
3. **Create module templates** - Reusable patterns
4. **Plan module sprints** - Group related modules
5. **Build progressively** - Simple → Complex

## Comparison: Single Module vs Full Coverage

| Aspect | Single Module (Events) | Full API Coverage |
|--------|----------------------|-------------------|
| **Modules** | 1 | ~10-15 |
| **Complexity** | Read-only | Full CRUD + workflows |
| **Timeline** | 4-6 weeks | 4-5 months (solo) |
| **Lines of Code** | ~500 | ~5,000-10,000 |
| **Test Files** | 1 | ~10-15 |
| **Documentation** | 5-7 docs | 20-30 docs |
| **PRs** | 5-10 | 20+ |
| **Learning Value** | Basic patterns | Complete mastery |
| **Production Use** | Limited | Full automation |

## Recommendation

### For Learning (Current Goal)
**Stick with Phases 1-10:**
- Events module (read-only)
- 1-2 additional read-only modules
- 1 CRUD module (clusters or infra_envs)
- Comprehensive documentation
- **Timeline: 2-3 months**
- **Result: Complete learning experience**

### For Production Use
**Build full coverage (Phases 1-20):**
- All major API endpoints
- Workflow automation
- Production-ready testing
- Complete documentation
- **Timeline: 4-5 months (solo) or 2-3 months (team)**
- **Result: Production-ready collection**

## Summary

Expanding to full API coverage means:
- ✅ **20 phases** instead of 10
- ✅ **10-15 modules** instead of 1
- ✅ **4-5 months** instead of 1-2 months
- ✅ **Complete automation** of Assisted Installer workflows
- ✅ **Deep mastery** of Ansible module development

The phased approach scales perfectly - each new module follows the same PR workflow and learning principles established in Phase 1-3.

---

**Current Status:** Phase 1 complete, focusing on events module (Phases 2-3)
**Decision Point:** After Phase 3, decide whether to continue with full coverage or stop after learning basics
