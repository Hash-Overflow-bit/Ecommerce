# 🏗️ Full-Stack Architecture Guide
### *Everything Connected — From Your Editor to the Database*

![Architecture Overview](C:\Users\Hashir Mehboob\.gemini\antigravity\brain\362439cf-b9ab-4021-8245-3c274c01ee06\architecture_hero_1778504832755.png)

> [!NOTE]
> This guide is written for **non-technical readers**. Every concept is explained with simple analogies, visual diagrams, and zero jargon.

---

## 📋 Table of Contents

1. [The Big Picture — How Everything Connects](#-the-big-picture)
2. [Cursor AI vs Claude Code — When to Use What?](#-cursor-ai-vs-claude-code)
3. [How to Connect Anthropic API in Cursor (CLI Agent)](#-connecting-anthropic-api-in-cursor)
4. [What is Supabase and How to Connect It](#-supabase--your-cloud-database)
5. [Where to Find Supabase API Keys](#-finding-your-supabase-api-keys)
6. [What is Drizzle ORM and Why Use It?](#-drizzle-orm--the-translator)
7. [API Keys Cheat Sheet — Which Key Does What?](#-api-keys-cheat-sheet)
8. [The Complete Flow — Step by Step](#-the-complete-flow)
9. [Who Pays for What? — Token & Billing Guide](#-who-pays-for-what--token--billing-guide)

---

## 🌍 The Big Picture

Think of building a web app like building a **restaurant**:

| Real World Analogy | Tech Equivalent | Purpose |
|---|---|---|
| 🍳 **The Kitchen** | **Cursor AI IDE** | Where you prepare (write) everything |
| 👨‍🍳 **The Chef** | **Claude Code CLI** | The expert that does the cooking (coding) for you |
| 📋 **Recipe Book** | **Anthropic API Key** | The Chef's license — proves they're authorized to work |
| 🗄️ **The Pantry/Fridge** | **Supabase** | Where all your ingredients (data) are stored |
| 🏷️ **Pantry Key** | **Supabase API Keys** | The keys to access your pantry |
| 📝 **The Menu Translator** | **Drizzle ORM** | Translates your orders into pantry language |

### Master Architecture Diagram

```mermaid
graph TB
    subgraph YOU["👤 YOU (The Developer)"]
        direction LR
        A["🖥️ Cursor AI IDE<br/><i>Your Workspace</i>"]
    end

    subgraph AI_LAYER["🤖 AI LAYER"]
        direction LR
        B["🧠 Claude Code CLI<br/><i>AI Agent in Terminal</i>"]
        C["🔑 Anthropic API Key<br/><i>Activates Claude</i>"]
    end

    subgraph DATA_LAYER["💾 DATA LAYER"]
        direction LR
        D["🗄️ Supabase<br/><i>Cloud Database</i>"]
        E["📝 Drizzle ORM<br/><i>Database Translator</i>"]
    end

    subgraph KEYS["🔐 API KEYS"]
        direction LR
        F["🟢 SUPABASE_URL<br/><i>Database Address</i>"]
        G["🟠 SUPABASE_ANON_KEY<br/><i>Public Access Key</i>"]
        H["🔴 SUPABASE_SERVICE_KEY<br/><i>Admin Access Key</i>"]
    end

    A -->|"Open Terminal"| B
    C -->|"Authorizes"| B
    B -->|"Writes Code"| A
    A -->|"Your Code Uses"| E
    E -->|"Talks To"| D
    F & G & H -->|"Stored in .env file"| A

    style YOU fill:#1a1a2e,stroke:#00d2ff,stroke-width:2px,color:#fff
    style AI_LAYER fill:#16213e,stroke:#a855f7,stroke-width:2px,color:#fff
    style DATA_LAYER fill:#0f3460,stroke:#22c55e,stroke-width:2px,color:#fff
    style KEYS fill:#1a1a2e,stroke:#f59e0b,stroke-width:2px,color:#fff
```

---

## 🤖 Cursor AI vs Claude Code

![Cursor vs Claude Comparison](C:\Users\Hashir Mehboob\.gemini\antigravity\brain\362439cf-b9ab-4021-8245-3c274c01ee06\cursor_vs_claude_1778504848024.png)

### The Simple Analogy

> **Cursor AI** = Your **office desk** with all your tools laid out  
> **Claude Code CLI** = A **brilliant assistant** sitting next to you, doing the work you describe

### When to Use Which?

```mermaid
graph LR
    subgraph CURSOR["🖥️ USE CURSOR AI WHEN..."]
        C1["📂 Browsing project files"]
        C2["✏️ Making small manual edits"]
        C3["👁️ Visually reviewing code"]
        C4["🏃 Running your app"]
        C5["🔍 Searching through code"]
    end

    subgraph CLAUDE["🧠 USE CLAUDE CODE WHEN..."]
        CL1["🏗️ Building entire features"]
        CL2["🐛 Debugging complex issues"]
        CL3["📦 Setting up project structure"]
        CL4["🔄 Refactoring large codebases"]
        CL5["📖 Explaining code to you"]
    end

    style CURSOR fill:#1e3a5f,stroke:#00d2ff,stroke-width:2px,color:#fff
    style CLAUDE fill:#2d1b4e,stroke:#a855f7,stroke-width:2px,color:#fff
```

### Side-by-Side Comparison

| Feature | 🖥️ Cursor AI IDE | 🧠 Claude Code CLI |
|---|---|---|
| **What is it?** | A code editor (like Word, but for code) | An AI agent that lives in your terminal |
| **How you talk to it** | Click buttons, type in editor | Type natural language commands |
| **Best for** | Seeing & organizing your project | Building & fixing things |
| **Needs API key?** | Has its own built-in AI | Yes — needs Anthropic API key |
| **Think of it as** | Your desk & monitor | Your expert assistant |

> [!IMPORTANT]
> **They work TOGETHER, not against each other!** You open Cursor AI → then launch Claude Code inside Cursor's terminal → Claude writes code directly into your Cursor project.

### How They Work Together — Flow

```mermaid
sequenceDiagram
    actor You as 👤 You
    participant Cursor as 🖥️ Cursor AI IDE
    participant Terminal as ⬛ Terminal (inside Cursor)
    participant Claude as 🧠 Claude Code CLI

    You->>Cursor: Open your project folder
    You->>Cursor: Press Ctrl + ` (backtick) to open terminal
    You->>Terminal: Type: claude
    Terminal->>Claude: Claude Code starts up ✨
    You->>Claude: "Build me a login page with Supabase"
    Claude->>Cursor: Creates files & writes code
    You->>Cursor: See the new files appear in sidebar!
    You->>Cursor: Click "Run" to see your app
```

---

## 🔗 Connecting Anthropic API in Cursor

> This is what makes Claude Code work. Without the API key, Claude Code won't start.

### What is an API Key?

> Think of it as a **membership card** 🪪. When you go to a gym, you swipe your card to get in. The API key is Claude's "membership card" that proves you're allowed to use it.

### Step-by-Step Setup

```mermaid
graph TD
    A["1️⃣ Go to console.anthropic.com"] --> B["2️⃣ Create an account / Sign in"]
    B --> C["3️⃣ Click 'API Keys' in sidebar"]
    C --> D["4️⃣ Click 'Create Key'"]
    D --> E["5️⃣ Copy the key<br/><i>⚠️ You can only see it ONCE!</i>"]
    E --> F["6️⃣ Open Cursor AI IDE"]
    F --> G["7️⃣ Open Terminal: Ctrl + backtick"]
    G --> H["8️⃣ Set the key in terminal"]
    H --> I["9️⃣ Type 'claude' to start!"]

    style A fill:#1a1a2e,stroke:#a855f7,stroke-width:2px,color:#fff
    style E fill:#1a1a2e,stroke:#ef4444,stroke-width:2px,color:#fff
    style I fill:#1a1a2e,stroke:#22c55e,stroke-width:2px,color:#fff
```

### The Commands (Copy-Paste These)

**Step 8 — Set your API key in the terminal:**
```bash
# On Windows (PowerShell) — paste this, replacing YOUR_KEY:
$env:ANTHROPIC_API_KEY = "sk-ant-xxxxx-YOUR-KEY-HERE"

# On Mac/Linux — paste this, replacing YOUR_KEY:
export ANTHROPIC_API_KEY="sk-ant-xxxxx-YOUR-KEY-HERE"
```

**Step 9 — Start Claude Code:**
```bash
claude
```

> [!TIP]
> To make the API key permanent (so you don't type it every time), add it to your system's Environment Variables. On Windows: **Settings → System → Advanced → Environment Variables → New** → Name: `ANTHROPIC_API_KEY`, Value: your key.

### Where Does the API Key Come From?

| Step | Where to Go | What to Do |
|---|---|---|
| 1 | 🌐 [console.anthropic.com](https://console.anthropic.com) | Create account or sign in |
| 2 | Left sidebar → **API Keys** | Navigate to the keys page |
| 3 | Click **"Create Key"** button | Generate a new key |
| 4 | 📋 Copy the key immediately | **You won't see it again!** |
| 5 | 🖥️ Cursor AI → Terminal | Paste the command above |

---

## 🗄️ Supabase — Your Cloud Database

### What is Supabase?

> **Supabase = Your online storage locker** 🗄️  
> Just like Google Drive stores your documents, Supabase stores your app's data (users, posts, orders, etc.) in organized tables.

### Why Supabase?

```mermaid
graph LR
    subgraph WHY["✅ Why Choose Supabase?"]
        A["🆓 Free tier available"]
        B["☁️ Cloud-hosted — no server setup"]
        C["🔐 Built-in user login system"]
        D["📊 Visual table editor"]
        E["⚡ Real-time data updates"]
        F["🔑 Auto-generates API keys"]
    end

    style WHY fill:#0f3460,stroke:#22c55e,stroke-width:2px,color:#fff
```

### How to Connect Supabase to Your Project

```mermaid
graph TD
    A["1️⃣ Go to supabase.com"] --> B["2️⃣ Create account / Sign in"]
    B --> C["3️⃣ Click 'New Project'"]
    C --> D["4️⃣ Name your project + set region"]
    D --> E["5️⃣ Wait for project to spin up ⏳"]
    E --> F["6️⃣ Go to Settings → API"]
    F --> G["7️⃣ Copy your URL + Keys"]
    G --> H["8️⃣ Create a .env file in your project"]
    H --> I["9️⃣ Paste the keys into .env"]
    I --> J["🔟 Install Supabase in your project"]

    style A fill:#1a1a2e,stroke:#22c55e,stroke-width:2px,color:#fff
    style G fill:#1a1a2e,stroke:#f59e0b,stroke-width:2px,color:#fff
    style J fill:#1a1a2e,stroke:#22c55e,stroke-width:2px,color:#fff
```

### The Commands (Copy-Paste These)

**Step 8 — Create the `.env` file in your project root:**
```env
# Your Supabase keys go here
SUPABASE_URL=https://xxxxx.supabase.co
SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR.....
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR.....
DATABASE_URL=postgresql://postgres:password@db.xxxxx.supabase.co:5432/postgres
```

**Step 10 — Install Supabase in your project (run in terminal):**
```bash
npm install @supabase/supabase-js
```

> [!WARNING]
> **Never share your `.env` file!** It contains secret keys. Always add `.env` to your `.gitignore` file so it doesn't get uploaded to GitHub.

---

## 🔍 Finding Your Supabase API Keys

![Supabase API Keys](C:\Users\Hashir Mehboob\.gemini\antigravity\brain\362439cf-b9ab-4021-8245-3c274c01ee06\supabase_keys_1778504866050.png)

### Step-by-Step: Where to Find Each Key

```mermaid
graph TD
    subgraph DASHBOARD["🌐 Supabase Dashboard"]
        A["Login at supabase.com"]
        B["Select your Project"]
        C["Click ⚙️ Settings (left sidebar)"]
        D["Click 'API' tab"]
    end

    subgraph KEYS_FOUND["🔑 Keys You'll Find"]
        E["🟢 Project URL<br/><code>https://xxxxx.supabase.co</code>"]
        F["🟠 anon / public key<br/><code>eyJhbGciOi...</code>"]
        G["🔴 service_role key<br/><code>eyJhbGciOi...</code>"]
    end

    subgraph DB_KEY["🔗 Database URL (Different Location)"]
        H["Click 'Database' in sidebar"]
        I["Click 'Connection String'"]
        J["🟣 Connection String<br/><code>postgresql://postgres:...</code>"]
    end

    A --> B --> C --> D
    D --> E & F & G
    B --> H --> I --> J

    style DASHBOARD fill:#1a1a2e,stroke:#00d2ff,stroke-width:2px,color:#fff
    style KEYS_FOUND fill:#0f3460,stroke:#f59e0b,stroke-width:2px,color:#fff
    style DB_KEY fill:#16213e,stroke:#a855f7,stroke-width:2px,color:#fff
```

### Navigation Path (Visual)

| What You Need | Where to Find It | Path in Dashboard |
|---|---|---|
| 🟢 **Project URL** | Settings → API | `supabase.com → Your Project → ⚙️ Settings → API → Project URL` |
| 🟠 **Anon Key** | Settings → API | `supabase.com → Your Project → ⚙️ Settings → API → anon public` |
| 🔴 **Service Role Key** | Settings → API | `supabase.com → Your Project → ⚙️ Settings → API → service_role` |
| 🟣 **Database URL** | Settings → Database | `supabase.com → Your Project → ⚙️ Settings → Database → Connection String` |

---

## 📝 Drizzle ORM — The Translator

### What is Drizzle?

> Imagine you speak **English** 🇬🇧 but your database speaks **SQL** 🗄️.  
> **Drizzle ORM is your translator** 🗣️ — it lets you talk to the database in JavaScript/TypeScript (a language you already know) instead of learning SQL.

### ORM = Object-Relational Mapper

```mermaid
graph LR
    A["👤 You write<br/>JavaScript Code"] -->|"Drizzle translates"| B["📝 Drizzle ORM"]
    B -->|"Becomes SQL"| C["🗄️ Database<br/>(Supabase/PostgreSQL)"]

    style A fill:#1a1a2e,stroke:#00d2ff,stroke-width:2px,color:#fff
    style B fill:#16213e,stroke:#22c55e,stroke-width:2px,color:#fff
    style C fill:#0f3460,stroke:#f59e0b,stroke-width:2px,color:#fff
```

### Why Use Drizzle? (vs Writing Raw SQL)

| Without Drizzle (Raw SQL) 😫 | With Drizzle ORM 😊 |
|---|---|
| `SELECT * FROM users WHERE age > 18;` | `db.select().from(users).where(gt(users.age, 18))` |
| Must learn SQL language | Write in JavaScript you already know |
| Easy to make typos in SQL | Auto-complete helps you |
| No error checking until runtime | Errors caught while you type |
| Hard to change database structure | Easy migration system |

### How Drizzle Fits in the Architecture

```mermaid
graph TD
    subgraph YOUR_APP["🖥️ Your Application"]
        A["Your Code<br/><i>JavaScript/TypeScript</i>"]
        B["Drizzle ORM<br/><i>The Translator</i>"]
    end

    subgraph SUPABASE["☁️ Supabase Cloud"]
        C["PostgreSQL Database<br/><i>Where data lives</i>"]
    end

    A -->|"1. You write:<br/>db.select().from(users)"| B
    B -->|"2. Drizzle converts to:<br/>SELECT * FROM users"| C
    C -->|"3. Database returns:<br/>[{name: 'Ali', age: 25}]"| B
    B -->|"4. Drizzle gives you<br/>clean JavaScript objects"| A

    style YOUR_APP fill:#1a1a2e,stroke:#a855f7,stroke-width:2px,color:#fff
    style SUPABASE fill:#0f3460,stroke:#22c55e,stroke-width:2px,color:#fff
```

### Install Drizzle (Copy-Paste These)

```bash
# Install Drizzle ORM + PostgreSQL driver
npm install drizzle-orm postgres

# Install Drizzle Kit (for managing database structure)
npm install -D drizzle-kit
```

---

## 🗂️ API Keys Cheat Sheet

### Which Key Does What?

```mermaid
graph TD
    subgraph ANTHROPIC["🧠 ANTHROPIC (AI)"]
        A1["🔑 ANTHROPIC_API_KEY<br/><b>Purpose:</b> Activates Claude Code<br/><b>Where:</b> console.anthropic.com<br/><b>Used by:</b> Terminal / CLI"]
    end

    subgraph SUPABASE_KEYS["🗄️ SUPABASE (Database)"]
        S1["🟢 SUPABASE_URL<br/><b>Purpose:</b> Address of your database<br/><b>Where:</b> Settings → API<br/><b>Used by:</b> Your app code"]
        S2["🟠 SUPABASE_ANON_KEY<br/><b>Purpose:</b> Public access to database<br/><b>Where:</b> Settings → API<br/><b>Used by:</b> Frontend code"]
        S3["🔴 SUPABASE_SERVICE_ROLE_KEY<br/><b>Purpose:</b> Admin/full access<br/><b>Where:</b> Settings → API<br/><b>Used by:</b> Backend only ⚠️"]
        S4["🟣 DATABASE_URL<br/><b>Purpose:</b> Direct database connection<br/><b>Where:</b> Settings → Database<br/><b>Used by:</b> Drizzle ORM"]
    end

    style ANTHROPIC fill:#2d1b4e,stroke:#a855f7,stroke-width:2px,color:#fff
    style SUPABASE_KEYS fill:#0f3460,stroke:#22c55e,stroke-width:2px,color:#fff
```

### Quick Reference Table

| Key Name | 🏷️ Type | 🔒 Secret? | 📍 Where to Find | 🎯 What It Does |
|---|---|---|---|---|
| `ANTHROPIC_API_KEY` | AI Access | ✅ Yes | [console.anthropic.com](https://console.anthropic.com) → API Keys | Lets you use Claude Code in terminal |
| `SUPABASE_URL` | Database Address | ❌ No | Supabase Dashboard → Settings → API | Tells your app where the database lives |
| `SUPABASE_ANON_KEY` | Public Access | ⚠️ Semi | Supabase Dashboard → Settings → API | Lets your app read/write data (with rules) |
| `SUPABASE_SERVICE_ROLE_KEY` | Admin Access | ✅ Yes | Supabase Dashboard → Settings → API | Full access — bypasses all security rules |
| `DATABASE_URL` | Direct Connection | ✅ Yes | Supabase Dashboard → Settings → Database | Drizzle uses this to connect directly |

> [!CAUTION]
> **🔴 SUPABASE_SERVICE_ROLE_KEY** = Master Key. **NEVER** put this in frontend/client code. Only use it in your backend server. If someone gets this key, they can delete all your data!

### Your `.env` File Should Look Like This

```env
# ═══════════════════════════════════════════
# 🧠 AI CONFIGURATION
# ═══════════════════════════════════════════
ANTHROPIC_API_KEY=sk-ant-api03-xxxxxxxxxxxx

# ═══════════════════════════════════════════
# 🗄️ SUPABASE CONFIGURATION
# ═══════════════════════════════════════════
SUPABASE_URL=https://abcdefghij.supabase.co
SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.xxxxx
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.xxxxx
DATABASE_URL=postgresql://postgres:YourPassword@db.abcdefghij.supabase.co:5432/postgres
```

---

## 🔄 The Complete Flow

### End-to-End: From Zero to Working App

```mermaid
graph TD
    START["🚀 START HERE"] --> A

    subgraph PHASE1["Phase 1: Set Up Your Tools"]
        A["1. Install Cursor AI IDE<br/><i>cursor.com → Download</i>"]
        B["2. Install Claude Code<br/><i>npm install -g @anthropic-ai/claude-code</i>"]
        C["3. Get Anthropic API Key<br/><i>console.anthropic.com</i>"]
        D["4. Set API key in terminal<br/><i>export ANTHROPIC_API_KEY=...</i>"]
    end

    subgraph PHASE2["Phase 2: Create Your Project"]
        E["5. Create project folder in Cursor"]
        F["6. Open terminal: Ctrl + `"]
        G["7. Type 'claude' to start AI agent"]
        H["8. Tell Claude what to build"]
    end

    subgraph PHASE3["Phase 3: Connect Database"]
        I["9. Go to supabase.com → New Project"]
        J["10. Copy API keys from Settings → API"]
        K["11. Create .env file in project"]
        L["12. Paste keys into .env"]
        M["13. Install packages<br/><i>npm install @supabase/supabase-js drizzle-orm</i>"]
    end

    subgraph PHASE4["Phase 4: Build & Ship 🎉"]
        N["14. Claude writes your database code"]
        O["15. Drizzle connects to Supabase"]
        P["16. Test your app locally"]
        Q["17. Deploy to Vercel"]
    end

    A --> B --> C --> D
    D --> E --> F --> G --> H
    H --> I --> J --> K --> L --> M
    M --> N --> O --> P --> Q

    style PHASE1 fill:#1a1a2e,stroke:#a855f7,stroke-width:2px,color:#fff
    style PHASE2 fill:#16213e,stroke:#00d2ff,stroke-width:2px,color:#fff
    style PHASE3 fill:#0f3460,stroke:#22c55e,stroke-width:2px,color:#fff
    style PHASE4 fill:#1a1a2e,stroke:#f59e0b,stroke-width:2px,color:#fff
    style START fill:#22c55e,stroke:#fff,stroke-width:3px,color:#000
```

---

## 🧩 How All Pieces Connect — Final Architecture

```mermaid
graph TB
    subgraph DEVELOPER["👤 DEVELOPER MACHINE"]
        CURSOR["🖥️ Cursor AI IDE<br/><i>Your workspace — see files, run app</i>"]
        TERMINAL["⬛ Terminal<br/><i>Lives inside Cursor</i>"]
        CLAUDE["🧠 Claude Code CLI<br/><i>AI agent — builds features for you</i>"]
        ENV[".env File<br/><i>All your secret keys</i>"]
        CODE["📁 Your Project Code<br/><i>JavaScript / TypeScript files</i>"]
        DRIZZLE["📝 Drizzle ORM<br/><i>Translates JS → SQL</i>"]
    end

    subgraph CLOUD["☁️ CLOUD SERVICES"]
        ANTHROPIC["🧠 Anthropic Servers<br/><i>Claude AI lives here</i>"]
        SUPABASE["🗄️ Supabase<br/><i>Your database lives here</i>"]
        VERCEL["🚀 Vercel<br/><i>Your live website</i>"]
        GITHUB["🐙 GitHub<br/><i>Code backup & sharing</i>"]
    end

    CURSOR --> TERMINAL
    TERMINAL --> CLAUDE
    CLAUDE -->|"Uses ANTHROPIC_API_KEY"| ANTHROPIC
    CLAUDE -->|"Creates & edits"| CODE
    CODE --> DRIZZLE
    DRIZZLE -->|"Uses DATABASE_URL"| SUPABASE
    CODE -->|"Uses SUPABASE_URL +<br/>SUPABASE_ANON_KEY"| SUPABASE
    ENV -->|"Provides keys to"| CODE
    CODE -->|"git push"| GITHUB
    GITHUB -->|"Auto-deploys to"| VERCEL
    VERCEL -->|"Uses env variables"| SUPABASE

    style DEVELOPER fill:#1a1a2e,stroke:#00d2ff,stroke-width:2px,color:#fff
    style CLOUD fill:#0f3460,stroke:#a855f7,stroke-width:2px,color:#fff
```

---

## 💰 Who Pays for What? — Token & Billing Guide

> [!IMPORTANT]
> **Cursor AI and Anthropic (Claude) are two SEPARATE companies.** They have completely different subscriptions. Paying for one does NOT give you tokens for the other.

### The Analogy

> Think of it like **Netflix** and **Spotify**:
> - Paying for Netflix doesn't give you free Spotify music
> - Paying for Cursor AI doesn't give you free Claude Code tokens
> - They are **separate memberships** that happen to work well together

### Billing Flow Diagram

```mermaid
graph TB
    subgraph CURSOR_BILLING["💳 CURSOR AI (Subscription #1)"]
        CB1["Cursor Free / Pro / Business"]
        CB2["Provides: Built-in AI features"]
        CB3["✅ Cmd+K — AI edit code"]
        CB4["✅ Cmd+L — AI chat panel"]
        CB5["✅ Tab — AI autocomplete"]
        CB6["❌ Does NOT power Claude Code CLI"]
    end

    subgraph ANTHROPIC_BILLING["💳 ANTHROPIC (Subscription #2)"]
        AB1["Claude Max / API Credits"]
        AB2["Provides: Claude Code CLI agent"]
        AB3["✅ 'claude' command in terminal"]
        AB4["✅ Building entire features"]
        AB5["✅ Complex coding tasks"]
        AB6["❌ Does NOT power Cursor's UI features"]
    end

    subgraph YOUR_WALLET["👛 YOUR WALLET"]
        W1["You pay Cursor separately"]
        W2["You pay Anthropic separately"]
    end

    YOUR_WALLET --> CURSOR_BILLING
    YOUR_WALLET --> ANTHROPIC_BILLING

    style CURSOR_BILLING fill:#1e3a5f,stroke:#00d2ff,stroke-width:2px,color:#fff
    style ANTHROPIC_BILLING fill:#2d1b4e,stroke:#a855f7,stroke-width:2px,color:#fff
    style YOUR_WALLET fill:#1a1a2e,stroke:#f59e0b,stroke-width:2px,color:#fff
```

### Three Ways to Access Claude — Which Tokens Get Used?

| How You Access AI | What Gets Used | Who Bills You |
|---|---|---|
| 🖥️ **Cursor's Cmd+K / Cmd+L / Tab** | Cursor's own AI tokens | **Cursor** ($20/mo Pro) |
| ⬛ **Type `claude` in terminal** (with Claude Max) | Your Claude Max subscription allowance | **Anthropic** ($100-200/mo Max) |
| ⬛ **Type `claude` in terminal** (with API key) | Your Anthropic API credit balance | **Anthropic** (pay-per-use) |

### Claude Max vs API Key — What's the Difference?

```mermaid
graph LR
    subgraph MAX["🟢 Claude Max Subscription"]
        M1["$100-200 / month"]
        M2["Fixed monthly price"]
        M3["Generous usage included"]
        M4["No surprise bills"]
        M5["Best for: Heavy daily use"]
    end

    subgraph API["🟠 Anthropic API Credits"]
        A1["Pay per token used"]
        A2["Top up credit balance"]
        A3["Can run out mid-task"]
        A4["Bills based on usage"]
        A5["Best for: Light/occasional use"]
    end

    style MAX fill:#0f3460,stroke:#22c55e,stroke-width:2px,color:#fff
    style API fill:#1a1a2e,stroke:#f59e0b,stroke-width:2px,color:#fff
```

| Feature | 🟢 Claude Max | 🟠 API Credits |
|---|---|---|
| **Pricing** | Fixed monthly ($100-200) | Pay-per-use (token based) |
| **Setup** | Subscribe at claude.ai → Use CLI | Get API key from console.anthropic.com |
| **Best for** | Daily heavy coding | Occasional use or testing |
| **Risk** | None — fixed cost | Can get expensive if heavy use |
| **How to activate CLI** | `claude` (auto-detects your Max plan) | `export ANTHROPIC_API_KEY=sk-...` then `claude` |

> [!CAUTION]
> **If you have Claude Max AND an API key set**, Claude Code will prioritize your **Max subscription** (so your API credits won't be consumed). But if your Max subscription is inactive or expired, it falls back to the API key and **will charge your API credits**.

### Visual Summary — Where Does Each Token Come From?

```mermaid
sequenceDiagram
    actor You as 👤 You

    box rgb(30, 58, 95) Cursor AI IDE
        participant CursorAI as 🤖 Cursor's Built-in AI
        participant Terminal as ⬛ Terminal
    end

    box rgb(45, 27, 78) Anthropic Cloud
        participant ClaudeCLI as 🧠 Claude Code CLI
        participant MaxSub as 💎 Claude Max Subscription
        participant APICredits as 💳 API Credits
    end

    You->>CursorAI: Cmd+K "edit this function"
    Note right of CursorAI: Uses CURSOR tokens ✅
    CursorAI-->>You: Code suggestion

    You->>Terminal: types "claude"
    Terminal->>ClaudeCLI: Starts Claude Code

    alt Has Claude Max
        ClaudeCLI->>MaxSub: Uses Max allowance ✅
        Note right of MaxSub: Your MAX subscription pays
    else Has API Key only
        ClaudeCLI->>APICredits: Uses API credits ✅
        Note right of APICredits: Your API BALANCE pays
    end

    ClaudeCLI-->>You: Builds feature / writes code
```

### 🎯 Bottom Line — Decision Table

| Your Situation | What You Need | Monthly Cost |
|---|---|---|
| "I just want Cursor's AI features" | Cursor Pro only | ~$20/mo |
| "I want Claude Code CLI for heavy coding" | Claude Max only | ~$100-200/mo |
| "I want both Cursor AI + Claude Code" | Cursor Pro + Claude Max | ~$120-220/mo |
| "I want to try Claude Code cheaply" | Cursor Free + Anthropic API credits | Pay-per-use |

---

## 💡 Common Confusions — Cleared Up

### ❓ "Do I need BOTH Cursor AI and Claude Code?"
**Yes, but they're different things:**
- **Cursor AI** = The app you open (like opening Microsoft Word)
- **Claude Code** = The AI assistant that runs *inside* Cursor's terminal
- Together, they're like having a **blank canvas** (Cursor) with a **robot painter** (Claude) that paints what you describe

### ❓ "If I buy Claude Max, will Cursor use those tokens?"
**NO!** They are completely separate:
- **Cursor's Cmd+K / Cmd+L / Tab** → Always uses **Cursor's** tokens
- **Typing `claude` in terminal** → Uses **your Anthropic account** (Max or API credits)
- Think of it like: **Netflix remote** (Cursor) vs **Spotify app** (Claude) — same TV, different subscriptions

### ❓ "Why so many Supabase keys?"
**Each key has a different security level:**

| Key | Security | Analogy |
|---|---|---|
| 🟠 Anon Key | Low — public facing | Front door key (visitors can enter) |
| 🔴 Service Role Key | High — full access | Master key (opens everything) |
| 🟣 Database URL | High — direct connection | Secret tunnel to the vault |

Use the **Anon Key** in your frontend. Use the **Service Role Key** only in your backend server.

### ❓ "Why use Drizzle when Supabase has its own client?"
**Two different ways to talk to Supabase:**

| Method | Best For | Analogy |
|---|---|---|
| `@supabase/supabase-js` | Simple queries, auth, real-time | Ordering food from a menu |
| `Drizzle ORM` | Complex queries, type safety, migrations | Cooking in the kitchen yourself |

Many projects use **both**: Supabase client for auth & real-time, Drizzle for complex data operations.

### ❓ "Where exactly do I type these commands?"
1. Open **Cursor AI** (the app)
2. Open your project folder
3. Press **Ctrl + `** (backtick key, above Tab)
4. A **terminal panel** appears at the bottom
5. Type commands there! 👇

```
PS C:\your-project> claude          ← starts the AI agent
PS C:\your-project> npm install     ← installs packages
PS C:\your-project> npm run dev     ← runs your app
```

---

> [!TIP]
> **Bookmark this guide!** Refer back to the [API Keys Cheat Sheet](#-api-keys-cheat-sheet) and [Token Billing Guide](#-who-pays-for-what--token--billing-guide) whenever you're confused.

---

*Last updated: May 11, 2026*
