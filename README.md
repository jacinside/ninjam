# NINJAM — `community` branch

This branch is upstream [`justinfrankel/ninjam`](https://github.com/justinfrankel/ninjam) `main` plus reviewed fixes that are pending upstream. Each fix is a separate commit with its original author, so any of them can be taken on its own. The branch is rebased when upstream `main` moves, and a fix is dropped from it once upstream has it.

| Fix | Upstream PR | Author | Status | How it was tested |
|---|---|---|---|---|
| `mpb`: out-of-bounds reads in the message parsers; pan read as signed | [#25](https://github.com/justinfrankel/ninjam/pull/25) | drawmeanelephant | pending upstream | parser test cases (malformed and truncated messages, negative pan) |
| server: strip control characters from relayed chat, topic, private room names and echoed privmsg targets | [#26](https://github.com/justinfrankel/ninjam/pull/26) | drawmeanelephant | pending upstream | client/server test suite; clients checked to never send control characters |
| server: `Net_Message` leaks on the pre-auth and lobby paths | [#27](https://github.com/justinfrankel/ninjam/pull/27) | drawmeanelephant | pending upstream | ownership of `Run()`'s returned message checked; client/server test suite |
| `njclient`: ignore bpm/bpi of 0 and values whose interval overflows `int` | [#31](https://github.com/justinfrankel/ninjam/pull/31) | drawmeanelephant | pending upstream | test case: beat info that doesn't fit keeps the previous interval |
| `njclient`: seed the GUID RNG with per-process entropy | [#32](https://github.com/justinfrankel/ninjam/pull/32) | Javier Cordero | pending upstream | clients started in the same second no longer get the same interval GUIDs |
| server build: `-fsigned-char` on Linux, so `ninjamsrv` builds on arm64 | not submitted yet | Javier Cordero | — | builds on Linux x86_64 and arm64 (see `.github/workflows`); upstream `main` fails on arm64 |

The "client/server test suite" is the one in [ninjamzap-core](https://github.com/jacinside/ninjamzap-core) (`tests/`, runs against a server in Docker).

## Adopting synchronized video (NinjamZap extension, optional)

Nothing in this branch adds video. Synchronized video is an optional extension: video is carried as regular NINJAM channel data and synchronized to the audio intervals by matching interval GUIDs. Clients that don't support it ignore video channels, and audio keeps working for everyone in the room.

| You have | What to use |
|---|---|
| A client based on upstream `njclient` (ReaNINJAM, the reference client and derivatives) | Merge branch [`feature/video-channels`](https://github.com/jacinside/ninjam/tree/feature/video-channels) (one commit on top of upstream `main`). You supply H.264 encode/decode and display. |
| A client with its own protocol implementation | Implement from the spec: [VIDEO_SYNC.md](https://github.com/jacinside/ninjamzap-core/blob/main/docs/VIDEO_SYNC.md) (section 10, Implementer's guide) and [ADOPTING.md](https://github.com/jacinside/ninjamzap-core/blob/main/docs/ADOPTING.md). |
| A new client | Use the [ninjamzap-core](https://github.com/jacinside/ninjamzap-core) library (GPL v2). |
| A server | Merge branch [`feature/server-video-relay`](https://github.com/jacinside/ninjam/tree/feature/server-video-relay) (one commit): `AllowVideoChannels` (advertised to clients as `server_caps` bit 1, which clients check before turning video on), a larger per-connection message queue, and audio relayed ahead of video so video never delays it. |

Both `feature/*` branches apply on upstream `main` and merge cleanly with this branch, separately or together.

Interoperability testing: the ninjamzap-core video-sync suite can be pointed at your server (`NJ_TEST_HOST` / `NJ_TEST_PORT`), and `video.ninjamzap.com:2049` has video enabled for testing a client next to the NinjamZap apps. Details in [ADOPTING.md](https://github.com/jacinside/ninjamzap-core/blob/main/docs/ADOPTING.md).

---

The original upstream README follows (also in `README`).

This is NINJAM, www.ninjam.com

To build the server, go to ninjam/server and run make

The various clients in ninjam/ are all old and probably need some attention to function

The REAPER ReaNINJAM plug-in is in jmde/fx/reaninjam/. It is more fully featured. You will need the VST2 SDK to compile it, though.
