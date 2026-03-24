# 🤖 Me.io — The Digital Surrogate

> **"Tired of being ghosted by an ATS? So was I. So I built a production-grade Agentic RAG system that doesn't sleep, doesn't filter, and actually knows my stack."**

![System Demo](WhatsAppVideo2026-03-22at10.31.45-ezgif.com-speed.gif)

## 📋 Overview
**Me.io** is a self-hosted, agentic ecosystem designed to act as my technical surrogate 24/7. It is a production-grade **Agentic RAG (Retrieval-Augmented Generation)** system with automated GDPR/Cybersecurity guardrails, orchestrated via **n8n** and self-hosted on a **Raspberry Pi 5**. 

While most "AI Twins" are simple GPT wrappers, **Me.io** uses a multi-tool reasoning engine to handle professional inquiries with zero-filler, human-level nuance, ensuring that recruiters and hiring managers get high-fidelity information even when I'm offline.

---

## 🚀 The Engineering Stack
I built this to prove that high-performance AI doesn't require massive cloud overhead—just smart orchestration and edge-computing optimization.

* **Orchestration:** n8n (Self-hosted via Docker)
* **LLM Engine:** Google Gemini 1.5 Flash (Optimized for technical reasoning)
* **Vector Memory:** Pinecone (Multi-namespace RAG for bio vs. security policy isolation)
* **Edge Networking:** ngrok (Secure static domain tunneling to home hardware)
* **Frontend:** Streamlit (Python-based reactive UI)
* **Hardware:** Raspberry Pi 5 (8GB RAM) with ZRAM optimization

---

## 🧠 Technical Wins & Logic Gates
* **The Corporate Foundation:** Engineered to reflect my experience managing **22M+ transaction records** at **Deloitte USI**. It understands data scale, ETL pipelines, and integrity.
* **Academic Distinction:** Capable of defending my MSc research on Multi-modal AI (BERT-ResNet fusion) where I achieved a **0.82 F1 score**.
* **Agentic Governance:** High-priority "Safety/GDPR" namespace check. The agent is programmed to verify GDPR compliance before disclosing private contact info or probing internal system logic.

---

## 🏗️ Architecture & Workflows

### 1. The RAG Chat & Security Tunnel
The frontend communicates with the local Pi 5 node. I’ve implemented header authentication and Docker resource limiting (`--memory="1.5g"`) to ensure 99.9% stability on home hardware.

![AI Twin Workflow](mermaid-diagram-2026-03-21-163009.png)

### 2. The Recruiter Intelligence (Lead Gen)
The system doesn't just wait; it identifies. Integrated **Apollo.io** nodes match recruiters based on job descriptions, archiving data into a centralized Google Sheets command center.

![Lead Generation](mermaid-diagram-2026-03-21-163116.png)

### 3. Automated Data Ingestion
Dynamic ingestion via **Google Drive**. New publications, updated certifications, or stack changes are automatically embedded and indexed into Pinecone via n8n.

![Ingestion Of Data](mermaid-diagram-2026-03-21-163128.png)

---

## 🛠️ Installation & Setup

1.  **Clone the Repo:**
    ```bash
    git clone [https://github.com/Foxtrot123-png/Me.io](https://github.com/Foxtrot123-png/Me.io)
    cd Me.io
    ```

2.  **Environment Setup:**
    * Configure `.streamlit/secrets.toml` with your `N8N_WEBHOOK_URL`.
    * Import `n8n_workflow_template.json` into your n8n instance.

3.  **Docker Deployment (Optimized for Pi):**
    ```bash
    docker run -d --name n8n \
      --memory="1.5g" \
      --cpus="1.5" \
      --restart always \
      -p 5678:5678 \
      -v ~/.n8n:/home/node/.n8n \
      n8nio/n8n
    ```

---

## 📧 Contact & Collaboration
I am currently open to roles in **Data Engineering, AI Strategy, and Agentic Systems.**

* **Email:** [ritikmohapatra94@gmail.com](mailto:ritikmohapatra94@gmail.com)
* **Live Demo:** [ritik-ai.streamlit.app](https://ritik-ai.streamlit.app)
* **LinkedIn:** [Inquire via Me.io for direct link]
