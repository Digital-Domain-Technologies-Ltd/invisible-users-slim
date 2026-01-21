---
author: "Tom Cranstoun"
date: "2026-01-22"
description: "Practical testing strategies to validate AI agent compatibility, including curl tests, validator tools, and agent simulation."
keywords: [testing, validation, curl-testing, schema-validation, agent-simulation, html-validation, readability-testing]
book: "Don't Make the AI Think"
chapter: 8
wordcount: 2808
ai-instruction: |
  This is a book manuscript chapter. Write as if it has always existed.
  NEVER include: publication dates, "we added", "new feature", "launching",
  "this update", or any meta-commentary about the book's development.
  Write definitive present tense. Historical context about subject matter
  (industry events, product launches) is allowed.
---

# Chapter 8: Testing with AI Agents

## Why testing matters

You can implement perfect semantic HTML, comprehensive Schema.org markup, and thoughtful navigation—but if you don't test, you won't know if it actually works.

Testing AI readability is different from traditional testing. You're not checking if buttons click or forms submit. You're checking if AI can understand, extract, and use your content to answer questions.

The good news: testing AI readability is simpler than you might think. You don't need specialist tools or expensive services. You need a methodical approach and some basic techniques.

## The morning-after test

This is your first and most important test. I mentioned it briefly in Chapter 1—now let's look at it properly.

**The basic version:**

1. Open your page in a browser
2. Right-click → View Page Source (not Inspect Element, the actual source)
3. Select all and copy the HTML
4. Open ChatGPT, Claude, or another LLM
5. Paste the HTML
6. Ask questions about the page

**Questions to ask:**

- "What is this page about?"
- "What products or services are offered?"
- "What actions can I take on this page?"
- "What is the price of [specific item]?"
- "Who is the contact person or company?"
- "When was this content last updated?"

The AI should answer accurately using only the HTML you pasted. If it can't, you've found a problem.

**Example conversation:**

```text
You: [paste HTML of product page]

You: What is this page about?

AI: This appears to be a product page for a standing desk called "Professional Standing Desk". It's an electric height-adjustable desk priced at £599.

You: What are the main features?

AI: The key features include:
- Electric height adjustment with memory presets
- Whisper-quiet motor
- Cable management system
- Dimensions: 120cm × 60cm with adjustable height from 70cm to 120cm
- Weight capacity: 80kg

You: Is it in stock?

AI: Yes, according to the page it is currently in stock.
```text

This tells you the AI can extract basic information. Now test edge cases:

```text
You: What's the warranty period?

AI: I don't see warranty information in the HTML provided.
```

That's a problem. You offer a warranty, but it's not in the HTML—perhaps it's loaded via JavaScript or hidden in a modal.

**The advanced version:**

Test with multiple AI systems:

- ChatGPT (OpenAI)
- Claude (Anthropic)
- Gemini (Google)

Each processes content slightly differently. If all three can extract the information, you're in good shape. If one struggles, it might indicate an edge case worth addressing.

## LLM-based extraction testing

Go beyond simple questions. Test if AI can extract structured information:

### Test 1: Data extraction

```text
You: [paste product page HTML]

You: Extract the following information in JSON format:
- Product name
- Price
- Availability
- Main features (as an array)

AI: {
  "productName": "Professional Standing Desk",
  "price": "599",
  "currency": "GBP",
  "availability": "In Stock",
  "features": [
    "Electric height adjustment",
    "Memory presets",
    "Cable management",
    "Whisper-quiet motor"
  ]
}
```text

If the AI can do this accurately, your structured data is working. If it gets confused or misses information, you need to improve your markup.

### Test 2: Relationship understanding

```text
You: [paste service page HTML]

You: What services does this company offer, and how are they organized?

AI: The company offers three main service categories:

1. Edge Delivery Services
   - Implementation
   - Migration
   - Support

2. AEM Consulting
   - Strategy
   - Architecture
   - Training

3. Training and Support
   - Workshops
   - Ongoing support
   - Documentation

The page uses a clear hierarchy with h2 headings for main services and h3 headings for sub-services.
```

