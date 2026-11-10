# Bilingual Support: engineering notes

A support answer needs both useful evidence and the right permission boundary. This assistant connects bilingual policy questions, scoped order lookup and human handoff.

## System path

~~~mermaid
flowchart LR
  CustomerSession --> Intent
  Intent --> ScopedOrderLookup
  Intent --> VersionedRetrieval
  VersionedRetrieval --> CitationCheck
  CitationCheck --> Answer
  Answer --> HumanHandoff
~~~

This diagram describes the demonstrated system boundary, not a production deployment topology.

## Decisions and tradeoffs

### Verify citations against retrieved passages

A model cannot turn an arbitrary citation into verified evidence. Quotes are located in the retrieved source before they receive verified status.

### Take identity from the session

Order access is decided on the server using the current customer identity, never a customer identifier supplied in the message.

### Version the knowledge, not just the answer

Publishing an article revision invalidates dependent cached answers, marks translations stale and triggers index rebuilding.

## Review questions

- What evidence demonstrates **verify citations against retrieved passages**, and what would fail without it?
- What evidence demonstrates **take identity from the session**, and what would fail without it?
- What evidence demonstrates **version the knowledge, not just the answer**, and what would fail without it?

## Verification boundary

12 database regressions covering English/Arabic policy basis, scoped orders, stale knowledge, citations and handoff. Six browser checks passed, including desktop journeys and narrow Arabic layout. Recorded chat, evidence drawer and operator workflow available.

The default experience uses sample customers and policy fixtures. Arabic content remains a draft pending language review. No real store integration is connected.
