# nesa-dashboard-g42
Azure Monitor Workbook for NESA CA-07 compliance dashboard – UAE cloud security demo
# NESA Compliance Dashboard – G42 Demo (CA-07)

Azure Monitor Workbook visualizing Azure Policy compliance for UAE NESA Information Assurance Standards (CA-07).

## Overview
- Overall compliance pie (57% NonCompliant in demo)
- Top non-compliant resources grid with details
- Built with Azure Resource Graph for real-time insights
- Targeted for UAE gov/semi-gov cloud roles (G42, ADNOC, DEWA, Etisalat)

## Screenshots
![Overall Compliance Pie](screenshots/pie-chart.png)
![Non-Compliant Resources Grid](screenshots/grid-tile.png)

## Loom Demo
[Watch 90-sec walkthrough](https://www.loom.com/share/YOUR-LOOM-ID)

## Setup
1. Assign Microsoft cloud security benchmark (or custom NESA initiative) at subscription level.
2. Create Azure Monitor Workbook.
3. Add Resource Graph queries (see below).

## Key Queries
**Compliance Pie**
```kql
policyresources
| where type == "microsoft.policyinsights/policystates"
| extend complianceState = tostring(properties.complianceState)
| summarize Count = count() by complianceState
| render piechart