This tests whether your heading hierarchy and content organization are clear.

### Test 3: Context awareness

```text
You: [paste blog post HTML]

You: Who wrote this article and when was it published?

AI: The article was written by Tom Cranstoun and published on 15 March 2024. It was last modified on 20 March 2024.

You: Is this person qualified to write about this topic?

AI: Based on the author bio in the HTML, Tom Cranstoun is described as "Principal Consultant at Digital Domain Technologies with 25 years of CMS experience", which suggests relevant qualifications for the topic of AEM migration.
```text

This checks if contextual information (author, dates, credentials) is properly marked up.

## Headless browser testing

Some AI agents use headless browsers. Simulate this approach with Puppeteer or Playwright:

**Basic Puppeteer test:**

```javascript
const puppeteer = require('puppeteer');

async function testPageReadability(url) {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  
  // Navigate to page
  await page.goto(url, { waitUntil: 'networkidle0' });
  
  // Extract key content
  const content = await page.evaluate(() => {
    // Get main heading
    const h1 = document.querySelector('h1')?.textContent?.trim();
    
    // Get all headings to understand structure
    const headings = Array.from(document.querySelectorAll('h1, h2, h3'))
      .map(h => ({
        level: h.tagName,
        text: h.textContent.trim()
      }));
    
    // Check for Schema.org data
    const schemaScripts = Array.from(
      document.querySelectorAll('script[type="application/ld+json"]')
    ).map(s => {
      try {
        return JSON.parse(s.textContent);
      } catch (e) {
        return null;
      }
    }).filter(Boolean);
    
    // Get all links
    const links = Array.from(document.querySelectorAll('a'))
      .map(a => ({
        text: a.textContent.trim(),
        href: a.href
      }))
      .filter(l => l.text && l.href);
    
    return {
      title: document.title,
      h1,
      headings,
      schemaData: schemaScripts,
      linkCount: links.length,
      sampleLinks: links.slice(0, 5)
    };
  });
  
  await browser.close();
  return content;
}

// Run the test
testPageReadability('https://example.com/products/desk-pro')
  .then(result => {
    console.log('Page Title:', result.title);
    console.log('Main Heading:', result.h1);
    console.log('\nHeading Structure:');
    result.headings.forEach(h => {
      const indent = '  '.repeat(parseInt(h.level[1]) - 1);
      console.log(`${indent}${h.level}: ${h.text}`);
    });
    console.log('\nSchema.org Data:', result.schemaData.length, 'items found');
    console.log('\nLinks:', result.linkCount, 'total');
    console.log('Sample links:', result.sampleLinks);
  })
  .catch(console.error);
```

This simulates what a browser-based AI agent sees after JavaScript execution.

**What to check:**

- Is the h1 meaningful?
- Do headings create a logical outline?
- Is Schema.org data present and valid?
- Are links descriptive?

**Red flags:**

```javascript
// Bad signs in output
{
  title: "Loading...",
  h1: null,
  headings: [],
  schemaData: [],
  linkCount: 3
}
```text

This suggests JavaScript hasn't finished loading or the page structure is broken.

## Structured data validation

Google provides free tools for validating Schema.org markup:

**Rich Results Test:**  
<https://search.google.com/test/rich-results>

Paste your URL or HTML snippet. Google will:

- Parse Schema.org markup
- Show what rich results are eligible
- Flag errors and warnings

**Common errors caught:**

```text
Error: Missing required field "price"
Warning: Recommended field "image" is missing
Error: Invalid date format - use ISO 8601
```

**Schema.org Validator:**  
<https://validator.schema.org/>

More permissive than Google's tool. Good for checking if your JSON-LD is syntactically valid, even if it won't trigger rich results.

**Command-line validation:**

For automated testing, use schema-dts or similar tools:

```javascript
const { validate } = require('schema-dts');

const schema = {
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Standing Desk",
  "price": "599" // Should be in offers
};

const errors = validate(schema);
if (errors.length > 0) {
  console.log('Schema errors:', errors);
}
```text

## The comparison test

Before and after testing shows the impact of your improvements:

**Before optimization:**

