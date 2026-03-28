---
description: Full VPS service health check. PM2 processes, systemd services, port availability, RAM/disk usage. Flags anything down, restarting, or running out of resources.
---

Use the service-monitor skill to run a full service health check.

Arguments: $ARGUMENTS

If a specific service name is provided, check that service only.
If no argument, check all services — PM2, systemd, ports, and system resources.
Return the full health report with critical issues first.
