# Recipe: Quick Voice Memo Brief

> **Industry:** Any team
> **Difficulty:** Easy
> **Time:** 1–2 minutes
> **Binaries:** `bonfyre-transcribe`, `bonfyre-transcript-clean`, `bonfyre-brief`

## What you already have

A voice memo — from your phone, a meeting, a drive, a walk, a quick thought capture.

## What Bonfyre does

Transcribes it, cleans it up, and extracts the most important points into a readable summary.

## What you get

A clean, organized brief from a messy voice recording. No typing, no cloud, no cost.

## Step by step

### 1. Transcribe

```sh
bonfyre-transcribe run memo.m4a -o transcript.txt
```

### 2. Clean

```sh
bonfyre-transcript-clean transcript.txt -o clean.txt
```

### 3. Brief

```sh
bonfyre-brief clean.txt -o brief.md
```

Done. `brief.md` has your key points.

## Or use the pipeline

```sh
bonfyre-pipeline run --input memo.m4a --output-dir ./memo-output
```

## Tips

- Works with `.wav`, `.mp3`, `.m4a`, `.flac`, `.ogg`.
- The brief uses TF-IDF to find the most distinctive sentences, not just the longest.
- Pipe the output into `bonfyre-emit` if you want HTML, PDF, or other formats.
