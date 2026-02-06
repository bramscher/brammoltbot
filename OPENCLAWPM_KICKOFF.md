# OpenClawPM — Project Kickoff

**Project:** OpenClaw SaaS Platform for Property Management  
**Pilot Customer:** HDPM  
**Status:** In Design → MVP Sprint 1

*OpenClawPM is a managed SaaS frontend + control plane specifically built for property management companies to deploy, configure, and manage OpenClaw instances with no code.*

---

## Tech Stack (Locked)

- **Framework:** Next.js (App Router, TypeScript)
- **Database:** Supabase (PostgreSQL + pgvector for embeddings)
- **Frontend:** React (modern, functional)
- **UI/Design:** Apple liquid glass / modern glassmorphism aesthetic
- **Styling:** Tailwind CSS + Shadcn/ui components
- **Deployment:** Vercel
- **Version Control:** GitHub
- **State Management:** React Query / TanStack Query
- **Auth:** Supabase Auth (email/magic link, OAuth)

---

## Architecture

```
┌────────────────────────────────────┐
│   Frontend (Next.js App Router)    │
│   Vercel Deployment                │
│   Glassmorphism UI / Shadcn        │
└──────────────┬─────────────────────┘
               │
┌──────────────▼─────────────────────┐
│   API Routes (Next.js /api)        │
│   - Instance management            │
│   - Agent CRUD                     │
│   - Knowledge base operations      │
│   - Analytics aggregation          │
└──────────────┬─────────────────────┘
               │
┌──────────────▼─────────────────────┐
│   Supabase (PostgreSQL + pgvector) │
│   - Users, org, team               │
│   - Agent configs                  │
│   - Knowledge base vectors         │
│   - Conversation logs              │
│   - Analytics snapshots            │
└────────────────────────────────────┘
               │
       ┌───────┴────────┐
       │                │
   ┌───▼──┐        ┌───▼──────┐
   │ Auth │        │ Realtime  │
   │      │        │ (websocket│
   └──────┘        │ optional) │
                   └───────────┘
```

---

## Database Schema (Initial)

### Core Tables

```sql
-- Users & Organizations
CREATE TABLE orgs (
  id UUID PRIMARY KEY,
  name TEXT,
  slug TEXT UNIQUE,
  owner_id UUID REFERENCES auth.users,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE users_orgs (
  user_id UUID REFERENCES auth.users,
  org_id UUID REFERENCES orgs,
  role TEXT ('admin', 'agent_builder', 'viewer'), -- RBAC
  created_at TIMESTAMP DEFAULT NOW(),
  PRIMARY KEY (user_id, org_id)
);

-- OpenClaw Instances (one per org, or multiple for advanced)
CREATE TABLE instances (
  id UUID PRIMARY KEY,
  org_id UUID REFERENCES orgs,
  name TEXT,
  gateway_url TEXT,
  gateway_token TEXT (encrypted),
  status TEXT ('running', 'stopped', 'error'),
  last_heartbeat TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Agents
CREATE TABLE agents (
  id UUID PRIMARY KEY,
  org_id UUID REFERENCES orgs,
  instance_id UUID REFERENCES instances,
  name TEXT,
  description TEXT,
  system_prompt TEXT,
  emoji TEXT,
  model TEXT DEFAULT 'anthropic/claude-sonnet-4-5',
  temperature NUMERIC DEFAULT 0.7,
  tools_enabled JSONB DEFAULT '[]',
  knowledge_base_ids UUID[] DEFAULT '{}',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Knowledge Bases
CREATE TABLE knowledge_bases (
  id UUID PRIMARY KEY,
  org_id UUID REFERENCES orgs,
  name TEXT,
  description TEXT,
  type TEXT ('pdf', 'webpage', 'github', 'notion', 'text'),
  source_url TEXT,
  file_path TEXT,
  chunk_strategy JSONB, -- {chunk_size, overlap}
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Vector embeddings (for RAG)
CREATE TABLE embeddings (
  id UUID PRIMARY KEY,
  knowledge_base_id UUID REFERENCES knowledge_bases ON DELETE CASCADE,
  chunk_text TEXT,
  metadata JSONB,
  embedding VECTOR(1536), -- OpenAI embedding dimension
  created_at TIMESTAMP DEFAULT NOW()
);

-- Conversation logs
CREATE TABLE conversations (
  id UUID PRIMARY KEY,
  org_id UUID REFERENCES orgs,
  agent_id UUID REFERENCES agents,
  user_id UUID,
  channel TEXT ('telegram', 'whatsapp', 'slack', etc),
  messages JSONB, -- array of {role, content, timestamp}
  tokens_used INT,
  cost NUMERIC,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Analytics snapshots (denormalized for fast queries)
CREATE TABLE analytics_snapshots (
  id UUID PRIMARY KEY,
  org_id UUID REFERENCES orgs,
  date DATE,
  agent_id UUID REFERENCES agents,
  conversations_count INT,
  tokens_total INT,
  cost_total NUMERIC,
  avg_response_time_ms NUMERIC,
  user_satisfaction NUMERIC,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### Indexes
```sql
CREATE INDEX idx_agents_org ON agents(org_id);
CREATE INDEX idx_instances_org ON instances(org_id);
CREATE INDEX idx_kb_org ON knowledge_bases(org_id);
CREATE INDEX idx_embeddings_kb ON embeddings(knowledge_base_id);
CREATE INDEX idx_embeddings_vector ON embeddings USING ivfflat (embedding vector_cosine_ops);
CREATE INDEX idx_conversations_org_agent ON conversations(org_id, agent_id);
CREATE INDEX idx_analytics_org_date ON analytics_snapshots(org_id, date);
```

---

## MVP Features (Sprint 1 - 4 weeks)

### Dashboard
- [ ] Org overview (total agents, conversations this month, cost)
- [ ] Instance health (gateway status, last heartbeat)
- [ ] Quick links (create agent, upload KB, view logs)

### Agent Builder
- [ ] Create agent (name, description, emoji, system prompt form)
- [ ] Edit agent (all fields)
- [ ] Delete agent
- [ ] Agent list view (with edit/delete actions)
- [ ] Model selection dropdown (Sonnet default, show Haiku/Opus options)
- [ ] Enable/disable tools (checkboxes for each available skill)
- [ ] Assign knowledge bases (multi-select from existing KBs)

### Knowledge Base Management
- [ ] Upload PDF (auto-chunk, auto-embed with pgvector)
- [ ] Add webpage (fetch, chunk, embed)
- [ ] View KB list (with source, size, last updated)
- [ ] Delete KB
- [ ] Test search (preview: "what does the lease say about..." → retrieve top chunks)

### Configuration
- [ ] Connect instance (paste gateway URL + token)
- [ ] Model selection (primary + fallback)
- [ ] Channel management (list available channels from instance)
- [ ] API keys vault (show/hide, regenerate)

### Analytics
- [ ] Conversation count (chart: last 30 days)
- [ ] Token usage (stacked bar: per agent, per day)
- [ ] Cost breakdown (pie: agent spend %)
- [ ] Average response time (trend)

### Auth
- [ ] Sign up (email)
- [ ] Sign in (magic link)
- [ ] Team invite (copy link with role selection)
- [ ] Role management (admin, agent_builder, viewer)

---

## Design System (Glassmorphism)

### Color Palette
- **Primary:** Modern blue (Apple ecosystem, #0071E3 or similar)
- **Accent:** Bright (supporting interactions)
- **Background:** Deep dark (charcoal, #0F1419 or white for light mode)
- **Glass:** Semi-transparent white on dark (rgba(255,255,255,0.1))
- **Border:** Subtle gradients, high blur

### Components
- Cards: Glass effect (backdrop-blur, border with gradient)
- Buttons: Glassmorphic with hover state (more opaque)
- Inputs: Glass panels with subtle focus glow
- Modals: Full-screen frosted glass overlay
- Navigation: Top bar (glass) with breadcrumbs

### Shadcn/ui Integration
- Customize Shadcn components with glass styling
- Use Tailwind `backdrop-blur`, `border-opacity`, gradients

---

## API Routes (MVP)

```
POST   /api/auth/signup
POST   /api/auth/signin
POST   /api/auth/logout

