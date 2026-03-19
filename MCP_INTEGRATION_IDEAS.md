# MCP (Model Context Protocol) Integration Ideas

**Status**: Planning - To be implemented after PR refactoring
**Date**: 2026-03-11

## Overview

This document outlines potential MCP server integrations that could enhance the `cld_assistedinstaller` project, making it easier for beginners to develop Ansible modules and work with the OpenShift Assisted Installer API.

## What is MCP?

Model Context Protocol (MCP) is a protocol that allows AI assistants like Claude to interact with external tools and data sources through standardized servers. For this project, MCP servers could provide:
- Direct API access for exploration and testing
- Development assistance tools
- Enhanced documentation access
- Mock data for testing without credentials

## Proposed MCP Servers

### 1. OpenShift Assisted Installer MCP Server ⭐ PRIORITY 1

**Purpose**: Wrap the OpenShift Assisted Installer API as an MCP server

**Priority**: ⭐⭐⭐⭐⭐
**Effort**: Medium
**Impact**: High - Enables API exploration and testing

#### Proposed Tools

```typescript
// Example tool definitions
{
  "list_events": {
    "description": "Get cluster events with filters",
    "parameters": {
      "cluster_id": "optional string",
      "limit": "optional integer",
      "order": "optional string (ascending/descending)",
      "offset": "optional integer",
      "severities": "optional array of strings"
    }
  },
  "get_cluster": {
    "description": "Retrieve cluster details",
    "parameters": {
      "cluster_id": "required string"
    }
  },
  "list_clusters": {
    "description": "List all clusters",
    "parameters": {
      "limit": "optional integer",
      "offset": "optional integer"
    }
  },
  "get_infra_env": {
    "description": "Get infrastructure environment details",
    "parameters": {
      "infra_env_id": "required string"
    }
  }
  // ... additional endpoints as we implement more modules
}
```

#### Benefits

- **Interactive API exploration**: Users can explore API endpoints without writing Ansible code first
- **Real-time API documentation**: Fetch live schema/documentation from the API
- **Easier testing**: Test API calls before implementing Ansible modules
- **Beginner-friendly**: Newcomers can experiment with the API through Claude before coding
- **Faster development**: Quickly verify API behavior during module development

#### User Workflow Example

```bash
# Install the MCP server
npm install -g @vjayaramrh/mcp-server-assisted-installer

# Configure in Claude Code MCP settings
# ~/.claude/mcp_settings.json

# Then users can ask Claude:
"Show me events for cluster abc123"
"What does the events API return?"
"Test the API with severity=critical"
"List all clusters with more than 10 nodes"
```

#### Implementation Notes

- Base URL: `https://api.openshift.com/api/assisted-install/v2`
- Authentication: Bearer token from environment variable
- Should support both `AI_API_TOKEN` and `AI_OFFLINE_TOKEN`
- Error handling for 401, 404, 500 responses
- Response caching for better performance

#### File Structure

```
mcp-server-assisted-installer/
├── package.json
├── tsconfig.json
├── src/
│   ├── index.ts          # Main MCP server
│   ├── api/
│   │   ├── client.ts     # HTTP client with auth
│   │   ├── events.ts     # Events endpoint handlers
│   │   ├── clusters.ts   # Clusters endpoint handlers
│   │   └── ...           # Other endpoints
│   ├── auth.ts           # Token management
│   └── types.ts          # TypeScript types
├── README.md
└── examples/
    └── usage.md
```

---

### 2. Testing & Mock API MCP Server ⭐ PRIORITY 2

**Purpose**: Provide mock API responses for testing without real credentials

**Priority**: ⭐⭐⭐⭐
**Effort**: Low
**Impact**: Medium - Enables offline development

#### Proposed Tools

```typescript
{
  "mock_events_api": {
    "description": "Return sample events data",
    "parameters": {
      "cluster_id": "optional string",
      "count": "optional integer (number of events to return)"
    }
  },
  "mock_cluster_api": {
    "description": "Return sample cluster data",
    "parameters": {
      "cluster_id": "optional string"
    }
  },
  "simulate_api_error": {
    "description": "Test error handling scenarios",
    "parameters": {
      "error_type": "required string (401, 404, 500, network_error)"
    }
  },
  "validate_request": {
    "description": "Check if request format matches API spec",
    "parameters": {
      "endpoint": "required string",
      "parameters": "required object"
    }
  }
}
```

#### Benefits

- **No authentication required**: Beginners can test without Red Hat account
- **Faster development iteration**: No network latency
- **Offline development**: Work without internet connection
- **Consistent test data**: Same data every time for reproducible tests
- **Error scenario testing**: Easily test error handling code

