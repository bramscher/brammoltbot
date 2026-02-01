# Notion Time Blocking Template Setup

## Database Structure

### 1. Create "Weekly Plan" Database

**Properties:**
- **Task** (Title) - What needs to happen
- **Day** (Select) - Mon, Tue, Wed, Thu, Fri, Sat, Sun
- **Time Block** (Select) - Deep Work, Meetings, Delegation, Admin, Personal, Flex
- **Start Time** (Date with time)
- **Duration** (Number) - in minutes
- **Status** (Select) - Planned, In Progress, Done, Moved
- **Type** (Select) - Brammo Only, Delegated, Collaborative
- **Assigned To** (Person/Text) - Who's doing it
- **Priority** (Select) - Critical, High, Medium, Low
- **Brammo Trap?** (Checkbox) - Flag if you're doing something you shouldn't

**Color Coding (by Time Block):**
- 🔵 Deep Work = Blue
- 🟢 Meetings = Green  
- 🟡 Delegation = Yellow
- ⚪ Admin = Gray
- 🏠 Personal = Purple
- 🔴 Flex = Red

---

## Views to Create

### View 1: **Weekly Board** (Board by Day)
- Group by: Day
- Sort by: Start Time
- Filter: This week only
- Drag cards between days

### View 2: **Time Block View** (Board by Time Block)
- Group by: Time Block
- Shows distribution across Deep Work/Meetings/etc
- Helps you see if you're over-allocated in meetings

### View 3: **Brammo Traps** (Table)
- Filter: "Brammo Trap?" = Checked
- Shows everything you're doing that you shouldn't
- Review weekly

### View 4: **Delegation Queue** (Table)
- Filter: Type = Delegated
- Group by: Assigned To
- Shows what you've handed off and to whom

### View 5: **Today** (List)
- Filter: Day = Today
- Sort by: Start Time
- Your daily dashboard

---

## Calendar Integration

**Link to Notion Calendar:**
1. Open Notion Calendar (calendar.notion.com)
2. Connect your Weekly Plan database
3. Map "Start Time" to calendar events
4. Color code by Time Block

**Result:** Your Notion database shows as calendar blocks you can drag/resize

---

## Daily Workflow

**Morning (5 min):**
1. Open "Today" view
2. Drag tasks from "Weekly Board" into time slots
3. Check for Brammo Traps
4. Set start times

**During day:**
- Update Status as you go
- Flag Brammo Traps when you catch yourself
- Move cards if things shift

**End of day (2 min):**
- Mark Done
- Move unfinished to tomorrow or Flex

---

## Weekly Workflow

**Sunday Planning (30 min):**
1. Clear last week's Done items
2. Review "Brammo Traps" - what pattern?
3. Drag upcoming tasks into Weekly Board
4. Block Deep Work first (mornings)
5. Batch meetings (afternoons)
6. Protect Personal blocks

**Friday Review (15 min):**
1. Check Delegation Queue - what landed?
2. Count hours: Deep Work vs Meetings vs Brammo Traps
3. Update accountability metrics

---

## Template Structure

Create this as a **Notion Template Button:**

```
Template Name: "New Week"

Auto-fills:
- Monday-Friday swim lanes
- Pre-blocked Deep Work (8-10am, 10:30am-12pm)
- Pre-blocked Delegation check-in (10-10:30am daily)
- Pre-blocked Meetings zone (1-3pm)
- Pre-blocked Admin (3-4pm)
- Pre-blocked Flex (4-5pm)
```

Hit the button every Sunday, drag your tasks in.

---

## Quick Start

1. Create database with properties above
2. Create the 5 views
3. Link to Notion Calendar
4. Create template button
5. Hit button, start using TODAY

No coding. No building. Just setup and go. 🎯

