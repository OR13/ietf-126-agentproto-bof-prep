# agentproto: layers of scope

A companion to the draft charter for **Agent Communication Protocols
(`agentproto`)**, a proposed IETF working group in the Applications and
Real-Time (ART) area. Read this first, then read the charter — the charter is
the text that binds.

This is an unofficial explainer. It is not a chair position and not a consensus
statement.

## Problem statement

There is a need to enable interoperable cross-trust-domain realtime media
communications, to deliver cost-effective streaming-media-based agentic
experiences at Internet scale.

Every clause is load-bearing. **Realtime media** is the case that existing
request/response plumbing does not serve: voice and video moving between
participants while text and tool results move alongside them, with interruption
and cancellation that must preempt work already in flight. **Cross trust domain**
is what makes it an interoperability problem rather than a framework problem —
inside one vendor's deployment this is already solved, badly and privately, N
times over. **Cost-effective at Internet scale** is the constraint that rules out
answers that work in a demo and collapse at fanout. And **agentic experiences**
is the demand driver, not a new physics: agents are why this traffic pattern
suddenly matters, not why it is hard.

## Scoping

The working group addresses this problem **in layers**, and the layering is a
deliberate adoption strategy rather than a taxonomy. An implementer must be able
to take one deliverable and benefit from it without taking the others. Someone
who only needs a shared vocabulary should get value from the first layer alone.
Someone who has already committed to a transport should be able to implement the
substrate over it without waiting for the working group's own binding. Partial
adoption is a design goal, and any deliverable that can only be used as part of
the full set has failed this test.

Two things are explicitly **out of scope**.

**Security** — identity, authentication, authorization, and credentialing — is
consumed, not defined. Agent identity work belongs in WIMSE, delegated
authorization in OAuth, automated-client authentication in webbotauth. The
working group will state what security properties its deliverables require and
raise gaps with the groups that own those mechanisms. It will not specify them
here.

**Discovery** is out of scope. How a party finds another party, and how
capabilities are advertised and resolved, is a separate problem with separate
existing work. The deliverables assume the participants have already found each
other.

Both exclusions are scope discipline, not dismissals. A cross-trust-domain
protocol that ignored security would be useless; the position is that this group
consumes those mechanisms rather than reinventing them.

## The layers, as deliverables

### 1. Semantics (Informational)

Describes how agents interact with each other in realtime, and provides a
vocabulary for the challenges and opportunities that arise as communication
scales and changes to support human and agent collaboration.

This layer names things: participant, turn, interruption, context, modality,
trust boundary, handoff. It does not specify bits. Its value is that two
implementers who have never spoken can describe the same failure to each other
and agree they are describing the same failure. It is also the layer that makes
the case — the interaction patterns documented here are the evidence that the
substrate is needed and the yardstick the substrate is measured against.

Usable alone, by anyone writing about agent communication or evaluating an
existing protocol against the problem statement.

### 2. Substrate (Proposed Standard)

Specifies how the semantics fit together to solve the problem, without binding
to a specific transport.

This is the protocol: how a realtime interaction is established, how context is
carried and propagated across a trust boundary, how modalities are negotiated
and multiplexed, how interruption and cancellation propagate, how a participant
joins, leaves, or is replaced. Transport independence is not architectural
tidiness — it is the requirement that this interoperability is needed in more
than one deployment context, and a substrate welded to one transport can only
serve one of them.

Usable alone, by anyone willing to specify their own binding over a transport
they have already chosen.

### 3. Substrate binding (Proposed Standard)

The working group shall determine how to evaluate candidate transports, select
one, and specify a concrete binding that, when deployed, addresses the problem
statement.

Two deliverables in sequence: the evaluation criteria, then the binding. The
criteria come first and in public, because the choice among modern IETF
transports is contested and a selection without stated criteria will be
relitigated indefinitely. The binding is what turns the substrate from a
specification into something two vendors can deploy and interoperate on.

Usable alone only in the sense that it is the fastest path to running code — it
depends on layer two by construction, which is the one place the layering does
not buy independence.

## Why this framing

The WG-forming BOF at IETF 126 supported the work and rejected the scope as
drawn. On a sense of the room — a hum, not a binding vote — a working group
should be formed (154 yes / 51 no), and the initial scope was not correct (38
yes / 124 no / 40 no opinion). The layering above is a response to that: a
narrower problem statement, deliverables that are separable, and two explicit
exclusions where the previous draft invited overlap with groups that already own
the work.

## Links

- Draft charter: <https://github.com/ietf-artarea/charters/blob/main/agentproto/charter.md>
  — revision happens in that repository; pull requests welcome.
- Mailing list: `agentproto@ietf.org` —
  [archive](https://mailarchive.ietf.org/arch/browse/agentproto) ·
  [subscribe](https://www.ietf.org/mailman/listinfo/agentproto)
- Datatracker group: <https://datatracker.ietf.org/group/agentproto/about/>
- BOF request: <https://datatracker.ietf.org/doc/bofreq-krishnan-agent-communication-protocols/>