#### Implementation Notes

- Store sample JSON responses in `fixtures/` directory
- Use realistic data based on actual API responses
- Support all query parameters for filtering
- Include edge cases (empty results, pagination, etc.)

---

### 3. Ansible Module Development Assistant MCP Server

**Purpose**: Provide development assistance specific to Ansible module creation

**Priority**: ⭐⭐⭐
**Effort**: Medium
**Impact**: Medium - Helps beginners write better code

#### Proposed Tools

```typescript
{
  "validate_module_syntax": {
    "description": "Check if module code follows Ansible conventions",
    "parameters": {
      "module_path": "required string"
    }
  },
  "generate_module_docs": {
    "description": "Auto-generate DOCUMENTATION section from code",
    "parameters": {
      "module_path": "required string"
    }
  },
  "test_module_locally": {
    "description": "Run module with test parameters",
    "parameters": {
      "module_name": "required string",
      "parameters": "required object"
    }
  },
  "check_ansible_best_practices": {
    "description": "Lint against Ansible guidelines",
    "parameters": {
      "module_path": "required string"
    }
  },
  "generate_test_cases": {
    "description": "Suggest test cases based on module parameters",
    "parameters": {
      "module_path": "required string"
    }
  }
}
```

#### Benefits

- **Real-time validation**: Check code as you write
- **Instant feedback**: Learn best practices immediately
- **Automated documentation**: Generate docs from code
- **Test suggestions**: Don't miss important test cases

---

### 4. Repository Context MCP Server

**Purpose**: Serve project documentation as MCP resources

**Priority**: ⭐⭐⭐
**Effort**: Low
**Impact**: Medium - Better documentation access

#### Proposed Resources

```typescript
{
  "beginners-guide": "docs/BEGINNERS_GUIDE.md",
  "module-walkthrough": "docs/MODULE_DEVELOPMENT_WALKTHROUGH.md",
  "concepts": "docs/CONCEPTS.md",
  "quick-reference": "docs/QUICK_REFERENCE.md",
  "learning-path": "docs/LEARNING_PATH.md",
  "testing-guide": "docs/TESTING_GUIDE.md",
  "events-module-guide": "docs/events_module_guide.md",
  "contributing": "CONTRIBUTING.md",
  "implementation-plan": "IMPLEMENTATION_PLAN.md",
  "project-requirements": "PROJECT_REQUIREMENTS.md"
}
```

#### Benefits

- **Context-aware help**: Claude can reference exact, up-to-date documentation
- **Smart suggestions**: Recommendations based on current learning stage
- **Synchronized docs**: Always refers to the latest version
- **Reduced copy-paste**: Documentation is directly accessible

#### Implementation Notes

- Can use the built-in filesystem MCP server
- Configure to watch the `docs/` directory
- Update as documentation evolves
- Could also expose code examples from `examples/`

---

### 5. Learning Progress Tracker MCP Server

**Purpose**: Track beginner progress through the learning path

**Priority**: ⭐⭐
**Effort**: Medium
**Impact**: Low - Nice to have for gamification

#### Proposed Tools

```typescript
{
  "mark_checkpoint_complete": {
    "description": "Mark a learning checkpoint as complete",
    "parameters": {
      "checkpoint_id": "required string",
      "notes": "optional string"
    }
  },
  "get_next_step": {
    "description": "Get the next recommended learning step",
    "parameters": {}
  },
  "show_progress": {
    "description": "Display learning progress summary",
    "parameters": {}
  },
  "recommend_resources": {
    "description": "Get context-aware resource recommendations",
    "parameters": {
      "current_topic": "optional string"
    }
  },
  "reset_progress": {
    "description": "Reset learning progress",
    "parameters": {}
  }
}
```

#### Benefits

- **Motivation**: Gamification encourages learning
- **Personalized path**: Adapts to individual progress
- **Progress persistence**: Remembers where you left off
- **Smart recommendations**: Suggests next steps based on completion

---

## Implementation Roadmap

### Phase 1: Core API Access (Highest Value)
**Target**: After PR refactoring complete

1. Implement OpenShift Assisted Installer MCP Server
2. Support events, clusters, infra-envs endpoints
3. Add authentication with token management
4. Create basic documentation
5. Publish to npm as `@vjayaramrh/mcp-server-assisted-installer`

**Deliverables**:
- Working MCP server npm package
- README with setup instructions
- Example usage scenarios
- Integration guide for Claude Code

### Phase 2: Testing Support
**Target**: During Phase 2-3 of module implementation

