---
description: Manage Nginx configuration. Check status and SSL expiry, validate config syntax, clear FastCGI cache, or add a new virtual host. Always validates before reloading.
---

Use the nginx-manager skill.

Arguments: $ARGUMENTS

Supported operations:
  /vps:nginx status           — Show active sites, SSL expiry, process status
  /vps:nginx validate         — Test current config syntax (nginx -t equivalent)
  /vps:nginx cache-clear      — Clear FastCGI cache directory
  /vps:nginx add [domain]     — Generate and add a new virtual host config
  /vps:nginx rate-limits      — Review 429 patterns in recent access logs

If no argument, run status check.
Never reload Nginx without running validate first.
