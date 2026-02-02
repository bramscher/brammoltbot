# HDPM Chatbot

**Status:** ✅ Deployed (Vercel)  
**URL:** https://hdpm-chatbot.vercel.app/  
**Repo:** https://github.com/bramscher/hdpm-chatbot (private)  
**Built:** 2026-02-02 (Claude Code)

---

## What It Is

A Next.js 14 RAG (Retrieval-Augmented Generation) chatbot that searches a knowledge base and returns AI-powered answers with inline citations.

**Primary use case:** Property management knowledge (Oregon landlord/tenant law, policy docs, training videos)

---

## Tech Stack

- **Framework:** Next.js 14 (App Router, TypeScript)
- **Database:** Supabase with pgvector extension
- **Vector Search:** pgvector (cosine similarity)
- **Embeddings:** OpenAI text-embedding-3-small (1536 dimensions)
- **Chat AI:** Claude Sonnet 4 via Anthropic API
- **UI:** Tailwind CSS + Shadcn/ui components
- **Hosting:** Vercel

---

## Features

✅ Floating chat widget (bottom right corner)  
✅ RAG system that searches Supabase/pgvector knowledge base  
✅ Inline citations [1][2][3] with clickable source links  
✅ Source type icons (⚖️ laws, 🎬 videos, 📄 docs)  
✅ Powered by Claude Sonnet 4 for responses  
✅ Auth-gated (login required)

---

## Database Schema

**Table:** `knowledge_chunks`

```sql
id              uuid (primary key)
content         text
embedding       vector(1536)
source_type     text (values: 'ors_90', 'loom_video', 'policy_doc')
source_title    text
source_url      text
source_section  text (nullable)
```

**Function:** `match_knowledge_chunks(query_embedding, threshold, count)`

Returns top N chunks by cosine similarity above threshold.

---

## RAG Flow

1. **User asks question** → "What are the late fee limits in Oregon?"
2. **Generate embedding** → OpenAI text-embedding-3-small
3. **Query Supabase** → `match_knowledge_chunks(embedding, 0.7, 5)` (top 5 results, 70% similarity threshold)
4. **Build context** → Concatenate top 5 chunk contents
5. **Call Claude Sonnet 4** → Context + question → answer
6. **Return with citations** → Inline [1][2][3] + bibliography with clickable links

---

## Project Structure

```
hdpm-chatbot/
├── app/
│   ├── api/chat/route.ts       # Chat API endpoint
│   ├── globals.css             # Global styles
│   ├── layout.tsx              # Root layout
│   └── page.tsx                # Landing page
├── components/
│   ├── ui/                     # Shadcn/ui components
│   ├── ChatWidget.tsx          # Floating chat button
│   ├── ChatWindow.tsx          # Chat interface
│   └── Message.tsx             # Message bubble with citations
├── lib/
│   ├── rag.ts                  # RAG functions
│   ├── supabase.ts             # Supabase client
│   └── utils.ts                # Utility functions
└── .env.local                  # Environment variables
```

---

## Citation Format

**Inline citations:**
> "Late fees are limited to $50 or 5%[1]"

**Bibliography:**
> [1] Oregon Revised Statutes 90.260 - Late Fees (⚖️)  
> [2] HDPM Late Fee Policy (📄)

**Source icons:**
- ⚖️ Oregon law (ors_90)
- 🎬 Loom training video (loom_video)
- 📄 Policy document (policy_doc)

---

## Next Steps (Konmashi Integration)

### Immediate (HDPM validation)
- [ ] Add property-specific knowledge (maintenance, leasing, etc.)
- [ ] Connect to Appolio API (live property data)
- [ ] Test with real HDPM tenants/owners
- [ ] Measure: response accuracy, user satisfaction

### Near-term (Agent personas)
- [ ] **Max** (Maintenance) - filter for maintenance knowledge
- [ ] **Sally** (Receptionist) - general inquiries, routing
- [ ] **Leesa** (Leasing) - focus on leasing process, availability

### Platform (Konmashi productization)
- [ ] Multi-tenant architecture (one chatbot, many PM companies)
- [ ] White-label branding (customize name, colors, logo)
- [ ] Knowledge base per tenant (upload docs, policies, local laws)
- [ ] Usage tracking (conversations, citations, satisfaction)
- [ ] Omnichannel expansion (phone, SMS, social media)

---

## Strengths

✅ **Production-ready** - deployed, auth-gated, fast  
✅ **RAG with citations** - answers are grounded in sources  
✅ **Clean UX** - floating widget, familiar chat interface  
✅ **Extensible** - clear separation (UI, API, RAG logic)  
✅ **Modern stack** - Next.js 14, Supabase, Claude Sonnet 4

---

## Questions / Decisions Needed

1. **Which agent is this?** Max, Sally, Leesa, or generic HDPM assistant?
2. **Target users?** Tenants, owners, or both?
3. **Knowledge scope?** Just Oregon law, or full HDPM operational knowledge?
4. **Phone integration?** (Vapi, Twilio, etc. for omnichannel Max/Sally/Leesa)

---

**Built by:** Craig Bramscher (Claude Code)  
**Documented by:** Brammolt  
**Last updated:** 2026-02-02
