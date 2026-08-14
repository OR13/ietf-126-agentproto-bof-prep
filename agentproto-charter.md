# Realtime Multimedia Agent Communications (agentproto)

Proposed charter revision for the `agentproto` working group, IETF Applications
and Real-Time (ART) area. For discussion on `agentproto@ietf.org`. Not adopted
text and not a chair position.

## Problem statement

Two agents in different trust domains have no standard protocol to carry a
realtime multimedia conversation. Every cross-organization deployment builds a
custom stack, so integration cost scales as O(N²) bilateral arrangements instead
of O(N) implementations.

A single conversation carries flows with incompatible timing:

- **Streaming** — continuous voice and video.
- **Messaging** — turn-based chat, hundred-millisecond tolerance.
- **Bulk** — large tool inputs, structured results, asynchronous execution
  output.

These cannot be split across separate connections, because control state has to
invalidate work in flight. Told "cancel the hotel, keep the flight," an agent's
cancellation must overtake an in-flight bulk payload, across hops and across
organizational boundaries.

A2A is the closest existing answer and is shaped for a different problem. Its
three bindings — JSON-RPC, gRPC, HTTP+JSON — are all HTTP-based, and a custom
binding has to be functionally equivalent to them, so the interaction model
survives any change of transport. That model is asymmetric by design: the client
sends, the server streams updates back, and the protocol does not require
bidirectional messaging during task execution. Barge-in needs the opposite, an
agent that keeps listening while it speaks. Cancellation acts on a task and says
nothing about preempting an artifact already streaming. Audio and video travel
by file reference, as artifacts rather than flows. `contextId` is an opaque key
grouping tasks within one agent's own view, not a structure that crosses a trust
boundary. And the interaction is two-party.

A2A's own tracker carries the request. Issue #997 asks for WebRTC and
WebTransport as first-class transports for voice assistants and streaming audio,
observing that it is "unclear how to implement these scenarios without breaking
A2A compliance." This work does not replace A2A; it addresses a gap A2A has
already named.

The working group's output succeeds when two stacks, built independently from
its documents by different organizations, establish a multimedia realtime
session — including a mid-stream interruption across a trust boundary — with no
prior bilateral arrangement.

## Scope

The working group works on realtime multimedia communication between agents, and
between humans and agents, across trust domains. It defines the semantics of
those interactions, a transport-agnostic substrate that realizes them, and one
concrete transport binding.

The three deliverables are deliberately separable. An implementer should be able
to adopt one without the others.

## Out of scope

**Agent to tool.** MCP defines how an agent invokes a tool and receives a
result; this work does not redefine it. Tool payloads ride the substrate as one
of its flow classes, but the calling convention that produces them is MCP's.

**Agent to inference.** How an agent reaches the model driving it runs over
proprietary inference APIs. That exchange is request/response with a streamed
response, which those APIs already serve, and it is not the mixed-media,
multi-party case this work exists for.

**Security.** Identity, authentication, authorization: consumed, not invented.
Agent identity in WIMSE, delegated authorization in OAuth, automated-client
authentication in webbotauth. A2A's most-reported weaknesses sit here — agent
card spoofing, credential handling left to implementers — and a realtime
substrate does not fix them. The working group states the security properties it
depends on and raises gaps with the groups that own the mechanisms.

**Discovery.** How endpoints locate each other and negotiate capabilities
happens out of band. A2A's discovery surface is spoofable and its registries
centralize; both are real problems and neither is this group's. These
deliverables assume the participants have already found each other.

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

## Milestones

Dates to be set on adoption.

1. Adopt the semantics draft.
2. Adopt the substrate draft.
3. Publish transport evaluation criteria — the properties a candidate transport
   has to provide, agreed before any candidate is named.
4. Select the transport — one chosen against those criteria, with the reasoning
   in the record.
5. Submit the semantics draft to the IESG (Informational).
6. Submit the substrate draft to the IESG (Proposed Standard).
7. Submit the transport binding to the IESG (Proposed Standard).

## Coordination

**MCP and A2A**, at the Linux Foundation, are the application protocols above
this work. The working group coordinates with both and redefines neither.

**WIMSE** on agent identity, **OAuth** on delegated authorization, and
**webbotauth** on automated-client authentication own the security mechanisms
this work consumes.

**MoQ, WebTransport, QUIC, TSVWG, and AVTCORE** own the transports the binding
will be evaluated against and selected from.

Where a deliverable needs a change to a protocol owned by another working group,
the working group raises it there rather than specifying it here.

## References

- Draft charter in revision:
  <https://github.com/ietf-artarea/charters/blob/main/agentproto/charter.md>
- Mailing list: `agentproto@ietf.org` —
  [archive](https://mailarchive.ietf.org/arch/browse/agentproto) ·
  [subscribe](https://www.ietf.org/mailman/listinfo/agentproto)
- Datatracker group: <https://datatracker.ietf.org/group/agentproto/about/>
- BOF request:
  <https://datatracker.ietf.org/doc/bofreq-krishnan-agent-communication-protocols/>
