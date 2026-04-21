## Onboarding Package

### Prerequisite Checklist
1. **Azure Subscription**: Ensure access to an active Azure subscription.
2. **GitHub Organization**: Verify access to the customer’s GitHub organization.
3. **Installed Tools**:
   - GitHub CLI (`gh`) version 2.0+
   - Node.js version 16+
   - Visual Studio Code with GitHub Copilot extension
4. **Roles and Permissions**:
   - Owner or Admin access to the GitHub repository.
   - Contributor role in the Azure subscription.

### Automated Setup Script (Bash)
```bash
#!/bin/bash

# Variables
GITHUB_ORG="customer-org"
AZURE_SUBSCRIPTION_ID="your-subscription-id"

# Check GitHub CLI
if ! command -v gh &> /dev/null; then
  echo "GitHub CLI not installed. Install it from https://cli.github.com/"
  exit 1
fi

# Check Node.js
if ! command -v node &> /dev/null; then
  echo "Node.js not installed. Install it from https://nodejs.org/"
  exit 1
fi

# Authenticate with GitHub
gh auth status || gh auth login

# Authenticate with Azure
az account show || az login

# Set Azure subscription
az account set --subscription $AZURE_SUBSCRIPTION_ID

echo "Setup complete. All prerequisites are met."
```

### Readiness Validator
```bash
#!/bin/bash

# Validate GitHub CLI
if ! command -v gh &> /dev/null; then
  echo "FAIL: GitHub CLI not installed."
  exit 1
else
  echo "PASS: GitHub CLI installed."
fi

# Validate Node.js
if ! command -v node &> /dev/null; then
  echo "FAIL: Node.js not installed."
  exit 1
else
  echo "PASS: Node.js installed."
fi

# Validate Azure CLI
if ! command -v az &> /dev/null; then
  echo "FAIL: Azure CLI not installed."
  exit 1
else
  echo "PASS: Azure CLI installed."
fi

echo "All checks passed. Ready to proceed."
```

---
