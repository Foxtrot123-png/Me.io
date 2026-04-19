# Me.io

![System Demo](WhatsAppVideo2026-03-22at10.31.45-ezgif.com-speed.gif)

A chatbot and a few automations that stand in for me during the job hunt. It runs on a Raspberry Pi 5 in my flat, orchestrated with n8n, exposed through an ngrok tunnel.

I built it because sending CVs into ATS black holes wasn't working. The idea was to have something always on that could answer recruiter questions about my background, keep itself current as I do new work, and take some of the outreach off my plate.

## What it does

Four workflows, fairly independent of each other.

**Chatbot.** A RAG agent that answers questions about me — career, projects, the MSc, technical topics. Pinecone is split into two namespaces (bio and technical) and the agent picks the right one per query. Gemini 1.5 Flash for reasoning, n8n's agent node for tool use. There's a guardrail step in front that refuses to leak PII or the system prompt if someone tries to extract either.

**Recruiter lookup.** Queries Apollo.io for UK-based technical recruiters and talent managers at companies I'm interested in, pulls verified emails, cleans the output, and appends to a Google Sheet. Apollo's rate limits are tight, so this runs through split-in-batches with wait nodes between chunks.

**Doc ingestion.** Watches a Google Drive folder. When I drop a new PDF in — a paper, a cert, a project write-up — it extracts the text, embeds it, and upserts into Pinecone. Means I don't have to manually reindex when my material changes.

**Per-application outreach.** Triggered by a form submission when I apply somewhere. Looks up the likely recruiter for that role via Apollo, runs the JD through an LLM chain that rewrites my CV bullets to match, and generates a QR code via QuickChart pointing to a landing page built for that specific application.

## Running it on a Pi

The Pi 5 with 8GB handles this, but it took some tuning. Early versions had n8n OOMing under any real load. Capping the Docker container at 1.5GB memory and 1.5 CPUs, plus enabling ZRAM on the host, fixed it — n8n is comfortable within those limits and leaves headroom for everything else running on the box.

Outbound is an ngrok tunnel. Encrypted, no router config, easy to rotate.

Memory-wise: Pinecone handles the long-term vector store, n8n's window buffer handles short-term conversation context in the chatbot.

## Background this leans on

Two things from my actual work history that the project reflects:

- At Deloitte USI I worked with transaction datasets in the 22M+ row range, which is where the batching / rate-limit / don't-load-everything-into-memory instincts come from rather than from tutorials.
- My MSc was on multi-modal AI — BERT and ResNet fused for a classification task, final F1 of 0.82. The thesis and supporting notes are in the Pinecone index, so the chatbot can go into real depth on it.

## Architecture diagrams

Main chatbot and RAG flow:

![AI Twin Workflow](mermaid-diagram-2026-03-21-163009.png)

Recruiter lookup:

![Lead Generation](mermaid-diagram-2026-03-21-163116.png)

Doc ingestion:

![Ingestion Of Data](mermaid-diagram-2026-03-21-163128.png)

## Deploy

```bash
git clone https://github.com/Foxtrot123-png/Me.io
cd Me.io
```

Import `n8n_workflow_template.json` into your n8n instance — that brings in all four workflows.

```bash
docker run -d --name n8n \
  --memory="1.5g" --cpus="1.5" \
  --restart always \
  -p 5678:5678 \
  n8nio/n8n
```

You'll need credentials for Pinecone, Gemini, Apollo, Google Drive, and Google Sheets set up in n8n before the flows will run.

## Contact

- Email: [ritikmohapatra94@gmail.com](mailto:ritikmohapatra94@gmail.com)
- Live chatbot: [ritik-ai-twin.streamlit.app](https://ritik-ai-twin.streamlit.app/)
- LinkedIn: [Ritik R Mohapatra](https://www.linkedin.com/in/ritik-r-mohapatra/)