```text
Test: Morning-after with product page HTML

Question: What is the price?
Answer: I cannot determine the price from the HTML provided.

Question: Is it in stock?
Answer: I don't see availability information.

Question: What are the key features?
Answer: I can see some text that appears to describe features, but they're not clearly structured.
```

**After optimization:**

```text
Test: Morning-after with optimized product page HTML

Question: What is the price?
Answer: £599

Question: Is it in stock?
Answer: Yes, currently in stock.

Question: What are the key features?
Answer: The main features are:
- Electric height adjustment with memory presets
- Cable management system
- Whisper-quiet motor
- Weight capacity of 80kg
- Dimensions: 120cm × 60cm, height adjustable from 70cm to 120cm
```text

Document this difference. It shows stakeholders the concrete impact of AI optimization work.

## Automated testing suite

Create a simple test suite you can run regularly:

```javascript
// test-ai-readability.js
const puppeteer = require('puppeteer');

const tests = [
  {
    url: 'https://example.com/',
    checks: {
      hasH1: true,
      hasSchema: true,
      hasNav: true,
      minLinks: 5
    }
  },
  {
    url: 'https://example.com/products/desk-pro',
    checks: {
      hasH1: true,
      hasSchema: true,
      hasProductPrice: true,
      hasProductImage: true
    }
  }
];

async function runTests() {
  const browser = await puppeteer.launch();
  const results = [];
  
  for (const test of tests) {
    const page = await browser.newPage();
    await page.goto(test.url, { waitUntil: 'networkidle0' });
    
    const pageData = await page.evaluate(() => ({
      h1: document.querySelector('h1')?.textContent,
      hasNav: !!document.querySelector('nav'),
      linkCount: document.querySelectorAll('a').length,
      schemaCount: document.querySelectorAll('script[type="application/ld+json"]').length,
      hasProductPrice: !!document.querySelector('[itemprop="price"], [data-price]'),
      hasProductImage: !!document.querySelector('[itemprop="image"]')
    }));
    
    const testResult = {
      url: test.url,
      passed: true,
      failures: []
    };
    
    // Check conditions
    if (test.checks.hasH1 && !pageData.h1) {
      testResult.passed = false;
      testResult.failures.push('Missing h1 element');
    }
    
    if (test.checks.hasSchema && pageData.schemaCount === 0) {
      testResult.passed = false;
      testResult.failures.push('No Schema.org markup found');
    }
    
    if (test.checks.hasNav && !pageData.hasNav) {
      testResult.passed = false;
      testResult.failures.push('No nav element found');
    }
    
    if (test.checks.minLinks && pageData.linkCount < test.checks.minLinks) {
      testResult.passed = false;
      testResult.failures.push(`Only ${pageData.linkCount} links found, expected ${test.checks.minLinks}+`);
    }
    
    if (test.checks.hasProductPrice && !pageData.hasProductPrice) {
      testResult.passed = false;
      testResult.failures.push('Product price not found in expected format');
    }
    
    if (test.checks.hasProductImage && !pageData.hasProductImage) {
      testResult.passed = false;
      testResult.failures.push('Product image not properly marked up');
    }
    
    results.push(testResult);
    await page.close();
  }
  
  await browser.close();
  return results;
}

runTests().then(results => {
  console.log('\nAI Readability Test Results:\n');
  
  let allPassed = true;
  results.forEach(result => {
    const status = result.passed ? '[PASS]' : '[FAIL]';
    console.log(`${status}: ${result.url}`);
    
    if (!result.passed) {
      allPassed = false;
      result.failures.forEach(failure => {
        console.log(`  - ${failure}`);
      });
    }
  });
  
  console.log('\n' + (allPassed ? 'All tests passed!' : 'Some tests failed.'));
  process.exit(allPassed ? 0 : 1);
});
```

Run this as part of your deployment process or on a schedule:

```bash
node test-ai-readability.js
```text

## The sitemap coverage test

Check if AI can discover all your important pages:

