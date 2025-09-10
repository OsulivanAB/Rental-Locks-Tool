# Branch Protection Setup

This repository is configured to require all GitHub workflows to pass before code can be merged to the main branch.

## Automated Setup (Recommended)

### Option 1: GitHub Settings App
1. Install the [GitHub Settings App](https://github.com/apps/settings) on your repository
2. The `.github/settings.yml` file in this repository will automatically configure branch protection rules

### Option 2: Manual Setup
If you prefer to set up branch protection manually:

1. Go to your repository's Settings tab
2. Click on "Branches" in the left sidebar
3. Click "Add rule" or edit the existing rule for the main branch
4. Configure the following settings:

   **Branch name pattern:** `main`
   
   **Protect matching branches:**
   - ☑️ Require a pull request before merging
     - ☑️ Require approvals: 1
     - ☑️ Dismiss stale pull request approvals when new commits are pushed
   - ☑️ Require status checks to pass before merging
     - ☑️ Require branches to be up to date before merging
     - **Required status checks:**
       - `Check Home Assistant Configuration`
       - `YAML Lint Check`
   - ☑️ Do not allow bypassing the above settings

## What This Protects Against

1. **Invalid Home Assistant Configuration:** The `check-config.yml` workflow validates that all Home Assistant YAML files are syntactically correct and follow HA standards
2. **YAML Formatting Issues:** The `yamllint.yml` workflow ensures all YAML files follow consistent formatting standards
3. **Direct Pushes to Main:** All changes must go through pull requests
4. **Unreviewed Changes:** At least one approval is required before merging

## Workflows in This Repository

### Check Home Assistant Configuration
- **File:** `.github/workflows/check-config.yml`
- **Purpose:** Validates Home Assistant configuration files
- **Triggers:** Push and Pull Request events
- **Uses:** Official Home Assistant Docker image

### YAML Lint
- **File:** `.github/workflows/yamllint.yml`  
- **Purpose:** Ensures YAML files follow formatting standards
- **Triggers:** Push and Pull Request events
- **Uses:** yamllint with strict parsing

## Testing Locally

You can run the same checks locally before pushing:

```bash
# Test YAML linting
yamllint .

# Test Home Assistant configuration
docker run --rm -v $(pwd):/config homeassistant/home-assistant:stable hass -c /config --script check_config
```

## Pre-commit Hooks

This repository includes pre-commit hooks for YAML linting:

```bash
# Install pre-commit
pip install pre-commit

# Install the hooks
pre-commit install

# Run hooks manually
pre-commit run --all-files
```