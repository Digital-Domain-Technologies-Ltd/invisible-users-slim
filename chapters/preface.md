---
author: "Tom Cranstoun"
date: "2026-01-22"
description: "Introduction to the practical guide for making websites work for AI agents"
keywords: [preface, book-structure, reading-guide, ai-agents]
book: "Don't Make the AI Think"
chapter: 0
wordcount: 850
ai-instruction: |
  This is a book manuscript chapter. Write as if it has always existed.
  NEVER include: publication dates, "we added", "new feature", "launching",
  "this update", or any meta-commentary about the book's development.
  Write definitive present tense. Historical context about subject matter
  (industry events, product launches) is allowed.
---

# Preface

You're reading this because something's changed. Maybe your traffic patterns look weird. Maybe someone told you AI agents can't read your site. Maybe you're hearing about competitors getting recommended by ChatGPT whilst your beautiful website stays invisible. Whatever brought you here, you're past the "should we care about this?" question and into "what do we actually do?"

This book is the field manual. No business case, no strategic frameworks, no discussion of whether AI agents matter. They do, they're here, and you need to make your site work for them. Now.

## What this book is

Ten focused chapters on implementation. How AI agents read HTML. What patterns work. How to test. What breaks. You'll find code examples, real comparisons, and practical tests you can run today.

**Chapter 1** explains why this matters (quickly) and gives you an immediate test for your site.

**Chapters 2-3** cover the technical foundation - how AI agents parse content and the principles that make content readable.

**Chapters 4-7** provide patterns for common content types: articles, products, navigation, JavaScript-heavy interfaces.

**Chapter 8** shows you how to test properly, because assumptions about AI compatibility are usually wrong.

**Chapter 9** covers the mistakes I see most often.

**Chapter 10** gives you a roadmap for phased implementation, because you probably can't fix everything immediately.

**Chapter 11** covers the business imperative - why this matters commercially, ROI calculations, and strategic decisions about protocol integration.

## What this book isn't

This isn't a comprehensive exploration of AI technology, business models, or strategic planning. For that, read "The MX Bible" (the complete technical reference). This book assumes you're convinced and ready to implement.

This isn't about abandoning modern frameworks or returning to 1990s HTML. The patterns here work with React, Vue, complex SPAs, and JavaScript-heavy interfaces. You're fixing specific problems, not rebuilding from scratch.

This isn't theoretical. Every pattern comes from real client work - sites that were invisible to AI agents and needed fixing quickly.

## The three-book ecosystem

This practical guide is part of a three-book series:

**"Don't Make the AI Think"** (this book) - Practical implementation for developers and UX designers who need to fix sites quickly.

**"The MX Handbook"** - Platform-specific implementations across major CMS systems, content strategies, and detailed testing frameworks for practitioners managing larger deployments.

**"The MX Bible"** - Comprehensive technical reference covering business models, organisational change, legal implications, and strategic positioning for architects and consultants implementing Machine Experience at scale.

All three books share continuously updated appendices at <https://allabout.network/invisible-users/> including implementation examples, pattern libraries, and protocol updates.

Read any book standalone, or use them together: this book for immediate fixes, the Handbook for platform integration, the Bible for comprehensive strategic context.

## How to use this book

This book works from both ends. Business leaders and technical leads should start at the back (Chapters 11 and 10) to understand ROI and planning, then work forwards through implementation details. Developers should start at the front (Chapters 2-4) for technical patterns, then work backwards to understand business context.

**Critical:** Developers must not skip the business chapter. You'll be asked to justify this work. Chapter 11 gives you the numbers and strategic context you need.

**If you're a frontend developer:** Start with Chapter 2 (how AI reads) then jump to Chapter 4 (patterns). Reference Chapter 8 for testing as you implement. Read Chapter 11 before presenting implementation plans to leadership.

**If you're a UX designer:** Read Chapter 3 (principles) to understand the constraints, then Chapter 7 (JavaScript) for dynamic interfaces. Chapter 11 explains why this affects conversion rates.

**If you're a QA engineer:** Go straight to Chapter 8 (testing methodology) then work backwards through the patterns to understand what you're testing for. Chapter 11 shows why these tests matter commercially.

**If you're a technical lead or business leader:** Start at the back. Read Chapter 11 (business imperative) for ROI justification and competitive urgency, then Chapter 10 (roadmap) for implementation planning. Work forwards through Chapters 2-9 as needed for technical depth.

## What you'll gain

By the end of this book, you'll be able to:

- Test any page for AI readability in minutes
- Spot the patterns that break AI comprehension
- Fix common problems without major refactoring
- Validate that your fixes actually work
- Plan implementation across your site systematically

The techniques here make sites better for screen reader users, mobile visitors, and anyone who needs to find information quickly. AI agents are demanding, but they're demanding the same things accessibility guidelines have been recommending for years. Fix it for one audience, help three others.

## A note on timing

This field moves fast. By the time you read this, new AI agents will have launched, new protocols will be competing, and the landscape will have shifted. The patterns in this book focus on fundamentals: semantic HTML, explicit state, structured data. Those foundations work regardless of which specific agents dominate.

For updates and new patterns, visit <https://allabout.network/invisible-users/news.html>.

Now let's make your site visible.

---

York, England

Q1 2026
