# Dockit for Unraid

Unraid Community Applications template for [Dockit](https://github.com/rapha57/dockit).

The container image is built from the product repo and published to GHCR on each release: `ghcr.io/rapha57/dockit`.

This repository only holds the Unraid XML (ports, appdata path, environment). It does not build the image.

## Install (test, before Community Apps)

1. Unraid → **Settings → Docker** → enable **Docker Authoring Mode**.
2. Copy `templates/dockit.xml` to `/boot/config/plugins/dockerMan/templates-user/` on the flash.
3. **Docker → Add Container** → pick **Dockit**.
4. Set **Edit password** (12+ characters). Leave SSO / LDAP secrets empty unless you want them on the Unraid side.

Or add this repo as a custom template source once it is on GitHub:

`https://raw.githubusercontent.com/rapha57/dockit-unraid/main/`

## What the template maps

| Unraid field | Container |
| --- | --- |
| WebUI | port **3000** |
| Appdata | `/mnt/user/appdata/dockit` → `/app/data` |
| Edit password | `PORTAL_EDIT_PASSWORD` (required) |
| Edit user | `PORTAL_EDIT_USER` (default `admin`) |
| Public origin / Trust proxy | reverse proxy |
| OIDC / LDAP bind | optional; otherwise configure inside Dockit |

ICMP (ping) is off unless you add `--cap-add=NET_RAW` under Extra Parameters. HTTP probes work without it.

## Support

https://github.com/rapha57/dockit/issues
