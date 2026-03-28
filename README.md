# VPS Ops Plugin for Claude Cowork

**Full server operations from natural language. No SSH terminal required.**

Built by [Artur Ferreira](https://thegeolab.net) | The GEO Lab

---

## What This Plugin Does

Every Monday you need to check 7 PM2 processes, 5 systemd services, nightly backups,
Nginx SSL expiry, and a week of access logs. This plugin runs all of it in one shot
and delivers a single actionable digest.

No other plugin in the Claude directory covers server operations. This is the first.

---

## Commands

| Command | What It Does |
|---------|-------------|
| `/vps:health` | All services — PM2, systemd, RAM, disk, ports |
| `/vps:logs [crawlers\|cache\|errors]` | Nginx log analysis — traffic, AI crawlers, cache HIT rate, errors |
| `/vps:backups` | Verify all backups completed — WordPress, PostgreSQL, configs |
| `/vps:nginx [status\|validate\|cache-clear\|add domain]` | Nginx config management with validation before every reload |

---

## Agent

`monday-digest` — Full weekly infrastructure check: services → logs → backups → SSL → WordPress. One consolidated report. Logs to Notion.

Invoke: *"Run the Monday digest"* or *"Check everything on the server"*

---

## Services Monitored

**PM2 Processes:**
- `seo-intelligence` :3001
- `geolab-links` :3002
- `geolab-backlinks` :4000
- `geolab-keywords` :4001
- `geolab-writer` :4002
- `command-center` :5000
- `command-center-worker`

**System Services:**
- Nginx · PHP 8.2-FPM · PostgreSQL · Redis · Certbot timer

---

## Required Connectors

| Connector | Used For |
|-----------|---------|
| Filesystem | Nginx logs, backup files, config files, PM2 status |
| WordPress *(optional)* | WordPress health check, plugin updates |
| Notion *(optional)* | Infrastructure log, incident tracking |

---

## Install

```bash
claude plugin marketplace add arturseo-geo/vps-ops-plugin
claude plugin install vps-ops@vps-ops-plugin
```

---

MIT License · [thegeolab.net](https://thegeolab.net) · [@TheGEO_Lab](https://x.com/TheGEO_Lab)
