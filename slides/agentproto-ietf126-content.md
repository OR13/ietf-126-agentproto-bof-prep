# agentproto BOF — content slides (IETF 126)

> **How to use:** these are the **content slides to add to the official chair
> template** (`official/ietf-chair-slide-template.pptx`), placed **after** its
> Note Well slide. The Note Well and policy front matter come from the official
> template and are **not** reproduced or edited here (per the IESG rule — do not
> add or alter any policy slides). One slide per `---`. Placeholders: `‹…›`.
>
> Identity: **agentproto — Agent Communication Protocols · WG-forming BOF ·
> IETF 126, Vienna.** This is *not* a CATALIST session; use agentproto title and
> footers throughout.

---

## [Title]  Agent Communication Protocols (`agentproto`)

WG-forming BOF · IETF 126, Vienna · Thu 23 Jul, 09:00–11:00 (CEST) · Grand Park Hall 3

Co-chairs: Leslie Daigle · Orie Steele
Responsible AD: Charles Eckel (ART)
List: agent2agent@ietf.org · Zulip: `agentproto`

*(The official template's Note Well slide immediately follows the title;
leave it exactly as shipped.)*

---

## [Administrivia]

- Agenda (datatracker): ‹link›
- Notes / minutes: ‹CodiMD link›
- Chat: Zulip stream `agentproto`
- Please **sign the bluesheet**
- Note-takers: ‹TBD› · Zulip scribe: ‹TBD›
- At the mic: state **name + affiliation**
- Session is recorded & minuted

---

## [Agenda]  (2 hours)

1. Administrivia & agenda bash — chairs (5)
2. Background & motivation — ‹presenter› (10)
3. Problem statement — ‹presenter› (15)
4. Proposed scope & deliverables — ‹presenter› (30)
5. Relationship to other work — ‹presenter› (15)
6. Draft charter walkthrough — chairs (15)
7. Discussion & consensus questions — chairs (30)
8. Wrap-up & next steps — chairs (5)

*(Agenda bash — comments?)*

---

## [BOF goals]  This is a WG-forming BOF

Today we decide whether to **charter a working group** — not to design
protocols. By the end we want consensus on:

- Is there a real, well-understood problem?
- Is the IETF the right venue?
- Is the proposed scope the right cut — and charterable?
- Are enough people committed to do the work (edit · review · implement)?

---

## [Background]  How we got here

- AI-agent interoperability discussed in IETF **side meetings** (IETF 123, 124)
  and coordinated via **CATALIST** (IETF 125).
- Ongoing discussion on **agent2agent@ietf.org**.
- Strawman charter: <https://github.com/jdrosen/aiproto-wg>.
- This session is the **WG-forming BOF** that work was building toward.

*(Mention CATALIST only as prior coordination — this BOF stands on its own.)*

---

## [Problem]  Problem statement

AI agents — autonomous software using LLMs to do tasks for users, often over
chat or voice — increasingly interact with Internet resources: **tools (APIs)**
and **other agents**.

These interactions are today largely **per-vendor and non-interoperable**. The
BOF request proposes standardizing open, vendor-neutral building blocks so that
tools and agents from *different* vendors can interoperate.

---

## [Considerations]  Called out in the BOF request as unique to agent protocols

- **Hallucination** (incl. of tool use) → risk when agents act wrongly;
  motivates user-approval / confirmation mechanisms.
- **Long-lived, context-heavy** sessions → reliability + transport.
- **Privacy** — exchanges carry PII / payment data.
- **Voice + very low latency** — fast barge-in / interruption, agent↔agent too.

---

## [Why IETF / why now]  The request's case — consensus question 2

The BOF request points to:

- Transport, identity & authorization building blocks already in IETF:
  **OAuth, MoQ, WebTransport, QUIC, DNS.**
- Relevant areas: **ART, SEC, WIT** (some INT); some pieces may land in
  **existing WGs** (e.g. OAuth) once requirements are clear.
- Convergence across **MCP, A2A, AGNTCY** as motivation for timing.

*Whether the IETF is the right venue is consensus question 2.*

---

## [Scope]  Proposed deliverables (standards-track)

*As proposed in the BOF request. Whether this is the right cut is consensus
question 3.*

1. **AI Agent session protocol** — long-lived, scalable, failure-surviving
   bidirectional sessions carrying real-time (voice), semi-real-time (chat), and
   non-real-time (tool I/O) data concurrently; over WebTransport / MoQ; usable
   by non-IETF protocols (MCP, A2A). *Foundational layer.*
2. **Agent-to-Agent protocol** — one agent invokes another; user-message
   exchange + lifecycle; built on (1).
3. **Human-confirmation protocol** — confirm agent-invoked operations at the
   orchestration layer; **cryptographic attestation / non-repudiation**.
4. **Constrained access tokens** — OAuth tokens with operation-bound, minimal
   scopes. *(May be better done in the OAuth WG.)*

---

## [Out of scope]  Non-goals (draft — for discussion)

- Defining the LLMs / model behavior.
- Re-specifying MCP, A2A, or AGNTCY (we interoperate with / build on them).
- Application-specific agent business logic.
- ‹others — to be agreed by the room›

---

## [Relationships]  Relationship to other work

- **MCP / A2A (Linux Foundation) / AGNTCY** — related existing work.
- **webbotauth WG** — dependency for agent authentication.
- **OAuth WG** — deliverable (4) may belong there.
- **MoQ / WebTransport / QUIC / DNS** — reused transport & discovery blocks.
- **Sibling IETF 126 agent BOFs** (discovery, delegation/traceability,
  multi-agent security) — coordinate scope; avoid overlap.

---

## [Charter]  Draft charter

Strawman charter:

- <https://github.com/jdrosen/aiproto-wg>

---

## [Consensus]  Questions for the room

We'll take a hum / show of hands on each:

1. **Is the problem clear and worth solving?**
2. **Is the IETF the right venue?**
3. **Is the proposed scope (4 deliverables) the right cut for one WG?**
   (Too broad? Should any item start elsewhere, e.g. OAuth?)
4. **Will you help?** contribute · review · edit a draft · implement.

---

## [Next steps]

- Take the consensus calls to the AD / IESG.
- Refine charter on agent2agent@ietf.org per today's feedback.
- ‹If chartered› identify document editors & milestones.
- Continue coordination with sibling agent efforts.

Thank you — discussion on **agent2agent@ietf.org**.

---

## [Backup]  Relevant Internet-Drafts

- `draft-rosenberg-aiproto-framework` — framework / use cases / requirements
- `draft-jennings-ai-mcp-over-moq` — MCP over MoQ
- `draft-rosenberg-aiproto-a2t` — agent-to-tool
- `draft-nandakumar-agent-sd-jwt` — agent SD-JWT identity
- `draft-nandakumar-ai-agent-moq-transport` — agent MoQ transport
- `draft-liu-agent-operation-authorization` — operation authorization
- `draft-liu-agent-protocol-over-moq` — agent protocol over MoQ
- `draft-diaconu-agents-authz-info-sharing` — authz info sharing
- `draft-yao-catalist-problem-space-analysis` — problem-space analysis
