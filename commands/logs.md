---
description: Analyse Nginx access and error logs. Traffic summary, cache HIT rate, AI crawler activity, 404 patterns, and error spikes.
---

Use the log-analyser skill.

Arguments: $ARGUMENTS

If "errors" is provided, focus on error log analysis.
If "crawlers" or "ai" is provided, focus on AI crawler activity.
If "cache" is provided, focus on FastCGI cache performance.
If no argument, run the full log analysis across all categories.
