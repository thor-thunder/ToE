# CLAUDE.md

Guidance for Claude Code (and other LLM agents) working in this repository.

## Reference documents

- [llm-wiki.md](llm-wiki.md) — the **LLM Wiki** pattern: how an LLM incrementally builds and maintains a persistent, interlinked markdown knowledge base (raw sources → wiki → schema). This is a reference/idea document, **not a skill**. It is the foundation for the Obsidian MCP server we are building: the MCP will let an agent operate on an Obsidian vault as a compounding wiki — ingesting sources, updating entity/concept pages, maintaining `index.md` and `log.md`, and linting the vault for contradictions and orphan pages. Read it before working on anything related to the Obsidian MCP or the knowledge-base tooling.
