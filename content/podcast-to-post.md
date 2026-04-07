# Recipe: Podcast Episode to Blog Post

> **Industry:** Publishers, podcasters, content teams
> **Difficulty:** Easy
> **Time:** 2–5 minutes
> **Binaries:** `bonfyre-media-prep`, `bonfyre-transcribe`, `bonfyre-brief`, `bonfyre-emit`

## What you already have

A podcast episode audio file — `.mp3`, `.m4a`, `.wav`, or similar.

## What Bonfyre does

Takes your episode recording and produces:
- A full transcript
- An editorial summary with key points
- A draft blog post
- Quote-ready excerpts

## What you get

A publishable blog post from every episode, with no manual transcription and no cloud APIs.

## Step by step

### 1. Normalize the audio

```sh
bonfyre-media-prep normalize episode.mp3 -o episode.wav
```

Converts to 16kHz mono WAV — the format whisper needs.

### 2. Transcribe

```sh
bonfyre-transcribe run episode.wav -o transcript.txt
```

Local transcription via whisper.cpp. No API key, no per-minute cost.

### 3. Clean up

```sh
bonfyre-transcript-clean transcript.txt -o clean.txt
```

Removes filler words, normalizes formatting, fixes common transcription artifacts.

### 4. Generate the brief

```sh
bonfyre-brief clean.txt -o brief.md
```

Extracts the most important sentences using TF-IDF scoring. The brief becomes your blog post draft.

### 5. Emit as HTML

```sh
bonfyre-emit brief.md --format html -o post.html
```

Produces a clean HTML file ready to paste into WordPress or any CMS.

## Or use the pipeline

```sh
bonfyre-pipeline run --input episode.mp3 --output-dir ./episode-output
```

Gets you transcript + brief + proof score + offer + packaged output in one command.

## Example output

**Input:** 45-minute podcast episode (42 MB mp3)

**Output:**
- `transcript.txt` — 4,500 words
- `clean.txt` — 4,200 words (filler removed)
- `brief.md` — 400-word summary with key quotes
- `post.html` — ready for WordPress

## Tips

- For multi-speaker podcasts, the transcript will interleave speakers. The brief will still extract the best content.
- Run `bonfyre-proof score brief.md` to get a quality score before publishing.
- Use `bonfyre-tag detect-lang clean.txt` to auto-tag the episode's language.
