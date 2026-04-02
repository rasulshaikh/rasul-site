# CLAUDE CODE PLAYBOOK — ELITE GTM OPERATING SYSTEM

> **153 Skills · 11 Agents · 8 Plugins · Persistent Memory · Deterministic Scripts**

---

## TABLE OF CONTENTS

1. [Architecture Overview](#1-architecture-overview)
2. [How Skills Work](#2-how-skills-work)
3. [How Agents Work](#3-how-agents-work)
4. [How to Use Everything](#4-how-to-use-everything)
5. [Command Reference](#5-command-reference)
6. [Memory System](#6-memory-system)
7. [Plugin Ecosystem](#7-plugin-ecosystem)
8. [Skills Library (Complete)](#8-skills-library-complete)
9. [Workflow Patterns](#9-workflow-patterns)
10. [Maintenance & Self-Annealing](#10-maintenance--self-annealing)

---

## 1. ARCHITECTURE OVERVIEW

Your Claude Code instance runs on a **Skills + Agents + Subagents** architecture:

```
You (Rasul) → Claude Opus → Picks Skill → Runs Script → Delivers Result
                            ↓
                       Spawns Agent for independent work
```

**Directory Structure:**
```
~/.claude/
├── CLAUDE.md           ← Operating instructions (always loaded)
├── settings.json       ← Model, plugins enabled
├── skills/             ← 153 skills (SKILL.md + scripts/)
├── agents/             ← 11 agent definitions (.md files)
├── execution/          ← Shared Python utilities
├── prompts/            ← Reusable prompt templates
├── projects/-Users-rasul/memory/  ← Persistent memory
├── .env                ← API keys
└── PLAYBOOK.md         ← This document
```

**Model:** `opus[1m]` — highest quality for complex GTM reasoning

---

## 2. HOW SKILLS WORK

A **skill** = intent + execution bundled together. Each skill has:
- `SKILL.md` — Instructions (what it does, how to use it)
- `scripts/` — Python/bash scripts (deterministic execution)
- `references/` — Supporting frameworks and templates

### How Skills Are Discovered
Claude auto-discovers all skills in `~/.claude/skills/`. When you ask for something, Claude matches your request to the right skill(s) by name and description.

### How to Trigger a Skill

**Method A: Just ask (auto-discovery)**
```
"Scrape leads from Google Maps"
→ Claude auto-triggers gmaps-leads skill
```

**Method B: Slash command**
```
/scrape-leads
→ Loads the skill explicitly
```

**Method C: Tell Claude to use a specific skill**
```
"Use gmaps-leads with city=San Francisco type=contractor"
```

### Skill Execution Flow
```
1. Claude reads SKILL.md
2. Claude identifies required scripts
3. Claude runs scripts with your parameters
4. Results go to cloud services (Smartlead, Sheets, Gmail)
5. Claude reports success/failure
```

---

## 3. HOW AGENTS WORK

An **agent** = a role-specific subagent that handles independent tasks.

Your 11 agents:

### Your Original 4
| Agent | What It Does | When It's Used |
|-------|-------------|----------------|
| `code-reviewer` | Reviews code, gives PASS/FAIL with severity-ranked issues | After writing code, before shipping |
| `qa` | Generates tests, runs them, reports pass/fail | After implementation, before deployment |
| `research` | Deep research via web search, file reads, codebase exploration | When you need investigation without context pollution |
| `email-classifier` | Classifies emails into Action Required / Waiting On / Reference | Gmail label skill uses this in parallel |

### Outbound Pipeline 7 (from janskuba/outbound-agents)
| Agent | What It Does | When It's Used |
|-------|-------------|----------------|
| `signal-scraper` | Auto-enriches company data via web search, extracts buying signals | First step of outbound pipeline |
| `lead-prioritizer` | Scores leads 1-100, assigns TIER_1-4 | After enrichment |
| `prospect-profiler` | Builds 60-second read profiles for sales reps | After prioritization |
| `hook-writer` | Crafts 120-char personalized opening lines, confidence-scored | After profiling |
| `sequence-builder` | Writes 7-touch, 21-day multi-channel outbound sequences | After hooks |
| `reply-classifier` | Classifies incoming replies by intent (INTERESTED, OBJECTION, etc.) | Anytime, independent |
| `meeting-prep` | Generates sub-500-word pre-call briefs | Before sales meetings |

---

## 4. HOW TO USE EVERYTHING

### Daily Workflow — "Tell me what you need, I handle the rest"

**You say:** *"Scrape 100 contractors in Austin"*
**I do:** Trigger `gmaps-leads` → Scrape Google Maps → Enrich websites → Extract emails → Save to Sheets

**You say:** *"Run a cold email campaign for web design services"*
**I do:** Trigger `onboarding-kickoff` → Generate leads → Create Instantly campaigns → Set up auto-reply

**You say:** *"Classify these emails"*
**I do:** Trigger `gmail-label` → Read inbox → Classify → Apply labels (Action Required / Waiting On / Reference)

### Outbound Pipeline (Full Stack)

This is your complete lead-to-meeting machine:

```
Company Names (even just names)
       ↓
  Signal Scraper     ← Auto-enriches via web search, extracts buying signals
  → 0-enriched.csv
  → 1-signals.csv
       ↓
  Lead Prioritizer   ← Scores 1-100, assigns TIER_1-4
  → 2-prioritized.csv
       ↓
  Prospect Profiler  ← Builds 60-second read profiles
  → 3-profiles.csv
       ↓
  Hook Writer        ← 120-char opening lines, confidence-scored
  → 4-hooks.csv
       ↓
  Sequence Builder    ← 7-touch, 21-day multi-channel cadences
  → 5-sequences.csv
       ↓
  Load into Instantly/Smartlead/Apollo
       ↓
  Reply Classifier   ← Classifies responses by intent (runs independently)
  → classified-replies.csv
       ↓
  Meeting Prep       ← Pre-call briefs before sales meetings
  → meeting-briefs.csv
```

**To run it:** Give me a CSV of company names. I'll run the full pipeline.

### Memory System

I have 6 persistent memories that shape every interaction:
1. **Who you are** — AI GTM Engineer at Omnibound.ai
2. **What you sell** — AI search citations, platform modules
3. **Your value prop** — 3 pillars, 4-step workflow
4. **Your tech stack** — Clay, Smartlead, 7-agent pipeline
5. **Your team** — Al, Soumitra, Abhishek
6. **Your L3 workflow** — 7-agent SEO displacement pipeline

These load automatically every session. You don't need to remind me.

### Writing + Editing Workflow
For code changes:
1. Write/edit code
2. Spawn `code-reviewer` → returns issues
3. Spawn `qa` → generates + runs tests
4. I apply fixes from both reports
5. Ship only after review + tests pass

### Video Editing
Give me a video file + instructions. Skills available:
- Remove silences + jump cuts (VAD-powered)
- Add 3D swivel transitions between cuts
- Face-swap YouTube thumbnails

---

## 5. COMMAND REFERENCE

### Slash Commands
| Command | What It Does |
|---------|-------------|
| `/scrape-leads` | Apify lead scraping pipeline |
| `/gmail-label` | Auto-label inbox |
| `/gmail-inbox` | Multi-account Gmail management |
| `/upwork-apply` | Scrape + propose on Upwork |
| `/cross-niche-outliers` | YouTube content research |
| `/youtube-outliers` | Niche viral video tracker |
| `/skool-monitor` | Skool community interaction |
| `/skool-rag` | Skool RAG queries |
| `/literature-research` | Academic paper search |
| `/modal-deploy` | Deploy to Modal |
| `/local-server` | Start local orchestrator |
| `/add-webhook` | Add Modal webhook |
| `/pan-3d-transition` | Add 3D video transitions |
| `/recreate-thumbnails` | Face-swap thumbnails |
| `/title-variants` | YouTube title generation |
| `/design-website` | Generate prospect website mockup |
| `/create-proposal` | Generate PandaDoc proposal |
| `/classify-leads` | LLM lead classification |
| `/casualize-names` | Convert formal → casual names |
| `/onboarding-kickoff` | Full client onboarding |
| `/instantly-campaigns` | Create Instantly email campaigns |
| `/instantly-autoreply` | Intelligent auto-reply |
| `/welcome-email` | Send welcome email sequence |
| `/create-memory` | Save/update persistent memory |
| `/video-edit` | Edit video (remove silences, transitions) |
| `/humanizer` | Remove AI writing patterns |
| `/generate-report` | Generate weather report PDF |
| `/gmaps-leads` | Google Maps lead scraping |
| `/help` | Get Claude Code help |

### Natural Commands (Just Talk)
You don't need slash commands. Just describe the task:

| You Say | What Happens |
|---------|-------------|
| "Find me leads" | Matches lead gen skills (gmaps-leads, scrape-leads) |
| "Write a proposal" | Triggers create-proposal |
| "Check my inbox" | Triggers gmail-label or gmail-inbox |
| "Deploy this" | Triggers modal-deploy |
| "Edit this video" | Triggers video-edit |
| "Research this topic" | Spawns research subagent |
| "Run the outbound pipeline" | Runs all 7 agents in sequence |
| "Score these leads" | Triggers lead-prioritizer agent |
| "Classify incoming replies" | Triggers reply-classifier agent |

### Built-in Claude Code Commands
| Command | What It Does |
|---------|-------------|
| `/cost` | Show session cost breakdown |
| `/plugin` | Install plugin from marketplace |
| `/plugin add skills` | Install skills from a GitHub repo |
| `/color` | Change terminal output color |
| `/export` | Export conversation to file |
| `/help` | Claude Code help |

---

## 6. MEMORY SYSTEM

**Location:** `~/.claude/projects/-Users-rasul/memory/`

### Memory Types
| Type | Purpose | Example |
|------|---------|---------|
| **User** | Who you are, how to work with you | Communication style, role |
| **Feedback** | How you like things done | "Don't mock DB in tests" |
| **Project** | Ongoing work, goals, deadlines | "Launch by Thursday" |
| **Reference** | External systems, URLs, tools | "Linear project: INGEST" |

### How to Save Memory
```
"Remember that we use Dark mode for all deliverables"
→ I write it to memory automatically
```

### How to Update Memory
```
"Update my tech stack — we switched from Smartlead to Instantly"
→ I update the relevant memory file
```

### How to Forget
```
"Remove the memory about the old domain"
→ I find and remove the specified file
```

---

## 7. PLUGIN ECOSYSTEM

**8 Plugins Enabled:**

| Plugin | What It Does |
|--------|-------------|
| **Superpowers** | Brainstorming, planning, code review, debugging, testing frameworks |
| **Firecrawl** | Web scraping, search, content extraction (replaces WebFetch/WebSearch) |
| **Playwright** | Full browser automation — click, fill forms, screenshot, snapshot |
| **Frontend Design** | Generate production-grade frontend interfaces |
| **Context7** | Fetch up-to-date library documentation for any tech stack |
| **CLAUDE.md Management** | Audit and improve CLAUDE.md files |
| **Vercel** | Deploy, manage env vars, status checks, marketplace integrations |
| **GitHub** | Repo management, PRs, issues, code review |

---

## 8. SKILLS LIBRARY (COMPLETE)

### Lead Generation (4+6=10)
| Skill | What | Scripts |
|-------|------|---------|
| `gmaps-leads` | Google Maps scraping + website contact extraction | scrape → enrich → extract → sheet |
| `scrape-leads` | Apify business scraping + LLM verification + email enrichment | apify → classify → enrich → sheet |
| `classify-leads` | LLM lead classification (SAAS vs agencies, etc.) | read_sheet → classify → update_sheet |
| `casualize-names` | Formal → casual name conversion | batch scripts for first/company/city names |
| `list-building-define-icp` | ICP definition with firmographic criteria | - |
| `list-building-source-companies` | Source companies from Apollo, Clay, HG Insights | - |
| `list-building-find-contacts` | Find decision makers via Sales Navigator + Clay | - |
| `list-building-persona-mapping` | Map buying committee personas | - |
| `list-building-qualify-accounts` | Qualify and score accounts with ICP matrix | - |
| `list-building-clean-validate` | Verify emails, manage bounce rates | - |

### Email & Campaigns (5+12=17)
| Skill | What |
|-------|------|
| `instantly-campaigns` | Create cold email campaigns in Instantly with A/B testing |
| `instantly-autoreply` | Auto-reply to Instantly threads with knowledge bases |
| `welcome-email` | 3-email welcome sequence (Nick, Peter, Sam) |
| `gmail-inbox` | Multi-account Gmail management |
| `gmail-label` | Auto-label: Action Required / Waiting On / Reference |
| `cold-email` | B2B cold emails and follow-up sequences |
| `cold-email-first-touch` | First cold email for outbound campaigns |
| `cold-email-follow-up` | Follow-up emails for non-responders |
| `cold-email-re-engagement` | Re-engage cold/lost leads |
| `cold-email-subject-lines` | Write/optimize subject lines |
| `cold-email-personalization` | Personalization at scale with AI prompts |
| `cold-email-4-sequence` | Standard 4-email sequence framework |
| `cold-email-templates-34` | 34 cold email templates library |
| `cold-email-copywriting` | Copywriting frameworks and sequence structure |
| `cold-email-email-infra` | Complete email infrastructure setup + troubleshooting |
| `cold-email-atl-messaging` | ATL (VP/C-Level/Director) email targeting |
| `cold-email-btl-messaging` | BTL (Manager/IC) email targeting |
| `email-sequence` | Drip campaigns, automated email flows |
| `email-1-variations-7` | 7 Email 1 variations + Email 2/3 templates |
| `email-metrics-benchmarks` | Email metrics tracking and 2X levers |
| `email-writing-frameworks` | 5 proven email frameworks |
| `ai-personalization-prompts` | 6 AI personalization prompts (lemlist style) |

### Sales & GTM (3+10=13)
| Skill | What |
|-------|------|
| `create-proposal` | PandaDoc proposal generation |
| `upwork-apply` | Upwork job scraping + personalized proposals |
| `onboarding-kickoff` | Full client onboarding (leads + campaigns + auto-reply) |
| `gtm-philosophy` | Core GTM principles, multi-channel strategy |
| `gtm-plays-11` | 11 GTM plays with execution templates |
| `revops` | Revenue operations, lead lifecycle, marketing-to-sales |
| `sales-enablement` | Sales decks, one-pagers, objection handling |
| `outreach-4-categories` | Inbound, Postbound, Bridgebound, Outbound |
| `inbound-triggers-30` | 30 inbound premise triggers |
| `outbound-triggers-6` | 6 outbound premise triggers |
| `bridgebound-firmographic-15` | 15 firmographic triggers |
| `bridgebound-history-16` | 16 history-based triggers |
| `bridgebound-in-market-20` | 20 in-market triggers |
| `bridgebound-relationship-39` | 39 relationship-based triggers |
| `bridgebound-symptoms-11` | 11 symptom-based triggers |

### Signal Intelligence (1+12=13)
| Skill | What |
|-------|------|
| `buying-signals-6` | 6 buying signals ranked by purchase correlation |
| `clay-buying-signals-5` | 5 buying signals for Clay workflows |
| `signal-sourcer-hiring` | Hiring signal tracking |
| `signal-sourcer-funding` | Funding round detection |
| `signal-sourcer-tech-changes` | Tech stack change tracking |
| `signal-sourcer-job-changes` | Job change signal tracking |
| `signal-sourcer-company-events` | M&A, expansion, IPO detection |
| `signal-sourcer-content-engagement` | Content engagement tracking |
| `signal-sourcer-competitor-signals` | Competitor engagement tracking |
| `signal-sourcer-website-visitors` | Website visitor identification |
| `signal-sourcer-multi-signal` | Multi-signal stacking and scoring |

### Clay Operations (10+2=12)
| Skill | What |
|-------|------|
| `clay-enrichment-9step` | 9-step Clay enrichment workflow (58+ templates) |
| `clay-table-setup` | Create/configure Clay tables |
| `clay-claygent` | Clay's AI web research agent |
| `clay-company-enrichment` | Firmographic/technographic enrichment |
| `clay-people-enrichment` | Contact enrichment and finding |
| `clay-phone-enrichment` | Phone number waterfall enrichment |
| `clay-email-waterfall` | Email waterfall enrichment setup |
| `clay-scoring` | Lead scoring in Clay |
| `clay-conditional-logic` | Clayscript formulas and conditional runs |
| `clay-debugging` | Troubleshoot Clay workflow issues |
| `clay-clay-operations` | Credit management, provider selection |

### n8n Automation (6)
| Skill | What |
|-------|------|
| `n8n-workflow-design` | Design n8n workflow architectures |
| `n8n-clay-integration` | Clay + n8n bidirectional integration |
| `n8n-crm-automation` | HubSpot/Salesforce/Slack automations |
| `n8n-triggers-webhooks` | Trigger and webhook configuration |
| `n8n-error-handling` | Error handling, retries, monitoring |
| `n8n-self-hosting` | Self-hosted n8n with Docker/PostgreSQL |

### LinkedIn (6+9=15)
| Skill | What |
|-------|------|
| `linkedin-limits-warmup` | LinkedIn limits + warm-up protocol |
| `linkedin-success-factors` | 7 success factors checklist |
| `linkedin-campaign-complete` | Complete campaign playbook |
| `linkedin-content-hooks` | High-converting hooks and first lines |
| `linkedin-content-storytelling` | Storytelling frameworks |
| `linkedin-content-engagement` | Engagement + dwell time strategy |
| `linkedin-content-formats` | Format selection + guidelines |
| `linkedin-content-cta` | CTA design + profile optimization |
| `linkedin-content-scheduling` | Posting times + frequency |
| `linkedin-content-repurposing` | Content repurposing tools |
| `linkedin-ads-abm-strategy` | LinkedIn Ads ABM strategy |
| `linkedin-ads-ads-outbound-sync` | Ads-to-outbound synchronization |
| `linkedin-ads-audiences` | Audience building + targeting |
| `linkedin-ads-bidding` | Bidding strategies + cost optimization |
| `linkedin-ads-campaign-setup` | Campaign architecture + checklists |
| `linkedin-ads-copy` | Ad copywriting frameworks |
| `linkedin-ads-creative` | Creative strategy + format selection |
| `linkedin-ads-measurement` | Attribution + conversion tracking |
| `linkedin-ads-optimization` | Troubleshooting + performance optimization |

### SEO (5+4=9)
| Skill | What |
|-------|------|
| `seo-audit` | SEO audit, technical SEO, ranking issues |
| `ai-seo` | AI search optimization, LLM citations |
| `programmatic-seo` | Template-driven SEO pages at scale |
| `schema-markup` | Structured data setup |
| `site-architecture` | Site hierarchy, URL structure, linking |
| `cross-niche-outliers` | Cross-niche YouTube content research |
| `youtube-outliers` | Niche viral video tracker |
| `title-variants` | YouTube title variations |

### Website & Conversion (6)
| Skill | What |
|-------|------|
| `page-cro` | Optimize marketing page conversions |
| `form-cro` | Form conversion optimization |
| `signup-flow-cro` | Signup/registration conversion |
| `onboarding-cro` | Post-signup onboarding optimization |
| `popup-cro` | Popup/modal/banner optimization |
| `paywall-upgrade-cro` | Paywall/upgrade screen optimization |

### Content & Marketing (8)
| Skill | What |
|-------|------|
| `content-strategy` | Content strategy and topic planning |
| `copywriting` | Marketing copy creation |
| `copy-editing` | Copy review and improvement |
| `josh-braun-copywriting` | Josh Braun's 5 cold email principles |
| `coldiq-messaging-templates` | 6 ColdIQ messaging templates |
| `personalization-6-buckets` | 6-bucket personalization framework |
| `personalization-hooks` | Strong vs lite hook patterns |
| `personalization-playbooks` | Personalization by outreach category |
| `atl-btl-messaging` | ATL vs BTL messaging framework |
| `marketing-ideas` | Marketing ideas and strategies |
| `marketing-psychology` | Psychological principles for marketing |
| `lead-magnets` | Lead magnet planning |
| `free-tool-strategy` | Free tool marketing strategy |
| `referral-program` | Referral/affiliate program design |

### Paid Ads (4)
| Skill | What |
|-------|------|
| `paid-ads` | Google Ads, Meta, LinkedIn, X campaigns |
| `ad-creative` | Ad creative generation at scale |
| `ab-test-setup` | A/B test design and implementation |
| `pricing-strategy` | Pricing decisions and monetization |

### Community (2)
| Skill | What |
|-------|------|
| `skool-monitor` | Skool community posts, replies, likes |
| `skool-rag` | Skool RAG pipeline with vector search |

### Writing & Reports (3)
| Skill | What |
|-------|------|
| `humanizer` | Remove AI writing patterns (Nick Saraev style) |
| `generate-report` | Weekly weather report PDF generation |
| `literature-research` | Academic paper search (PubMed, etc.) |

### Video & Media (4)
| Skill | What |
|-------|------|
| `video-edit` | Remove silences + 3D swivel transitions |
| `pan-3d-transition` | 3D pan/swivel video transitions |
| `recreate-thumbnails` | Face-swap YouTube thumbnails with AI |
| `pan-3d-transition` | 3D pan/swivel video transitions |

### Infrastructure (4)
| Skill | What |
|-------|------|
| `modal-deploy` | Deploy scripts to Modal cloud |
| `local-server` | Run Claude orchestrator locally |
| `add-webhook` | Add Modal webhooks |
| `design-website` | Premium prospect website mockups |

### Custom (1)
| Skill | What |
|-------|------|
| `create-memory` | Save/update/remove persistent memories |
| `churn-prevention` | Reduce churn, save offers, retention |
| `customer-research` | Customer research and synthesis |
| `lead-sources-guide` | Lead sources with Clay templates |
| `list-building-tips` | Pro tips for B2B list building |

---

## 9. WORKFLOW PATTERNS

### Pattern A: Client Onboarding (Full Stack)
```
1. "Onboard new client: [name, email, company]"
   → onboarding-kickoff runs all: lead gen → campaigns → autoreply
2. "Send welcome sequence"
   → welcome-email sends 3 emails (Nick, Peter, Sam)
3. "Classify their inbox"
   → gmail-label sorts incoming emails
```

### Pattern B: Lead Generation Pipeline
```
1. "Find contractors in [city]"
   → gmaps-leads scrapes → enriches → saves to sheets
2. "Run the full outbound pipeline"
   → signal-scraper → prioritizer → profiler → hooks → sequences
3. "Classify incoming replies"
   → reply-classifier sorts by intent + suggests next actions
```

### Pattern C: YouTube Content Strategy
```
1. "Find viral videos in my niche"
   → youtube-outliers scrapes + analyzes
2. "Find cross-niche inspiration"
   → cross-niche-outliers finds adjacent content patterns
3. "Generate title variants"
   → title-variants creates options from outliers
```

### Pattern D: Code Development
```
1. "Build [feature]"
   → brainstorming → plan → implementation
2. "Review the code"
   → code-reviewer agent + qa agent in parallel
3. "Deploy"
   → modal-deploy or vercel
```

### Pattern E: Proposal + Sales
```
1. "Create a proposal for [client]"
   → create-proposal generates PandaDoc
2. "Prep me for a meeting with [company]"
   → meeting-prep agent generates brief
```

---

## 10. MAINTENANCE & SELF-ANNEALING

### Self-Annealing Protocol
When something breaks:
1. Read the error
2. Fix the script
3. Test again
4. Update the SKILL.md with what I learned
5. System is now stronger

### Keep Your Skills Updated
- New skills via: `npx skills add <github-repo>`
- Update existing skills: check `~/.claude/skills/<skill>/SKILL.md` dates
- Remove stale skills: I delete from `~/.claude/skills/`

### Session Tips
- Long conversations get auto-summarized — start fresh for new tasks
- Use subagents in parallel for independent tasks (I do this automatically)
- Memory persists across sessions — I remember who you are and what you've told me
- CLAUDE.md is loaded every session — your operating instructions are always active

### Files to Watch
| File | What to Update |
|------|---------------|
| `CLAUDE.md` | Operating instructions, rules, preferences |
| `settings.json` | Model, plugins |
| `.env` | API keys |
| `memory/*.md` | Role, feedback, project context |

---

*Built for Rasul — AI GTM Engineer at Omnibound.ai*
*Last audited: 2026-04-02*
