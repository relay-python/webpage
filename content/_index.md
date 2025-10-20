---
title: "Relay SDK"
lead: "Relay is a lightweight Python layer that smooths out the differences between OpenAI, Anthropic, and every provider you plug in next."
cards:
  - title: "Single Predictable Client"
    description: "Instantiate `relay.LLM` once and swap providers by changing the identifier—no rewrites, no bespoke client code."
  - title: "Smart Defaults & Normalized Responses"
    description: "Provider defaults, models, and usage metrics are resolved for you so downstream code always receives the same structure."
  - title: "Extensible Provider Registry"
    description: "Drop in new providers by subclassing `BaseProvider` and registering it, without touching the rest of the SDK."
overview:
  - "Relay sits in front of provider SDKs and exposes a compact façade that always accepts standard chat messages and returns a unified payload. It maximises portability so teams can experiment with different models without rewriting integrations."
  - "The internal design prioritises clarity: configuration errors surface early, HTTP failures are wrapped in typed exceptions, and every provider shares the same lifecycle. New contributors can trace requests end-to-end in just a few modules."
providers:
  - name: "OpenAI"
    summary: "Handles the Chat Completions API with curated parameter support, defaulting to `gpt-4o-mini` while letting teams tweak temperature, token limits, and output formats."
    highlights:
      - "Gracefully surfaces API errors with status codes and raw payloads."
      - "Normalises chat messages and usage metrics, including prompt and completion tokens."
      - "Supports organisational scoping, configurable base URLs, and request timeouts."
  - name: "Anthropic"
    summary: "Bridges Anthropic’s Messages API, translating Relay messages into Claude-friendly payloads and extracting text blocks from streaming-style responses."
    highlights:
      - "Combines multiple system prompts and enforces supported roles up front."
      - "Exposes knobs for temperature, top-p/top-k, and stop sequences."
      - "Maps Anthropic usage fields into Relay’s `Usage` dataclass."
code:
  description: "The `LLM` façade unifies both chat and completion workflows. Provide a provider slug (optionally with a model) and an API key—Relay handles the rest."
  install: "pip install relay"
  snippet: |
    from relay import LLM

    client = LLM(name="openai:gpt-4o-mini", api_key="sk-...")
    response = client.chat(
        [
            {"role": "system", "content": "You are Relay, a helpful SDK assistant."},
            {"role": "user", "content": "Give me a short fun fact about Python."},
        ],
        temperature=0.3,
    )

    print(f"[{response.provider}:{response.model}] {response.content}")
architecture:
  flow: "Calls go through the lightweight `LLM` façade, which parses the provider identifier, merges global defaults, and delegates to a provider implementation retrieved from the registry."
  extensibility: "Every provider subclasses `BaseProvider`, implements `chat`, and inherits a shared `complete` fallback. The registry (`relay.providers`) keeps the surface area stable while exposing `register_provider` for custom integrations."
roadmap:
  upcoming:
    - "Add more providers such as Mistral, Gemini, and local runtimes."
    - "Deliver streaming responses and tool/function calling helpers."
    - "Offer both sync and async flavours for production workloads."
  contributing: "Follow the Developer Guidelines: set up a virtualenv, install in editable mode, keep changes typed and tested with `pytest`, and document new workflows in the README and examples."
---
