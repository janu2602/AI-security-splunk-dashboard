# AI Security Splunk Dashboard

![Splunk](https://img.shields.io/badge/Splunk-Enterprise-orange) ![SPL](https://img.shields.io/badge/SPL-Queries-blue)

SOC-ready Splunk SIEM dashboard for AI application security. 8 panels, 10 SPL queries, 1 saved alert.

## Dashboard Panels
| Panel | Type | Shows |
|-------|------|-------|
| 1 | Line chart | Injection attempts over time |
| 2 | Pie chart | Verdict breakdown |
| 3 | Table | Top high-risk users |
| 4 | Single value | Active alert count |
| 5 | Bar chart | PII categories detected |
| 6 | Bar chart | Injection pattern frequency |
| 7 | Area chart | Session alerts timeline |
| 8 | Column chart | Blocked messages per hour |

## Quick Start
```bash
git clone https://github.com/YOUR_USERNAME/ai-security-splunk-dashboard
python3 splunk_setup.py   # generates 100 sample events + all 10 SPL queries
```

## Key SPL Query
```spl
index=ai_security | where risk_score >= 70
| stats count AS Events, avg(risk_score) AS AvgRisk BY user_id | sort -Events
```

## NIST Lifecycle Mapping
Detect → Analyze → Contain → Review — each dashboard panel maps to one phase.
# AI-security-splunk-dashboard
