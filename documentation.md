# 3psLCCA User Guide

![Main Logo](logo/logo-3psLCCA-light.png)

> **Version:** 2026.04.1 | **Developed at:** Osdag, FOSSEE, IIT Bombay | **Supported by:** ConstructSteel, Ministry of Steel, INSDAG

---

## Introduction

**3psLCCA** is a desktop application for **Life Cycle Cost Analysis (LCCA)** of bridge infrastructure projects, developed at IIT Bombay.

LCCA evaluates the total cost of a bridge across its entire service life — not just initial construction, but maintenance, repair, demolition, recycling, and associated environmental and social costs. All costs are brought to a common present-day value using discounting, allowing direct comparison of different design alternatives.

The analysis is structured around **three pillars of sustainability**:

![Sustainability Components](documentation_images/sustainablity_pillars.png)

- **Economic** — direct monetary costs: construction, maintenance, demolition
- **Social** — road user costs: delays, accident costs, and detour expenses incurred during construction and maintenance activities
- **Environmental** — carbon emission costs across the bridge life cycle

This guide uses a single example project throughout: a **2-lane RCC T-Girder road bridge** over the Sone River on a state highway in Bihar. This is a straightforward, commonly built bridge type — suitable for demonstrating all features of the application without introducing complexity specific to long-span or special structures. All field values, quantities, and screenshots in this guide refer to this project.

**Coverage:**

1. Launching the application and the Home screen
2. Creating and opening projects
3. Comparing projects
4. General Information and Bridge Data input
5. Construction Work Data (Foundation, Sub Structure, Super Structure, Miscellaneous)
6. Financial, Traffic, Maintenance, Demolition, and Carbon Emission parameters
7. Running the analysis and interpreting results
8. Generating a PDF report

> Technical terms are defined inline at their first occurrence throughout this guide.

---

## Part A — Home Screen, New Project, Open, and Compare

### A.1 Launching the Application

Activate the conda environment and launch the application from the terminal:

```bash
conda activate 3psLCCA
threePSLCCA
```

A splash screen is displayed while the application loads its material databases and configuration.

![Splash Screen](documentation_images/partA/01_splash_screen.png)

---

### A.2 The Home Screen

The Home Screen is the first screen you see after the app loads. It is divided into three structural areas: the **Left Sidebar**, the **Top Bar**, and the **Main Content Area**.

<!-- ============================================================
IMAGE PLACEHOLDER — A.2
File: documentation_images/partA/02_home_screen_annotated.png

HOW TO CAPTURE:
- Launch the app with at least one existing project visible
- Full window screenshot (include window titlebar)

