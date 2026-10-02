# HR Analytics Dashboard · Built with Agentic AI Development

A two-page **Power BI** HR dashboard taken from raw mock data to a documented, version-controlled project using **Claude as an AI development agent**. I set the direction, constraints and reviews. Claude designed, prototyped, built, debugged and documented it using real tools (Canva, HTML, Power BI Modeling MCP, PBIR authoring).

<img width="3000" height="1410" alt="development-cycle" src="https://github.com/user-attachments/assets/ec30d88e-4420-4e28-90b7-75d69059bbce" />

---

## 📊 The dashboard

<!-- PLACEHOLDER: upload Power BI screenshots to /images with these exact names -->
| Workforce Overview | Pay & Performance |
|-------------------|-------------------|
| ![Workforce Overview](https://github.com/user-attachments/assets/819dd6c4-8e33-43a2-a446-7cc58b3e62ca) | ![Pay & Performance](https://github.com/user-attachments/assets/830280e8-3431-479f-ac55-320d05566844) |
**Page 1: Workforce Overview.** KPIs: Headcount · Attrition Rate · Avg Absence Days · Avg Engagement Score, each compared with the previous year.
Visuals: headcount trend with hires and exits (quarter → month drill) · attrition by department vs company average · gender split by job level · exit reasons (voluntary / involuntary).

**Page 2: Pay & Performance.** KPIs: Avg Monthly Salary · Avg Performance Rating · Avg Training Hours · Avg Overtime Hours, each compared with the previous year.
Visuals: salary by job level and gender · performance rating distribution · attrition and engagement by rating · training vs overtime by department.

**Filters (synced across pages):** Year · Month · Department · Job Level · Gender · Age Band · Location · Employment Type · Reset.

---

## 🤖 How I built it: agentic development with Claude

I treated Claude as a developer on my team. I wrote the brief, set the constraints and approved each stage. Claude did the hands-on work using tools connected to my environment.

### 1 · Data
I prepared a synthetic HR dataset: **106,903 rows** of monthly employee snapshots (Jan 2024 – Dec 2025) across 8 departments, 6 Malaysian locations and 5 job levels, with salary (MYR), performance, engagement, absence, overtime, training and hire/exit events. Claude profiled it to agree the grain, KPIs and date logic.

### 2 · Design: Canva wireframe
Brief: *4 KPIs, 4 charts, using my earlier TVME dashboard as the style reference.* Claude read the reference design through the **Canva MCP** (layout, palette, KPI card style) and drafted the first wireframe directly in Canva.

### 3 · Prototype: interactive HTML wireframe
Static mockups don't show how a dashboard *feels*, so Claude rebuilt the design as a **clickable HTML prototype** on real data: working slicers, tooltips, page navigation. It used Power BI's 1920×1080 canvas and only visuals that exist natively in Power BI, so it could be rebuilt 1:1.

| Prototype · Page 1 | Prototype · Page 2 |
|---|---|
| ![HTML wireframe page 1](https://github.com/user-attachments/assets/b1000647-d625-4f78-9aa6-306d5093dd04) | ![HTML wireframe page 2](https://github.com/user-attachments/assets/2efe6aed-b037-49cb-aaa4-6660ebd67e0a) |

▶️ Try it: download [`hr_dashboard_wireframe.html`](hr_dashboard_wireframe.html) and open it in any browser.

### 4 · User testing
Users tested the prototype before any Power BI work started. Their feedback was applied in minutes:
- removed the developer notes overlay
- added a second page, **Pay & Performance**
- removed the Previous Year / Previous Month toggles, moving comparisons into the KPI cards

### 5 · Build: Power BI (PBIP)
My constraints: *flat table only, all measures in a `_measures` table, and it must look identical to the wireframe.* Claude used the **Power BI Modeling MCP** and **PBIR report-authoring tools** to produce:
- a single import table `HR_Data` plus a `_measures` table
- **51 DAX measures** in display folders: base KPIs, previous-year, KPI caption and delta labels, and conditional-format colours ([measures.md](measures.md))
- **2 pages with 80 visuals**, written as PBIR files to match the prototype's positions, colours and fonts
- validation of every field reference before handover

### 6 · Debug
I opened the project in Power BI Desktop and sent screenshots of the issues. Claude diagnosed and fixed them:
- **Circular dependency:** sort-by columns referenced their own source. Fixed with sorted display copies ([data-dictionary.md](data-dictionary.md)).
- **Theme-blue outlines and boxes** on shapes and cards. Fixed with explicit transparent fills and outlines.

### 7 · Document
Claude wrote this documentation, generated the measure catalogue directly from the model's TMDL, and replaced the hard-coded Excel path with a `Source File Path` parameter so anyone can open the project.

---

## 💡 What this demonstrates

- **Agentic AI workflow:** an AI agent working through real tools (MCP servers, CLIs, file system), not just chat answers
- **Human-in-the-loop control:** my brief, constraints and approval at every stage
- **Design-first BI:** wireframe → prototype → user test → build, so feedback lands before development cost
- **Power BI as code:** PBIP / TMDL / PBIR files that can be reviewed in Git
- **DAX:** end-of-period headcount, attrition rate, previous year without a date table (`EDATE` + `TREATAS`), dynamic labels and colours

---

## 📁 Repository

| File / folder | What it is |
|---|---|
| `HR Dashboard.pbip` | Open this in Power BI Desktop |
| `HR Dashboard.Report/` | Report definition (PBIR: pages and visuals) |
| `HR Dashboard.SemanticModel/` | Model definition (TMDL: table, measures, parameter) |
| `HR_Dashboard_Mock_Data.xlsx` | Synthetic source data |
| `hr_dashboard_wireframe.html` | Interactive prototype used for user testing |
| [`measures.md`](measures.md) | DAX measure catalogue |
| [`data-dictionary.md`](data-dictionary.md) | Columns, calculated columns, parameter |
| `images/` | Screenshots and diagrams |

## ▶️ How to open it

1. Install **Power BI Desktop** and enable the PBIP / TMDL / PBIR preview features (*Options → Preview features*).
2. Clone or download this repo, then open `HR Dashboard.pbip`.
3. Go to **Transform data → Manage parameters** and set **Source File Path** to where `HR_Dashboard_Mock_Data.xlsx` is saved on your machine.
4. **Refresh.**

## 🛠 Tools

Power BI Desktop (PBIP · TMDL · PBIR) · DAX · Power Query · Canva · HTML/CSS/JS · **Claude** (Canva MCP, Power BI Modeling MCP, report authoring) · Git/GitHub

> All data is synthetic. No real employee information. Built as a self-learning portfolio project.
