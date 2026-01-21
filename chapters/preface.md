---
author: "Tom Cranstoun"
date: "2026-01-22"
description: "Why AI agents need clear, structured websites - and why fixing this problem helps everyone"
keywords: [preface, book-structure, ai-agents, practical-guide]
book: "Don't Make the AI Think"
chapter: 0
wordcount: 2800
ai-instruction: |
  This is a book manuscript chapter. Write as if it has always existed.
  NEVER include: publication dates, "we added", "new feature", "launching",
  "this update", or any meta-commentary about the book's development.
  Write definitive present tense. Historical context about subject matter
  (industry events, product launches) is allowed.
---

# Preface

I didn't set out to write about AI agents. I set out to book a holiday.

It was late 2024, and I was comparing tour operators for a trip through Southeast Asia. I'd delegated the research to an AI assistant, expecting it to save me hours of clicking through brochures. Instead, it gave me confident but wrong advice about which company had the better itinerary.

The agent had looked at one tour operator's paginated day-by-day breakdown for a 14-day tour, seen only Day 1, and concluded that was the entire trip. The competitor's single-page itinerary was readable in full. Based on this, my assistant recommended the wrong company.

I caught the error. That mistake led me to investigate why AI agents fail - and what that means for businesses.

## The Pattern Emerges

The same design choices that confused my AI assistant also confused users with disabilities. People who rely on keyboards rather than mice. Those using screen readers to navigate. Voice control users who cannot make precise movements.

We'd built a web that worked brilliantly for one specific type of user: someone with good vision, working on a desktop, with focused attention and plenty of time. Everyone else had been struggling quietly for many years. Now AI agents were struggling loudly, and there was finally commercial pressure to fix the problems.

## The Market Moved Fast

When I started writing, AI agents accessing websites felt like something to monitor and prepare for gradually. By early 2026, the landscape had fundamentally transformed.

January 2026: Four major platforms launched agent systems within eight days. Amazon's Alexa+ (January 5th) for voice-initiated purchasing. Microsoft's Copilot Checkout (January 8th) for transactions within the AI assistant. Google's Universal Commerce Protocol (January 11th) backed by Target and Walmart. Anthropic's Claude Cowork (January 12th) for autonomous workflows.

This isn't a distant future. Agent-mediated commerce is happening now, and businesses that aren't ready are being excluded from high-conversion transactions.

## Understanding the Five Types of AI Agents

Before we can fix websites for AI agents, we need to understand what they actually are. Not all agents work the same way, and these technical differences matter.

**Server-Side Agents (ChatGPT, Claude)** run on remote servers and fetch your website as raw text. They cannot execute JavaScript or render CSS. They see HTML structure and text content, but miss everything that loads dynamically. If your product catalogue loads via JavaScript, server-side agents see an empty page.

**In-Browser Agents (Microsoft Copilot, Browser Extensions)** run within web browsers and have full access to rendered pages. They can execute JavaScript and access the DOM after it updates. They see dynamic content but miss visual hierarchy from CSS. If your form submission shows a toast notification that vanishes in 3 seconds, in-browser agents might miss it.

**Browser Automation Agents (Perplexity, Playwright-based)** control full browsers programmatically and can take screenshots. They can see layout, colour, and size relationships through computer vision. They can see your "Add to Cart" button is red and prominent, but still need proper HTML button elements to click reliably.

**Local Agents (Ollama, On-Device LLMs)** run on users' personal computers with limited resources. They use smaller models with limited context windows. If your page serves 10,000 words of marketing copy before getting to product details, local agents may never reach the important content.

**Agentic Operating Systems (Anthropic Cowork)** orchestrate multiple agents working in parallel. They combine capabilities of other agent types - managing files, executing browser automation, processing server-side content - whilst coordinating complex multi-step workflows. If your checkout works for browser agents but breaks for server-side agents, agentic operating systems cannot reliably complete purchases.

Each type has different capabilities. But all five need the same fundamental patterns: semantic HTML, explicit state management, and structured data. When you fix your website for one agent type, you improve it for all five.

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

The techniques here make sites better for screen reader users, mobile visitors, and anyone who needs to find information quickly. AI agents are demanding, but they're demanding the same things accessibility guidelines have been recommending for many years. Fix it for one audience, help three others.

## The Convergence Principle

Here's the key insight: patterns that help AI agents also help humans with disabilities.

Semantic HTML that helps screen readers also helps server-side agents. Explicit state management that helps keyboard users also helps browser-based agents. Structured data that helps voice assistants also helps all types of agents extract accurate information.

You're not choosing between audiences. You're not trading off business goals against accessibility compliance. One implementation serves everyone: users with disabilities, search engines, and AI agents.

The work compounds across multiple channels. The same patterns that improve AI agent compatibility also improve search engine rankings, accessibility compliance, and user experience for people in non-ideal conditions.

## Why This Matters Now

In January 2025, Tailwind CSS laid off 75% of its team after traffic-dependent revenue collapsed. When AI agents started answering developer questions without sending traffic to documentation sites, companies relying on pageviews found their monetisation broken.

This isn't theoretical. Companies are failing right now because their business models assume human browsing behaviour that no longer dominates discovery.

## Acknowledgements

This book exists because problems became visible when I looked closely at failures I'd typically have ignored. I'm grateful to everyone who has written about web accessibility over many years; their work laid the foundations on which this analysis builds.

Thank you to colleagues, clients, and collaborators who reviewed early drafts and asked uncomfortable questions.

## A note on timing

This field moves fast. By the time you read this, new AI agents will have launched, new protocols will be competing, and the landscape will have shifted. The patterns in this book focus on fundamentals: semantic HTML, explicit state, structured data. Those foundations work regardless of which specific agents dominate.

For updates and new patterns, visit <https://allabout.network/invisible-users/news.html>.

Now let's make your site visible.

---

York, England

Q1 2026
