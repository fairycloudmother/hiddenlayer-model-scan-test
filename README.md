# HiddenLayer Model Scan – Hugging Face Integration

This repository demonstrates the use of HiddenLayer's GitHub Action to scan machine learning models hosted on Hugging Face. It uses **Community Scan** mode to analyze models for potential vulnerabilities or malicious behavior.

![Scan workflow](https://github.com/fairycloudmother/hiddenlayer-model-scan-test/actions/workflows/scan-hf-model.yml/badge.svg)

---

## Model Being Scanned

| Source        | Model ID        | Version |
|---------------|------------------|---------|
| Hugging Face | ScanMe/Models     | main    |

---

## GitHub Actions Workflow

This repository includes a GitHub Actions workflow that triggers a security scan on a specified Hugging Face model. The workflow can be manually triggered from the **Actions** tab.

## Workflow File

`.github/workflows/scan-hf-model.yml`

```yaml
name: Scan HuggingFace Model (ScanMe/Models)

on:
  workflow_dispatch:

jobs:
  scan_huggingface_model_community_scan:
    runs-on: ubuntu-latest
    name: Scan ScanMe/Models via Community Scan
    steps:
      - uses: actions/checkout@v3
      - name: Scan model on HuggingFace
        id: scan_model_huggingface
        uses: hiddenlayerai/hiddenlayer-model-scan-github-action@v1.0.2
        with:
          model_path: ScanMe/Models
          model_version: main
          community_scan: HUGGING_FACE
        env:
          HL_CLIENT_ID: ${{ secrets.HL_CLIENT_ID }}
          HL_CLIENT_SECRET: ${{ secrets.HL_CLIENT_SECRET }}

---

## Prerequisites

Before using this workflow, ensure you have:

- A GitHub account with access to this repository
- A [HiddenLayer](https://hiddenlayer.ai) account with API credentials

---

## Getting Started

To use this workflow in your own project:

1. **Fork or clone** this repository.
2. Update the `model_path` and `model_version` in `.github/workflows/scan-hf-model.yml` to target your desired Hugging Face model.
3. Add the required secrets to your GitHub repository:
   - `HL_CLIENT_ID`
   - `HL_CLIENT_SECRET`
4. Navigate to the **Actions** tab in your GitHub repository.
5. Select the workflow titled **Scan HuggingFace Model**.
6. Click **Run workflow** to trigger a scan.

---

## Required Secrets

To run the scan, add the following secrets in your repository settings:

- `HL_CLIENT_ID` – your HiddenLayer API client ID  
- `HL_CLIENT_SECRET` – your HiddenLayer API client secret

> These can be obtained from your [HiddenLayer account](https://hiddenlayer.ai) under the API section.

---

## Scan Results

Scan results will appear directly in the GitHub Actions log output. These include:

- Vulnerability findings
- Warnings about malicious behavior
- Model metadata and scan diagnostics

> If you're on a plan that supports it, HiddenLayer may also provide a downloadable report or link to a scan dashboard.

---

## Resources

- [HiddenLayer Model Scanner GitHub Action](https://github.com/hiddenlayerai/hiddenlayer-model-scan-github-action)
- [HiddenLayer Website](https://hiddenlayer.ai)
- [ScanMe/Models on Hugging Face](https://huggingface.co/ScanMe/Models)

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