```javascript
const axios = require('axios');
const xml2js = require('xml2js');

async function testSitemapCoverage() {
  // Fetch sitemap
  const response = await axios.get('https://example.com/sitemap.xml');
  const parser = new xml2js.Parser();
  const result = await parser.parseStringPromise(response.data);
  
  const urls = result.urlset.url.map(u => u.loc[0]);
  
  console.log(`Found ${urls.length} URLs in sitemap`);
  
  // Check a sample
  const sampleSize = Math.min(10, urls.length);
  const sample = urls.slice(0, sampleSize);
  
  for (const url of sample) {
    const pageResponse = await axios.get(url);
    const hasContent = pageResponse.data.includes('<h1');
    const hasSchema = pageResponse.data.includes('application/ld+json');
    
    console.log(`${url}:`);
    console.log(`  - Has h1: ${hasContent}`);
    console.log(`  - Has Schema.org: ${hasSchema}`);
  }
}

testSitemapCoverage().catch(console.error);
```

This verifies:

- Your sitemap is accessible
- Listed URLs are reachable
- Each page has basic semantic structure

## The link text audit

Extract and review all link text from a page:

```javascript
async function auditLinkText(url) {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto(url, { waitUntil: 'networkidle0' });
  
  const links = await page.evaluate(() => {
    return Array.from(document.querySelectorAll('a'))
      .map(a => ({
        text: a.textContent.trim(),
        href: a.href,
        ariaLabel: a.getAttribute('aria-label')
      }))
      .filter(l => l.text || l.ariaLabel);
  });
  
  await browser.close();
  
  // Flag problematic link text
  const problematic = links.filter(l => {
    const text = l.text.toLowerCase();
    return (
      text === 'click here' ||
      text === 'here' ||
      text === 'read more' ||
      text === 'learn more' ||
      text === 'more' ||
      text.length < 3
    );
  });
  
  console.log(`Total links: ${links.length}`);
  console.log(`Problematic links: ${problematic.length}`);
  
  if (problematic.length > 0) {
    console.log('\nLinks to improve:');
    problematic.forEach(l => {
      console.log(`  "${l.text}" → ${l.href}`);
    });
  }
  
  return {
    total: links.length,
    problematic: problematic.length,
    issues: problematic
  };
}

auditLinkText('https://example.com').catch(console.error);
```text

## Mobile AI readability

Some AI agents access sites via mobile user agents. Test how your content appears on mobile:

```javascript
async function testMobileReadability(url) {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  
  // Emulate mobile device
  await page.emulate({
    viewport: {
      width: 375,
      height: 667,
      isMobile: true
    },
    userAgent: 'Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) AppleWebKit/605.1.15'
  });
  
  await page.goto(url, { waitUntil: 'networkidle0' });
  
  // Check content visibility
  const content = await page.evaluate(() => {
    const h1 = document.querySelector('h1');
    const main = document.querySelector('main');
    
    return {
      h1Visible: h1 ? h1.offsetHeight > 0 : false,
      mainVisible: main ? main.offsetHeight > 0 : false,
      h1Text: h1?.textContent?.trim(),
      viewportHeight: window.innerHeight,
      contentHeight: document.body.scrollHeight
    };
  });
  
  await browser.close();
  return content;
}
```

Check if:

- Content is visible on mobile viewports
- Headings aren't hidden
- Main content isn't pushed below the fold by oversized headers

## The accessibility-AI overlap test

Many accessibility tools catch AI readability issues:

**axe DevTools:**  
Browser extension that audits accessibility. Issues it catches that also affect AI:

- Missing alt text on images
- Improper heading hierarchy
- Forms without labels
- Links without descriptive text
- Missing ARIA labels

**WAVE:**  
<https://wave.webaim.org/>

Visual accessibility checker. Highlights:

- Semantic structure problems
- Missing form labels
- Contrast issues (not AI-relevant, but good to fix)
- Document outline problems

**Lighthouse:**  
Built into Chrome DevTools (Lighthouse tab).

The "Accessibility" section flags many AI readability issues:

- Image elements do not have alt attributes
- Heading elements are not in a sequentially-descending order
- Form elements do not have associated labels

Run Lighthouse, fix accessibility issues, and you'll improve AI readability as a side effect.

## Continuous monitoring

