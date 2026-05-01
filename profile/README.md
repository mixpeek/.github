<p align="center">
  <a href="https://mixpeek.com">
    <img src="https://mixpeek.com/brand/mixpeek_color.png" alt="Mixpeek" width="200" />
  </a>
</p>

<h3 align="center">Give your agents eyes and ears.</h3>

<p align="center">
  Mixpeek breaks every video, image, and audio file into structured features<br/>
  your agents can search, reason over, and trust.
</p>

<p align="center">
  <a href="https://docs.mixpeek.com">Docs</a> &middot;
  <a href="https://mixpeek.com/start">Get Started</a> &middot;
  <a href="https://docs.mixpeek.com/overview/quickstart">Quickstart</a> &middot;
  <a href="https://mixpeek.com/blog">Blog</a> &middot;
</p>

---

## What is Mixpeek?

Mixpeek is multimodal infrastructure for AI agents. Upload video, images, audio, and documents — Mixpeek automatically extracts features (faces, objects, transcripts, embeddings, structured metadata) and indexes them into searchable collections. Your agent queries a single endpoint and gets structured results back.

**Index** &rarr; Upload files to buckets. Mixpeek runs feature extraction automatically — faces, objects, transcripts, embeddings, and structured metadata all get indexed.

**Search** &rarr; Build retrieval pipelines. Semantic search, face search, object search, transcript search — chain them into multi-stage retrievers exposed as a single endpoint.

**Integrate** &rarr; Wire Mixpeek into your agent as a LangChain tool, an MCP server, or a direct REST call.

## Quickstart

```bash
pip install mixpeek
```

```python
from mixpeek import Mixpeek

mx = Mixpeek(api_key="YOUR_API_KEY")

# Upload a video
mx.buckets.upload(bucket_id="my-bucket", file_path="video.mp4")

# Search across all extracted features
results = mx.retrievers.execute(
    retriever_id="my-retriever",
    inputs={"query_text": "person wearing a red jacket"},
    limit=10,
)
```

Also available as:
- **JavaScript SDK**: `npm install mixpeek`
- **MCP Server**: Connect Claude, Cursor, or any MCP-compatible agent
- **REST API**: `POST https://api.mixpeek.com/v1/retrievers/{id}/execute`
- **CLI**: `mixpeek --version` (included in the Python SDK)

## What Gets Extracted

| File Type | Features |
|-----------|----------|
| **Video** | Face embeddings (ArcFace), scene descriptions (Gemini), visual embeddings (Vertex AI), transcripts (Whisper), keyframes |
| **Images** | Visual embeddings (SigLIP / Vertex AI), face embeddings (ArcFace), OCR, descriptions, structured extraction |
| **Audio** | Transcripts (Whisper), transcript embeddings (E5-Large), multimodal audio embeddings |
| **Documents** | Text chunks, text embeddings (E5-Large), OCR for scanned PDFs, structured extraction |

Each extracted feature becomes an independently searchable document. A single video can produce hundreds of documents — one per face, one per transcript segment, one per scene.

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                      Your Agent                         │
│         (LangChain · MCP · REST · SDK · CLI)            │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                   API Layer                              │
│            FastAPI + Celery Workers                      │
│   Buckets · Collections · Retrievers · Webhooks         │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                 Engine Layer                             │
│                Ray Serve Cluster                         │
│   SigLIP · ArcFace · Whisper · Gemini · E5 · LayoutLM  │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                    Storage                               │
│       MongoDB · Qdrant · Redis · S3-compatible          │
└─────────────────────────────────────────────────────────┘
```

## Integrations

**Object Storage**: AWS S3, Google Cloud Storage, Azure Blob, Cloudflare R2, Backblaze B2, Supabase, Wasabi, Tigris, Mux, Box

**Agent Frameworks**: LangChain, MCP (Model Context Protocol), OpenAI Function Calling, direct REST

**Data Warehouses**: Snowflake, Databricks

## Use Cases

- **Video understanding** — Search surveillance footage by face, scene, or spoken word
- **Content moderation** — Detect brand logos, faces, and unsafe content across media libraries
- **Document intelligence** — Extract structured data from scanned PDFs, invoices, and forms
- **Media asset management** — Find the exact frame across millions of hours of video
- **E-commerce** — Visual similarity search, product matching, catalog enrichment

## Related Repos

| Repo | Description |
|------|-------------|
| [mixpeek/recipes](https://github.com/mixpeek/recipes) | Ready-to-run examples |
| [mixpeek/use-cases](https://github.com/mixpeek/use-cases) | End-to-end demos |
| [mixpeek/showcase](https://github.com/mixpeek/showcase) | Community showcase |
| [mixpeek/multimodal-benchmarks](https://github.com/mixpeek/multimodal-benchmarks) | Benchmarks |

## Resources

- [Documentation](https://docs.mixpeek.com)
- [API Reference](https://docs.mixpeek.com/api-reference)
- [Studio](https://studio.mixpeek.com) — Visual dashboard for managing namespaces, collections, and retrievers
- [Status](https://status.mixpeek.com)

