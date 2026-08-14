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

**1. Semantics (Informational).** Describes what is hard about realtime
communication that carries human and agent content in one conversation —
barge-in, attribution of synthetic content, turn-taking between parties bound by
different clocks — and gives that problem space a vocabulary.

**2. Substrate (Proposed Standard).** Defines the interaction patterns that make
those semantics operational — session lifecycle, context propagation across a
trust boundary, modality multiplexing, mid-flight cancellation, and participant
join, leave, and handoff — without reference to any particular transport.

**3. Transport binding (Proposed Standard).** Maps the substrate onto one
selected IETF transport, so two vendors implementing it interoperate off the
shelf.

The semantics document states the problem in terms that transfer to any stack,
the substrate answers it, and the binding makes that answer deployable on one
wire. Only the last of the three needs the one before it. A team can take the
semantics to audit a system it already runs, or implement the substrate over a
transport it has already committed to, and stop there.

### Milestones

Both fall under deliverable 3, and the order between them is the point.

1. **Transport evaluation criteria.** The properties a candidate transport has
   to provide, agreed before any candidate is named.
2. **Transport selection.** One transport chosen against those criteria, with
   the reasoning in the record.

## Links

- Draft charter: <https://github.com/ietf-artarea/charters/blob/main/agentproto/charter.md>
  — revision happens there; pull requests welcome.
- Mailing list: `agentproto@ietf.org` —
  [archive](https://mailarchive.ietf.org/arch/browse/agentproto) ·
  [subscribe](https://www.ietf.org/mailman/listinfo/agentproto)
- Datatracker group: <https://datatracker.ietf.org/group/agentproto/about/>
- BOF request: <https://datatracker.ietf.org/doc/bofreq-krishnan-agent-communication-protocols/>
