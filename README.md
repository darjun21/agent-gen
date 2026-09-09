# Agent GEN

A voice-first, RAG-grounded AI companion for students in The Gen Academy's
Mastering Agentic AI Certification cohort — built with ElevenLabs
Conversational AI, GPT-4o, retrieval-augmented generation, and an explicit
honesty guardrail against hallucinating cohort-specific facts.

## What It Does

Agent GEN answers cohort questions by voice: deadlines, project submissions,
session logistics, and concept explanations (RAG, AI agents, embeddings,
chunking, and more). It's built to behave like a knowledgeable, encouraging
teaching assistant — not a generic chatbot — and it explicitly refuses to
guess at cohort-specific facts (deadlines, exact session times, policy
details) it can't verify from its knowledge base, deferring to Maven/Discord
instead.

This project serves two purposes: a genuinely useful tool for The Gen
Academy cohort, and a real, technically defensible Conversational AI / Voice
AI portfolio project.

## Architecture

See docs/architecture.md for the full breakdown. Summary:

Student (voice) -> ElevenLabs STT -> Agent GEN (GPT-4o + RAG over knowledge base)
-> Honesty guardrail -> ElevenLabs TTS -> Student (voice)

## Tech Stack

- ElevenLabs Agents (Conversational AI platform)
- GPT-4o (primary LLM)
- RAG over a custom knowledge base document
- Eleven v3 Conversational voice model with Expressive Mode

## Evaluation

Phase 1 was evaluation-driven, not demo-driven:

- RAG retrieval: 6/6 test queries passed
- Automated tests: grounding and honesty-guardrail scenarios, both PASS
- Live multi-turn voice tests: identity, grounding, concept teaching,
  honesty-under-pressure, and natural conversation flow, all PASS

Full results: docs/evaluation-results.md and evals/test-cases.md.

Development included real debugging, not just configuration — see the
"Issues Found and Fixed" section in the evaluation
