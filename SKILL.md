---
name: ux-sentiment-research
description: Pulls UX sentiment and friction patterns about a specific company's product from public sources (G2, Capterra, App Stores, Reddit, YouTube, Glassdoor, targeted Google) and turns them into interview-ready talking points, improvement ideas, and questions. Use this whenever someone is preparing for a product or design interview at a specific company, wants to evaluate a product's UX maturity from outside, or asks any variant of "what do users say is broken about [product]," "research [company]'s UX before my interview," or "find the pain points in [product]." Also use when someone wants to demonstrate product judgment in writing (blog post, case study) about a product they don't work on. Trigger on phrases like "research [company] product," "what's the UX like at [company]," "prep for [company] interview," or any time a designer mentions an upcoming interview at a named company.
argument-hint: [company name or product URL]
---

# UX Sentiment Research

## Target

Run this workflow against: **$ARGUMENTS**

If `$ARGUMENTS` is empty, ask the user one short question: "Which company or product do you want me to research?" Then proceed with their answer as the target for every step below.

## What this skill does

Pulls real user sentiment about a specific product from public sources, identifies friction patterns, and produces three artifacts:
1. A pain-point list with quotes and sources
2. Two or three concrete improvement ideas framed as discussion starters
3. Three to five sharp questions to ask in the interview

It's designed for product and design interview prep, but it also works for competitive analysis, due diligence on a tool you're evaluating, or building a public case study.

## When to use it

Trigger this skill when:
- A user mentions an upcoming interview at a specific named company
- A user asks "what do people say about [product]"
- A user asks for UX friction patterns or pain points for a known product
- A user is writing a product critique, case study, or blog post about a real product

Don't use it for:
- Pre-launch products or products with no public footprint
- General UX questions not tied to a specific product
- Internal proprietary tools (no public sources to pull from)

## Time budget

Aim for 30 to 45 minutes of search and synthesis. If you find yourself past 60 minutes, you are over-collecting. Cut to synthesis.

## The seven-step workflow

### Step 1: Confirm scope (2 minutes)

The target product is **$ARGUMENTS** (resolved above). Now establish the basics before searching:

- The product's full name and primary URL
- Whether it has a mobile app (changes which sources matter)
- Whether it's B2B SaaS, consumer, developer tool, marketplace, or mission-driven tech (changes which review sites have signal)
- Whether the user wants the output framed for an interview, a blog post, or competitive analysis

If category and intent aren't clear from context, ask one short question. Don't ask three.

### Step 2: Run the parallel search pass (10 minutes)

Run searches across these sources in roughly this order. The first pass is broad, the second is targeted at friction. Replace `[product]` in every query below with the actual target name from `$ARGUMENTS`.

**Broad pass** (one query each):
- `[product name] reviews pros cons`
- `[product name] G2 reviews`
- `[product name] Capterra reviews`
- `[product name] reddit`
- `[product name] App Store review` (if mobile)
- `[product name] alternatives` (reveals competitive friction)

**Friction pass** (targeted negative-sentiment queries):
- `[product name] frustrating`
- `[product name] difficult` or `[product name] confusing`
- `[product name] doesn't work` or `[product name] broken`
- `[product name] missing feature`
- `[product name] vs [main competitor]` (where competitor is found in alternatives)

For each result, capture the quote, source name, and reviewer role if visible. Do not paraphrase yet. Verbatim quotes give you credibility in the interview.

### Step 3: Pull the actual product's surface (5 minutes)

Read the product's marketing site and look for:
- What it claims to do
- What plans cost
- What the home dashboard looks like (from screenshots)
- What's in the help center's "popular articles" (high-volume help topics = friction)

The gap between the marketing site's promise and the review site's reality is where the interview-worthy material lives.

### Step 4: Pattern-match the friction (5 minutes)

Group raw complaints into categories. Common categories:
- **Wayfinding / IA**: navigation confusion, can't find features, overwhelm
- **Error handling and recovery**: things break, no clear path back
- **Onboarding and learning curve**: too steep, no in-context guidance
- **Performance and reliability**: slow, crashes, sync issues
- **Feature gaps**: things users explicitly say they wish existed
- **Integration friction**: bouncing between this and another tool
- **Pricing or value clarity**: confusion about what's included
- **Trust and communication**: emails, notifications, surprises

If a pattern is mentioned by two or more independent reviewers, it's real. One-off complaints are noise unless they're specific and serious.

### Step 5: Generate improvement ideas (5 minutes)

For the top two or three friction patterns, propose a concrete improvement. Each idea needs:
- **The problem in one sentence** with a real quote attached
- **The proposed change** in two or three sentences
- **Why it's worth doing now** (impact, scope, who benefits)

Bias toward improvements that are structural rather than cosmetic. Bias toward improvements you could actually prototype in Claude Code or Figma in a week.

Avoid: "they should redesign their whole product." Useless and arrogant in an interview.

### Step 6: Draft the interview questions (5 minutes)

Generate three to five questions that demonstrate:
- You did the research (reference specific findings, not generic platitudes)
- You're thinking about the problem strategically (not just listing complaints)
- You're inviting collaboration, not auditing them

Good question shape: "I noticed [specific signal from research]. Has the team explored [specific direction]? What's blocked that?"

Bad question shape: "What are your biggest UX challenges?" (Generic. Wastes the interviewer's time. Shows no preparation.)

### Step 7: Package and write (5 to 10 minutes)

Produce the output in this structure (see `references/output-template.md` for the full template):

1. **The pattern** (one paragraph: what's the overall story)
2. **Top friction patterns** with verbatim quotes and sources
3. **What this tells you about the product team** (one short section)
4. **Two or three concrete improvements** (the format above)
5. **Three to five interview questions**
6. **What to verify in conversation** (gaps your research couldn't close)
7. **Honest read on the product's maturity stage**

Keep the whole output under 1,500 words. If it's longer, you're hedging.

## Source priority by company type

See `references/sources-by-company-type.md` for the full matrix. Quick version:
- **B2B SaaS**: G2, Capterra, Software Advice, TrustRadius, Reddit (industry subreddits)
- **Consumer mobile**: App Store / Play Store reviews, Reddit (product subreddit), YouTube reviews
- **Consumer web**: Reddit, Trustpilot, YouTube, BBB complaints
- **Developer tools**: GitHub issues, Stack Overflow, Hacker News threads, Reddit r/programming
- **Marketplaces**: Both buyer and seller subreddits, BBB, Trustpilot
- **Civic / nonprofit tech**: Capterra, Glassdoor (for internal product complaints), specific community forums

## What not to do

- **Don't quote verbatim more than 15 words from any single source.** Paraphrase. Use short quotes for emphasis.
- **Don't treat one negative review as a pattern.** Two independent reviewers minimum.
- **Don't ignore positive signal.** What people love tells you what the team is good at and what won't change easily.
- **Don't pad with research methodology in the final output.** The user doesn't need to see your work, they need the conclusions.
- **Don't propose redesigns of things you haven't used.** Stay on patterns you've seen evidence for.
- **Don't fabricate quotes.** If you can't find a real quote that says it, don't put quote marks around it.

## Output checklist

Before handing off, verify:
- [ ] Every friction pattern is supported by at least one verbatim quote with a named source
- [ ] Improvement ideas are concrete enough to prototype, not generic
- [ ] Questions reference specific research findings, not platitudes
- [ ] The output is under 1,500 words
- [ ] There's a section the user can copy directly into a conversation

## Reference files

- `references/output-template.md` : Full template structure with example
- `references/sources-by-company-type.md` : Which sources matter for which product categories
- `references/query-patterns.md` : Specific search query templates that work well
