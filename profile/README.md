<p align="center">
  <a href="https://mixpeek.com">
    <img src="https://mixpeek.com/brand/mixpeek_color.png" alt="Mixpeek" width="200" />
  </a>
</p>

<h3 align="center">Turn any data into answers.</h3>

<p align="center">
  The multimodal warehouse for AI. Extract, index and retrieve what's inside<br/>
  video, images, audio and documents. Skip the infrastructure.
</p>

<p align="center">
  <a href="https://docs.mixpeek.com">Docs</a> &middot;
  <a href="https://mixpeek.com/start">Get Started</a> &middot;
  <a href="https://docs.mixpeek.com/overview/quickstart">Quickstart</a> &middot;
  <a href="https://mixpeek.com/blog">Blog</a> &middot;
</p>

---

## What is Mixpeek?

Mixpeek makes any data searchable by AI. Upload video, images, audio and documents, and Mixpeek extracts features (faces, objects, transcripts, embeddings, structured metadata) and indexes them into searchable collections. Your app or agent queries a single endpoint and gets structured results back. Already have embeddings? Bring your own vectors and search them on object storage with MVS.

**Index** &rarr; Upload files to buckets. Mixpeek runs feature extraction automatically, indexing faces, objects, transcripts, embeddings and structured metadata.

**Search** &rarr; Build retrieval pipelines. Chain semantic, face, object and transcript search into multi-stage retrievers exposed as a single endpoint.

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
- **Bring your own vectors**: `POST https://api.mixpeek.com/v1/namespaces/{namespace_id}/documents/upsert`

## What Gets Extracted

| File Type | Features |
|-----------|----------|
| **Video** | Face embeddings (ArcFace), scene descriptions (Gemini), visual embeddings (Vertex AI), transcripts (Whisper), keyframes |
| **Images** | Visual embeddings (SigLIP / Vertex AI), face embeddings (ArcFace), OCR, descriptions, structured extraction |
| **Audio** | Transcripts (Whisper), transcript embeddings (E5-Large), multimodal audio embeddings |
| **Documents** | Text chunks, text embeddings (E5-Large), OCR for scanned PDFs, structured extraction |

Each extracted feature becomes an independently searchable document. A single video can produce hundreds of documents: one per face, one per transcript segment, one per scene.

## Use Cases

- **Ad creative**: Find what makes your best ads work, by searching the hooks and patterns in your top-performing video ads
- **Video understanding**: Search surveillance footage by face, scene, or spoken word
- **Content moderation**: Detect brand logos, faces, and unsafe content across media libraries
- **Document intelligence**: Extract structured data from scanned PDFs, invoices, and forms
- **Media asset management**: Find the exact frame across millions of hours of video
- **E-commerce**: Visual similarity search, product matching, catalog enrichment