1. Implement Mock API MCP Server
2. Create fixture data for all endpoints
3. Add error simulation capabilities
4. Document testing workflow with mock server

**Deliverables**:
- Mock MCP server
- Fixture data library
- Testing guide using mock server
- CI/CD integration examples

### Phase 3: Development Tools
**Target**: After core modules implemented

1. Implement Ansible Module Development Assistant
2. Add validation and linting tools
3. Create doc generation tools
4. Add test case suggestions

**Deliverables**:
- Development assistant MCP server
- Ansible best practices checker
- Documentation generator
- Test scaffolding tools

### Phase 4: Enhanced Experience (Optional)
**Target**: Future enhancement

1. Repository Context MCP Server setup
2. Learning Progress Tracker (if desired)
3. Integration with CI/CD
4. Advanced features based on user feedback

## Integration with Learning Path

The MCP servers should be introduced in the learning path as follows:

### For Beginners (BEGINNERS_GUIDE.md)
- Add section: "Using the MCP Server to Explore the API"
- Show how to test API calls before writing code
- Demonstrate mock server for offline practice

### In Walkthrough (MODULE_DEVELOPMENT_WALKTHROUGH.md)
- Add Step 0.5: "Explore the API with MCP"
- Show API exploration before implementation
- Use MCP to understand API responses

### In Testing Guide (TESTING_GUIDE.md)
- Document mock MCP server usage
- Show how to test without credentials
- Demonstrate error scenario testing

## Technical Considerations

### Authentication
- Support both `AI_API_TOKEN` and `AI_OFFLINE_TOKEN` environment variables
- Implement token refresh for offline tokens
- Cache tokens to reduce SSO requests
- Clear error messages for auth failures

### Error Handling
- Graceful degradation if API is unavailable
- Detailed error messages for debugging
- Retry logic for transient failures
- Offline mode with mock data

### Performance
- Response caching with configurable TTL
- Request rate limiting to respect API quotas
- Parallel request support where appropriate
- Efficient JSON parsing and validation

### Security
- Never log or expose tokens
- Secure token storage
- HTTPS only for API calls
- Input validation to prevent injection

### Documentation
- Clear setup instructions
- Example workflows for common tasks
- Troubleshooting guide
- API endpoint reference

## Success Metrics

How to measure if MCP integration is successful:

1. **Adoption**: Number of users installing MCP servers
2. **Engagement**: API calls through MCP vs direct module usage
3. **Learning**: Time to first working module (before/after MCP)
4. **Feedback**: User ratings and comments
5. **Contribution**: PRs from users who used MCP for learning

## Resources Required

### Development
- 2-3 weeks for Phase 1 (OpenShift MCP Server)
- 1 week for Phase 2 (Mock Server)
- 2 weeks for Phase 3 (Dev Assistant)
- 1 week for Phase 4 (Documentation/Learning)

### Documentation
- MCP server README files
- Integration guides for Claude Code
- Tutorial updates to include MCP workflows
- Troubleshooting documentation

### Testing
- Unit tests for MCP server tools
- Integration tests with Claude Code
- Mock data validation
- Performance testing

### Maintenance
- Keep up with API changes
- Update mock data as API evolves
- Respond to user issues
- Regular dependency updates

## Related Projects

Similar MCP implementations to learn from:

1. **GitHub MCP Server**: API wrapper pattern
2. **Filesystem MCP Server**: Resource serving pattern
3. **Brave Search MCP Server**: External API integration
4. **Postgres MCP Server**: Structured data access

## Questions to Resolve

Before implementation:

1. Should we create separate MCP servers or one unified server?
2. What's the preferred installation method (npm, pip, docker)?
3. Should mock data be bundled or downloaded separately?
4. How to handle API versioning (v2 vs future v3)?
5. Should we contribute upstream to official OpenShift tooling?

## Next Steps

1. ✅ Document MCP integration ideas (this file)
2. ⏳ Complete PR refactoring
3. ⏳ Implement core Ansible modules
4. ⏳ Create OpenShift Assisted Installer MCP Server prototype
5. ⏳ Test with real beginners
6. ⏳ Gather feedback and iterate
7. ⏳ Publish stable version

## References

- [MCP Specification](https://modelcontextprotocol.io/)
- [OpenShift Assisted Installer API](https://api.openshift.com/?urls.primaryName=assisted-service%20service)
- [Ansible Module Development](https://docs.ansible.com/ansible/latest/dev_guide/developing_modules_general.html)
- [TypeScript MCP SDK](https://github.com/modelcontextprotocol/typescript-sdk)

---

**Note**: This is a living document. Update as ideas evolve and implementation progresses.
