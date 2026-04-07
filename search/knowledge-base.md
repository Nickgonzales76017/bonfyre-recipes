# Recipe: Build a Knowledge Base

> **Industry:** Any team with documentation
> **Difficulty:** Moderate
> **Time:** 5–10 minutes (setup), then automatic
> **Binaries:** `bonfyre-embed`, `bonfyre-vec`, `bonfyre-query`

## What you already have

A folder of documents — markdown, text files, transcripts, FAQs, help docs, internal guides.

## What Bonfyre does

Embeds every document into a local vector database, then lets you search by meaning instead of exact keywords.

## What you get

A semantic search engine for your internal knowledge. Ask a question in plain language, get the most relevant documents back.

## Step by step

### 1. Create the database

```sh
bonfyre-embed --create-db knowledge.db
```

### 2. Index your documents

```sh
for doc in docs/*.md; do
  bonfyre-embed "$doc" --insert-db knowledge.db
done
```

Each document gets embedded as a 384-dimensional vector using the local ONNX sentence transformer.

### 3. Search

```sh
bonfyre-query knowledge.db "how do we handle refunds"
```

Returns the most semantically similar documents, ranked by cosine similarity.

## Tips

- Re-index after adding new documents. The database is just a SQLite file — back it up like any other file.
- Combine with `bonfyre-transcribe` to index audio content: transcribe first, then embed the transcripts.
- Use `bonfyre-vec` directly for low-level vector operations (insert, search, cosine similarity).
- The ONNX model (`all-MiniLM-L6-v2.onnx`) is ~22 MB and runs locally — no API calls.
