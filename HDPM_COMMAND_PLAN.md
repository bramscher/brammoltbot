# HDPM Command - Property Management Operations Platform

**OpenClaw-inspired business operations system for HDPM Inc.**

## Vision

A comprehensive property management platform that gives every HDPM employee instant access to:
- Complete business knowledge base
- Real-time KPIs and reporting
- Integration with Konmashi AI agents
- Property/tenant operations
- Appfolio data sync
- Task and maintenance tracking

## Core Modules

### 1. Knowledge Base 📚
**The Brain of HDPM**
- SOPs and processes
- Property information
- Vendor contacts
- Training materials
- Legal/compliance docs
- AI-powered search (RAG)
- Markdown + PDF support
- Version history

### 2. KPI Dashboard 📊
**Real-time Business Metrics**
- Occupancy rates by property
- Maintenance response times
- Tenant satisfaction scores
- Revenue per property
- Expense tracking
- Lead conversion rates
- Marketing performance
- Custom metric builder

### 3. Property Management 🏢
**Operations Hub**
- Property profiles
- Unit/tenant management
- Maintenance requests
- Lease tracking
- Move-in/move-out workflows
- Inspection schedules
- Document storage

### 4. Konmashi Integration 🤖
**AI Agent Coordination**
- Max (Maintenance) status
- Sally (Receptionist) activity
- Leesa (Leasing) pipeline
- Agent performance metrics
- Content calendar
- Video production queue
- Social media analytics

### 5. Appfolio Sync 🔄
**Data Integration**
- Property data sync
- Tenant information
- Financial reports
- Maintenance requests
- Lease documents
- Payment tracking
- Two-way updates

### 6. Task Management ✅
**Operations Coordination**
- Team task assignments
- Maintenance workflows
- Vendor coordination
- Inspection checklists
- Follow-up reminders
- Priority management

### 7. Reporting & Analytics 📈
**Business Intelligence**
- Custom report builder
- Export to Excel/PDF
- Scheduled reports
- Trend analysis
- Comparative analytics
- Forecasting tools

### 8. Team Collaboration 👥
**Employee Portal**
- Role-based access
- Internal messaging
- Shift scheduling
- Training progress
- Performance reviews
- Document sharing

## Technical Architecture

### Stack (Craig's Preferences)
```
Framework: Next.js 15 (App Router, TypeScript)
Database: Supabase (PostgreSQL + pgvector for RAG)
UI: Tailwind CSS + shadcn/ui
Design: Apple glassmorphism aesthetic
AI: OpenAI / Anthropic for RAG
Search: pgvector for semantic search
Real-time: Supabase Realtime
Auth: Supabase Auth (multi-user)
Deployment: Vercel
```

### Key Features
- **RAG Knowledge Base** - Semantic search across all company docs
- **Real-time Updates** - Supabase subscriptions for live data
- **Role-Based Access** - Employees see only what they need
- **Mobile-First** - On-site access for maintenance/inspections
- **Offline Capable** - PWA for field work
- **API-First** - Easy integration with Konmashi, Appfolio, etc.

## Phase 1: MVP (Week 1-2)

**Core Infrastructure**
- [ ] Next.js + Supabase setup
- [ ] Authentication & user roles
- [ ] Basic UI with glassmorphism
- [ ] Property database schema
- [ ] KPI dashboard skeleton

**Knowledge Base**
- [ ] Document upload (PDF, markdown, docs)
- [ ] Basic search
- [ ] Category organization
- [ ] Access controls

**Properties Module**
- [ ] Property CRUD
- [ ] Basic property profiles
- [ ] Unit/tenant listing

## Phase 2: Intelligence (Week 3-4)

**Advanced Knowledge Base**
- [ ] RAG implementation (pgvector)
- [ ] Semantic search
- [ ] AI-powered Q&A
- [ ] Related documents

**KPI System**
- [ ] Metric tracking
- [ ] Dashboard widgets
- [ ] Real-time updates
- [ ] Custom metrics

