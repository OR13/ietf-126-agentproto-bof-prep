# agentproto: layers of scope

A companion to the draft charter for **Agent Communication Protocols
(`agentproto`)**, a proposed IETF working group in the Applications and
Real-Time (ART) area. Read this first, then read the charter — the charter is
the text that binds.

This is an unofficial explainer. It is not a chair position and not a consensus
statement.

## Problem statement

Two agents in different trust domains cannot hold a realtime conversation over
any standard protocol. Each deployment that needs one builds its own stack, so
integration cost grows with the number of pairs rather than the number of
participants.

The gap is specific. A single agent conversation carries flows with
incompatible latency requirements at the same time: voice and video that must
arrive continuously, chat that tolerates hundreds of milliseconds, and tool
inputs and outputs that are often large and can wait. Those flows stay coupled,
because a control message can invalidate work already in flight. An agent
booking travel is told "cancel the hotel, keep the flight," and the cancellation
has to overtake a bulk transfer already underway, across parties and across
hops.

No existing protocol covers that combination. HTTP is stateless and carries no
interaction that survives a turn. WebSocket offers no multiplexing, no priority,
and no partial teardown. SIP and WebRTC establish sessions but manage context
mostly at initiation, where here the context has to persist and travel with a
participant across devices and time. MoQ is the closest fit and was not designed
for this traffic.

Within one operator's network these pieces get assembled privately, and they
are, repeatedly. The problem surfaces at the boundary. Once a conversation spans
two organizations, every assembly decision has to be agreed in advance, and
today it is agreed bilaterally or not at all — which is the cost that scales
badly.

Success is checkable: two implementations built independently from these
documents, run by different organizations, hold a multimodal realtime
conversation — including an interruption that crosses the trust boundary —
with no prior bilateral arrangement.

## Scoping

The working group addresses this in layers, and an implementer must be able to
take one deliverable and benefit from it without taking the rest. Someone who
needs only a shared vocabulary should get value from the first layer alone.
Someone who has already committed to a transport should be able to implement the
substrate over it without waiting for the working group's own binding. A
deliverable usable only as part of the full set has failed this test.

Two areas are out of scope.

**Security** — identity, authentication, authorization, credentialing — is
consumed here and defined elsewhere. Agent identity belongs in WIMSE, delegated
authorization in OAuth, automated-client authentication in webbotauth. This
group states the security properties its deliverables depend on and raises gaps
with the groups that own the mechanisms.

**Discovery** is out of scope. How one party finds another, and how capabilities
are advertised and resolved, is separate work. These deliverables assume the
participants have already found each other.

Excluding both is a bet that the group moves faster consuming that work than
relitigating it. A cross-trust-domain protocol still has to satisfy the security
properties; it just does not specify them.

## The layers, as deliverables

### 1. Semantics (Informational)

Describes how agents interact with each other in realtime, and provides a
vocabulary for the challenges and opportunities that arise as communication
scales and changes to support human and agent collaboration.

This layer names things: participant, turn, interruption, context, modality,
trust boundary, handoff. It specifies no bits. Two implementers who have never
spoken should be able to use it to describe the same failure and recognize it as
the same failure. The interaction patterns documented here are also the evidence
that the substrate is needed, and the yardstick it gets measured against.

Usable alone by anyone writing about agent communication, or evaluating an
existing protocol against the problem statement.

### 2. Substrate (Proposed Standard)

Specifies how the semantics fit together to solve the problem, without binding
to a specific transport.

This is the protocol: establishing a realtime interaction, carrying context
across a trust boundary, negotiating and multiplexing modalities, propagating
interruption and cancellation, and handling a participant that joins, leaves, or
is replaced. Transport independence follows from the problem statement — this
interoperability is needed in more than one deployment context, and a substrate
welded to a single transport serves only one of them.

Usable alone by anyone willing to specify their own binding over a transport
they have already chosen.

### 3. Substrate binding (Proposed Standard)

The working group shall determine how to evaluate candidate transports, select
one, and specify a concrete binding that addresses the problem statement when
deployed.

Two pieces in sequence: the evaluation criteria, then the binding. Criteria come
first and in public, because the choice among modern IETF transports is
contested and a selection without stated criteria gets relitigated indefinitely.
The binding is what turns the substrate into something two vendors can deploy
and interoperate on.

This layer depends on layer two by construction — the one place the layering
buys no independence.

## Why this framing

The WG-forming BOF at IETF 126 supported the work and rejected the scope as
drawn. On a sense of the room — a hum, not a binding vote — a working group
should be formed (154 yes / 51 no), and the initial scope was not correct (38
yes / 124 no / 40 no opinion). The layering above responds to that with a
narrower problem statement, separable deliverables, and two explicit exclusions
where the earlier draft invited overlap with groups that already own the work.

## Links

- Draft charter: <https://github.com/ietf-artarea/charters/blob/main/agentproto/charter.md>
  — revision happens in that repository; pull requests welcome.
- Mailing list: `agentproto@ietf.org` —
  [archive](https://mailarchive.ietf.org/arch/browse/agentproto) ·
  [subscribe](https://www.ietf.org/mailman/listinfo/agentproto)
- Datatracker group: <https://datatracker.ietf.org/group/agentproto/about/>
- BOF request: <https://datatracker.ietf.org/doc/bofreq-krishnan-agent-communication-protocols/>
