# Reactor

Reactor converts a recording (WAV, M4A, or Standard MIDI File) into a three-dimensional, audio-reactive video, rendered entirely in the browser. All motion is driven by the audio signal itself; variation is produced by seeded procedural generation and deterministic algorithmic mutation, so any result can be reproduced exactly from its seed. No artificial intelligence is used at any stage, and no file leaves the visitor's machine. MIDI files are parsed and synthesised in the browser, so a VariTheory export, or any Standard MIDI File, serves directly as a video source.

## Live demonstration

- [Reactor](https://frozen-in-flames.github.io/reactor/): the full application, running in the browser.

## How it works

Every **seed** is one complete, repeatable interpretation of the song. A seeded recipe picks:

- **Scene** — Spectrum Wall, Radial Burst, Helix, Tunnel, Synth Terrain, Crystal (Babylon.js, WebGL)
- **Lens** — the interpretive layer. A lens decides which audio signal (kick onsets, sub, bass, mids, highs, RMS loudness, spectral flux, spectral centroid) drives size, spin, color and effects. Same song, read five different ways.
- **Camera** — Orbit, Dolly, Handheld, Static, Sweep
- **Palette** — eight color systems
- **Backdrop** — Dark, Vivid or Pale: the same palette rendered against a near-black, mid-tone or near-white ground
- **Color flow** — Linear, Reverse, Ping-pong or Mono: how the palette is traversed across the scene
- **Post effects** — bloom, chromatic aberration, grain, vignette, particle bursts on kick hits, background flash
- **Format** — 9:16, 1:1, 4:5, 16:9 (or Mix)

With one clip-start candidate the recipe space is already 1,843,200 combinations; longer songs add more start points. The counter in the app shows the live number for your song.

## Length: the song decides

A video defaults to the **full song**: the whole WAV or M4A from 0:00 to the end, or for a MIDI file the full span of its notes. There is no arbitrary length cap. A shorter video is something you ask for on purpose: switch Clip to **Clip**, set the seconds, and the clip starts on a musical boundary. Start points come from a novelty analysis of the song itself (three-band envelope flux; peaks mark drops, chorus entries and section changes), so clips begin on the music instead of on an arbitrary second.

During playback every motion phase is driven by the audio analysis, never by a free-running clock: if the song goes silent, the picture holds still. Lows and highs are felt as movement, which is the point of a synesthesia visualizer.

## Mutations

Like VariTheory, Reactor treats a recipe as a genome and the song as the ground that never changes.

- **Mutate** perturbs 1 to 3 genes of the current seed (plus a possible hue or bloom drift) using a stream seeded from the seed and the mutation count, so a mutation chain is exactly reproducible. The song, the format and the length never mutate.
- **Cross with seed** breeds the current recipe with another seed's recipe gene by gene; the child keeps the current seed and format and records its lineage.
- The readout shows the lineage (for example `Seed 123456 · mutation 3` or `Crossover 111 × 222`), and exported filenames carry it, so any video can be traced back to the exact recipe that made it.

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
