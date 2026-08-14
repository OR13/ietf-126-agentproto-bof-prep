# agentproto: the three layers of scope

A companion to the draft charter for **Agent Communication Protocols
(`agentproto`)**, a proposed IETF working group in the Applications and
Real-Time (ART) area. Read this first, then read the charter — this explains the
shape of the scope, and the charter is the text that actually binds.

This is an unofficial explainer written to help people orient. It is not a chair
position, not a consensus statement, and not a substitute for anything on the
list.

- Draft charter: <https://github.com/ietf-artarea/charters/blob/main/agentproto/charter.md>
- Datatracker group: <https://datatracker.ietf.org/group/agentproto/about/>
- BOF request: <https://datatracker.ietf.org/doc/bofreq-krishnan-agent-communication-protocols/>
- Mailing list: `agentproto@ietf.org` —
  [archive](https://mailarchive.ietf.org/arch/browse/agentproto) ·
  [subscribe](https://www.ietf.org/mailman/listinfo/agentproto)

## Why a primer about scope specifically

At the WG-forming BOF at IETF 126 in Vienna, the room supported almost
everything except the scope. On a sense of the room — a hum, not a binding vote,
with roughly 315 people participating — the need for interoperability was clear
(155 yes / 30 no), the IETF was the right venue (158 / 30), and a working group
should be formed on this topic (154 / 51). Asked whether the initial scope from
the charter was correct, the room said no: **38 yes, 124 no, 40 no opinion.**
Deliverables split, 92 / 58 / 49.

That is an unusual result. It is not "this work doesn't belong here." It is "we
want this work, and the boundaries as drawn are wrong." Every argument since has
been an argument about where the lines go, which is why the charter is best read
as three distinct layers of scope rather than one block of text. They differ in
what they produce, in how contested they are, and — most importantly — in
whether they put anything new on the wire.

## The picture the charter is drawing

Before the three layers, fix the vertical position, because most of the
objections at the mic were really objections about position.

**Above** sit the application protocols people already use: MCP and A2A,
developed under the Linux Foundation, and whatever succeeds them. The charter
does not propose to replace, absorb, or re-plumb these. It proposes a substrate
they can sit on. Say this plainly and often, because "rip and replace" is the
fear in the room and it is the fear that most distorts the reading of the
charter.

**Below** sit modern IETF transports: QUIC, WebTransport, MoQ, WebRTC. The
charter consumes these. It does not design them, and any change one of them
needs goes to the group that owns it.

**Beside** sit identity, authorization, and discovery: OAuth for delegated
authorization, WIMSE for workload and agent identity, webbotauth for automated
clients, and the discovery and operational work in the INT and OPS areas. The
charter is explicit that extensions to OAuth happen in OAuth and extensions for
independent agent identity happen in WIMSE. agentproto composes their outputs;
it does not redefine them.

The working group's own scope is agent-to-agent and agent-to-tool communication,
plus the *protocol* mechanisms for human-to-agent communication — establishing
sessions, negotiating modalities, exchanging multimodal data. The design of the
user interface and the rendering of agent output is explicitly out. That
distinction is worth holding onto; "human-agent communication" reads as UX to
anyone skimming, and it isn't.

## Layer one: the wire

The **AI Agent Session Protocol** is the only deliverable that puts new bits on
the wire. It creates and maintains a session between agents, or between an agent
and a tool, carrying model context, tool-call results, and chat messages
bidirectionally. It has to survive network and server failures and recover
gracefully, span short-lived and long-lived interactions, carry real-time voice
and video alongside semi-real-time chat and non-real-time bulk transfer, and
support point-to-multipoint as well as point-to-point.

The motivating example from the BOF was mundane and sharp: an agent books a
business trip, and the user says "cancel the hotel, keep the flight." That
cancellation has to preempt work already in flight, across parties and across
hops, on a control path faster than the bulk path it is interrupting. HTTP is
stateless. WebSocket has no multiplexing, no priority, no partial teardown. MoQ
is close but not agent-aware. That gap is the entire argument for this layer.

This is also the layer the room told the group to sharpen. The strongest thread
was that "session" is the wrong word — the application layer above already uses
it for something specific, and MCP is moving toward statelessness. Ted Hardie
proposed reframing the deliverable as a signaling protocol for the setup and
management of **context propagation** across trust boundaries, multi-party and
multimodal, noting that SIP and WebRTC manage context mostly at initiation
whereas here the context must persist and travel with a party across devices and
time. Jonathan Rosenberg reached the same place from the other direction: a
context management protocol, distinct from SIP, that starts a context, appends
audio and video and text to it, pauses it, resumes it. Brian Trammell agreed on
substance and warned that "context propagation" will confuse AI researchers, and
pressed the question that should govern this layer — what is the **minimum
viable set of primitives** that makes the genuinely new thing work? What is new,
on his reading, is not that programs talk to each other but the dynamicity of
connectivity and deployment.

So: one protocol, deliberately small, defined by the minimum set of primitives
for managing context across trust boundaries, with an explicit statement of what
it standardizes, what it consumes, and what it leaves to the layers above and
below.

## Layer two: the composition

The **AI Agent Protocol Framework** puts nothing on the wire. It names the
building blocks, says how they compose into a working agent scenario, and marks
where the gaps are that other groups should fill. It is architecture, and it is
the contested layer.

The case for it: agent communication is a protocol *suite*, not a protocol, and
something has to bind the pieces the IETF defines (Zaheduzzaman Sarker). It
describes the slots that the identity and authorization groups fill (Justin
Richer). It takes the outputs of other groups and presents them in a form an
implementer can consume (Suresh Krishnan). It is how you understand the layers
at all (Jonathan Rosenberg), and it should arguably come *before* the protocol
work rather than in parallel (Ted Hardie).

The case against: keep it as a terminology reference and nothing more (Brian
Trammell); drop it and wait for someone to produce a proof of concept that the
authorization information really can be passed around safely, then fill the
identified gaps (Stephen Farrell); leave it out entirely rather than redefine
work already under way elsewhere, including at the ITU (Arnaud Taddei).

Both readings are coherent, which is why the deliverables question split 92/58.
The live proposal is that this layer either gets re-scoped with a concrete
articulation of what it is *for* and a committed editor, or it gets withdrawn.
If you have a view, this is the one to bring to the list.

## Layer three: the evidence

**Use cases, gap analysis, and requirements** — informational drafts that
establish what agents actually need to do, which existing protocols already do
it, and what is genuinely missing. This layer was not contested at the BOF. It
was repeatedly named as the thing that should come first, because it is what
converts "we believe there is a gap" into a demonstrated gap that a protocol can
be measured against.

Treat this as load-bearing rather than preliminary. Layer one is only justified
to the extent layer three shows that QUIC, HTTP/2, WebTransport, and MoQ do not
already cover it. Layer two is only useful to the extent layer three shows which
slots are empty. The informational layer is where the argument is either won or
lost, and it needs editors more urgently than anything else on the list.

## The one-paragraph version

agentproto proposes to add exactly one new protocol to the Internet — a minimal
protocol for setting up and managing context as it propagates across trust
boundaries, multi-party and multimodal — sitting below MCP and A2A and above
QUIC, WebTransport, MoQ, and WebRTC. Around it, a framework document that
composes identity and authorization work owned by OAuth, WIMSE, and webbotauth
rather than reinventing it, and a set of informational drafts establishing that
the gap is real. The BOF said the problem is worth solving and the IETF is the
place. It also said these boundaries are not yet drawn correctly. Getting them
right is the work in front of the list.

## What to read next

Read the [draft charter](https://github.com/ietf-artarea/charters/blob/main/agentproto/charter.md)
in full — it is short. Charter revision happens in that repository, and pull
requests are welcome. Discussion happens on `agentproto@ietf.org`
([subscribe](https://www.ietf.org/mailman/listinfo/agentproto),
[archive](https://mailarchive.ietf.org/arch/browse/agentproto)). The
[datatracker group page](https://datatracker.ietf.org/group/agentproto/about/)
is the system of record, and the
[BOF request](https://datatracker.ietf.org/doc/bofreq-krishnan-agent-communication-protocols/)
gives the original framing the room responded to.

Positions attributed above are drawn from the IETF 126 BOF record and are
summaries, not quotations; the minutes are the authority on what anyone actually
said.
