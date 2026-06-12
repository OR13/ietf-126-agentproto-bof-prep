# agentproto BOF — Chair Slides (DRAFT)

> **DRAFT / unofficial prep.** Working draft of chair slides for the
> **agentproto** (Agent Communication Protocols) **WG-forming BOF** at
> **IETF 126, Vienna**. Built from public sources: the IETF 125 CATALIST
> "AI Protocols" deck, `bofreq-krishnan-agent-communication-protocols-02`,
> and the draft charter at <https://github.com/jdrosen/aiproto-wg>.
> One slide per `---`. Placeholders marked `‹…›`.

---

## Agent Communication Protocols (`agentproto`)

WG-forming BOF · IETF 126, Vienna · ‹day / time / room TBD›

Chairs: ‹TBD› · ‹TBD›
Responsible AD: Charles Eckel (ART)
Mailing list: agent2agent@ietf.org · Zulip: `agentproto`

---

## Note Well

Standard IETF Note Well. By participating you agree to the IETF policies
on IPR disclosure (BCP 79), conduct (BCP 54), and contributions
(BCP 78/79). Be aware: this session is recorded and minuted.

<https://www.ietf.org/about/note-well/>

---

## Meeting administrivia

- Minutes (CodiMD/Notes): ‹link TBD›
- Zulip stream: `agentproto`
- Agenda on datatracker: ‹link TBD›
- Please sign the bluesheet
- Note-takers: ‹TBD› · Jabber/Zulip scribe: ‹TBD›
- Mic etiquette: state name + affiliation

---

## Agenda  (2 hours)

1. Note Well, agenda bash — chairs (5 min)
2. Background & how we got here — ‹presenter› (10 min)
3. Problem statement & motivation — ‹presenter› (15 min)
4. Proposed scope & deliverables — ‹presenter› (30 min)
5. Relationship to other work — ‹presenter› (15 min)
6. Draft charter walkthrough — chairs (15 min)
7. Discussion & consensus questions — chairs (30 min)
8. Wrap-up & next steps — chairs (5 min)

*(Agenda bash: comments?)*

---

## What is a WG-forming BOF?

The goal today is **not** to design protocols. It is to decide whether to
**charter a working group**. By the end we want to answer:

- Is there a real, well-understood problem?
- Is the IETF the right place to solve it?
- Is the proposed scope the right scope — and is it charterable?
- Are there enough people willing to do the work (edit, review, implement)?

---

## How we got here

- AI Protocols **side meetings**: IETF 123 (Madrid), IETF 124 (Montreal),
  IETF 125 (Shenzhen — under CATALIST).
- Ongoing discussion on **agent2agent@ietf.org**.
- A growing set of Internet-Drafts (see "Relevant drafts").
- Strawman charter drafted in the open: `jdrosen/aiproto-wg`.
- IETF 125 CATALIST conclusion: *"expecting to be ready with a
  working-group-forming BoF for IETF 126."* → that's this session.

---

## Problem statement

AI agents — autonomous software using LLMs to accomplish tasks for users,
often over chat or voice — increasingly interact with Internet resources:
**tools (APIs)** and **other agents**.

Today these interactions are **per-vendor and non-interoperable**. To let
tools and agents from *different* vendors work together, we need open,
standardized protocol building blocks. That interoperability is the job.

---

## Why these problems are different

Considerations relatively unique to AI-agent protocols:

- **Hallucination** (incl. of tool use) → risk when agents act wrongly →
  need user-approval / confirmation mechanisms.
- **Long-lived, context-heavy** sessions → reliability + transport.
- **Privacy** — exchanges carry PII / payment data → must be protected.
- **Voice + very low latency** — fast barge-in / interruption, agent↔agent too.

---

## Why IETF / why now

- The transport, identity, and authorization building blocks are **IETF's
  home turf**: OAuth, MoQ, WebTransport, QUIC, DNS.
- Relevant areas: **ART, SEC, WIT** (and some INT). Some pieces may land in
  **existing WGs** (e.g. OAuth) once requirements are fleshed out.
- The ecosystem (MCP, A2A, AGNTCY) is converging *now* — open
  interoperability work is timely before silos harden.

---

## Proposed scope — deliverables

From the draft charter (standards-track):

1. **AI Agent session protocol** — long-lived, scalable, failure-surviving
   bidirectional sessions carrying real-time (voice), semi-real-time (chat),
   and non-real-time (tool I/O) data concurrently; over WebTransport / MoQ;
   usable by non-IETF protocols (MCP, A2A). *Foundational layer.*
2. **Agent-to-Agent protocol** — one agent invokes another; user-message
   exchange + lifecycle; next-gen of the Linux Foundation A2A; built on (1).
3. **Human-confirmation protocol** — confirm agent-invoked operations at the
   orchestration layer; **cryptographic attestation / non-repudiation**.
4. **Constrained access tokens** — OAuth tokens with extremely limited,
   operation-bound scopes. *(May be better done in the OAuth WG.)*

---

## Out of scope / non-goals  (DRAFT — for discussion)

- Defining the LLMs / model behavior themselves.
- Re-specifying MCP, A2A, or AGNTCY (we interoperate with / build on them).
- Application-specific agent business logic.
- ‹others — to be agreed by the room›

---

## Relationship to other work

- **MCP / A2A (Linux Foundation) / AGNTCY** — prior art; we layer on / build
  next-gen, not replace.
- **webbotauth WG** — charter dependency for agent authentication.
- **OAuth WG** — deliverable (4) may belong there.
- **MoQ / WebTransport / QUIC / DNS** — reused transport & discovery building blocks.
- **Sibling IETF 126 agent BOFs** (discovery, delegation/traceability,
  multi-agent security) — coordinate scope; avoid overlap.

---

## Draft charter

Strawman charter developed in the open — please read & comment on the list:

- Repo: <https://github.com/jdrosen/aiproto-wg>
- Naming note: datatracker mnemonic `agentproto`; charter proposes WG name
  `aiproto` ("AI Agent Protocols WG") — to be settled.

---

## Questions for the room

We'll take a hum / show of support on each:

1. **Is the problem clear and worth solving?**
2. **Is the IETF the right venue?**
3. **Is the proposed scope (4 deliverables) the right cut for one WG?**
   - Too broad? Should any deliverable start elsewhere (e.g. OAuth)?
4. **Will you help?** contribute · review · edit a draft · implement.

---

## Next steps

- Take the consensus calls back to the ‹AD / IESG›.
- Refine charter on agent2agent@ietf.org per today's feedback.
- ‹If chartered› identify document editors & milestones.
- Continue coordination with sibling agent efforts.

Thank you — discussion on **agent2agent@ietf.org**.

---

## Backup — relevant Internet-Drafts

- `draft-rosenberg-aiproto-framework` — framework / use cases / requirements
- `draft-jennings-ai-mcp-over-moq` — MCP over MoQ
- `draft-rosenberg-aiproto-a2t` — agent-to-tool
- `draft-nandakumar-agent-sd-jwt` — agent SD-JWT identity
- `draft-nandakumar-ai-agent-moq-transport` — agent MoQ transport
- `draft-liu-agent-operation-authorization` — operation authorization
- `draft-liu-agent-protocol-over-moq` — agent protocol over MoQ
- `draft-diaconu-agents-authz-info-sharing` — authz info sharing
- `draft-yao-catalist-problem-space-analysis` — problem-space analysis
