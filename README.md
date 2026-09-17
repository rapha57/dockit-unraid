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
| Extra Parameters | `--user 0` (entrypoint chowns appdata, then drops to PUID) |
| Edit password | `PORTAL_EDIT_PASSWORD` (required) |
| Edit user | `PORTAL_EDIT_USER` (default `admin`) |
| Public origin / Trust proxy | reverse proxy |
| OIDC / LDAP bind | optional; otherwise configure inside Dockit |

Keep `--user 0` in Extra Parameters. If you add ICMP (ping), use `--user 0 --cap-add=NET_RAW`. HTTP probes work without `NET_RAW`.

Do not run the container as root for the whole process: `--user 0` is only so the entrypoint can fix appdata ownership.

## Support

https://github.com/rapha57/dockit/issues
