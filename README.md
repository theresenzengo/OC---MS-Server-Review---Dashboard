# Oetker Collection — Microsoft Server Licensing Dashboard v15

## 🚀 100% Dynamic — Zero Hardcoded Data

This dashboard reads **all data live from Google Sheets**. To update the dashboard, simply edit the Google Sheet — no HTML changes needed.

## Architecture

```
Google Sheets (1RldtkHxCkFH9iDVNxEuAW_C1bWSzOlNOv_e5aPjvBFc)
├── "Data"          → BU cards, KPIs, workflow steps, contact names
├── "Entitlements"  → License entitlements (G3 + EA), compliance bars
├── "Requirements"  → License requirements per subsidiary, compliance bars
└── (BU Requirements Detail) → Reference only (not read by dashboard)
         │
         ▼
   Dashboard (index.html)
   ├── Fetches all 3 sheets via Google Sheets API v4
   ├── Auto-refresh every 5 minutes
   ├── Subsidiary filter, search, tabs
   ├── Compliance bars (entitled vs required)
   ├── EOS modal (computed from eos_risk column)
   ├── Entitlements modal (from Entitlements sheet)
   └── PDF export
```

## How to Update

| What to change | Where to edit | Dashboard effect |
|---|---|---|
| Add/remove a BU | Sheet: "Data" tab | New card appears automatically |
| Update license entitlements | Sheet: "Entitlements" tab | Compliance bars update |
| Update license requirements | Sheet: "Requirements" tab | Compliance bars update |
| Change BU priority/status | Sheet: "Data" tab | Card color/badge updates |
| Add contact name | Sheet: "Data" → contact_name column | Shows on BU card |
| Fix EOS risk | Sheet: "Data" → eos_risk column | EOS modal recalculates |

## Columns in "Data" Sheet

| Column | Description |
|---|---|
| unit_id | Unique BU identifier (BU-01, BU-02...) |
| unit_name | Display name |
| subsidiary | Parent subsidiary (filters) |
| country | Country/region |
| **contact_name** | **IT contact person (new in v15)** |
| questionnaire_status | Complete / In Progress / Pending / N/A |
| response_rate | 0-100% |
| priority | CRITICAL / HIGH / MEDIUM / LOW |
| esxi_hosts | Number of ESXi/Hyper-V hosts |
| total_physical_cores | Total physical cores |
| total_vms | Total VMs |
| windows_vms | Windows Server VMs |
| sql_instances | SQL Server instances |
| users | Total users |
| vmotion_drs | vMotion/DRS status |
| hypervisor | VMware / Hyper-V / Azure Local |
| ws_versions_deployed | WS versions in use |
| sql_versions_deployed | SQL versions in use |
| rds_in_use | RDS usage details |
| eos_risk | End of Support risk (NO / YES - details) |
| critical_notes | Key findings and notes |
| steps | Workflow steps (true,false,true,...) |

## Deployment

1. Push all files to GitHub repository
2. Enable GitHub Pages (Settings → Pages → Source: main branch)
3. Access at: `https://<username>.github.io/<repo>/`

## Files

- `index.html` — Single-file React dashboard (v15)
- `manifest.json` — PWA manifest
- `sw.js` — Service worker (network-first for API, cache-first for static)
- `README.md` — This file

## Configuration

The Google Sheets API key and Spreadsheet ID are in the `CONFIG` object at the top of `index.html`:

```javascript
const CONFIG = {
  GOOGLE_SHEETS: {
    API_KEY: 'AIzaSyD7F4sjl8DUYvfLBOq5N5cXm-AThaDnGdY',
    SPREADSHEET_ID: '1RldtkHxCkFH9iDVNxEuAW_C1bWSzOlNOv_e5aPjvBFc',
    SHEETS: { DATA: 'Data', ENTITLEMENTS: 'Entitlements', REQUIREMENTS: 'Requirements' }
  },
  AUTO_REFRESH_MINUTES: 5
};
```

---
*v15 — February 2026 — SAM Unit, KTOKEA sasu*
