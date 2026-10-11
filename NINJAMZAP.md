# NinjamZap changes — `ninjamzap/core`

This branch carries NinjamZap's changes to the NINJAM client core (`njclient`, `mpb`, `netmsg`) as used by the NinjamZap apps: raw-data / video channels with interval sync, voice-chat live video, per-local-channel send gain, GUID RNG seeding, server video capability detection.

- **Base:** upstream `405036d2` (2025-06-01), the version NinjamZap started from.
- **Commits:** replayed from [ninjamzap-core](https://github.com/jacinside/ninjamzap-core) with their original author, dates and messages; only `ninjam/njclient.*`, `ninjam/mpb.*`, `ninjam/netmsg.*` (in ninjamzap-core they live in `core/ninjamclient/libninjamcore/`; include paths differ, so this branch is for reading and comparing, not building).
- **Source of truth:** [ninjamzap-core](https://github.com/jacinside/ninjamzap-core). This branch is a mirror kept for comparing with and contributing to [justinfrankel/ninjam](https://github.com/justinfrankel/ninjam); it is not edited by hand.
- **License:** GPL, as upstream.

Generic fixes meant for upstream go on `upstream/<topic>` branches off `main`.
