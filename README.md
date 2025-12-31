# WhiteDevil-93 Centralized GitHub Actions Workflows

This repository contains enhanced, autonomous GitHub Actions workflows designed for the WhiteDevil-93 personal account. These workflows can be referenced by any repository in your personal account.

## Repository Structure

```
.github/
├── workflows/
│   ├── CI_Pipeline_Enhanced.yml          # Continuous Integration
│   ├── Central_Command_AI_Enhanced.yml   # Issue-based code analysis
│   ├── Deployment_Pipeline_Enhanced.yml  # Autonomous deployments
│   ├── Jules_Apply_Changes_Enhanced.yml  # Automatic patch application
│   ├── Jules_Integration_Enhanced.yml    # AI agent review system
│   ├── Minimax_Review_Enhanced.yml       # Configurable code review
│   ├── Minimax_Verify_Jules_Enhanced.yml # Autonomous verification
│   └── Security_Compliance_Enhanced.yml  # Security scanning
└── README.md
```

## Features

### 🤖 Autonomous Capabilities
- **Intelligent Retry Logic**: Exponential backoff for transient failures
- **Circuit Breaker Pattern**: Prevents cascading failures
- **Automatic Fallback**: Graceful degradation when services are unavailable
- **Self-Healing**: Auto-fix capabilities for common issues
- **Dynamic Configuration**: Adapts behavior based on context

### 📊 Enhanced Workflows

1. **CI Pipeline Enhanced**
   - Auto-fixing code formatters (Black, Prettier)
   - Test retry with flaky test detection
   - Security scan with false positive filtering
   - Quality gate with non-critical failure tolerance

2. **Deployment Pipeline Enhanced**
   - Docker build with retry and cache recovery
   - Multi-environment support (dev, staging, prod)
   - Configurable deployment strategies
   - Automatic health checks with rollback

3. **Security & Compliance Enhanced**
   - Configurable scan depth (quick, full, deep)
   - Automatic false positive filtering
   - License compliance checking
   - Comprehensive reporting

4. **Jules Integration Enhanced**
   - Configurable AI model selection
   - Comprehensive compliance scoring
   - Security finding extraction
   - Agent architecture analysis

5. **Minimax Review Enhanced**
   - Configurable scope (full, files, changed)
   - Analysis depth options (quick, standard, thorough)
   - Intelligent file selection
   - Issue categorization

6. **Central Command AI Enhanced**
   - Automatic project type detection
   - Dynamic file extension selection
   - Circuit breaker protection
   - Priority file analysis

7. **Minimax Verify Jules Enhanced**
   - Branch detection and comparison
   - Confidence scoring (0-100%)
   - Automatic fallback to manual review
   - Recovery action generation

8. **Jules Apply Changes Enhanced**
   - Patch parsing and categorization
   - Safety checks before applying
   - Git stash backup
   - Automatic PR generation

## Usage

### Method 1: Direct Copy
Copy workflow files to your repository's `.github/workflows/` directory.

### Method 2: Git Submodule
Add this repository as a submodule:
```bash
git submodule add https://github.com/WhiteDevil-93/.github.git .github/workflows-templates
```

### Method 3: Template Reference
Reference workflows using `uses`:
```yaml
jobs:
  my-job:
    uses: WhiteDevil-93/.github/.github/workflows/CI_Pipeline_Enhanced.yml@main
```

### Method 4: Repository Dispatch
Trigger workflows from other repositories via API:
```bash
curl -X POST \
  -H "Authorization: token $GITHUB_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  "https://api.github.com/repos/WhiteDevil-93/.github/dispatches" \
  -d '{"event_type": "trigger-ci", "client_payload": {"repo": "your-repo"}}'
```

## Configuration

### Workflow Inputs

Many workflows accept configurable inputs via `workflow_dispatch`:

```yaml
on:
  workflow_dispatch:
    inputs:
      scope:
        description: 'Analysis scope'
        type: choice
        options:
          - full
          - incremental
      depth:
        description: 'Analysis depth'
        type: choice
        options:
          - quick
          - standard
          - thorough
```

### Secrets Required

Configure these secrets in your repository:

- `ATLAS_API_KEY` - For Minimax/Jules verification
- `MINIMAX_API_KEY` - For Minimax code review
- `PERSONAL_ACCESS_TOKEN` - For cross-repository access
- `GITHUB_TOKEN` - Auto-provided by GitHub Actions

### Environment Variables

Workflows use sensible defaults but can be customized:

```yaml
env:
  MAX_RETRIES: 3
  SEVERITY_THRESHOLD: 'medium'
  HEALTH_CHECK_TIMEOUT: 120
```

## Autonomy Features Explained

### Retry Logic with Exponential Backoff

```yaml
# Example from workflow
env:
  MAX_RETRIES: 3
  BACKOFF_FACTOR: 2

steps:
  - name: Call API with retry
    run: |
      for attempt in $(seq 1 $MAX_RETRIES); do
        if curl --max-time 30 "https://api.example.com"; then
          break
        fi
        sleep $((attempt * BACKOFF_FACTOR))
      done
```

### Circuit Breaker Pattern

```yaml
# Automatic circuit breaker prevents cascading failures
env:
  CIRCUIT_BREAKER_THRESHOLD: 3

steps:
  - name: Protected API call
    run: |
      # After 3 failures, skip remaining attempts
      # and use fallback mechanism
```

### Auto-Fixing

```yaml
# Black formatter auto-fix
- name: Auto-fix formatting
  run: black .  # Automatically fixes issues

# Prettier auto-fix  
- name: Auto-fix formatting
  run: prettier --write .
```

### False Positive Filtering

```python
# Security scans automatically filter known patterns
KNOWN_FALSE_POSITIVES = [
    "placeholder",
    "test_key", 
    "dummy_value",
    "example"
]
```

## Best Practices

1. **Start with dry-run mode** for deployment workflows
2. **Configure severity thresholds** based on your security requirements
3. **Set up notifications** to receive alerts for workflow failures
4. **Monitor retry counts** to identify persistent issues
5. **Review compliance reports** weekly
6. **Update AI models** as new versions become available

## Troubleshooting

### Common Issues

1. **Workflow not triggering**
   - Check event triggers in workflow file
   - Verify repository permissions
   - Ensure secrets are configured

2. **API rate limiting**
   - Reduce workflow frequency
   - Use caching to minimize API calls
   - Implement exponential backoff (already included)

3. **Deployment failures**
   - Check dry-run mode first
   - Verify Kubernetes/configurations
   - Review health check settings

4. **Security scans finding false positives**
   - Update false positive filters
   - Adjust severity thresholds
   - Add custom ignore patterns

### Logs and Debugging

- Check workflow run logs in GitHub Actions tab
- Review artifact files for detailed reports
- Enable debug mode with `ACTIONS_STEP_DEBUG: true`

## Contributing

To update workflows:

1. Fork this repository
2. Make enhancements
3. Submit pull request
4. After merge, update dependent repositories

## Support

- Review workflow documentation inline
- Check GitHub Actions documentation
- Open issues for bugs or feature requests

## License

These workflows are provided as-is for personal use. Modify as needed for your specific requirements.

---

**Repository**: https://github.com/WhiteDevil-93/.github  
**Enhanced Workflows**: 8 autonomous workflows with self-healing capabilities
