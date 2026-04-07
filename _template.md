# Recipe: [Title]

> **Industry:** [e.g., Property Management]
> **Difficulty:** Easy
> **Time:** 2–5 minutes
> **Binaries:** `bonfyre-transcribe`, `bonfyre-brief`, `bonfyre-pack`

## What you already have

[Describe the messy input the user already has — recordings, notes, files, etc.]

## What Bonfyre does

[Describe what Bonfyre does with that input in plain language.]

## What you get

[Describe the organized, useful output.]

## Step by step

### 1. Prepare the input

```sh
# If you have an audio file:
bonfyre-media-prep normalize input.m4a -o prepared.wav
```

### 2. Transcribe

```sh
bonfyre-transcribe run prepared.wav -o transcript.txt
```

### 3. Clean up

```sh
bonfyre-transcript-clean transcript.txt -o clean.txt
```

### 4. Generate summary

```sh
bonfyre-brief clean.txt -o brief.md
```

### 5. Package output

```sh
# Create a deliverable packet
bonfyre-proof score brief.md -o proof-summary.json
bonfyre-proof bundle clean.txt brief.md proof-summary.json -o proof-dir/
bonfyre-pack assemble proof-dir/ offer-dir/ output/
```

## Or use the pipeline

```sh
bonfyre-pipeline run --input input.m4a --output-dir ./output
```

## Example output

[Show a brief example of what the final output looks like.]

## Tips

- [Any tips specific to this industry or workflow.]
