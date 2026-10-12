# NinjamZap changes — `ninjamzap/core`

This branch carries NinjamZap's changes to the NINJAM client core (`njclient`, `mpb`, `netmsg`) as used by the NinjamZap apps: raw-data / video channels with interval sync, voice-chat live video, per-local-channel send gain, GUID RNG seeding, server video capability detection.

- **Base:** upstream `405036d2` (2025-06-01), the version NinjamZap started from.
- **Commits:** replayed from [ninjamzap-core](https://github.com/jacinside/ninjamzap-core) with their original author, dates and messages; only `ninjam/njclient.*`, `ninjam/mpb.*`, `ninjam/netmsg.*` (in ninjamzap-core they live in `core/ninjamclient/libninjamcore/`; include paths differ, so this branch is for reading and comparing, not building).
- **Source of truth:** [ninjamzap-core](https://github.com/jacinside/ninjamzap-core). This branch is a mirror kept for comparing with and contributing to [justinfrankel/ninjam](https://github.com/justinfrankel/ninjam); it is not edited by hand.
- **License:** GPL, as upstream.

## For NINJAM client developers

If your client is built on upstream's `njclient` (a fork of this repository), take our work from these branches instead of copying code. Each is one change on top of upstream `main`, builds in the upstream tree, and is meant to be merged or cherry-picked as is:

| Branch | What it adds |
|---|---|
| [`feature/video-channels`](https://github.com/jacinside/ninjam/tree/feature/video-channels) | Video channels that play in sync with the audio intervals: sending, per-user receive buffers, interval matching by audio GUID, frame delivery from `AudioProc`, voice-chat live video, `server_caps` video detection. Clients that ignore non-`OGGv` channels are unaffected. |
| [`fix/guid-entropy`](https://github.com/jacinside/ninjam/tree/fix/guid-entropy) | Interval GUIDs no longer repeat across clients started in the same second (they used to mix up streams). Independent of video. |

When we change these areas, the branches are updated with new commits on top (never rewritten), so a `git merge` brings you up to date.

If your client has its own implementation (another language or codebase), use the protocol description and implementer's guide instead: [VIDEO_SYNC.md](https://github.com/jacinside/ninjamzap-core/blob/main/docs/VIDEO_SYNC.md). It covers the wire format, how to detect a video-capable server, how to announce and subscribe to video channels, and common pitfalls. Known difference to plan for: the NinjamZap apps decode H.264 only.

Questions and interop reports: open an issue on [ninjamzap-core](https://github.com/jacinside/ninjamzap-core/issues).

Fixes meant for upstream NINJAM go on their own branch off `main` (like `fix/guid-entropy`) and are offered as pull requests to justinfrankel/ninjam.
