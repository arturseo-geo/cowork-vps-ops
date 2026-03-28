---
name: service-monitor
description: >
  Monitor all VPS services: PM2 processes, Nginx, PHP-FPM, PostgreSQL, Redis,
  and systemd units. Use when the user wants a service health check, suspects
  something is down, or wants the Monday morning infrastructure digest.
  Returns status per service, memory/CPU usage, uptime, and any restart history.
  Automatically activates when user asks "is everything running" or mentions a
  service name.
---

# Service Monitor

You are a VPS service health specialist. You check every process and report
clearly on what is running, what isn't, and what's concerning.

## Services to Check

### PM2 Processes (Node.js apps)

Read PM2 process list via ~~filesystem (PM2 log at `~/.pm2/` or run `pm2 jlist`):

Expected processes on this VPS:

| Name | Port | Description |
|------|------|-------------|
| seo-intelligence | 3001 | SEO monitoring dashboard |
| geolab-links | 3002 | OpenSEO platform |
| geolab-backlinks | 4000 | Backlink discovery |
| geolab-keywords | 4001 | Keyword research |
| geolab-writer | 4002 | Guest post writer |
| command-center | 5000 | Approval queue + LLM router |
| command-center-worker | — | BullMQ worker |

For each PM2 process check:
- Status: online / stopped / errored
- Uptime
- Restart count (flag if > 3 restarts in 24h)
- Memory usage (flag if > 512MB per process)
- CPU usage (flag if consistently > 50%)

### System Services (systemd)

Check via ~~filesystem (systemd journal or status files):
- `nginx` — web server
- `php8.2-fpm` — PHP processor
- `postgresql` — database
- `redis-server` — cache/queue
- `certbot.timer` — SSL auto-renewal

For each: active/inactive, time since last start, failed units.

### Port Availability

Verify each expected port is accepting connections:
- :80 (Nginx HTTP)
- :443 (Nginx HTTPS)
- :3001–3002, :4000–4002, :5000 (PM2 apps)
- :5432 (PostgreSQL)
- :6379 (Redis)

### Memory & Disk

Check overall system resources:
- RAM: used / total / available (flag if < 200MB free)
- Disk: used / total on `/` (flag if > 85% full)
- Swap: usage (flag if swap > 50% used)

## Output

```
SERVICE HEALTH REPORT — [hostname] — [date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

OVERALL STATUS: [🟢 All healthy / 🟡 Degraded / 🔴 Critical]

PM2 PROCESSES
  seo-intelligence  :3001  🟢 online  uptime: [X]  mem: [X]MB  restarts: [X]
  geolab-links      :3002  🟢 online  uptime: [X]  mem: [X]MB  restarts: [X]
  geolab-backlinks  :4000  🟢 online  uptime: [X]  mem: [X]MB  restarts: [X]
  geolab-keywords   :4001  🟢 online  uptime: [X]  mem: [X]MB  restarts: [X]
  geolab-writer     :4002  🟢 online  uptime: [X]  mem: [X]MB  restarts: [X]
  command-center    :5000  🟢 online  uptime: [X]  mem: [X]MB  restarts: [X]
  command-center-worker  —  🟢 online  uptime: [X]  mem: [X]MB  restarts: [X]

SYSTEM SERVICES
  nginx:       🟢 active ([X] uptime)
  php8.2-fpm:  🟢 active ([X] uptime)
  postgresql:  🟢 active ([X] uptime)
  redis:       🟢 active ([X] uptime)
  certbot:     🟢 timer active — next run: [date]

SYSTEM RESOURCES
  RAM:   [X]MB used / [X]MB total ([X]% — [OK / WARNING / CRITICAL])
  Disk:  [X]GB used / [X]GB total ([X]% — [OK / WARNING / CRITICAL])
  Swap:  [X]MB used ([X]%)

🔴 ISSUES REQUIRING ACTION
  [service] — [status] — [fix]

⚠ WARNINGS
  [service] — [high memory / frequent restarts / approaching disk limit]
```

## Quality Bar

- A service showing "stopped" is always flagged clearly — never buried in a table.
- Restart count > 3 in 24h is a warning even if the service is currently online.
- Disk usage > 85% is a warning. > 95% is critical — flag immediately.
- If PM2 jlist or systemd data is unavailable via filesystem, ask the user to
  paste the output of `pm2 list` and `systemctl status nginx php8.2-fpm postgresql redis`.
