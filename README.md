# AWS FinOps Dashboard Setup guide

## Overview

 The AWS FinOps Dashboard is an open-source Python-based CLI tool designed for comprehensive AWS cost monitoring and operational hygiene checks. Built using the Rich library, it provides detailed multi-account cost summaries, budget insights, EC2 instance states, cost trend charts, and audit reports — all accessible directly from your terminal.

 

## **Key Features**

- Multi-account Cost Explorer
- Budget Monitoring & Alerts
- EC2 Resource Status (Running / Stopped)
- 6-Month Cost Trends with Charts
- FinOps Audits (Untagged, Idle, Budget Breaches)
- Report Export (CSV / JSON / PDF)
- Supports Tags, Regions, Profiles
- Beautiful Terminal UI using Rich

## Prerequisites

- A Linux-based system (e.g., Ubuntu)
- Python and `pip` installed
- Git installed
- AWS CLI configured with named profiles
- AWS credentials with permissions

## Installation Steps 

**Step 1: Update the System and Install Dependencies**

```bash
sudo apt update
sudo apt install unzip -y
```
**step 2: Install pipx and AWS FinOps Dashboard**

```bash
sudo apt install pipx
pipx install aws-finops-dashboard

```

## Step 3: Install AWS CLI 

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

### Verify AWS CLI Installation

```bash
aws --version
```


## Step 4: Clone the AWS FinOps Dashboard Repository

```bash
git clone https://github.com/ravikiranvm/aws-finops-dashboard.git
cd aws-finops-dashboard
```

## Step 5: Install Python Dependencies

```bash
pip install -e .
```

## Step 6: Update Environment Path

```bash
echo 'export PATH=$PATH:/home/ubuntu/.local/bin' >> ~/.bashrc
source ~/.bashrc
```

## Step 7: Configure AWS CLI

```bash
aws configure --profile dev
```

You will be prompted to enter:

- AWS Access Key ID
- AWS Secret Access Key
- Default region name
- Output format

## AWS FinOps Command Usage Table

| **Command**                                                                                       | **Description**                                                                                                  |
|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `aws-finops`                                                                                      | Use the default profile, show output in terminal only.                                                           |
| `aws-finops --profiles dev prod`                                                                  | Use specific profiles `dev` and `prod`.                                                                          |
| `aws-finops --all`                                                                               | Use all available profiles.                                                                                       |
| `aws-finops --all --combine`                                                                      | Combine profiles from the same AWS account.                                                                      |
| `aws-finops --regions us-east-1 eu-west-1 ap-southeast-2`                                          | Specify custom regions to check for EC2 instances.                                                                |
| `aws-finops --time-range 30`                                                                      | View cost data for the last 30 days instead of the current month.                                                 |
| `aws-finops --tag Team=DevOps`                                                                    | View cost data only for a specific tag (e.g., `Team=DevOps`).                                                    |
| `aws-finops --tag Team=Devops Env=Prod`                                                           | View cost data for multiple tags (e.g., `Team=Devops` and `Env=Prod`).                                           |
| `aws-finops --all --report-name aws_dashboard_data --report-type csv`                             | Export data to CSV only.                                                                                         |
| `aws-finops --all --report-name aws_dashboard_data --report-type json`                            | Export data to JSON only.                                                                                        |
| `aws-finops --all --report-name aws_dashboard_data --report-type csv json`                        | Export data to both CSV and JSON formats simultaneously.                                                         |
| `aws-finops --profiles dev prod --combine --report-name report --report-type csv --dir output_reports` | Export combined data for `dev` and `prod` profiles to a specific directory.                                       |
| `aws-finops --profiles dev prod -r us-east-1 --trend`                                              | View cost trend analysis as bar charts for profile `dev` and `prod`.                                             |
| `aws-finops --all --trend --tag Team=DevOps`                                                      | View cost trend analysis for all CLI profiles for a specific cost tag (`Team=DevOps`).                           |
| `aws-finops -p dev -r us-east-1 --audit`                                                          | View audit report for profile `dev` in region `us-east-1`.                                                       |
| `aws-finops -p dev -r us-east-1 --audit -n Dev_Audit_Report -y pdf`                               | View audit report for profile `dev` in region `us-east-1` and export it as a PDF file to the current working dir with file name `Dev_Audit_Report`. |


##  Cost Usecase 

**Multi-Account Cost Tracking:**  View daily/monthly AWS spend across multiple accounts in one place.

**Cost Trend Analysis:** Detect unusual spikes or drops in cost over time.

**Budget Breach Alerts:** Receive alerts for budget breaches and adjust accordingly.

**Compare Environments:** Contrast spend between dev, prod, qa environments to optimize usage.

**Early Overspend Detection** Catch over-budget scenarios early with real-time budget vs. actual cost tracking.

**Idle Resource Cost Detection** Highlight resources (like stopped EC2) still incurring charges.

**Export Cost Reports** Share detailed cost reports (CSV, JSON, PDF) with finance or leadership.












