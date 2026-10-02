# video-srt-cleaner

Clean auto-generated SRT subtitle files: fix capitalization, remove filler words, merge short segments, renumber. Browser only.

**Live demo:** https://0xelitesystem.github.io/video-srt-cleaner/

## Use

Open [`index.html`](./index.html). Paste your SRT in the left panel, choose cleanup options, click Clean. The cleaned SRT appears on the right with a diff summary. Copy or download the result.

## Cleanup options

- **Fix sentence capitalization** - capitalize first word of each segment, first letter after sentence-ending punctuation, and standalone "i" / "i'm" / "i've"
- **Strip filler words** - removes "uh", "um", "you know" (interjection), "I mean", "sort of", "kind of", "like" (filler use)
- **Merge short segments** - combines consecutive segments shorter than the threshold (default 2 seconds) into a single readable segment, when the gap between them is small
- **Trim trailing whitespace** - collapse double spaces, normalize newlines
- **Renumber sequence indices** - after merges and removals, renumber 1, 2, 3...

## Why this exists

YouTube auto-captions and most ASR tools produce SRT files that work but read badly:

- Everything lowercase including names and proper nouns
- "I" rendered as "i"
- Fillers transcribed verbatim ("uh", "um", "you know")
- Segments under 1 second that flicker on screen too fast to read
- No punctuation in many cases

You're going to fix all of this manually before uploading polished captions. This automates the boring part. You still review the output before uploading.

It is one HTML file with no dependencies, no tracking and no network calls, released under MIT.

## What this is NOT

- Not a transcription tool. Bring your own SRT.
- Not a translator.
- Not a punctuation-inferrer. (That's a much harder problem; this only adds capitalization where punctuation already exists.)
- Not connected to YouTube or any ASR service.

## Privacy

The SRT file you paste stays in your browser. No upload, no requests, no analytics. Verify with DevTools network tab.

The page saves one thing in localStorage: your light or dark theme choice, under the key `theme`. Download builds the cleaned file inside your browser.

## Run locally

```
git clone https://github.com/0xelitesystem/video-srt-cleaner
cd video-srt-cleaner
```

Open `index.html` in any browser. Or:

```
python -m http.server 8000
```

## Contribute

PRs welcome:

- Localized filler lists (German, French, Spanish, Hindi, etc.)
- Better punctuation inference (using sentence-boundary heuristics)
- WebVTT support (similar format with `.vtt` extension)
- Bulk mode (drop a folder of files, get cleaned versions)

Don't add: external ASR APIs, telemetry, npm dependencies. Single file by design.

## Build

No build. Single HTML file.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT.

## Related

- [youtube-chapter-marker-builder](https://github.com/0xelitesystem/youtube-chapter-marker-builder) - validate chapter timestamps
- [youtube-creator-checklist](https://github.com/0xelitesystem/youtube-creator-checklist) - pre-publish checks (caption review)
