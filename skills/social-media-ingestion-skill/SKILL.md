# Social Media Ingestion Skill

## Purpose

Transform social media content into durable, traceable knowledge.

This skill handles acquisition, metadata preservation, transcription and preparation for downstream knowledge extraction.

## Primary Path

Use local and scriptable tooling first.

```text
YouTube / Instagram
        ↓
yt-dlp
        ↓
Video
Metadata
Subtitles
        ↓
Whisper or compatible speech-to-text
        ↓
Markdown transcript
        ↓
knowledge-extraction-skill
        ↓
integration-candidate-skill if needed
```

## Secondary Path

NotebookLM may be used only as an optional analysis and visualization path.

```text
Transcript or source bundle
        ↓
NotebookLM
        ↓
Report
Mind map
Table
        ↓
knowledge-extraction-skill
```

NotebookLM must not be treated as the durable knowledge store.

## Use When

- YouTube videos should be analyzed.
- Instagram reels or videos should be analyzed.
- Social media content may contain durable knowledge.
- A transcript should be converted into second-brain knowledge.
- The original source URL and metadata must remain traceable.

## Do Not Use When

- The user only wants to watch, download or archive media.
- The content is entertainment without durable knowledge value.
- Legal, privacy or platform-policy restrictions prohibit download or processing.
- The source cannot be accessed legitimately.

## Supported Source Types

Version 1 supports:

```yaml
source_type: youtube
source_type: instagram
```

Future source types may include:

```yaml
source_type: tiktok
source_type: linkedin
source_type: podcast
source_type: x-video
```

## Required Metadata

Capture these fields whenever available:

```yaml
source_type:
source_url:
creator:
published:
duration:
language:
downloaded_at:
transcript_tool:
```

Optional fields:

```yaml
title:
description:
tags:
platform_id:
thumbnail:
subtitle_source:
media_file:
transcript_file:
```

## Core Rules

1. Preserve the original source URL.
2. Preserve creator, title, publication date and duration when available.
3. Prefer subtitles when reliable.
4. Use speech-to-text when subtitles are missing or low quality.
5. Store transcripts as Markdown before analysis.
6. Remove influencer filler, calls-to-action and engagement bait.
7. Preserve durable knowledge, workflows, tools, claims, examples and decisions.
8. Keep metadata separate from extracted knowledge.
9. Forward extracted content to `knowledge-extraction-skill`.
10. Use `integration-candidate-skill` when existing knowledge should be updated.

## Quality Filter

Discard content that only contains:

- like and subscribe prompts
- follow-me calls
- sales funnels without reusable knowledge
- engagement bait
- reaction-only content
- context-free opinions

Preserve content that contains:

- frameworks
- workflows
- tools
- architectures
- research findings
- benchmarks
- implementation details
- decisions
- reusable examples
- recipes and cooking instructions

### Recipe Content

Food and recipe content is never discarded.

If the content contains a complete or partial recipe, apply:

```yaml
extraction_decision: create-knowledge
```

Store the extracted recipe as a knowledge note under:

```text
30-knowledge/rezepte/
```

Use this frontmatter for recipe notes:

```yaml
---
type: knowledge
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
source_url: <instagram-url>
creator: <creator>
tags:
  - rezept
  - kochen
---
```

Include at minimum:

- Zutaten (ingredients)
- Zubereitung (preparation steps)
- Quelle (source URL and creator)

## Output Structure

Use this structure for prepared transcripts:

```markdown
---
type: social-media-source
status: captured
source_type: youtube
source_url:
creator:
published:
duration:
language:
downloaded_at:
transcript_tool:
tags: []
---

# Title

## Source Metadata

## Transcript

## Extraction Notes
```

## Decision Handoff

This skill prepares the content.

It does not decide the final knowledge outcome.

After ingestion, call `knowledge-extraction-skill` to decide:

```yaml
extraction_decision: discard
extraction_decision: create-reference
extraction_decision: create-knowledge
extraction_decision: create-task
extraction_decision: create-candidate
extraction_decision: update-existing
```

## Integration With Other Skills

When multiple skills apply, use this order:

1. `social-media-ingestion-skill`
2. `knowledge-extraction-skill`
3. `integration-candidate-skill`
4. `action-first-skill`

## File Naming Conventions

### Download Strategy

Always download the full video including audio. Do not use audio-only mode unless explicitly requested.

Reasons:

- Visual content may be relevant for analysis (on-screen text, diagrams, demonstrations)
- A local copy ensures content is available even if the source is taken down
- ffmpeg is required and available via `imageio-ffmpeg`

Default download command:

```bash
yt-dlp -f "bestvideo+bestaudio" --merge-output-format mp4 --cookies-from-browser firefox -o "<output-path>"
```

Audio-only mode is an **exception** and requires explicit user request:

```bash
yt-dlp -x --audio-format m4a --cookies-from-browser firefox -o "<output-path>"
```

### Video Quality

Select quality based on use case:

| Quality | yt-dlp flag | Use case |
|---------|-------------|----------|
| Best available (default) | `-f "bestvideo+bestaudio"` | Archiving, visual analysis, full quality |
| Compressed 720p | `-f "bestvideo[height<=720]+bestaudio"` | Storage-conscious, transcription only |
| Compressed 480p | `-f "bestvideo[height<=480]+bestaudio"` | Minimal storage, audio focus |
| Audio only | `-x --audio-format m4a` | Exception – only on explicit request |

Default output format: `mp4` (requires ffmpeg for stream merging).

If ffmpeg is not available as a system command, use the bundled binary from `imageio-ffmpeg`:

```bash
python -c "import imageio_ffmpeg; print(imageio_ffmpeg.get_ffmpeg_exe())"
```

Pass the result via `--ffmpeg-location <path>` if needed.

---

### Temporary Media Storage

Store downloaded media files under:

```text
.tools/.temp/YYYY-MM-DD_<short-title>/
```

The date is the **download date**, not the publication date.
The short-title is a human-readable slug derived from the content topic.

Examples:

```text
.tools/.temp/2026-06-13_llm-counsel/
.tools/.temp/2026-06-14_whisper-v3-benchmark/
```

Add `.tools/.temp/` to `.gitignore` to prevent binary and temporary files from being committed.

### Media File Names

Name individual media files as:

```text
<short-title>_<published-date>.<ext>
```

The published date is the original publication date of the source content.

Examples:

```text
llm-counsel_2026-06-11.m4a
llm-counsel_2026-06-11.info.json
llm-counsel_2026-06-11.txt
```

### Transcript Note File Names

Use the standard inbox naming convention for transcript Markdown notes:

```text
YYYY-MM-DD-HHmm_<short-title>.md
```

The timestamp is the processing or download time.

Examples:

```text
2026-06-13-0822_llm-counsel-jannikhi.md
2026-06-14-1030_whisper-v3-benchmark-openai.md
```

---

## Safety and Compliance

Only process content that the user is allowed to access and use.

Respect platform terms, copyright, privacy and personal data constraints.

Do not bypass access controls or process private content without explicit authorization.
