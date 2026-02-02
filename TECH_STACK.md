# Tech Stack Preferences

**Craig's default stack for all projects.**

---

## Framework

**Next.js** (App Router, TypeScript)
- Modern, fast, great DX
- Server components + API routes
- Vercel deployment

---

## Database

**Supabase**
- PostgreSQL (SQL)
- pgvector extension (vector embeddings)
- Built-in auth, real-time, storage
- Great Next.js integration

---

## AI Integration

**Any provider, context-dependent:**
- Anthropic (Claude) - reasoning, long context
- OpenAI - embeddings, function calling
- Google (Gemini) - web search, research
- xAI (Grok) - social search

**Always use RAG when dealing with knowledge bases** (vector search + LLM).

---

## Design Aesthetic

**Apple Glassmorphism / Liquid Glass**
- Modern, clean, minimal
- Frosted glass effects (backdrop-blur)
- Subtle transparency
- Smooth animations
- Light/shadow depth
- Clean typography

**UI Libraries:**
- Tailwind CSS (utility-first)
- Shadcn/ui (accessible components)
- Framer Motion (animations)

**Color philosophy:**
- Clean, neutral base
- Accent colors used sparingly
- Dark mode first (or support both)

---

## Deployment

**Vercel** (Next.js native hosting)
- Automatic deployments from GitHub
- Preview environments per branch
- Edge functions, analytics

---

## Authentication

**Supabase Auth** (when needed)
- Email/password
- OAuth (Google, GitHub, etc.)
- Magic links
- Built-in session management

---

## File Storage

**Supabase Storage** (when needed)
- S3-compatible
- Public/private buckets
- Direct uploads from client

---

## Real-time (when needed)

**Supabase Realtime**
- WebSocket subscriptions
- Database changes
- Presence (who's online)

---

## Examples in Production

### HDPM Chatbot
- ✅ Next.js 14
- ✅ Supabase (pgvector for RAG)
- ✅ Claude Sonnet 4 (chat AI)
- ✅ OpenAI (embeddings)
- ✅ Shadcn/ui components
- ✅ Clean, modern UI (glassmorphism coming)

---

**Default answer for "What stack should we use?":**

> Next.js + Supabase + AI integration + Glassmorphism aesthetic

**Last updated:** 2026-02-02
