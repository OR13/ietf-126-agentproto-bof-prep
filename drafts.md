# Input Internet-Drafts (public)

Drafts the BOF request cites as relevant. The aiproto **framework** is the
conceptual anchor; the rest cover transport, identity, authorization, use cases.

| Draft | Author(s) | Role | Link |
|-------|-----------|------|------|
| `draft-rosenberg-aiproto-framework` | Rosenberg, Jennings | Anchor: framework, use cases, requirements, gaps | <https://datatracker.ietf.org/doc/draft-rosenberg-aiproto-framework/> |
| `draft-jennings-ai-mcp-over-moq` | Jennings | MCP over Media-over-QUIC | <https://datatracker.ietf.org/doc/draft-jennings-ai-mcp-over-moq/> |
| `draft-liu-agent-protocol-over-moq` | Liu | Agent protocol over MOQ | <https://datatracker.ietf.org/doc/draft-liu-agent-protocol-over-moq/> |
| `draft-klrc-aiagent-auth` | (KLRC) | Agent authentication | <https://datatracker.ietf.org/doc/draft-klrc-aiagent-auth/> |
| `draft-liu-agent-operation-authorization` | Liu | Operation authorization | <https://datatracker.ietf.org/doc/draft-liu-agent-operation-authorization/> |
| `draft-agentic-ai-usecases-requirements` | — | Use cases & requirements | <https://datatracker.ietf.org/doc/> |
| `draft-yao-catalist-problem-space-analysis` | Yao | Problem-space analysis (CATALIST) | <https://datatracker.ietf.org/doc/draft-yao-catalist-problem-space-analysis/> |

Related aiproto-family drafts (background): `-a2t` (Agent-to-Tool),
N-ACT (Normalized API for Calling Tools), `-cheq` (human-in-the-loop confirmation).

## aiproto framework — summary

Authors: Jonathan Rosenberg, Cullen Fluffy Jennings. (-00 expired; discussion
input — verify against any newer revision.)

**Protocol categories:** User→Agent (voice/chat/video); Agent→API
(intra-/inter-domain invocation); Agent→Agent (transfer topologies: Blind,
Supervised, Sidebar, Conference, Passthrough).

**Requirement themes:** proof-of-knowledge auth; well-known OpenAPI discovery;
service-account / OBO / inter-domain-OAuth authz with scope negotiation;
user-confirmation annotations; channel-capability negotiation; sync/async
lifecycle + callbacks; context transfer; conveyed-identity vs re-authentication;
cryptographically-assured user confirmations; prompt-injection diagnosis,
logging, and attribution.

**Prior-art gaps it identifies:** MCP lacks intra-/inter-domain security; A2A
lacks channel-capability + user confirmation; AGNTCY lacks capability
negotiation, lifecycle, authN/authZ, and user confirmations.
