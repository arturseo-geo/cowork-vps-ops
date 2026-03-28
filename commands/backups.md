---
description: Verify all VPS backups completed successfully. Checks WordPress, PostgreSQL, Nginx config, and PM2 backups for recency, file size, and integrity.
---

Use the backup-manager skill.

Arguments: $ARGUMENTS

If a specific backup name is provided (e.g. "wordpress", "postgresql"), check that only.
If no argument, verify all backups in the inventory.
Flag any missing, zero-byte, overdue, or anomalously small backups as critical.