Don't just test once. Set up ongoing monitoring:

**Weekly automated tests:**

```javascript
// In your CI/CD pipeline or cron job
const schedule = require('node-schedule');

schedule.scheduleJob('0 9 * * 1', async function() {
  console.log('Running weekly AI readability tests...');
  
  const results = await runTests();
  
  if (!results.allPassed) {
    // Send alert email or Slack message
    await sendAlert({
      subject: 'AI Readability Tests Failed',
      results: results
    });
  }
});
```text

**Google Search Console monitoring:**

Check for:

- Structured data errors (increases over time)
- Pages with missing or invalid markup
- Crawl errors that might hide content from AI

**Traffic pattern monitoring:**

Track:

- Referrals from AI chat interfaces (if trackable)
- Increases/decreases in organic search
- Voice search queries (often use AI extraction)

## Creating a testing checklist

For each important page type, maintain a checklist:

**Product Page Checklist:**

- [ ] Has meaningful h1
- [ ] Product name visible in HTML (not just JavaScript)
- [ ] Price visible in HTML with proper markup
- [ ] Availability status clear
- [ ] Images have descriptive alt text
- [ ] Schema.org Product markup present
- [ ] Offers markup with price and currency
- [ ] Features listed (ul or ol, not divs)
- [ ] Specifications in definition list or table
- [ ] Links have descriptive text
- [ ] Breadcrumbs present

**Blog Post Checklist:**

- [ ] Has h1 with article title
- [ ] Heading hierarchy is logical (h1 → h2 → h3)
- [ ] Author name visible and marked up
- [ ] Publication date in HTML (ISO format)
- [ ] Schema.org Article markup present
- [ ] Meta description present
- [ ] Images have alt text
- [ ] Internal links use descriptive text
- [ ] Related articles linked
- [ ] Categories/tags marked up

**Service Page Checklist:**

- [ ] Clear h1 describing the service
- [ ] Service description in first paragraph
- [ ] Benefits/features listed properly
- [ ] Pricing information (if applicable)
- [ ] Contact information visible
- [ ] Related services linked
- [ ] Case studies or examples linked
- [ ] Schema.org Service markup (if applicable)

Run through these checklists before publishing new pages or after major updates.

## The human review

Automated tests catch technical issues, but sometimes you need human judgement:

**Have someone unfamiliar with your content:**

1. Read just your HTML source (view page source)
2. Attempt to answer:
   - What is this page about?
   - What can I do here?
   - What's the main message?
   - How do I contact the company?

If they struggle, AI will struggle too.

## Real-world testing workflow

Here's how I test client sites:

### Phase 1: Initial audit (2-3 hours)

1. Run morning-after test on 5-10 key pages
2. Check sitemap exists and is valid
3. Run Lighthouse accessibility audit
4. Validate Schema.org markup
5. Review link text across main navigation
6. Document findings

### Phase 2: Detailed analysis (4-6 hours)

1. Headless browser testing on key pages
2. Test with JavaScript disabled
3. Mobile viewport testing
4. Schema.org validation on all markup
5. Content structure review (heading hierarchy)
6. Internal linking audit

### Phase 3: Automated setup (2-4 hours)

1. Create automated test suite
2. Set up weekly monitoring
3. Configure alerts for failures
4. Document baseline metrics

### Phase 4: Ongoing (30 minutes weekly)

1. Review automated test results
2. Check for new errors
3. Test any new pages added
4. Monitor traffic patterns

Total initial investment: 10-15 hours  
Ongoing: 30 minutes per week

The return: knowing your site works for AI, catching problems before they affect visibility.

## What you've learned

If you've implemented the patterns from earlier chapters and validated them with these testing methods, you now have:

- Content that AI can discover (sitemaps, navigation)
- Structure that AI can parse (semantic HTML)
- Metadata that AI can extract (Schema.org)
- Confidence that it all works (testing)

But there's one more thing to address: the common mistakes that undermine all this work. The next chapter covers anti-patterns—the things to avoid.

---

**Coming up in Chapter 9:** Common anti-patterns—mistakes that make you invisible to AI and how to fix them.
