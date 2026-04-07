# Recipe: Discovery Call to Proposal Packet

> **Industry:** Agencies, consultants, freelancers
> **Difficulty:** Easy
> **Time:** 3–5 minutes
> **Binaries:** `bonfyre-transcribe`, `bonfyre-brief`, `bonfyre-proof`, `bonfyre-offer`, `bonfyre-pack`

## What you already have

A recorded discovery call, client intake conversation, or sales meeting — any audio file.

## What Bonfyre does

Takes the raw call recording and produces:
- A full transcript
- An executive summary with key points and action items
- A quality score on the conversation
- A dynamically priced proposal/offer
- A packaged deliverable ready to send

## What you get

A professional proposal packet from every sales call — no manual note-taking, no forgetting details, no hours writing proposals by hand.

## Step by step

### 1. Transcribe the call

```sh
bonfyre-transcribe run call.m4a -o transcript.txt
```

### 2. Clean

```sh
bonfyre-transcript-clean transcript.txt -o clean.txt
```

### 3. Generate the brief

```sh
bonfyre-brief clean.txt -o brief.md
```

The brief extracts the client's needs, pain points, and action items using TF-IDF scoring.

### 4. Score quality

```sh
bonfyre-proof score brief.md -o proof-summary.json
```

Scores across 4 dimensions: structure, vocabulary density, clarity, and coverage. Helps you know if the brief is client-ready.

### 5. Bundle the proof

```sh
bonfyre-proof bundle clean.txt brief.md proof-summary.json -o proof-dir/
```

### 6. Generate a priced offer

```sh
bonfyre-offer proof-dir/ -o offer-dir/
```

Dynamic pricing based on word count, quality score, and complexity. Outputs `offer.json`, `offer.md`, and `outreach.md`.

### 7. Package everything

```sh
bonfyre-pack assemble proof-dir/ offer-dir/ ./proposal-packet/
```

Or create a `.tar.gz`:

```sh
bonfyre-pack archive proof-dir/ offer-dir/ proposal-packet.tar.gz
```

## Or use the pipeline

```sh
bonfyre-pipeline run --input call.m4a --output-dir ./proposal
```

One command. All 8 steps.

## Example output

**Input:** 22-minute discovery call (18 MB m4a)

**Output packet contains:**
- `transcript.txt` — full conversation
- `deliverable.md` — executive summary
- `proof-bundle.json` — quality scores (structure: 22/25, density: 18/25, clarity: 20/25, coverage: 19/25)
- `offer.json` — dynamic price ($29, based on 4,500 words, pass quality)
- `offer.md` — formatted proposal
- `outreach.md` — client-ready email draft

## Tips

- Review `offer.md` before sending — the pricing is algorithmic but you can adjust.
- For repeat clients, the proof scores let you track conversation quality over time.
- Use `bonfyre-distribute send offer.json --webhook <URL>` to push to your CRM or Slack.
