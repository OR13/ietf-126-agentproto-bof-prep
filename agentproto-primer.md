# agentproto: layers of scope

Companion to the draft charter for **Agent Communication Protocols
(`agentproto`)**, a proposed working group in the IETF Applications and
Real-Time (ART) area. Read this first, then read the
[draft charter](https://github.com/ietf-artarea/charters/blob/main/agentproto/charter.md)
— the charter is the text that binds. Unofficial: not a chair position, not a
consensus statement.

## Problem statement

Two agents in different trust domains have no standard protocol to carry a
realtime conversation. Every cross-organization deployment builds a custom
stack, so integration cost scales as O(N²) bilateral arrangements instead of
O(N) implementations.

One session has to multiplex flows with incompatible timing:

- **Streaming** — continuous voice and video.
- **Messaging** — turn-based chat, hundred-millisecond tolerance.
- **Bulk** — large tool inputs, structured results, asynchronous execution
  output.

These cannot be split across separate connections, because control state has to
invalidate work in flight. Told "cancel the hotel, keep the flight," an agent's
cancellation must overtake an in-flight bulk payload, across hops, across
organizational boundaries.

Existing protocols each miss part of it:

- **HTTP** — stateless; no multi-turn session context.
- **WebSocket** — no multiplexing, prioritization, or partial teardown.
- **SIP / WebRTC** — strong session establishment; not built for persistent,
  portable context that evolves over long durations and moves across devices.
- **MoQ** — nearest fit for the streaming, not designed for control-plane state.

Inside one platform, engineers assemble these with proprietary glue. Across
trust domains, every choice has to be negotiated bilaterally first.

Success: two stacks built independently from these documents, by different
organizations, establish a multimodal realtime session — including a mid-stream
interruption across a trust boundary — with no prior bilateral arrangement.

## Scoping

Three layers, deliberately separable. An implementer should be able to adopt one
without the others.

Out of scope:

**Security.** Identity, authentication, authorization: consumed, not invented.
Agent identity in WIMSE, delegated authorization in OAuth, automated-client
authentication in webbotauth. This group states the security properties it
depends on and raises gaps with the groups that own the mechanisms.

**Discovery.** How endpoints locate each other and negotiate capabilities
happens out of band. These deliverables assume the participants have already
found each other.

## Deliverables

### 1. Semantics (Informational)

Shared taxonomy for realtime agent interaction; no wire format. Participant,
turn, interruption, context, modality, trust boundary, handoff.

Alone, it gives two implementers who have never spoken a common way to describe
the same failure, and a yardstick for measuring an existing stack against the
problem statement.

### 2. Substrate (Proposed Standard)

The protocol operations, independent of transport: session lifecycle, context
propagation across a trust boundary, modality multiplexing, mid-flight
cancellation, and participant join, leave, and handoff.

Transport independence follows from the problem statement — this interop is
needed in more than one deployment context, and a substrate welded to one
transport serves one of them.

Alone, it lets a team implement standard semantics over a transport they have
already chosen.

### 3. Transport binding (Proposed Standard)

Two documents in order: evaluation criteria for candidate transports, then the
binding to the selected one. Criteria first and in public, because the choice
among modern IETF transports is contested and a selection without stated
criteria gets relitigated indefinitely.

This is the layer vendors need for off-the-shelf interop, and the one layer that
depends on another — layer two, by construction.

## Why this framing

The WG-forming BOF at IETF 126 backed the work and rejected the scope. Sense of
the room, not a binding vote: form a working group, 154 yes / 51 no; initial
scope correct, 38 yes / 124 no / 40 no opinion. This framing narrows the
problem, separates the deliverables, and hands security and discovery to the
groups that already own them.

## Links

- Draft charter: <https://github.com/ietf-artarea/charters/blob/main/agentproto/charter.md>
  — revision happens there; pull requests welcome.
- Mailing list: `agentproto@ietf.org` —
  [archive](https://mailarchive.ietf.org/arch/browse/agentproto) ·
  [subscribe](https://www.ietf.org/mailman/listinfo/agentproto)
- Datatracker group: <https://datatracker.ietf.org/group/agentproto/about/>
- BOF request: <https://datatracker.ietf.org/doc/bofreq-krishnan-agent-communication-protocols/>
