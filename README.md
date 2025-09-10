# Rental-Locks-Tool
Tool to help me manage my rental locks

This repository contains Home Assistant configuration for managing rental property locks and automation.

## Branch Protection

This repository requires all GitHub workflows to pass before code can be merged. See [BRANCH_PROTECTION.md](BRANCH_PROTECTION.md) for setup instructions.

## Workflows

- **Home Assistant Config Check**: Validates configuration files
- **YAML Lint**: Ensures proper YAML formatting

## Getting Started

1. Review the `configuration.yaml` file and customize for your setup
2. Configure your actual lock platforms (replace commented examples)
3. Test your configuration locally before pushing changes

## Local Testing

```bash
# Test YAML formatting
yamllint .

# Test Home Assistant configuration  
docker run --rm -v $(pwd):/config homeassistant/home-assistant:stable hass -c /config --script check_config
```
