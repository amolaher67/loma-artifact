# The E.A.R.N. Architectural Framework

### 1. 📊 **E**stimate (Rough Order of Magnitude)
Never give a single deadline date. Give a T-shirt size and a team-based duration range.
* **Format:** *[T-Shirt Size]* | *[Range in Team-Months]* | *[Variance Window]*
* **Example:** "This sounds like a **Large** initiative. Based on the concept, we are looking at roughly **4 to 6 months** for a single cross-functional team, with our standard early-stage variance of -50% to +100%."

### 2. 🧱 **A**ssumptions (Scope Boundaries)
Explicitly state what must be true for your estimate to hold. This defines what you *think* they are asking for and draws a boundary.
* **Architecture Reuse:** Can you leverage existing infrastructure, databases, or auth systems?
* **Third-Party Tech:** Are you building it from scratch or buying a SaaS/API solution?
* **Exclusions (The "Not" List):** What is explicitly out of scope for version 1.0?
* **Example:** "My estimate assumes we are **reusing our existing user identity service** and integrating a third-party SMS API rather than building our own notification engine. It **excludes internationalisation** and compliance for regions outside our current market."

### 3. ⚡ **R**isks (The Swing Factors)
Identify the high-complexity items that could completely blow up the timeline. These are your architectural "known unknowns."
* **Integration Points:** Are you relying on unstable or poorly documented legacy systems?
* **Performance & Scale:** Does this introduce massive data volumes, real-time sync, or strict SLA requirements?
* **Skill Gaps:** Does the team have the technical expertise to build this today?
* **Example:** "The two biggest swing factors here are **real-time data sync** and **offline mobile support**. If we need the app to function entirely offline and sync data later, it will easily push us to the higher end of that 6-month estimate due to conflict resolution logic."

### 4. 🚀 **N**ext Steps (The Discovery Gate)
Propose a time-boxed engineering spike or architectural discovery phase to shrink the uncertainty window.
* **The Pitch:** Give them a low-cost option to get a high-accuracy estimate.
* **Example:** "To narrow this down to a tighter 15% window, let’s do a **3-day architectural discovery**. I will draft a high-level system context diagram and map out the data flows. Let's sync on Friday afternoon to review the refined options."

---

## ⏱️ The 5-Minute "Elevator Pitch" Template
*Copy, paste, and fill this out for quick Slack messages or verbal syncs:*

> **"Hey [PM Name], off the top of my head based on the idea..."**
> * **Size/Effort:** It feels like a **[Medium/Large]** effort, likely **[X to Y months]** for a team.
> * **If we assume:** We can reuse **[Existing Component]** and don't have to build **[Complex Feature]**.
> * **The biggest risks are:** **[Risk 1]** and **[Risk 2]**, which could swing the timeline.
> * **To move forward:** Let's spend **[2-3 days]** on a quick architectural spike to map the integration points and get you a solid roadmap number.

--------------------------------
# High-Level Estimate: Restaurant Logistics Application Example

Let's practice this scenario. Imagine your manager, Sarah, walks up to you and says:

> "Hey, we want to add a new 'Restaurant Logistics' app to our ecosystem. It needs to handle > driver dispatch, route optimization, and real-time delivery tracking for our food orders. 
> What’s the ballpark estimate for this?"

As an Architect, here is exactly how you should structure your immediate response using the "Estimate, Assume, Risk, Next Step" framework.


### 1. 📊 **E**stimate (Rough Order of Magnitude)
* **T-Shirt Size:** Large
* **Duration:** **3 to 6 Team-Months** (1 to 2 quarters for a dedicated product team).
* **Variance Window:** -50% to +100% (High uncertainty due to initial concept stage).

### 2. 🧱 **A**ssumptions (Scope Boundaries)
* **Context Reuse:** We will leverage our existing core customer, restaurant, and order data models. We are *not* rebuilding the core ordering database.
* **Map Services:** We will integrate third-party APIs (like Google Maps or Mapbox) for route calculation rather than writing a proprietary routing algorithm.
* **Infrastructure:** The application will live in our existing cloud environment and use our current CI/CD pipeline, avoiding new infrastructure setup overhead.
* **Out of Scope:** This estimate **excludes** cold-chain/temperature hardware tracking or automated drone delivery. It assumes standard vehicle/bike delivery.

### 3. ⚡ **R**isks (The Swing Factors)
* **Real-Time Scaling:** Real-time driver tracking requires a WebSocket or event-driven architecture. If our current infrastructure cannot support high-frequency location pings from thousands of drivers, this will require a heavy backend refactor.
* **The Mobile Dilemma:** Do drivers need a native iOS/Android app with background location tracking, or can they use a mobile web app? A native app adds months of development and app store approval risks.
* **The "Courier Assignment" Algorithm:** Is the matching logic simple (e.g., assign to the closest driver) or complex (e.g., batched orders, predictive arrival times)? Complex logic requires data science resources we may not have.

### 4. 🚀 **N**ext Steps (The Discovery Gate)
* **The Proposal:** Let's initiate a **3-day architectural discovery spike**.
* **The Deliverables:** I will sit down with the Product Manager to map out the 3 core integration points with our existing system and sketch a high-level data flow diagram.
* **The Goal:** Sync on Thursday afternoon to review the refined options and narrow this estimate down to a tighter 20% variance window.
