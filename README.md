# 🟢 Greenlight Zero-Trust Security Audit

[![Release](https://img.shields.io/github/v/release/devexsolutions/greenlight-action?style=flat-square&color=10b981)](https://github.com/devexsolutions/greenlight-action/releases)
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![Zero Trust](https://img.shields.io/badge/Architecture-Zero%20Trust-10b981?style=flat-square)](#zero-trust-architecture)

**Greenlight** is an enterprise-grade DevSecOps auditing tool designed specifically for modern iOS and Apple platform ecosystems. 

This official GitHub Action allows you to seamlessly integrate our powerful scanning engine into your CI/CD pipelines, ensuring your code meets App Store guidelines and security standards *before* it gets deployed.

## 🛡 Zero-Trust Architecture

We believe your source code is your most valuable asset. That's why Greenlight operates on a strict **Zero-Trust (Push-Only) Model**:
1. **Local Execution:** Our scanning binary runs entirely within your GitHub Actions runner infrastructure.
2. **No Source Code Access:** We **never** clone, download, or access your repository's code on our servers.
3. **Telemetry Only:** The Action only transmits the final metadata report (status, issues count, and security findings) to the Greenlight Dashboard.

## 🚀 Quick Start

### 1. Get your API Token
Log in to your [Greenlight Dashboard](https://greenlight.qercus.tech) and copy your **Integration Credential Token**.

### 2. Configure GitHub Secrets
In your GitHub repository, navigate to `Settings > Secrets and variables > Actions > New repository secret`.
*   **Name:** `GREENLIGHT_API_TOKEN`
*   **Secret:** Paste your token here.

### 3. Add the Workflow
Create a new file in your repository at `.github/workflows/greenlight-audit.yml` and paste the following code:

```yaml
name: Greenlight Security Audit

on:
  push:
    branches: [ "main", "develop" ]
  pull_request:
    branches: [ "main" ]

jobs:
  audit:
    runs-on: ubuntu-latest
    name: Code Scan
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Run Greenlight Zero-Trust Scan
        uses: qercustech/greenlight-action@v1
        with:
          api_token: ${{ secrets.GREENLIGHT_API_TOKEN }}
```

⚙️ Inputs

| Input     | Description                                           | Required | Default                                             |
|-----------|-------------------------------------------------------|----------|-----------------------------------------------------|
| api_token | Your Greenlight Integration Token                     | Yes      | null                                                |
| api_url   | Override the default telemetry endpoint (for testing) | No       | https://greenlight.qercus.tech/api/telemetry/report |
|           |                                                       |          |                                                     |


📊 Viewing Results
Once the Action completes, the results are immediately broadcasted in real-time to your Greenlight Dashboard. You can review failed checks, view specific App Store guideline violations, and get actionable fixes directly from the UI.

🤝 Support & Documentation
For detailed guides, troubleshooting, and best practices, please visit our Official Documentation.

Built with precision for developers by QercusTech.
