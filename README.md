<div align="center">

# ODS

**Osmantic Deployment System**

<p align="center">
  <a href="../../releases" target="_blank" rel="noopener noreferrer">
    <img src="ods/docs/images/osmantic-lockup.png" alt="Osmantic" width="800">
  </a>
</p>

**Turn your PC, Mac, or Linux box into a private AI server.**

AI server and homelab setup is rapidly becoming a solved problem.
It should feel that way for everyone.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/Osmantic/ODS)](https://github.com/Osmantic/ODS/stargazers)
[![Release](https://img.shields.io/github/v/release/Osmantic/ODS)](https://github.com/Osmantic/ODS/releases)


</div>

ODS installs and wires together everything you need to run AI locally, so you do not have to assemble Ollama, Open WebUI, n8n, ComfyUI, and privacy tools by hand:

- **Local model inference** — run open models on your own hardware
- **ChatGPT-style web UI** — talk to your models from any browser
- **Control dashboard** — manage models, services, setup, GPU status, and extensions from one place
- **Voice, agents, and workflows** — build automations that can listen, speak, call tools, and get work done
- **RAG and search** — connect local documents, private search, and retrieval workflows
- **Image generation** — run local image tools without sending prompts to a hosted API
- **Privacy and ops** — keep service auth, secrets, observability, and diagnostics in one local stack

No cloud required. No subscriptions required. Your prompts and data stay on your machine unless you choose otherwise. Cloud and hybrid API modes are optional when you want them.

## Get Started

## Install

[View all releases](../../releases)

| Platform | Download | Run |
|----------|----------|-----|
| **Windows x64** | [ODS-x64.7z](../../releases) | Run installer → launch `ODS-x64.exe` |
| **Linux x64** | [ODS-Linux-x64.run](../../releases) | `chmod +x` → run installer |
| **macOS Apple Silicon** | [ODS-macOS-arm64.dmg](../../releases) | Open DMG → drag to Applications |

---

## At A Glance

| Question | Answer |
|----------|--------|
| **What is it?** | A local AI server stack for your own hardware, with a one-command Linux/macOS installer and a PowerShell installer for Windows. |
| **Who is it for?** | People who want private AI at home, in a lab, or on a workstation without hand-wiring a dozen services. |
| **What do I get?** | Local inference, Open WebUI chat, a control dashboard, voice, agents, workflows, RAG, search, image generation, privacy tools, observability, and developer tools. |
| **What does it run on?** | Linux, Windows with WSL2/Docker Desktop, and macOS Apple Silicon. |
| **Is cloud required?** | No. Local mode is the default; cloud and hybrid API modes are optional. |

| If you know... | ODS adds... |
|----------------|----------------------|
| **Ollama / llama.cpp** | The surrounding server stack: chat, dashboard, voice, RAG, workflows, agents, privacy, and service management. |
| **Open WebUI** | A full installer and control plane around Open WebUI, plus pre-wired local services. |
| **AnythingLLM** | Broader local AI appliance behavior beyond RAG: inference, chat, voice, workflows, image generation, and ops. |
| **n8n self-hosted AI starter kits** | Workflow automation as one part of a larger private AI server. |

---

> **Current Platform Support**
>
> | Platform | Status |
> |----------|--------|
> | **Linux** (NVIDIA + AMD + Intel Arc) | **Supported** — install and run today |
> | **Windows** (NVIDIA + AMD) | **Supported** — install and run today |
> | **macOS** (Apple Silicon) | **Supported** — install and run today |

---

## Why ODS?

A handful of companies control the vast majority of global AI traffic — and with it, your data, your costs, and your uptime. Every query you send to a centralized provider is business intelligence you don’t own, running on infrastructure you don’t control, priced on terms you can’t negotiate.

If AI is becoming critical infrastructure, it shouldn’t be rented. Self-hosting local AI should be a sovereign human right, not a career choice.

Because running your own AI shouldn't require a CS degree and a weekend of debugging CUDA drivers. Right now, setting up local AI means stitching together a dozen projects, writing Docker configs from scratch, and praying everything talks to each other. Most people give up and go back to paying OpenAI.

We built ODS so you don't have to.

- **One command** — detects your GPU, picks the right model, generates credentials, launches everything
- **Chatting in under 2 minutes** — bootstrap mode gives you a working model instantly while your full model downloads in the background
- **Full service stack, pre-wired** — chat, agents, voice, workflows, search, RAG, image generation, privacy tools, observability, and developer tools. All talking to each other out of the box
- **Fully moddable** — every service is an extension. Drop in a folder, run `ods enable`, done
---

## What's In The Box

### Chat & Inference
- **Open WebUI** — full-featured chat interface with conversation history, web search, document upload, and 30+ languages.
- **llama-server** — high-performance LLM inference with continuous batching, auto-selected for your GPU; Linux Docker host API defaults to `localhost:11434`, native macOS/Windows paths use `localhost:8080`, and container API runs on `8080`
- **LiteLLM** — API gateway supporting local/cloud/hybrid modes
- **TEI Embeddings** — text embedding service for RAG and search workflows

### Voice
- **Whisper** — speech-to-text
- **Kokoro** — text-to-speech

### Agents & Automation
- **Hermes Agent** — default local-first autonomous/browser agent with memory, skills, and a magic-link-gated proxy
- **OpenClaw** — deprecated legacy autonomous agent, still opt-in during the migration window
- **n8n** — workflow automation with 400+ integrations (Slack, email, databases, APIs)
- **APE** — Agent Policy Engine for auditing and governing autonomous tool calls
- **OpenCode** — browser-based AI coding assistant wired to the local stack
- **Memory Shepherd** — host/systemd helper for agent memory lifecycle management

### Knowledge & Search
- **Qdrant** — vector database for retrieval-augmented generation (RAG)
- **SearXNG** — self-hosted web search (no tracking)
- **Perplexica** — deep research engine
- **Brave Search** — optional paid Brave Search API integration

### Creative
- **ComfyUI** — node-based image generation

### Privacy & Ops
- **Privacy Shield** — PII scrubbing proxy for API calls
- **Dashboard** — real-time GPU metrics, service health, model management
- **Dashboard API** — service health, setup, status, metrics, and management API behind the dashboard
- **Token Spy** — token usage monitor for local and proxied LLM traffic
- **Langfuse** — optional LLM observability and tracing

---

## Hardware Auto-Detection

The installer detects your GPU and first assigns a deterministic hardware tier. Linux and macOS then run the versioned catalog selector (`ods/scripts/select-model.py`), while Windows uses the PowerShell catalog selector in `ods/installers/windows/lib/tier-map.ps1`; both read `ods/config/model-library.json` to choose the best installable GGUF for the detected memory envelope. The final choice is written to `.env` as `LLM_MODEL`, `GGUF_FILE`, `MAX_CONTEXT`, and `MODEL_RECOMMENDATION_*`.

`MODEL_PROFILE=qwen` is the default non-Gemma catalog profile, so the effective pick can be Qwen, Phi, or DeepSeek depending on what fits best. `MODEL_PROFILE=gemma4` forces Gemma 4 where available, and `MODEL_PROFILE=auto` uses Gemma 4 on NVIDIA, Apple Silicon, and Intel Arc tiers. Override tier selection with `./install.sh --tier 3`; override the model family with `MODEL_PROFILE=gemma4 ./install.sh` or `MODEL_PROFILE=auto ./install.sh`.

When Hermes is enabled, which is the default agent path, installers keep the first-run bootstrap model at a 64K context floor and promote the full local model context to 128K where the selected model supports it. That avoids Hermes's hard 64K minimum while preserving the under-2-minute first chat experience. The examples below are current catalog-selector outputs for common hardware envelopes; exact installs can differ with detected VRAM/RAM, host architecture, existing downloads, or explicit profile overrides. Throughput still needs a local benchmark after first launch.

### NVIDIA

| Tier / envelope | Current default catalog pick | Context | Example hardware |
|------|--------------|---------|--------------|
| 0 / 8 GB CPU fallback | Qwen3.5 2B (Q4_K_M) | 8K | Low-RAM CPU-only |
| 1 / 8 GB discrete VRAM | Qwen3.5 9B (Q4_K_M) | 32K | RTX 4060, RTX 3060 12GB |
| 2 / 12 GB discrete VRAM | Phi-4 14B (Q4_K_M) | 16K | RTX 4070-class cards |
| 3 / 24 GB discrete VRAM | Qwen3.5 27B (Q4_K_M) | 32K | RTX 4090, A6000 |
| 4 / 48 GB discrete VRAM | DeepSeek R1 Distill Llama 70B (Q4_K_M) | 32K | A6000 Ada, L40S |
| NV_ULTRA / 90+ GB amd64 discrete VRAM | Qwen3 Coder Next (Q4_K_M) | 128K | Multi-GPU A100/H100 |
| NV_ULTRA / 90+ GB arm64 unified memory | Qwen3.6 35B-A3B (UD-Q4_K_M) | 128K | DGX Spark / GB10-class hosts |

### AMD Strix Halo (Unified Memory)

| Tier / envelope | Current default catalog pick | Context | Hardware |
|------|--------------|---------|----------|
| SH_COMPACT / 64 GB unified RAM | Qwen3.6 35B-A3B (UD-Q4_K_M) | 128K | Ryzen AI MAX+ 395 (64GB) |
| SH_LARGE / 96 GB unified RAM | DeepSeek R1 Distill Llama 70B (Q4_K_M) | 32K | Ryzen AI MAX+ 395 (96GB) |
| SH_LARGE / 124 GB unified RAM | Qwen3.6 35B-A3B (UD-Q4_K_M) | 128K | Ryzen AI MAX+ 395 (128GB class) |

The selector routes unified-memory hosts away from Qwen3 Coder Next when that model would otherwise be selected, because current repo policy documents correctness issues on those backends.

### Apple Silicon (Unified Memory, Metal)

| Tier / envelope | Current default catalog pick | Context | Example hardware |
|------|--------------|---------|-----------------|
| 0 / 8 GB unified RAM | Phi-4 Mini (Q4_K_M) | 128K | M1/M2 base (8GB) |
| 1 / 16 GB unified RAM | Qwen3.5 9B (Q4_K_M) | 32K | M4 Mac Mini (16GB) |
| 2 / 32 GB unified RAM | Phi-4 14B (Q4_K_M) | 16K | M4 Pro Mac Mini, M3 Max MacBook Pro |
| 3 / 48 GB unified RAM | Qwen3.5 27B (Q4_K_M) | 32K | M4 Pro (48GB), M2 Max (48GB) |
| 4 / 64+ GB unified RAM | Qwen3.6 35B-A3B (UD-Q4_K_M) | 128K | M2 Ultra Mac Studio, M4 Max (64GB+) |

### Intel Arc (Linux, SYCL)

| Tier / envelope | Current default catalog pick | Context | Example hardware |
|------|--------------|---------|------------------|
| ARC_LITE / 6 GB discrete VRAM | Phi-4 Mini (Q4_K_M) | 128K | Arc A380 |
| ARC_LITE / 8 GB discrete VRAM | Qwen3.5 9B (Q4_K_M) | 32K | Arc A750 |
| ARC / 16 GB discrete VRAM | Phi-4 14B (Q4_K_M) | 16K | Arc A770 16GB, newer Arc GPUs |

Gemma 4 profile tiers remain in the installer tier maps: E2B on entry hardware, E4B on midrange hardware, 26B-A4B on pro hardware, and 31B on large/ultra hardware.

---

## Bootstrap Mode

No waiting for large downloads. ODS uses bootstrap mode by default:

1. Downloads a tiny 1.5B model in under a minute
2. You start chatting immediately
3. The full model downloads in the background
4. Hot-swap to the full model when it's ready — zero downtime

The bootstrap model starts with a 64K context window so Hermes can work during the first session. After the background download finishes, ODS swaps to the full model and restores the Hermes/full-model context target.

Skip bootstrap: `./install.sh --no-bootstrap`

---

## Switching Models

The installer picks a model for your hardware, but you can switch anytime:

```bash
ods model current              # What's running now?
ods model list                 # Show all available tiers
ods model swap T3              # Switch to a different tier
```

If the new model isn't downloaded yet, pre-fetch it first:

```bash
./scripts/pre-download.sh --tier 3    # Download before switching
ods model swap T3                    # Then swap (restarts llama-server)
```

Already have a GGUF you want to use? Drop the single `.gguf` file in
`data/models/`, then open Dashboard -> Models and load the local entry. For
older installs or headless maintenance, update `GGUF_FILE` and `LLM_MODEL` in
`.env`, then restart with the CLI:

```bash
ods restart llm
```

Or restart the container directly from the installed `ods` directory:

```bash
docker compose restart llama-server
```

Rollback is automatic — if a new model fails to load, ODS reverts to your previous model.

---

## ods-cli

The `ods` CLI manages your entire stack:

```bash
ods status                # Health checks + GPU status
ods list                  # All services and their state
ods logs llm              # Tail logs (aliases: llm, stt, tts)
ods restart [service]     # Restart one or all services
ods start / stop          # Start or stop the stack

ods mode cloud            # Switch to cloud APIs via LiteLLM
ods mode local            # Switch back to local inference
ods mode hybrid           # Local primary, cloud fallback

ods model swap T3         # Switch to a different hardware tier
ods enable n8n            # Enable an extension
ods disable whisper       # Disable one

ods config show           # View .env (secrets masked)
ods preset save gaming    # Snapshot current config
ods preset load gaming    # Restore it
```

---

## How It Compares

Other tools get you part of the way. ODS gets you the whole way.

| | ODS | Ollama + Open WebUI | LocalAI |
|---|:---:|:---:|:---:|
| **Scope** | Full AI stack — inference to agents to workflows | LLM + chat | LLM only |
| One-command install | Everything, auto-configured | LLM + chat only | LLM only |
| Hardware auto-detect + model selection | NVIDIA + AMD Strix Halo + Apple Silicon + Intel Arc + CPU/cloud fallback | No | No |
| AMD APU unified memory support | Platform-specific accelerated backend, selected by installer | Partial (Vulkan) | No |
| Autonomous AI agents | Hermes Agent default; OpenClaw legacy opt-in | No | No |
| Workflow automation | n8n (400+ integrations) | No | No |
| Voice (STT + TTS) | Whisper + Kokoro | No | No |
| Image generation | ComfyUI | No | No |
| RAG pipeline | Qdrant + embeddings | No | No |
| Extension system | Manifest-based, hot-pluggable | No | No |
| Multi-GPU | Yes (NVIDIA) | Partial | Partial |

---

---

## License

Apache 2.0 — Use it, modify it, ship it. See [LICENSE](LICENSE).
