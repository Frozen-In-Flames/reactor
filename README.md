# Reactor

One song in, thousands of videos out.

**Live demo:** https://frozen-in-flames.github.io/reactor/

Upload a WAV, M4A or MIDI file and Reactor renders a social video that reacts to your audio. Everything runs in your browser; nothing is uploaded anywhere. MIDI files are parsed and synthesized in-browser, so a VariTheory export (or any Standard MIDI File) becomes a video source directly.

## How it works

Every **seed** is one complete, repeatable interpretation of the song. A seeded recipe picks:

- **Scene** — Spectrum Wall, Radial Burst, Helix, Tunnel, Synth Terrain, Crystal (Babylon.js, WebGL)
- **Lens** — the interpretive layer. A lens decides which audio signal (kick onsets, sub, bass, mids, highs, RMS loudness, spectral flux, spectral centroid) drives size, spin, color and effects. Same song, read five different ways.
- **Camera** — Orbit, Dolly, Handheld, Static, Sweep
- **Palette** — eight color systems
- **Post effects** — bloom, chromatic aberration, grain, vignette, particle bursts on kick hits, background flash
- **Format and clip start** — 9:16, 1:1, 4:5, 16:9 (or Mix), starting at one of the song's loudest windows

With one clip-start candidate the recipe space is already 153,600 combinations; longer songs add more start windows. The counter in the app shows the live number for your song.

## Export

- **Preview** plays the current seed's interpretation.
- **Export video** records it in real time (keep the tab visible) and saves an MP4 where the browser supports it, WebM otherwise.
- **Export batch** records a run of consecutive seeds, up to 200 videos from one song, each saved to your downloads.

There is also a built-in demo beat, so the app can be tried with no file at all.

## Tech

Single `index.html`. Babylon.js 6.49.0 is loaded pinned from the jsDelivr CDN, so the page needs a network connection for the library and its font; your audio files never leave the device. Audio analysis is a 64-band logarithmic spectrum with RMS, spectral flux, centroid and a low-band onset detector for kick hits.

## License

Apache License 2.0. See [LICENSE](LICENSE).

Copyright 2026 Aries Hilton / Frozen In Flames.
