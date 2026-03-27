# Indeed Tailored CV Skill — Complete Guide

> **What this skill does:** Automatically searches Indeed for jobs that match your profile, then generates a fully tailored, ATS-optimised `.docx` CV for each one — all in a single conversation with Claude.

---

## Table of Contents

1. [What This Skill Does](#1-what-this-skill-does)
2. [How to Install the Skill in Claude](#2-how-to-install-the-skill-in-claude)
3. [How to Connect the Indeed MCP Server](#3-how-to-connect-the-indeed-mcp-server)
4. [How to Use the Skill — Step by Step](#4-how-to-use-the-skill--step-by-step)
5. [What Claude Does Automatically](#5-what-claude-does-automatically)
6. [Output You Will Receive](#6-output-you-will-receive)
7. [Trigger Phrases](#7-trigger-phrases)
8. [Supported Locations & Country Codes](#8-supported-locations--country-codes)
9. [Tips & Best Practices](#9-tips--best-practices)
10. [Troubleshooting](#10-troubleshooting)

---

## 1. What This Skill Does

The **Indeed Tailored CV** skill combines three capabilities into one automated workflow:

```
Upload CV → Extract Profile → Search Indeed → Select Jobs → Draft CV → AI-Check (human score) → Revise → Final CV
```

| Step | What Happens |
|------|-------------|
| **Profile Extraction** | Claude reads your uploaded CV (PDF or DOCX) and extracts your name, contact info, skills, work history, and education |
| **Job Search** | Claude searches Indeed for 10 relevant job openings in your target city using your skills and job title as search keywords |
| **CV Generation** | Claude generates one fully tailored `.docx` CV per job, rewriting the summary, reordering skills, and adjusting bullet points to match each job description |

Each generated CV is:
- **ATS-safe** — single-column layout, standard headings, no tables or graphics that confuse Applicant Tracking Systems
- **Human-sounding** — written to avoid AI-detection red flags, with varied verb openings and natural prose
- **Job-specific** — the professional summary, skills order, and work experience bullets are each customised to the target role
- **Ready to send** — exported as `.docx`, downloadable directly from the results dashboard

> **Note:** This skill is optimised for Gulf-region job searches (Doha, Dubai, Riyadh, etc.) but works globally for any city with an Indeed presence.

---

## 2. How to Install the Skill in Claude

Skills are installed by uploading the `.skill` file into your Claude Projects workspace. Follow these steps:

### Step 1 — Open Claude Projects

Go to [claude.ai](https://claude.ai) and open or create a **Project** (Projects are available on Pro, Team, and Enterprise plans).

> Skills only work inside Projects. They do not work in regular one-off conversations.

### Step 2 — Open Project Settings

Click the **⚙ Settings** icon (or the project name) in the left sidebar to open the project configuration panel.

### Step 3 — Upload the Skill File

1. Look for the **Skills** or **Knowledge** section in the project settings
2. Click **"Add skill"** or **"Upload file"**
3. Select the file: `indeed-tailored-cv.skill`
4. Wait for the upload to complete — you should see `indeed-tailored-cv` appear in the skills list

### Step 4 — Confirm Installation

Start a new conversation inside the Project and type:

```
What skills do you have available?
```

Claude should mention `indeed-tailored-cv` in its response.

---

## 3. How to Connect the Indeed MCP Server

The skill uses the **Indeed MCP (Model Context Protocol) server** to search for live job listings. Without this connection, Claude will fall back to web search — which still works but returns less structured job data.

### What is MCP?

MCP (Model Context Protocol) is a standard that lets Claude connect to external services — like Indeed — and call their APIs directly within a conversation. Think of it as giving Claude a live plugin.

### Step-by-Step: Connect Indeed MCP in Claude

#### Option A — Claude.ai Interface (Recommended)

1. Go to **[claude.ai](https://claude.ai)** and open your Project
2. Click **⚙ Settings** → **Integrations** or **Connectors**
3. Look for **"Add MCP Server"** or **"Connect a tool"**
4. Enter the following details:

   | Field | Value |
   |-------|-------|
   | **Name** | `Indeed` |
   | **Server URL** | `https://mcp.indeed.com/claude/mcp` |
   | **Type** | `URL` (SSE-based) |

5. Click **Save** / **Connect**
6. Authorise the connection if Indeed prompts for OAuth or an API key

#### Option B — Claude API (For Developers)

If you are calling Claude via the API and want to include the Indeed MCP server programmatically, add the `mcp_servers` parameter to your request:

```javascript
const response = await fetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({
    model: "claude-sonnet-4-20250514",
    max_tokens: 1000,
    messages: [
      { role: "user", content: "Find me software engineer jobs in Doha" }
    ],
    mcp_servers: [
      {
        type: "url",
        url: "https://mcp.indeed.com/claude/mcp",
        name: "Indeed"
      }
    ]
  })
});
```

### Verifying the Connection

Once connected, start a conversation and type:

```
Search Indeed for software engineer jobs in Doha, Qatar
```

If Claude returns live job listings from Indeed (with job IDs and apply links), the connection is working correctly.

### What If Indeed MCP Is Not Connected?

The skill still works without the MCP server. Claude will use **web search** to scrape Indeed job listings from `qa.indeed.com` (or the relevant country domain). The results are slightly less structured but functionally equivalent for CV generation.

---

## 4. How to Use the Skill — Step by Step

### Step 1 — Upload Your CV

In a conversation inside your Claude Project, upload your CV file. Both formats are supported:

- `YourName_CV.pdf`
- `YourName_CV.docx`

### Step 2 — Tell Claude Your Target Location

After reading your CV, Claude will ask:

> "Where would you like me to search for jobs? Please provide a city and country (e.g. Dubai, UAE / London, UK / Riyadh, Saudi Arabia / Doha, Qatar)."

Reply with your preferred location. Claude will not start the job search until you confirm a city and country.

### Step 3 — Trigger the Skill

You can trigger it with the shorthand command:

```
/indeed-tailored-cv  [city] [country]
```

**Examples:**

```
/indeed-tailored-cv  doha qatar
/indeed-tailored-cv  dubai uae
/indeed-tailored-cv  london uk
/indeed-tailored-cv  riyadh saudi arabia
```

You can also trigger it conversationally:

```
Find me software engineer jobs in Doha and create a tailored CV for each one
```

```
Search for React developer jobs in Dubai and tailor my CV to the top 10 results
```

### Step 4 — Wait for Results

Claude will automatically:
1. Extract your profile from the uploaded CV
2. Run 2 parallel Indeed searches using your job title and primary skills as keywords
3. Deduplicate results and select the top 10 most relevant jobs
4. Show you a match table in chat (job title, company, location, match reason, apply link)
5. Generate one tailored `.docx` CV per job — automatically, without asking you to pick
6. Present an interactive results dashboard

This typically takes 1–3 minutes depending on CV length and network speed.

### Step 5 — Download Your CVs

The results dashboard shows a table with all 10 jobs. Each row has:
- The job title and company
- Why it matched your profile
- What was tailored in that CV
- An **Apply on Indeed** link (opens in new tab)
- A **⬇ Download** button for the `.docx` CV file

The 10 `.docx` files are also made available individually in the chat as a backup download method.

---

## 5. What Claude Does Automatically

You do not need to configure any of the following — Claude handles them automatically based on the skill instructions:

### Profile Extraction
- Reads PDF via `pdfminer.six` or DOCX via `pandoc`
- Extracts: full name, contact info, job titles, years of experience, skills, work history, and education
- Stores first name and last name separately for file naming

### Job Searching
- Runs 2 parallel Indeed searches (job title + skills keywords)
- Deduplicates up to 20 candidates by job ID
- Scores relevance by: title match, skills overlap, industry alignment, seniority level
- Fetches full job descriptions via `Indeed:get_job_details`
- Always produces exactly 10 jobs (runs a 3rd broader search if deduplication leaves fewer)

### CV Tailoring (Per Job)
- Rewrites the **Professional Summary** to mirror each job's language and requirements
- Reorders the **Skills** section to front-load keywords from the job description
- Rewrites **Work Experience** bullets to highlight the most relevant achievements for each role
- Surfaces relevant **Certifications** for each target role
- Applies human writing style rules (varied verbs, concrete language, no AI-typical phrases)
- Runs an **AI-detection self-check** before finalising each CV — if more than 2 red flags are found in any section, that section is rewritten before the `.docx` is generated
- Proofs for grammar, spelling, and punctuation

### File Generation
- Generates ATS-safe `.docx` files using the `docx-js` library
- Names files as: `FirstName_LastName_JobTitle_CompanyName.docx`
- Embeds files as base64 in the HTML dashboard for direct browser download

---

## 6. Output You Will Receive

After the skill completes, you receive:

### Interactive HTML Dashboard
An HTML file (`YourName_CV_Dashboard.html`) containing:
- A table of all 10 jobs with match reasoning and tailoring notes
- One-click download buttons for each CV (no server needed — files are embedded)
- Apply links to Indeed job postings
- A collapsible "💡 Tips to strengthen your applications" section with skill gap notes per role

### 10 Individual DOCX Files
Each file is also available as a standalone download, named:
```
FirstName_LastName_JobTitle_CompanyName.docx
```

For example:
```
Ahmed_AlRashid_SeniorSoftwareEngineer_QatarEnergy.docx
Sara_Mohammed_FrontendDeveloper_Ooredoo.docx
```

### CV Structure (Each File)
Every generated CV follows this ATS-standard layout:

```
[Full Name]
[Target Job Title]
[Email · Phone · LinkedIn · Location]

PROFESSIONAL SUMMARY
3–4 sentences tailored to this specific job

CORE SKILLS
Comma-separated skills list, prioritised for this job's keywords

PROFESSIONAL EXPERIENCE
Job Title
Company  |  Location
Start Date – End Date
  • Bullet point 1
  • Bullet point 2

EDUCATION
Degree
Institution
Location

CERTIFICATIONS (if applicable)
Relevant certifications surfaced for this specific role
```

---

## 7. Trigger Phrases

The skill activates when Claude detects any of these phrases (with or without a CV upload):

| Phrase Type | Examples |
|-------------|---------|
| **Command** | `/indeed-tailored-cv doha qatar` |
| **Job search** | "find me jobs", "search for jobs in Dubai", "job hunting in Riyadh" |
| **CV request** | "tailored CV", "customised resume", "match my CV to jobs" |
| **Application help** | "help me apply", "create CV for job", "update my CV for these roles" |
| **Combined** | "find React developer jobs in Doha and tailor my CV" |

---

## 8. Supported Locations & Country Codes

The skill works for any city with an Indeed presence. Common Gulf and international locations:

| Country | ISO Code | Example City Input |
|---------|----------|-------------------|
| Qatar | `QA` | `Doha, Qatar` |
| UAE | `AE` | `Dubai, UAE` or `Abu Dhabi, UAE` |
| Saudi Arabia | `SA` | `Riyadh, Saudi Arabia` or `Jeddah, Saudi Arabia` |
| Kuwait | `KW` | `Kuwait City, Kuwait` |
| Bahrain | `BH` | `Manama, Bahrain` |
| Oman | `OM` | `Muscat, Oman` |
| United Kingdom | `GB` | `London, UK` or `Manchester, UK` |
| United States | `US` | `New York, USA` or `San Francisco, USA` |
| Canada | `CA` | `Toronto, Canada` |
| Australia | `AU` | `Sydney, Australia` |
| Germany | `DE` | `Berlin, Germany` |
| Egypt | `EG` | `Cairo, Egypt` |

---

## 9. Tips & Best Practices

### For Best CV Results
- **Upload a detailed CV** — the more experience and bullet points you provide, the more material Claude has to tailor each CV with. A 2–3 page CV produces better output than a 1-page summary.
- **Include quantified achievements in your original CV** — Claude will reuse your real numbers (e.g. "automated workflows for 30+ banks") rather than inventing figures.
- **Keep your CV in English** — Indeed Qatar and Gulf job postings are almost entirely in English. If you need Arabic output, mention it explicitly.

### For Better Job Matches
- **Be specific about your target role** — instead of "find me jobs", say "find me senior React developer jobs" for more accurate results.
- **Refine after the first search** — after seeing the 10 results, you can say "also look for Node.js backend roles" or "skip junior-level jobs" and Claude will re-run searches.
- **Check the tips section** — the collapsible tips panel in the dashboard highlights skill gaps per role (e.g. "AWS certification would strengthen this application").

### For ATS Compliance
- Do not add logos, photos, or graphics to the generated CVs before submitting — this breaks ATS parsing.
- The generated files use Arial/Calibri font and standard section headings intentionally — resist the urge to reformat into a fancy template for online applications.
- Use the fancy-formatted version for in-person interviews; use the plain ATS version for online submissions.

---

## 10. Troubleshooting

### "I don't see the skill in my project"
→ Make sure you are inside a **Project** (not a regular conversation). Skills only work in Projects. Re-upload the `.skill` file via Project Settings → Skills.

### "Claude searched the web instead of using Indeed directly"
→ The Indeed MCP server is not connected. Follow [Section 3](#3-how-to-connect-the-indeed-mcp-server) to connect it. The skill still works via web search as a fallback — job results are slightly less structured but CVs are still generated.

### "Only a few jobs were found"
→ Claude will automatically run a 3rd broader search if deduplication leaves fewer than 10 results. If this still yields few results, try a broader phrase like "software engineer" instead of a very specific title.

### "The CV doesn't mention a skill I have"
→ Make sure that skill is clearly listed in your uploaded CV. Claude only uses information that exists in your original CV — it never invents experience or skills.

### "The download button doesn't work"
→ The dashboard HTML embeds CVs as base64 data URIs. If your browser blocks these downloads, try: right-click → Save link as, or open the HTML file locally in Chrome/Edge.

### "I want CVs for a different city after the first run"
→ Simply say: "Now search for the same roles in Dubai, UAE" and Claude will re-run the job search and generate a new set of 10 CVs for the new location.

### "Claude generated fewer than 10 CVs"
→ Claude is designed to always produce exactly 10. If it falls short, ask: "Please run an additional search and generate CVs for the remaining slots."

---

*Skill version: 1.0 · Compatible with Claude claude-sonnet-4-20250514 and above · Indeed MCP server: `https://mcp.indeed.com/claude/mcp`*