HOW TO ANNOTATE:
- Use filled blue circles (⬤ #2563EB, white number inside) for all callouts
- ① Draw a tall rectangular blue box (#2563EB, 2px) enclosing the entire left sidebar strip
  Label outside the box to the right: "① Left Sidebar"
  Arrow: horizontal arrow from label pointing left into the sidebar box
- ② Draw a rectangular blue box along the top bar (from window title to right edge)
  Label above: "② Top Bar — project filter controls and search"
  Arrow: downward arrow from label into the bar
- ③ Draw a rectangular blue box around the entire main content area (project cards region)
  Label: "③ Main Content Area — project cards"
  Arrow: arrow pointing into the card grid
- Do NOT annotate individual buttons or text within — that is done in subsequent screenshots
============================================================ -->

![Home Screen — Overview](documentation_images/partA/02_home_screen_annotated.png)

---

#### A.2.1 Left Sidebar

The left sidebar is fixed and visible on every screen in the application. It contains five navigation buttons, each leading to a distinct area.

![Left Sidebar — Annotated](documentation_images/partA/03_sidebar_annotated.png)

| Button | Action |
|--------|--------|
| **Home** | Returns to the project dashboard from anywhere in the app |
| **New** | Opens the New Project dialog |
| **Open** | Opens a file browser to load an existing `.3psLCCA` project file |
| **Compare** | Opens the project comparison view |
| **Settings** | Opens application preferences and agency profile management |

---

#### A.2.2 Top Bar and Project Views

The toolbar sits between the greeting area and the project grid. It contains a **dynamic section label**, a **refresh button**, a **search field**, and **four view filter buttons** — Recent, All, Starred, and Compare. The section label updates automatically to reflect the active view.

![Top Bar — Annotated](documentation_images/partA/04_topbar_annotated.png)

| Button | Section Label shown | What is listed |
|--------|---------------------|----------------|
| **Recent** | RECENT PROJECTS | All projects, sorted by last opened or last modified — most recent first |
| **All** | ALL PROJECTS — A-Z | All projects, sorted alphabetically by name |
| **Starred** | STARRED PROJECTS | Only projects you have starred (pinned). If none are starred, shows an empty state with instructions. |
| **Compare** | READY TO COMPARE | Only projects that have been fully calculated and locked. Enables multi-select mode for loading into the Compare view. |

The **search field** applies on top of whichever view is active — typing filters the current list in real time and changes the section label to `RESULTS FOR "..."`.

Each view is shown individually below.

##### Recent View

![View — Recent](documentation_images/partA/04a_view_recent.png)

##### All View

![View — All](documentation_images/partA/04b_view_all.png)

##### Starred View

![View — Starred](documentation_images/partA/04c_view_starred.png)

##### Compare View

<!-- Will do later -->
<!-- ![View — Compare](documentation_images/partA/04d_view_compare.png) -->

> Projects appear in the Compare view only if they have been fully calculated and locked. A project that is still in progress will not appear here.

---

#### A.2.3 Project Cards

Each project in the list is shown as a card in the main content area.

![Project Card — Annotated](documentation_images/partA/05_project_card_annotated.png)

Each card shows:

- **Project name**
- **Last modified** — relative timestamp ("2 hours ago", "Yesterday")
- **Status badge**:

| Badge | Meaning |
|-------|---------|
| `OK` | Project is intact and ready to open |
| `Open` | Project is currently open in another window |
| `Needs Recovery` | Project was not closed cleanly; app will attempt recovery on open |
| `Corrupted` | Project file is unreadable and cannot be opened |

---

### A.3 Creating a New Project

Click **New** in the sidebar, or the **+ New Project** button on the Home Screen. The New Project dialog opens.

![New Project Dialog](documentation_images/partA/06_new_project_dialog.png)

| Field | Required | Behaviour |
|-------|----------|-----------|
| **Project Name** | Yes | Free text. Can be edited later in the General Information section. |
| **Country** | Yes | Selects the material rate database and regional standards. **Locked after creation.** |
| **Currency** | Auto | Auto-filled when Country is selected. All monetary values across the project use this currency. **Locked after creation.** |
| **Unit System** | Yes | `Metric (SI)`: metres and kilograms. `Imperial (English)`: feet and pounds. **Locked after creation.** |

> Country, Currency, and Unit System cannot be changed after the project is created because every cost calculation, unit conversion, and material rate lookup in the project depends on them. Changing them mid-project would produce inconsistent results across all sections.

**Values used in this guide:**

```
Project Name : Sone River Road Bridge
Country      : India
Currency     : INR
Unit System  : Metric (SI)
```

Click **Create**. The app initialises the project and opens the project workspace.

---

### A.4 Opening an Existing Project

**From the Home Screen:** Click any project card. The project opens immediately.

**From disk:** Click **Open** in the sidebar. A file browser opens — navigate to the `.3psLCCA` file and select it.

![Open File Browser](documentation_images/partA/07_open_file_browser.png)

> A `.3psLCCA` file is a self-contained project archive. It holds all input data, results, and checkpoints for a single project. It can be copied, moved, or shared like any other file.

---

### A.5 Comparing Projects

The Compare view places two or more projects side by side, showing a breakdown of their life cycle costs. This is the primary tool for evaluating design alternatives against each other — for example, a concrete box girder bridge versus a cable-stayed bridge at the same location.

> Only projects that have been fully calculated (via the **Calculate** button) produce data in the comparison view.

#### A.5.1 Opening the Compare View

Click **Compare** in the sidebar.

<!-- ============================================================
IMAGE PLACEHOLDER — A.5.1
File: documentation_images/partA/08_compare_empty.png

HOW TO CAPTURE:
- Click Compare in the sidebar before any projects are loaded into comparison
- Full window screenshot

HOW TO ANNOTATE:
- ① Draw a rectangular blue box around the project selector / "Add Project" control
  Label: "① Select projects to compare"
- ② If an empty-state illustration or message is shown in the centre, draw a blue box
  Label: "② No projects loaded yet"
============================================================ -->

![Compare — Empty](documentation_images/partA/08_compare_empty.png)

#### A.5.2 Loading Projects and Reading the Comparison Table

Add projects using the selector at the top of the Compare view. The table populates once at least two calculated projects are loaded.

<!-- ============================================================
IMAGE PLACEHOLDER — A.5.2
File: documentation_images/partA/09_compare_loaded.png

HOW TO CAPTURE:
- Load two or more calculated projects into the Compare view
- Full window screenshot showing the populated comparison table

HOW TO ANNOTATE:
- ① Draw a rectangular blue box along the top row containing project name headers
  Label: "① Project columns — one per project"
- ② Draw a rectangular blue box around one complete cost row
  (e.g. the "Initial Construction Cost" row)
  Label: "② Cost item row"
- ③ Draw a rectangular blue box around the grand total / LCCA total row at the bottom
  Label: "③ Total Life Cycle Cost (present value)"
- ④ If a bar chart or pie chart is visible, draw a rectangular blue box around it
  Label: "④ Visual cost breakdown"
- ⑤ Draw a rectangular blue box around the Add / Remove project controls
  Label: "⑤ Add or remove projects"
============================================================ -->

![Compare — Loaded](documentation_images/partA/09_compare_loaded.png)

Each column in the table corresponds to one project. Each row is a cost category. The **Total Life Cycle Cost** row at the bottom is the single number used to compare alternatives.

---

### A.6 Settings

Click **Settings** in the sidebar. The Settings dialog opens as a modal window with two tabs: **General** and **Profiles**.

#### A.6.1 General Tab

The General tab controls display name and appearance.

![Settings — General Tab](documentation_images/partA/10_settings_general.png)

| Field | Description |
|-------|-------------|
| **Display Name** | Your name as it will appear in generated reports. |
| **Appearance Mode** | `Auto` follows the OS light/dark setting. `Light` and `Dark` override it. |
| **Light Theme** | Colour scheme used when in light mode. |
| **Dark Theme** | Colour scheme used when in dark mode. |

> Theme changes take effect immediately on clicking **Save**.

#### A.6.2 Profiles Tab

The Profiles tab stores agency details — name, logo, address, and contact information — that can be reused across projects.

![Settings — Profiles Tab](documentation_images/partA/11_settings_profiles.png)

| Element | Description |
|---------|-------------|
| **Avatar** | Displays the first letter of the profile name, or the uploaded logo. Click to upload a PNG/JPG. |
| **Profile selector** | Dropdown listing all saved profiles. Select `+ New Profile` to create one. |
| **Delete Profile** | Permanently removes the selected profile from local storage. |
| **Form fields** | Assessor's name, organisation name, logo, address, country, email, phone. |

> Profiles are stored locally on the machine — not inside any project file. To populate a project's General Information section with a saved profile, use **Load Agency Profile** inside that project.

---

### A.7 Frequently Asked Questions

**Q: Can I rename a project after creation?**
Yes. The Project Name field in the **General Information** section is editable at any time. Country, Currency, and Unit System cannot be changed.

**Q: What happens if I open a project that is already open in another window?**
The app detects this and shows an `Open` status badge on the project card. Opening it again will prompt you to confirm.

**Q: The app shows "Needs Recovery" on my project. Is data lost?**
Not necessarily. This badge appears when the project was not closed cleanly (e.g. a crash or force-quit). Open the project — the app will attempt to recover the last saved state automatically. Check your data after recovery and use a Checkpoint if anything looks incorrect.

**Q: I cannot find my project on the Home Screen.**
Use the **Search bar** — type any part of the project name. Alternatively, use **Open** to browse directly to the `.3psLCCA` file on disk.

**Q: Can I share a project file with a colleague?**
Yes. Copy the `.3psLCCA` file and send it. Your colleague can open it using **Open** in their installation of 3psLCCA. All data, inputs, and results are embedded in the single file.

**Q: Compare shows zero values for one of my projects.**
The Compare tool only shows data for projects that have been calculated. Open the project, complete all required inputs, and click **Calculate** to generate results before comparing.

---



## Part B: Project Workspace and Basic Data Entry

After creating or opening a project, the project workspace opens. This is the main working environment where all project data is entered, edited, and calculated.

---

### B.1 The Project Workspace Layout

The workspace follows a consistent three-zone layout that persists across all data entry pages.

<!-- ============================================================
IMAGE PLACEHOLDER — B.1
File: documentation_images/partB/01_workspace_overview.png

HOW TO CAPTURE:
- Create the example project (Sone River Road Bridge) and open it
- Take a full window screenshot showing the project workspace
- General Information page should be active (it's the first page)

HOW TO ANNOTATE:
- ① Draw a rectangular blue box around the entire left sidebar
  Label: "① Navigation menu — access all data sections"
- ② Draw a rectangular blue box around the top header bar
  Label: "② Project header — name, status, action buttons"
- ③ Draw a rectangular blue box around the main content area
  Label: "③ Data entry area — forms, tables, and inputs"
- Use arrows pointing from labels outward to their respective zones
============================================================ -->

![Project Workspace Overview](documentation_images/partB/01_workspace_overview.png)

#### B.1.1 Left Navigation Menu

The left sidebar provides access to all project data sections.

<!-- ============================================================
IMAGE PLACEHOLDER — B.1.1
File: documentation_images/partB/02_left_navigation.png

HOW TO CAPTURE:
- Crop tightly to just the left sidebar navigation menu
- Height should include all menu items from top to bottom

HOW TO ANNOTATE:
- Draw rectangular blue boxes around each menu item, numbered ① to ⑩:
  ① "General Information"
  ② "Bridge Data"
  ③ "Construction Work Data"
  ④ "Financial Data"
  ⑤ "Traffic and Road Data"
  ⑥ "Maintenance Data"
  ⑦ "Demolition Data"
  ⑧ "Carbon Emission"
  ⑨ "Recycling"
  ⑩ "Results"
- For items ③ and ⑧, add a small note: "Has sub-menus"
============================================================ -->

![Left Navigation Menu](documentation_images/partB/02_left_navigation.png)

| Menu Item | Purpose | Sub-pages |
|-----------|---------|-----------|
| **General Information** | Project metadata, agency details, basic settings | — |
| **Bridge Data** | Technical specifications, location, life cycle | — |
| **Construction Work Data** | Material quantities and costs for structural components | Foundation, Sub Structure, Super Structure, Misc |
| **Financial Data** | Economic parameters (discount rate, inflation, interest) | — |
| **Traffic and Road Data** | Traffic volume, accident rates, road parameters | — |
| **Maintenance Data** | Routine, periodic, and major maintenance schedules | — |
| **Demolition Data** | End-of-life costs and duration | — |
| **Carbon Emission** | Carbon footprint calculations | Material, Transportation, Machinery, Traffic Diversion, Social Cost |
| **Recycling** | Material recyclability and recovered value | — |
| **Results** | LCCA calculation results and comparison charts | — |

> The active page is highlighted in the menu. All menu items remain clickable at all times.

#### B.1.2 Project Header Bar

The top bar shows project identification and primary action buttons.

<!-- ============================================================
IMAGE PLACEHOLDER — B.1.2
File: documentation_images/partB/03_project_header.png

HOW TO CAPTURE:
- Crop to just the header bar area (top of window, full width)
- Include project name, status indicator, and buttons

HOW TO ANNOTATE:
- ① Blue arrow pointing to the project name text
  Label: "① Project name"
- ② Blue arrow pointing to the status indicator (dot or icon)
  Label: "② Status — unsaved changes / saved / calculated"
- ③ Draw a rectangular blue box around the "Save" button
  Label: "③ Save checkpoint"
- ④ Draw a rectangular blue box around the "Calculate" button
  Label: "④ Run LCCA analysis"
- ⑤ If visible, draw a rectangular blue box around the "Report" button
  Label: "⑤ Generate PDF report"
============================================================ -->

![Project Header Bar](documentation_images/partB/03_project_header.png)

| Element | Description |
|---------|-------------|
| **Project name** | Display name of the current project. Click to edit. |
| **Status indicator** | Visual indicator of project state: white dot (unsaved), green check (saved), lock icon (calculated and locked). |
| **Save** | Creates a checkpoint. Saves all current data to the project file. |
| **Calculate** | Validates all inputs and runs the LCCA computation. Required before viewing Results or Compare. |
| **Report** | Generates a PDF report (available after calculation). |

---

### B.2 General Information

Click **General Information** in the left navigation menu. This page captures project metadata and agency details.

<!-- ============================================================
IMAGE PLACEHOLDER — B.2
File: documentation_images/partB/04_general_info_overview.png

HOW TO CAPTURE:
- Navigate to General Information page
- Full window screenshot
- If agency profile fields are empty, fill in example values first

HOW TO ANNOTATE:
- ① Draw a rectangular blue box around the "Project Information" section
  Label: "① Project Information"
- ② Draw a rectangular blue box around the "Evaluating Agency" section
  Label: "② Evaluating Agency"
- ③ Draw a rectangular blue box around the "Reviewed By" section
  Label: "③ Reviewed By"
- ④ Draw a rectangular blue box around the "Project Settings" section
  Label: "④ Project Settings — locked at creation"
- ⑤ Draw a rectangular blue box around the "Load Agency Profile" button
  Label: "⑤ Load saved profile"
============================================================ -->

![General Information Overview](documentation_images/partB/04_general_info_overview.png)

#### B.2.1 Project Information

| Field | Editable | Description |
|-------|----------|-------------|
| **Project Name** | Yes | Display name used in reports and project listings. |
| **Project Code** | Yes | Internal reference code or contract number. |
| **Description** | Yes | Brief narrative description of the project. |
| **Remarks** | Yes | Additional notes, assumptions, or special conditions. |

#### B.2.2 Evaluating Agency

This section auto-populates when **Load Agency Profile** is clicked (if a profile was saved in Settings).

| Field | Description |
|-------|-------------|
| **Agency Logo** | PNG or JPG image. Appears on the cover page of generated reports. |
| **Agency Name** | Full legal name of the evaluating organisation. |
| **Contact Person** | Name of the primary assessor or engineer. |
| **Address** | Physical address of the agency. |
| **Country** | Country where the agency is based. |
| **Email** | Contact email address. |
| **Phone** | Contact phone number. |

#### B.2.3 Reviewed By

| Field | Description |
|-------|-------------|
| **Name** | Reviewer or approver name. |
| **Organization** | Reviewer's organisation. |
| **Address** | Reviewer's address. |
| **Country** | Reviewer's country. |
| **Email** | Reviewer's email. |
| **Phone** | Reviewer's phone. |

#### B.2.4 Project Settings

These fields are set at project creation and **cannot be changed**.

| Field | Description |
|-------|-------------|
| **Project Country** | Determines the material rate database and regional standards. |
| **Project Currency** | All monetary values use this currency. |
| **Unit System** | `Metric (SI)` or `Imperial (English)`. Affects all length and weight inputs. |
| **Material Suggestions** | Toggle auto-suggestions from the built-in material database. |

---

### B.3 Bridge Data

Click **Bridge Data** in the left navigation menu. This page captures the technical specifications and physical characteristics of the bridge.

<!-- ============================================================
IMAGE PLACEHOLDER — B.3
File: documentation_images/partB/05_bridge_data_overview.png

HOW TO CAPTURE:
- Navigate to Bridge Data page
- Fill in example values for the Sone River Road Bridge:
    Name of the Bridge: Sone River Road Bridge
    Owner: [Example State PWD or similar]
    Type of Bridge: Girder
    Span: 45 (metres)
    Carriageway Width: 7.5 (metres)
    Number of Lanes: 2
    Vehicle Path Direction: Two Way
    Footpath: No footpath (or Footpath at one side)
    Design Life: 50 (years)
    Year of Construction: 2024 (or current year)
    Duration of Construction: 18 (months)
- Full window screenshot

HOW TO ANNOTATE:
- ① Draw a rectangular blue box around the "Bridge Identification" section
  Label: "① Bridge Identification"
- ② Draw a rectangular blue box around the "Location" section
  Label: "② Location"
- ③ Draw a rectangular blue box around the "Technical Specifications" section
  Label: "③ Technical Specifications"
- ④ Draw a rectangular blue box around the "Life Cycle" section
  Label: "④ Life Cycle"
- ⑤ Draw a rectangular blue box around the "Construction Schedule" section
  Label: "⑤ Construction Schedule"
- ⑥ Draw a rectangular amber box around the "Clear All" button
  Label: "⑥ Clear All — resets all fields"
============================================================ -->

![Bridge Data Overview](documentation_images/partB/05_bridge_data_overview.png)

#### B.3.1 Bridge Identification

| Field | Description |
|-------|-------------|
| **Name of the Bridge** | Official name of the bridge structure. |
| **Owner** | Name of the owner, client, or responsible agency. |

#### B.3.2 Location

| Field | Description |
|-------|-------------|
| **Country** | Auto-filled from project creation. Locked. |
| **Bridge Alignment & Location** | Description of start point, end point, crossed feature (river, valley, railway), and nearby landmarks. |

#### B.3.3 Technical Specifications

| Field | Description | Typical Range |
|-------|-------------|---------------|
| **Type of Bridge** | Structural classification. Options: Girder, Arch, Cable-Stayed, Suspension, Truss, Box Girder, Slab, Other. | — |
| **Span** | Total span length between supports. | 20–500 m (girder bridges typically 30–100 m) |
| **Carriageway Width** | Clear width of the roadway portion. | 3.5–15 m |
| **Number of Lanes** | Total traffic lanes. | 1–8 |
| **Vehicle Path Direction** | One Way or Two Way traffic flow. | — |
| **Footpath** | Pedestrian provision: No footpath / Footpath at one side / Footpath at both sides. | — |

> **Validation warnings:** The app highlights unusual values. Span > 5000 m, carriageway width < 1.5 m or > 50 m, or lanes > 16 trigger verification prompts.

#### B.3.4 Life Cycle

| Field | Description | Typical Value |
|-------|-------------|---------------|
| **Design Life** | Expected operational service life in years. | 50–100 years |
| **Year of Construction** | Year of construction (past or future). | Current year or future |

> **Validation:** Year of Construction before the current year triggers a warning to verify the input is intentional.

#### B.3.5 Construction Schedule

| Field | Description | Typical Value |
|-------|-------------|---------------|
| **Duration of Construction** | Total construction time in months. | 6–48 months |
| **Working Days per Month** | Assumed working days for scheduling. Default: 22 | 20–26 days |
| **Days per Month** | Days per month the road traffic is affected. Default: 30 | 29–31 days |

> **Cross-field validation:** Working Days per Month cannot exceed Days per Month. If violated, a warning appears on the Working Days field.

