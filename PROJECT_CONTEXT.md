# Project Context — cowork-vps-ops

## Purpose
VPS / Infrastructure Ops Cowork Plugin for Claude Cowork. Packages domain-specific skills, commands, and an autonomous agent into a single installable plugin.

## Architecture
- **Skills (4):** log-analyser, nginx-manager, service-monitor, backup-manager
- **Commands (4):** /vps:logs, /vps:nginx, /vps:health, /vps:backups
- **Agent:** monday-digest

## Design Decisions
- Skills contain the domain knowledge and step-by-step instructions
- Commands are lightweight entry points that invoke the right skill
- The agent chains multiple skills into an autonomous workflow
- MCP connectors declared in .mcp.json (user configures credentials)

## Installation
Cowork → Customize → Browse Plugins → Upload → select ZIP.

## Author
Artur Ferreira / The GEO Lab (thegeolab.net)
