# Bonfyre Recipes

Ready-to-use workflows for [Bonfyre](https://github.com/Nickgonzales76017/bonfyre) — the 47-binary local-first backend engine.

Each recipe is a step-by-step guide that shows how Bonfyre turns messy business input (calls, files, notes, recordings) into organized, searchable, reusable output.

## How recipes work

Every recipe follows the same pattern:

1. **Input** — a file you already have (audio, notes, documents)
2. **Pipeline** — the Bonfyre binaries that process it
3. **Output** — what you get (summaries, packets, searchable archives, deliverables)

Recipes are designed for non-technical teams. You don't need to understand the binaries.

## Recipe index

### By industry

| Industry | Recipe | Binaries used |
|----------|--------|---------------|
| Property Management | [Maintenance voicemail pipeline](property-management/maintenance-voicemail.md) | media-prep, transcribe, brief, proof, pack |
| Property Management | [Inspection report generator](property-management/inspection-report.md) | transcribe, brief, render, emit |
| Bars & Nightlife | [Shift recap from voice memo](hospitality/shift-recap.md) | transcribe, clean, brief, emit |
| Bars & Nightlife | [Event post-mortem](hospitality/event-postmortem.md) | transcribe, brief, proof, pack |
| Restaurants | [Manager meeting summary](hospitality/manager-meeting.md) | transcribe, brief, emit |
| Restaurants | [Staff training doc from walkthrough](hospitality/staff-training.md) | transcribe, clean, brief, render, emit |
| Salons & Barbershops | [Service SOP generator](personal-services/service-sop.md) | transcribe, brief, render, emit |
| Gyms & Fitness | [Class description from coach recording](fitness/class-description.md) | transcribe, clean, brief, emit |
| Local Services | [Job-site voice note to estimate](trades/jobsite-to-estimate.md) | transcribe, brief, offer, pack |
| Real Estate | [Buyer consultation summary](real-estate/buyer-consult.md) | transcribe, brief, proof, pack |
| Insurance | [Client call intake processor](insurance/call-intake.md) | ingest, transcribe, brief, proof, pack |
| Law Offices | [Client intake packet](legal/client-intake.md) | ingest, transcribe, brief, proof, pack |
| Medical/Dental | [Staff SOP from walkthrough](medical/staff-sop.md) | transcribe, brief, render, emit |
| Nonprofits | [Program debrief to board packet](nonprofit/program-debrief.md) | transcribe, brief, proof, render, emit, pack |
| Schools | [Workshop recording to course material](education/workshop-to-course.md) | transcribe, brief, render, emit |
| Churches | [Sermon to newsletter pipeline](faith/sermon-pipeline.md) | transcribe, brief, render, emit, distribute |
| Museums | [Oral history archival pipeline](cultural/oral-history.md) | transcribe, clean, brief, embed, pack |
| Agencies | [Discovery call to proposal](agency/discovery-to-proposal.md) | transcribe, brief, proof, offer, render, pack |
| Clubs & Events | [Post-event recap generator](hospitality/event-recap.md) | transcribe, brief, emit, distribute |

### By workflow type

| Workflow | Recipe | Best for |
|----------|--------|----------|
| Audio → Summary | [Quick voice memo brief](core/voice-memo-brief.md) | Any team |
| Audio → Blog post | [Podcast episode to post](content/podcast-to-post.md) | Publishers, podcasters |
| Audio → Deliverable | [Call to client packet](core/call-to-packet.md) | Agencies, consultants |
| Audio → Training doc | [Recording to SOP](core/recording-to-sop.md) | Any business |
| Content → Multi-format | [Repurpose one source](content/repurpose.md) | Content teams |
| Docs → Search | [Build a knowledge base](search/knowledge-base.md) | Any team with docs |
| File → Archive | [Searchable archive entry](search/archive-entry.md) | Libraries, research |

## Prerequisites

- [Bonfyre installed](https://github.com/Nickgonzales76017/bonfyre#install) (`make && make install`)
- Models downloaded (`make models`)
- Audio files in `.wav`, `.mp3`, `.m4a`, `.flac`, or `.ogg` format

## Running a recipe

```sh
# Example: voice memo to brief
bonfyre-transcribe run memo.m4a -o transcript.txt
bonfyre-transcript-clean transcript.txt -o clean.txt
bonfyre-brief clean.txt -o brief.md
```

Or use the pipeline command for the full chain:

```sh
bonfyre-pipeline run --input memo.m4a --output-dir ./output
```

## Contributing

Add a new recipe by creating a markdown file in the appropriate industry folder. Follow the template in [_template.md](_template.md).

## License

MIT — same as Bonfyre.
