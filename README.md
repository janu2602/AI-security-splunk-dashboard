# 📊 AI Security Splunk SIEM Dashboard

![Splunk](https://img.shields.io/badge/Splunk-Enterprise-FF5500?style=flat)
![SPL](https://img.shields.io/badge/SPL-10%20Queries-blue?style=flat)
![Panels](https://img.shields.io/badge/Dashboard-8%20Panels-534AB7?style=flat)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat)

---

## 🔍 The Problem

Raw JSON logs are unreadable in a crisis. A SOC analyst on duty needs a single screen to immediately understand: *Is the system under attack right now? Who is highest risk? Which attack types are trending?*

**This dashboard answers all of those questions at a glance.**

---

## 📊 Dashboard Panels

| # | Panel | Visualization | Answers |
|---|-------|--------------|---------|
| 1 | Injection attempts over time | Line chart | Are attacks increasing? |
| 2 | Verdict breakdown | Pie chart | What % are being blocked? |
| 3 | Top high-risk users | Table | Who are the worst offenders? |
| 4 | Active alert count | Single value | How many open alerts? |
| 5 | PII categories detected | Bar chart | What data is at risk? |
| 6 | Injection pattern frequency | Bar chart | Which attacks are most common? |
| 7 | Session alerts timeline | Area chart | When do persistent attacks happen? |
| 8 | Blocked messages per hour | Column chart | What is the blocking rate? |

---

## 🚀 Quick Start

```bash
git clone https://github.com/YOUR_USERNAME/ai-security-splunk-dashboard
cd ai-security-splunk-dashboard

# Generate 100 sample log events for testing
python3 splunk_setup.py

# Output: ai_security_monitor.log + all 10 SPL queries printed
```

---

## 📝 Key SPL Queries

**Top high-risk users:**
```spl
index=ai_security | where risk_score >= 70
| stats count AS Events, avg(risk_score) AS AvgRisk BY user_id
| sort -Events | head 10
```

**Injection attempts over time:**
```spl
index=ai_security | where risk_score > 50
| timechart span=1h count AS "Injection Attempts"
```

**Active alerts (last 24h):**
```spl
index=ai_security level=ALERT earliest=-24h
| stats count AS "Active Alerts"
```

---

## 🔧 Splunk Setup Steps

1. **Install Splunk Enterprise** (free trial at splunk.com)
2. **Configure data input:** Settings → Data Inputs → Files & Directories
   - Source: path to `ai_security_monitor.log`
   - Source type: `_json`
   - Index: `ai_security`
3. **Verify:** Run `index=ai_security | head 5` in Search
4. **Create dashboard:** Dashboards → New → paste each SPL query
5. **Set saved alert:** Trigger when risk_score >= 90 for 2+ events in 5 min

---

## 🗺️ NIST Incident Response Mapping

| NIST Phase | Dashboard Support |
|-----------|------------------|
| **Detect** | Alert count tile, injection trend line |
| **Analyze** | User table, pattern frequency chart |
| **Contain** | Session ID drill-down, user blocking |
| **Review** | Time-based charts for timeline reconstruction |

---

## 🛠️ Skills Demonstrated

- Splunk Enterprise administration
- SPL query writing (stats, timechart, where, sort, mvexpand)
- Dashboard design for SOC operations
- Saved alert configuration
- NIST incident response lifecycle

---