**Appfolio Integration**
- [ ] API connection
- [ ] Data sync
- [ ] Webhook handling

## Phase 3: Konmashi Integration (Week 5-6)

**AI Agent Portal**
- [ ] Max/Sally/Leesa status boards
- [ ] Performance metrics
- [ ] Content pipeline view
- [ ] Social media integration

**Advanced Reporting**
- [ ] Report builder
- [ ] Export functionality
- [ ] Scheduled reports
- [ ] Analytics dashboard

## Phase 4: Operations (Week 7-8)

**Task Management**
- [ ] Team workflows
- [ ] Maintenance tracking
- [ ] Vendor coordination
- [ ] Notifications

**Team Features**
- [ ] Employee profiles
- [ ] Messaging system
- [ ] Training modules
- [ ] Performance tracking

## Database Schema

### Core Tables
```sql
-- Properties
properties
  - id, name, address, type
  - units_count, occupancy_rate
  - manager_id, status

-- Units
units
  - id, property_id, unit_number
  - bedrooms, bathrooms, sqft
  - rent_amount, status

-- Tenants
tenants
  - id, name, email, phone
  - unit_id, lease_start, lease_end
  - status

-- Knowledge Base
documents
  - id, title, content, type
  - category, access_level
  - embedding (vector)

-- KPIs
metrics
  - id, name, value, property_id
  - period, target
  - timestamp

-- Tasks
tasks
  - id, title, description
  - assigned_to, property_id
  - status, priority, due_date

-- AI Agents (Konmashi)
agent_activities
  - id, agent_name, activity_type
  - property_id, performance_data
  - timestamp
```

## Integration Points

### Konmashi API
- Agent status updates
- Content calendar
- Performance metrics
- Lead tracking

### Appfolio API
- Property/tenant sync
- Financial data
- Maintenance requests
- Document management

### Future Integrations
- QuickBooks (accounting)
- Mailchimp (marketing)
- Twilio (SMS notifications)
- Zapier (automation)

## UI/UX Design

**Design System**
- Apple glassmorphism throughout
- Dark mode support
- Responsive (mobile-first)
- Quick actions everywhere
- Contextual search
- Keyboard shortcuts

**Key Screens**
1. Dashboard - KPIs at a glance
2. Knowledge Base - Search + browse
3. Properties - Map + list view
4. Konmashi - Agent status board
5. Reports - Interactive analytics
6. Tasks - Team coordination
7. Profile - Employee portal

## Success Metrics

**Adoption**
- All employees using daily
- 90%+ knowledge base search success rate
- <5 minute average task completion

**Business Impact**
- Faster response times
- Better tenant satisfaction
- Increased efficiency
- Data-driven decisions

**Technical**
- <2 second page loads
- 99.9% uptime
- Real-time updates (<1s latency)
- Mobile performance

## Rollout Strategy

**Phase 1: Internal Beta**
- Craig + 2-3 key employees
- Knowledge base + KPIs only
- Gather feedback

**Phase 2: Team Rollout**
- All HDPM employees
- Full feature set
- Training sessions

**Phase 3: Optimization**
- User feedback integration
- Performance tuning
- Advanced features

## Competitive Advantages

vs. Standard Property Management Software:
- ✅ AI-powered knowledge base
- ✅ Konmashi integration (unique!)
- ✅ Modern, fast UI
- ✅ Mobile-optimized
- ✅ Real-time everything
- ✅ Custom KPIs
- ✅ Built for HDPM's workflow

## Budget & Timeline

**Development Time**: 8-10 weeks MVP
**Ongoing**: Iteration based on use

**Cost Savings**:
- Eliminate multiple tools
- Faster training
- Better decision-making
- Scalable as HDPM grows

---

**Next Steps:**
1. Approve architecture
2. Set up project repo
3. Build Phase 1 MVP
4. Internal testing
5. Iterate based on feedback

**Goal**: HDPM becomes the most efficient, data-driven property management company in Bend, OR - powered by AI and modern tech.
