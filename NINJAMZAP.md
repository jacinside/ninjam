# NinjamZap changes — `ninjamzap/server`

This branch carries NinjamZap's changes to the NINJAM server (ninjamsrv) with video channel relay, thread-per-room groups with video priority and congestion control, `server_caps` video bit, `RoomPassword` and HMAC-signed room codes for `PrivateGroupMode`.

- **Base:** upstream `405036d2` (2025-06-01), the version NinjamZap started from.
- **Commits:** replayed from [ninjamzap-server](https://github.com/jacinside/ninjamzap-server) with their original author, dates and messages; only `ninjam/` (server, `mpb`, `netmsg`).
- **Source of truth:** [ninjamzap-server](https://github.com/jacinside/ninjamzap-server). This branch is a mirror kept for comparing with and contributing to [justinfrankel/ninjam](https://github.com/justinfrankel/ninjam); it is not edited by hand.
- **License:** GPL, as upstream.

## For NINJAM server operators and developers

To host rooms with video for clients that support it (see the client branch [`feature/video-channels`](https://github.com/jacinside/ninjam/tree/feature/video-channels)), take [`feature/server-video-relay`](https://github.com/jacinside/ninjam/tree/feature/server-video-relay): one change on top of upstream `main` that sizes the server's limits and TCP buffers for video, drops video (never audio) for subscribers whose send queue is backing up, gives video transfers a longer timeout, and advertises video support with `AllowVideoChannels yes` (`server_caps` bit 1). Options are documented in `ninjam/server/example.cfg`. A stock server also relays video, since interval data is opaque to it; this branch keeps it from delaying audio.

This branch also has per-room threads for `PrivateGroupMode` (audio relayed before video within each room); that part is not offered as a separate branch yet.

Fixes meant for upstream NINJAM go on their own branch off `main` and are offered as pull requests to justinfrankel/ninjam.
