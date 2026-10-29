# Bifrost Maintenance for Home Assistant

Install the tested `dev-2026-10-28-maint.1` **amd64** build from the
[gmaclean1981 source fork](https://github.com/gmaclean1981/bifrost).
Bifrost exposes Zigbee2MQTT lights through an emulated Hue bridge.

[![Open your Home Assistant instance and add this repository.](https://my.home-assistant.io/badges/supervisor_addon.svg)](https://my.home-assistant.io/redirect/supervisor_addon/?repository_url=https%3A%2F%2Fgithub.com%2Fgmaclean1981%2Fbifrost-hassio)

## Install

1. Open **Settings → Apps → Install app**. In the menu, choose **Repositories**
   and add `https://github.com/gmaclean1981/bifrost-hassio`.
2. Install **Bifrost Maintenance**. It builds a small container locally, downloads
   the exact release binary bundle, verifies SHA256, and applies Debian updates.
3. Follow [configuration and migration instructions](bifrost_maintenance/DOCS.md).
4. Start the app, verify the logs and Hue controls, then enable **Start on boot**.

Only amd64 is currently packaged and validated. Zigbee2MQTT and a working Bifrost
configuration are required. This is a Home Assistant OS/Supervised app repository.

## Existing Bifrost installations

All these builds use the shared `/config/bifrost` directory and host network ports.
Back it up while Bifrost is stopped. Keep the old app installed with Start on boot
off, and run **only one Bifrost app** at a time. A repository-installed app has a
different full app ID from a local app; adding this repository does not migrate,
replace or start an existing installation. See [the migration and rollback guide](bifrost_maintenance/DOCS.md).

## Release contents and validation

The binary is the same executable tested with real Hue-app on/off, brightness and
state updates. Corresponding source and dependency notices are available beside
the binary in the [source release](https://github.com/gmaclean1981/bifrost/releases/tag/dev-2026-10-28-maint.1).
See [validation and known limits](https://github.com/gmaclean1981/bifrost/blob/master/VALIDATION.md).
Upstream changes include room/zone and schedule improvements; physical Hue Sync
was not separately validated in this release. This remains a development build.

## Attribution and licensing

- **Bifrost:** originally created by Christian Iversen and contributors at
  [chrivers/bifrost](https://github.com/chrivers/bifrost).
- **Upstream used here:** Christian Duvholt and contributors at
  [duvholt/bifrost](https://github.com/duvholt/bifrost).
- **mDNS library:** Han Xu and contributors, `mdns-sd` 0.13.2,
  [keepsimple1/mdns-sd](https://github.com/keepsimple1/mdns-sd).

Bifrost and this modified combined program are distributed under **GPL-3.0-only**.
The original license and copyright notices are retained. The mDNS library is
dual licensed Apache-2.0 OR MIT; this distribution retains both license texts
and uses its MIT permission. Other dependencies retain their individual terms.
The binary bundle includes dependency license/notice files. The accompanying
corresponding-source archive includes the locked dependency sources and their
notices, plus the patched application and build scripts.

This is an independent personal maintenance build, without upstream endorsement.
New maintenance contributions: Copyright (c) 2026 gmaclean1981 and contributors,
GPL-3.0-only. Existing authorship and notices remain in their respective files.

## AI-agent disclosure

The maintenance modifications, regression tests, build scripts, documentation,
and Home Assistant packaging in this fork were coded using an AI coding agent
(OpenAI Codex), with direction and hands-on device testing by the repository
owner. Bifrost itself and its upstream features were created by their original
authors and contributors; this disclosure does not attribute their work to AI.

