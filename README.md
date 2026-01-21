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

See the parent repository's [CLAUDE.md](../../CLAUDE.md) and [docs/architecture/GIT-README.md](../../docs/architecture/GIT-README.md) for comprehensive guidance.

## Overview

This slim guide provides practical, immediately actionable patterns for making websites work effectively with AI agents. Written as a companion to "The Invisible Users" (the comprehensive 13-chapter guide), this book focuses on implementation over context.

**Market timing:** January 2026 saw Amazon, Microsoft, and Google launch agent commerce systems within seven days, accelerating the transition from experimental to infrastructure. This guide provides patterns that work regardless of platform dominance.

This is the streamlined "slim" version of The Invisible Users, focused on:

- **Practical patterns** you can implement immediately
- **Anti-patterns** to avoid
- **Testing methodologies** for validation
- **Implementation roadmap** with priority levels
- **Business justification** for technical teams

**This book works from both ends:**

- Business leaders and technical leads start at the back (Chapters 11→10) for ROI and planning
- Developers start at the front (Chapters 2-4) for technical patterns
- Everyone reads Chapter 11 before presenting implementation plans to leadership

## Status

**Publication:** Due Q1 2026
**Word count:** Focused for quick reference
**Current state:** Complete and ready for publication

## Contents

### Front Matter

- **Cover page** - Professional cover with distribution notice
- **Preface** - How to use this book and reading guidance

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
11. **Business Imperative** - ROI, competitive urgency, and strategic decisions

### Supporting Materials

- **CHAPTERS-GUIDE.md** - Chapter organization and structure guide
- **chapters/** - Individual chapter markdown files

## Relationship to "The Bible"

This book is derived from the comprehensive "Bible" version but focuses on:

- **What to implement** (not why)
- **How to implement** (step-by-step patterns)
- **Priority-based approach** (not time-based)
- **Business justification** for technical teams (Chapter 11)

For complete context including business models, organisational change, legal implications, and strategic positioning, see [The Bible](../bible/).

## Live Resources

Appendices, code examples, and industry news are shared between all books and continuously updated online:

- **Live appendices:** <https://allabout.network/invisible-users/>
- **Industry news:** <https://allabout.network/invisible-users/news.html>
- **Pattern library:** Production-ready implementation examples
- **Protocol updates:** Latest developments in ACP, UCP, and Copilot integration

These resources are maintained separately from the book content to ensure readers always have access to current information as the AI agent ecosystem evolves.

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
- **Technical leads** planning implementation roadmaps and justifying resource allocation
- **QA engineers** testing AI compatibility
- **Business leaders** evaluating ROI and competitive positioning (Chapter 11)

**Reading guidance:**

- **Technical staff:** Start at the front (Chapters 2-4) for patterns, read Chapter 11 for business justification
- **Business leaders:** Start at the back (Chapters 11→10) for ROI and planning, skim forward for technical depth
- **Everyone:** Chapter 11 provides essential ROI calculations and strategic context

If you need comprehensive business case analysis, legal context, or strategic guidance beyond implementation planning, see [The Bible](../bible/).

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
