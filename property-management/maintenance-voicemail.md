# Recipe: Maintenance Voicemail Pipeline

> **Industry:** Property management, apartment complexes, HOAs
> **Difficulty:** Easy
> **Time:** 2–3 minutes
> **Binaries:** `bonfyre-media-prep`, `bonfyre-transcribe`, `bonfyre-brief`, `bonfyre-proof`, `bonfyre-pack`

## What you already have

A resident voicemail, maintenance call recording, or voice note from a property walk-through.

## What Bonfyre does

Takes the audio and produces:
- A clean transcript of the request
- A summary noting the likely issue type, urgency, and follow-up items
- A quality score
- A packaged maintenance ticket ready for staff review

## What you get

Fewer missed requests. Faster vendor coordination. A paper trail that doesn't depend on someone remembering to write it down.

## Step by step

### 1. Normalize the audio

```sh
bonfyre-media-prep normalize voicemail.m4a -o voicemail.wav
```

### 2. Transcribe

```sh
bonfyre-transcribe run voicemail.wav -o transcript.txt
```

### 3. Clean up

```sh
bonfyre-transcript-clean transcript.txt -o clean.txt
```

### 4. Generate the summary

```sh
bonfyre-brief clean.txt -o brief.md
```

The brief identifies the key issue, any urgency signals, and follow-up items.

### 5. Score and package

```sh
bonfyre-proof score brief.md -o proof-summary.json
bonfyre-proof bundle clean.txt brief.md proof-summary.json -o ticket/
```

### 6. Package for staff

```sh
bonfyre-pack assemble ticket/ ticket/ ./maintenance-packet/
```

## Or use the pipeline

```sh
bonfyre-pipeline run --input voicemail.m4a --output-dir ./maintenance-packet
```

## Example output

**Input:** 90-second resident voicemail about a leaking faucet

**Output:**
- `transcript.txt` — "Hi, this is unit 204. The kitchen faucet has been dripping since yesterday..."
- `brief.md` — Summary: kitchen faucet leak, unit 204, resident requests repair, no emergency but persistent
- `proof-summary.json` — quality score 71/100
- `maintenance-packet/` — everything packaged for the maintenance coordinator

## Tips

- Set up a shared folder where staff drops voicemail files. Run the pipeline on each new file.
- The brief will catch urgency words like "flood," "emergency," "no hot water" and score them higher.
- Use `bonfyre-tag detect-lang` if you serve multilingual communities — it handles language identification per chunk.
