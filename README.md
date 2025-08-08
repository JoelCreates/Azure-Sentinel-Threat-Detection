# Azure Sentinel Threat Detection Lab

## Objective
Detect and investigate three simulated attacks using Microsoft Sentinel, then document investigation steps, detections, playbooks, and measurable improvements. This repo is designed to look like professional SOC artefacts rather than course notes.

## Scenarios Covered
1. **Encoded PowerShell abuse** that downloads and runs a script.
2. **RDP brute-force pattern** against a test host.
3. **OneDrive data exfiltration signal** to mimic abnormal file access or sync behaviour.

## Tools and Services
- Microsoft Azure tenant
- Microsoft Sentinel
- Microsoft Defender for Cloud
- Microsoft Defender for Endpoint (optional but recommended)
- KQL for analytics rules and hunting queries
- PowerShell where needed to simulate activity

## Architecture (high level)
- Windows test VM onboarded to Defender for Endpoint
- Log sources: Sign-in logs, Microsoft 365, Defender, and VM telemetry where available
- Sentinel workspace with data connectors enabled

## What you will produce
- **KQL analytics rules** for each scenario
- **Investigation reports** with timeline, entities, query outputs, and conclusion
- **Response playbooks** showing steps taken
- **Screenshots** of alerts, investigation graph, and before/after suppression tuning
- **Metrics** like MTTA improvement after rule tuning

## Folder Guide
- `kql-rules/` KQL files for analytics rules and hunts
- `incident-reports/` One report per scenario
- `playbooks/` Stepwise response runbooks
- `screenshots/` Evidence of alerts, queries, and investigations

## Step-by-step Instructions
1. **Provision**: Create a new Azure tenant or use an existing subscription. Enable Microsoft Sentinel and create a Log Analytics workspace.
2. **Connect data**: Enable Microsoft Entra sign-in logs, Microsoft 365 data, Defender for Cloud, and Defender for Endpoint if available.
3. **Onboard a VM**: Join a Windows VM to Defender for Endpoint so you can simulate PowerShell events.
4. **Simulate attacks**:
   - Encoded PowerShell: run an innocuous Base64-encoded command that touches the network or file system.
   - RDP brute-force: generate failed sign-in attempts from a controlled source to your test VM.
   - OneDrive signal: access and sync a burst of files to create outlier activity.
5. **Write KQL rules** for each scenario and save them in `kql-rules/`. Include a short header comment describing intent and false-positive considerations.
6. **Investigate and document**: When alerts fire, take screenshots, capture query outputs, and write a concise report in `incident-reports/` following the template below.
7. **Tune and measure**: Suppress noisy conditions, then record before/after MTTA or alert volume changes in the README and the relevant report.
8. **Publish**: Push to GitHub. Add the Microsoft Applied Skill badge link in the README once completed.

## Incident Report Template
- **Title**: Short name of the incident
- **Date/Time (UTC)**:
- **Detection source**: Sentinel analytics rule or hunting query
- **Entities**: Users, hosts, IPs, file hashes
- **Timeline**: Bullet timestamps with actions and evidence
- **Query snippets**: The exact KQL used and a one-line result explanation
- **Triage outcome**: True positive, benign, or needs more data
- **Response**: Steps taken
- **Lessons learned**: What to improve next time

## Playbook Template
1. Validate the alert context and severity
2. Correlate with sign-in logs, Defender signals, and endpoint telemetry
3. Contain the host or user if required
4. Collect artefacts (proc tree, hashes, command line, network)
5. Eradicate persistence or misconfiguration
6. Recover service and monitor
7. Close with categorisation and tags

## Mapping to Microsoft Applied Skills
- **Investigate threats using Microsoft Sentinel**: This lab fulfils and goes beyond the badge scenario. After completion, add your badge link under “Badges” below.

## Badges
- Microsoft Applied Skill: Investigate threats using Microsoft Sentinel — _link to badge_

## How to use this repo
Populate the folders as you run the lab. Redact anything sensitive. Keep screenshots clear and labelled.

## Create and push this repo to GitHub
```bash
# 1) Create new repo on GitHub named azure-sentinel-threat-detection (empty, no README)
# 2) Initialise locally and push
git init
git add .
git commit -m "Initial commit: Sentinel threat detection lab scaffold"
git branch -M main
git remote add origin https://github.com/<your-username>/azure-sentinel-threat-detection.git
git push -u origin main
```