GET    /api/dashboard
POST   /api/agents
GET    /api/agents
PATCH  /api/agents/[id]
DELETE /api/agents/[id]

POST   /api/knowledge-bases
GET    /api/knowledge-bases
DELETE /api/knowledge-bases/[id]
POST   /api/knowledge-bases/[id]/search  (test search)

GET    /api/instances/[id]
POST   /api/instances/[id]/verify

GET    /api/analytics/conversations
GET    /api/analytics/tokens
GET    /api/analytics/cost

POST   /api/invite
GET    /api/team
PATCH  /api/team/[user_id]/role
```

---

## Repository Setup

```bash
# Create repo on GitHub
git init
git remote add origin https://github.com/bramscher/konmashi-control-plane.git
git branch -M main

# Directory structure
konmashi-control-plane/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   ├── dashboard/
│   ├── agents/
│   ├── knowledge-bases/
│   ├── settings/
│   └── api/
│       ├── auth/
│       ├── agents/
│       ├── knowledge-bases/
│       ├── analytics/
│       └── instances/
├── components/
│   ├── ui/          (Shadcn)
│   ├── Layout.tsx
│   ├── Sidebar.tsx
│   └── ...
├── lib/
│   ├── supabase.ts
│   ├── auth.ts
│   └── utils.ts
├── styles/
│   └── globals.css  (glass effects)
├── .env.local
├── next.config.ts
├── tailwind.config.ts
└── tsconfig.json
```

---

## Deployment (Vercel)

1. Connect GitHub repo to Vercel
2. Set environment variables:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `SUPABASE_SERVICE_KEY`
3. Deploy to `konmashi.vercel.app` (or custom domain)

---

## Timeline (Estimated)

- **Week 1-2:** Supabase setup, Next.js scaffolding, auth
- **Week 2-3:** Dashboard, agent CRUD, KB upload
- **Week 3-4:** Analytics, config panel, polish

**Target:** Live for HDPM testing by end of Month 1

---

## Next Steps

1. Create GitHub repo
2. Initialize Next.js project with Tailwind + Shadcn
3. Set up Supabase project & schema
4. Build auth flow
5. Scaffold main dashboard + sidebar
6. Start Sprint 1

Ready to go?
