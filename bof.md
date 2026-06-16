# agentproto BOF — dossier (public)

**Agent Communication Protocols** · mnemonic `agentproto` ·
[datatracker](https://datatracker.ietf.org/group/agentproto/about/) ·
WG-forming BOF (not yet chartered) · ART area · AD Charles Eckel ·
chairs Leslie Daigle & Orie Steele · 2h · ~200 expected.
Source: `bofreq-krishnan-agent-communication-protocols-02` and the public draft
charter at <https://github.com/jdrosen/aiproto-wg>.

## Problem statement

AI agents — autonomous software using LLMs to accomplish tasks for a user,
often via chat or voice — increasingly interact with Internet resources: tools
(APIs) and other agents. Cross-vendor interoperability matters so tools and
agents from different vendors can interoperate. The BOF/WG aims to standardize
the protocol building blocks that enable this.

### Considerations called out as unique to agent protocols

- **Hallucination** (incl. of tool use) → risk when agents act erroneously;
  needs user-approval / confirmation mechanisms.
- **Long-lived, context-heavy** interactions → reliability + data-transport
  considerations.
- **Privacy** — exchanges can carry PII and payment data; must be protected.
- **Voice + low latency** — fast barge-in/interruption, agent↔agent too.

## Proposed deliverables (from the draft charter — 4, standards-track)

1. **AI Agent session protocol** — long-lived, scalable, failure-surviving
   bidirectional sessions carrying real-time (voice), semi-real-time (chat), and
   non-real-time (tool I/O) data concurrently. Foundational layer atop modern
   IETF transports (**WebTransport, MOQ**); usable by non-IETF protocols (MCP, A2A).
2. **Agent-to-Agent protocol** — one agent invoking another; user-message
   exchange (voice/video/image/chat) + lifecycle management. Built on the
   session protocol; framed as a next-gen version of the Linux Foundation A2A.
3. **Human-confirmation protocol** — user confirms agent-invoked operations at
   the orchestration layer (hallucination defense); spans single/multi-agent;
   **cryptographic attestation for non-repudiation**.
4. **OAuth limited-scope tokens** — bound to the specific operations an agent is
   permitted to perform. *(Charter notes this might be better in the OAuth WG.)*

The charter states aiproto expects to **work closely with the `webbotauth` WG**
for agent authentication.

> The original BOF request listed 2 deliverables (session protocol + a generic
> framework); the public charter has since expanded to the 4 above.

## Acknowledged prior art

Model Context Protocol (MCP), Agent2Agent (A2A), AGNTCY framework.

## Proponents (public)

Cullen Jennings · Jonathan Rosenberg · Suresh Krishnan · Dapeng Liu ·
Zaheduzzaman Sarker · Lionel Morand · Kehan Yao · Arashmid Akhavain ·
Hesham Moussa. Responsible AD: Charles Eckel.

## Analysis (notes)

- WG-forming: debate will be **scope/charterability**, not "is this real."
- Breadth is large (4 standards-track items) — expect pushback on whether it's
  one WG or several, and on overlap with sibling agent efforts at 126.
- **Transport-forward** framing (WebTransport/MOQ) is the IETF-native
  differentiator vs MCP/A2A's HTTP/JSON-RPC heritage — likely a contention point.
- Deliverable (4) explicitly flagged as possibly belonging in OAuth; (3) overlaps
  delegation/traceability work elsewhere.
