# Don't Make AI Think: Designing Web Interfaces for AI Agents

**Focused practical implementation guide for developers and designers.**

## Repository Purpose and Structure

**This is a content-only repository used as a git submodule.**

This repository exists for **separation of concerns** - keeping content version-controlled independently from build tooling and orchestration. Key characteristics:

- **No package.json** - No npm packages, no dependencies, no scripts, no dependency management
- **No build tooling** - Cannot be built independently
- **Content focus** - Pure markdown content for version control
- **Parent repository controls building** - All build commands, PDF generation, and linting are executed from the parent `invisible-users` repository

To work with this content:

1. Use the parent repository (`invisible-users`) for all build operations
2. Edit content directly in this submodule
3. Commit changes here first, then update the parent repository pointer

See the parent repository's [CLAUDE.md](../../CLAUDE.md) and [docs/repo/GIT-README.md](../../docs/repo/GIT-README.md) for comprehensive guidance.

## Overview

This is the streamlined "slim" version of The Invisible Users, focused on:

- **Practical patterns** you can implement immediately
- **Anti-patterns** to avoid
- **Testing methodologies** for validation
- **Implementation roadmap** with priority levels

## Status

**Publication:** Due Q1 2026
**Word count:** Focused for quick reference
**Current state:** Complete and ready for publication

## Contents

### Chapters

1. **Don't Make AI Think** - Introduction and core philosophy
2. **How AI Reads** - Understanding agent parsing models
3. **Guiding Principles** - Essential patterns for AI-friendly design
4. **Content Architecture** - Structural patterns for common page types
5. **Metadata That Works** - Schema.org and metadata implementation
6. **Navigation** - Site discovery and navigation patterns
7. **JavaScript** - Making dynamic sites AI-readable
8. **Testing** - Testing methodologies for AI readability validation
9. **Anti-Patterns** - Common mistakes and fixes
10. **Implementation** - Practical roadmap

### Supporting Materials

- **CHAPTERS-GUIDE.md** - Chapter organization and structure guide
- **chapters/** - Individual chapter markdown files

## Relationship to "The Bible"

This book is derived from the comprehensive "Bible" version but focuses on:

- **What to implement** (not why)
- **How to implement** (step-by-step patterns)
- **Priority-based approach** (not time-based)

For complete context including business, legal, and strategic perspectives, see [The Bible](../bible/).

## Shared Resources

This book references shared resources maintained in separate packages:

- **Appendices:** [packages/shared-appendices/](../shared-appendices/) - Quick reference guides, code examples
- **Code examples:** [packages/shared-code-examples/](../shared-code-examples/) - Production-ready implementations

## Build Commands

Generate book outputs (from repository root):

```bash
# Generate HTML
npm run pdf:dont-html

# Generate A4 PDF
npm run pdf:dont-generate

# Generate 6"×9" PDF for Kindle Direct Publishing
npm run pdf:dont-kindle

# Generate simple PDF
npm run pdf:dont-simple

# Generate all formats
npm run pdf:dont-all
```

## Writing Style

- **British English** throughout (organise, colour, whilst)
- **Second-person instructional** ("you should...")
- **Imperative headings** ("Add Schema.org", "Test with ChatGPT")
- **Concise, actionable** guidance
- **Real code examples** over theory

See [docs/for-ai/writing-style.md](../../docs/for-ai/writing-style.md) for complete guidelines.

## Target Audience

This streamlined version is designed for:

- **Frontend developers** implementing patterns immediately
- **UX designers** understanding AI interaction models
- **Technical leads** planning implementation roadmaps
- **QA engineers** testing AI compatibility

If you need business case justification, legal context, or strategic guidance, start with [The Bible](../bible/).

## Implementation Approach

Focus on **priority levels**, not time estimates:

- **Priority 1:** Critical Quick Wins (semantic HTML, Schema.org)
- **Priority 2:** Essential Improvements (navigation, structured data)
- **Priority 3:** Core Infrastructure (testing, monitoring)
- **Priority 4:** Advanced Features (dynamic content handling)

See [packages/shared-appendices/appendix-f-implementation-roadmap.md](../shared-appendices/appendix-f-implementation-roadmap.md) for detailed guidance.

## Contributing

This manuscript is in final editing for publication. For questions or corrections:

- Email: <tom.cranstoun@gmail.com>
- Website: <https://allabout.network>

## License

PROPRIETARY - All rights reserved
