# Indeed Tailored CV Skill — Complete Guide

> **What this skill does:** Searches Indeed for jobs that match your profile (via web search or MCP integration), then generates fully tailored, ATS-optimised `.docx` CVs for each one — in a conversation with Claude.

---

## Table of Contents

1. [What This Skill Does](#1-what-this-skill-does)
2. [How to Install the Skill in Claude](#2-how-to-install-the-skill-in-claude)
3. [How Job Searching Works](#3-how-job-searching-works)
4. [How to Use the Skill — Step by Step](#4-how-to-use-the-skill--step-by-step)
5. [What Claude Does Automatically](#5-what-claude-does-automatically)
6. [Output You Will Receive](#6-output-you-will-receive)
7. [Trigger Phrases](#7-trigger-phrases)
8. [Supported Locations & Country Codes](#8-supported-locations--country-codes)
9. [Tips & Best Practices](#9-tips--best-practices)
10. [Troubleshooting](#10-troubleshooting)
11. [Limitations & Known Constraints](#11-limitations--known-constraints)

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

> **Heads-up:** See [Limitations & Known Constraints](#11-limitations--known-constraints) for honest notes about what to expect.

---

## 2. How to Install the Skill in Claude

Skills are installed by uploading the `.skill` file into your Claude Projects workspace. Follow these steps:

### What Is a `.skill` File?

A `.skill` file is simply a **ZIP archive** containing a `SKILL.md` file — the instructions that tell Claude how to behave. You can verify this yourself by renaming it to `.zip` and opening it. Claude Projects accept this format directly.

Alternatively, you can **extract the ZIP** and paste the contents of `indeed-tailored-cv/SKILL.md` directly into a Project's Knowledge section if your plan doesn't support `.skill` uploads.

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

## 3. How Job Searching Works

The skill searches Indeed for live job listings using one of two methods. **Web search is the default and most reliable method today.**

### Method 1 — Web Search (Default)

No setup required. Claude uses its built-in web search capability to find jobs on Indeed's public job pages (e.g. `qa.indeed.com`, `ae.indeed.com`). This works out of the box on any Claude plan that supports web search.

Simply start a conversation and say:

```
Search Indeed for software engineer jobs in Doha, Qatar
```

Claude will scrape job listings, extract titles, companies, and descriptions, and present them in a match table.

### Method 2 — MCP Server (Future / Custom)

MCP (Model Context Protocol) is a standard that lets Claude connect to external services directly. If Indeed or a third party publishes an MCP-compatible job search server in the future, you can connect it for more structured results.

> **⚠️ Note:** As of this writing, there is no official public Indeed MCP server available. The URL `https://mcp.indeed.com/claude/mcp` is a **placeholder** for illustration. If an official server becomes available, connect it via:
>
> 1. Go to **[claude.ai](https://claude.ai)** → your Project → **⚙ Settings** → **Integrations**
> 2. Click **"Add MCP Server"**
> 3. Enter the server name and URL
> 4. Click **Save** / **Connect**

If you have your own MCP-compatible job search server, you can connect it the same way.

### Verifying Job Search Works

Start a conversation inside your Project, upload your CV, and say:

```
Find me software engineer jobs in Doha, Qatar and tailor my CV
```

If Claude returns a table of job listings with titles, companies, and apply links, everything is working.

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
→ Make sure you are inside a **Project** (not a regular conversation). Skills only work in Projects. Re-upload the `.skill` file via Project Settings → Skills. Alternatively, extract the ZIP and paste the `SKILL.md` content into your Project's Knowledge section.

### "Claude searched the web instead of using Indeed directly"
→ Web search is the default and expected behaviour. See [Section 3](#3-how-job-searching-works) for details. If you have a custom MCP server configured, check that it's connected in Project Settings → Integrations.

### "Only a few jobs were found"
→ Claude will automatically run a 3rd broader search if deduplication leaves fewer than 10 results. If this still yields few results, try a broader phrase like "software engineer" instead of a very specific title.

### "The CV doesn't mention a skill I have"
→ Make sure that skill is clearly listed in your uploaded CV. Claude only uses information that exists in your original CV — it never invents experience or skills.

### "The download button doesn't work"
→ The dashboard HTML embeds CVs as base64 data URIs. If your browser blocks these downloads, try: right-click → Save link as, or open the HTML file locally in Chrome/Edge.

### "I want CVs for a different city after the first run"
→ Simply say: "Now search for the same roles in Dubai, UAE" and Claude will re-run the job search and generate a new set of 10 CVs for the new location.

### "Claude generated fewer than 10 CVs"
→ Claude is designed to always produce exactly 10. If it falls short, ask: "Please run an additional search and generate CVs for the remaining slots." Note: generating all 10 in a single turn may occasionally hit output limits — see [Limitations](#11-limitations--known-constraints).

---

## 11. Limitations & Known Constraints

This skill works well for most use cases, but here are honest notes on what to expect:

| Constraint | Detail |
|------------|--------|
| **No official Indeed MCP server** | As of March 2026, Indeed has not published a public MCP server. The skill uses web search to find jobs, which works well but returns slightly less structured data than a direct API would. |
| **Output length limits** | Generating 10 fully tailored DOCX files in a single conversation turn may occasionally hit Claude's output limits. If this happens, ask Claude to continue generating the remaining CVs. |
| **Dashboard file size** | The HTML dashboard embeds all 10 DOCX files as base64, which can result in a large file (2–5 MB). Some browsers may be slow to render it. |
| **Processing time** | Expect 2–5 minutes for the full workflow with a detailed CV. Longer CVs or slow network conditions may take longer. |
| **Sandbox paths** | The skill's internal instructions reference paths specific to Claude's execution environment. These are handled automatically — you don't need to configure them. |
| **Web search variability** | Job results from web search may vary between runs. Indeed's public pages may not always show the same listings. |

---

*Skill version: 1.1 · Compatible with Claude Sonnet 4 and above · [MIT License](LICENSE)*
