# Recipe: Sermon to Newsletter Pipeline

> **Industry:** Churches, faith communities, ministries
> **Difficulty:** Easy
> **Time:** 3–5 minutes
> **Binaries:** `bonfyre-transcribe`, `bonfyre-brief`, `bonfyre-render`, `bonfyre-emit`, `bonfyre-distribute`

## What you already have

A sermon audio recording, teaching session, or ministry talk.

## What Bonfyre does

Takes the recording and produces:
- A full transcript (searchable archive)
- A devotional summary with key themes
- Newsletter-ready content in HTML
- Multi-format exports (PDF for print, HTML for email)

## What you get

Every sermon becomes reusable content — newsletter, study guide, archive entry — without hours of manual work.

## Step by step

### 1. Transcribe

```sh
bonfyre-transcribe run sermon.mp3 -o transcript.txt
```

### 2. Clean

```sh
bonfyre-transcript-clean transcript.txt -o clean.txt
```

### 3. Generate the summary

```sh
bonfyre-brief clean.txt -o brief.md
```

The brief captures key themes, scripture references, and takeaways.

### 4. Render as newsletter content

```sh
bonfyre-emit brief.md --format html -o newsletter.html
```

### 5. Create a PDF for print

```sh
bonfyre-emit brief.md --format pdf -o sermon-summary.pdf
```

### 6. Distribute (optional)

```sh
bonfyre-distribute send newsletter.html --webhook https://your-email-service/api
```

## Or use the pipeline

```sh
bonfyre-pipeline run --input sermon.mp3 --output-dir ./sermon-output
```

## Example output

**Input:** 35-minute Sunday sermon (28 MB mp3)

**Output:**
- `transcript.txt` — 5,200 words
- `clean.txt` — 4,900 words
- `brief.md` — 500-word summary with key themes and takeaways
- `newsletter.html` — styled HTML ready for email
- `sermon-summary.pdf` — printable handout

## Tips

- Build a searchable sermon archive over time by running `bonfyre-embed` on each transcript.
- Use `bonfyre-tag detect-lang` for multilingual congregations.
- The full transcript makes sermons accessible to deaf and hard-of-hearing members.
