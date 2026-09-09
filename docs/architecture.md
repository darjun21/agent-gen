# Agent GEN Architecture

## What It Is

Agent GEN is a voice-first AI companion for students in The Gen Academy's
Mastering Agentic AI Certification cohort. It answers cohort logistics
questions (deadlines, submissions, sessions), explains agentic AI concepts
(RAG, embeddings, agents, etc.), and encourages students — with an explicit
honesty guardrail that defers to Maven/Discord rather than guessing at
uncertain cohort-specific facts.

## Phase 1 Architecture (current)
Student (voice)
↓
ElevenLabs Speech-to-Text (Scribe v2 Realtime)
↓
Agent GEN system prompt + conversation state
↓
GPT-4o (primary LLM)
↓
RAG retrieval over AgentGEN_KnowledgeBase.docx
↓
Grounded response, filtered by honesty guardrail
↓
ElevenLabs Text-to-Speech (Eleven v3 Conversational, Expressive Mode)
↓
Student (voice)

## Key Design Decisions

- **Voice-first, not text-first.** Response style is explicitly tuned for
  spoken delivery — short, natural sentences rather than written-style lists
  or long paragraphs.
- **RAG grounding over a static knowledge base doc**, rather than relying on
  the LLM's general knowledge for cohort-specific facts. This is what makes
  the honesty guardrail enforceable: the agent can point to what it does and
  doesn't have grounded information for.
- **Explicit honesty guardrail for uncertain schedules/deadlines.** The agent
  is instructed to say "I don't know, check Maven/Discord" rather than
  guess — including under direct pressure to guess. This was tested
  adversarially, not just for the happy path.
- **General AI knowledge is allowed for concept teaching** (RAG, embeddings,
  agents, etc.) but is explicitly subordinate to the knowledge base whenever
  the two would conflict on course-specific definitions.
- **Platform-level guardrails** (Focus, Manipulation) were enabled on top of
  prompt-level instructions, rather than relying on the prompt alone.
- **Conversation timing tuned for a study-companion use case.** Default
  "take turn after silence" settings assume fast customer-support-style
  turnaround; this was loosened to give students room to think mid-pause
  without the agent interjecting prematurely.
- **Evaluation-driven, not demo-driven.** Automated grounding/honesty tests
  and live adversarial voice tests were run before considering Phase 1 done
  — see `evals/test-cases.md`.

## What's Explicitly Not in Phase 1

- No dynamic/live schedule data — the knowledge base is a static document,
  so the agent correctly declines to give exact session times rather than
  inventing them. Solving this dynamically is the goal of Phase 2.
- No proactive reminders (Discord/SMS) — Phase 1 is pull-only (student asks,
  agent answers), not push (agent reaching out unprompted).

See `phase-2/roadmap.md` for the planned architecture that addresses these.
