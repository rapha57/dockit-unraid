# Dockit for Unraid

Unraid Community Applications template for [Dockit](https://github.com/rapha57/dockit).

**Pin your URLs.** One shared page for the tools the team actually opens — Grafana, Proxmox, GitLab, the firewall, the wiki — organised by space, category and card. Self-hosted. One JSON file, no database.

The container image is published to GHCR on each Dockit release: `ghcr.io/rapha57/dockit`. This repository only holds the Unraid XML. It does not build the image.

## Install

Community Apps → search **Dockit** → Install. Set **Edit password** (12+ characters). Leave SSO / LDAP secrets empty unless you want them on the Unraid side.

WebUI: `http://[IP]:3000/` — sign in as `admin` with that password.

## What the template maps

| Unraid field | Container |
| --- | --- |
| WebUI | port **3000** |
| Appdata | `/mnt/user/appdata/dockit` → `/app/data` (rw) |
| PUID / PGID | `99` / `100` (Unraid `nobody:users`) |
| Edit password | `PORTAL_EDIT_PASSWORD` (required) |
| Edit user | `PORTAL_EDIT_USER` (default `admin`) |
| Public origin / Trust proxy | reverse proxy |
| OIDC / LDAP bind | optional; otherwise configure inside Dockit |

The image starts as root, chowns appdata to PUID:PGID, then drops. A Force Update is enough; no Extra Parameters. ICMP (ping): `--cap-add=NET_RAW`. HTTP probes work without it.

## Support

https://github.com/rapha57/dockit/issues
