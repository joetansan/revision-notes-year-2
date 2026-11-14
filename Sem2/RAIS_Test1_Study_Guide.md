# RAIS — Test 1 Study Guide
### Responsible AI for Sustainability · Topics 1–4

> **Test format (from the announcement)**
> | | |
> |---|---|
> | **Structure** | 15 MCQ + 2 or 3 SAQ |
> | **Total marks** | 25 |
> | **Time** | 40 minutes |
> | **When** | Week 5, first thing in the lesson (tutorial debrief after) |
>
> **Implied mark breakdown:** 15 MCQ × 1 mark = 15 marks, leaving **10 marks of SAQ** (e.g. 4 + 3 + 3).
> **Timing plan:** MCQ 15 min (≈1 min each, no stalling — flag and move) → SAQ 20 min → 5 min review.
>
> ⭐ = high-yield. These are the items most likely to be tested, based on slide emphasis and tutorial coverage.

---

## 0. The single most important idea

This module is **not technical**. There is nothing to calculate except payback period / ROI. Every mark comes from **knowing the exact vocabulary and the exact lists**. Most MCQs are "which of these is NOT…" or "which is the best definition…". That means:

1. **Learn the lists verbatim** (4 pillars, 6 OECD principles, 6 AI principles, 6 AI risks, 6 key assets, 7 COBIT components, 5 life-cycle phases, 5 portfolio processes, 3 agility loops, 3 barriers).
2. **Learn the pairs that get swapped** — this is where the marks are lost (conformance vs performance, pain point vs trigger event, business vs intermediate benefits, expression vs specification vs implementation barrier).
3. **In SAQs, use the slide's own phrases.** Markers are looking for keywords, not prose.

---

# TOPIC 1 — Introduction to Governance, Responsible AI & Sustainability

## 1.1 ⭐ The three governance definitions (learn word-for-word)

| Type | Definition (slide wording) | Scope |
|---|---|---|
| **Corporate Governance** | Ensure that the company is **run and managed to achieve the company's mission and vision**, in accordance with the **stakeholders' needs**. | The whole corporation |
| **IT Governance** | Ensure that **IT is managed to achieve the company's business objectives**, in the **most efficient manner**, **maximizing the benefits** to achieve stakeholders' needs. | The role of IT in the corporation |
| **AI Governance** | Ensure that **AI is managed through effective controls**, implemented in the **most efficient manner to create value** to achieve stakeholders' needs. | AI *within* IT governance |

### ⭐ How the three relate (near-certain MCQ)

- Each model is **independent of the other**
- **Different emphasis but similar objectives**
- Not interchangeable, not sequential steps, not unrelated

> **The hierarchy:** Corporate governance ⊃ IT governance ⊃ AI governance. AI governance sits *inside* IT governance, which sits inside corporate governance — but each is an independent model in its own right.

**Trap:** "Identical frameworks that can be used interchangeably" (✗) and "Sequential steps in a single overarching governance process" (✗). The correct phrasing is **"independent but related models with different emphases but similar objectives."**

## 1.2 ⭐ The Four Pillars of IT Governance

| # | Pillar | What it covers |
|---|---|---|
| 01 | **Strategic Management** | Aligning IT with business strategy (Topic 3) |
| 02 | **Benefits Realization** | Ensuring investments deliver promised value (Topic 4) |
| 03 | **Risk Optimization** | Identifying, assessing, mitigating IT risk |
| 04 | **Resource Optimization** | Efficient use of IT resources |

> **Wording warning:** the slides say **Risk Optimization** and **Resource Optimization**. The Tutorial 1 quiz lists "Risk Management" — treat "Risk Management" as the same pillar. What is **NOT** a pillar: **Software Development** (that's an engineering activity, not a governance pillar).

**Memory hook — "SBRR":** **S**trategic, **B**enefits, **R**isk, **R**esource. Notice that **Topics 3 and 4 of this module are literally pillars 1 and 2** — that's why they're examined.

## 1.3 What governance provides (slide 4)

IT Governance is: **"…the system by which the use of IT within an organisation is directed and controlled, ensuring alignment with business strategy, management of risk, and delivery of value."**

Five things governance provides (slide 4):

| Provides | Meaning |
|---|---|
| **Structure** | Without governance, technology growth outpaces our ability to manage its risks |
| **Risk Management** | Identify, assess, and mitigate IT risks before they become crises |
| **Accountability** | Define who is responsible for IT decisions, outcomes, and assets |
| **Compliance & Trust** | Align with laws, regulations, industry standards to build stakeholder trust |
| **Value Creation** | Ensure IT investments deliver measurable business value and ROI |

## 1.4 Code of Corporate Governance (Singapore)

- ⭐ **Published by the Monetary Authority of Singapore (MAS)**
- Applies to **publicly-listed companies** (shares traded on the stock exchange)
- Describes the **composition and various functions of the board** in running the company
- Provides for **accountability, transparency and confidence** in the company

> **Trap:** SGX, IMDA and MDDI are all plausible-sounding Singapore bodies. The Code is **MAS**. (SGX runs the exchange; IMDA is infocomm/media; MDDI is the ministry.)

### The Code emphasises five things ⭐

| Emphasis | What it means |
|---|---|
| **Board Composition and Independence** | Strong independent element; clear separation of Chairman and CEO roles where possible |
| **Accountability and Transparency** | Clear reporting, disclosure, and risk management practices |
| **Remuneration Practices** | Executive and board pay fair, transparent, linked to performance |
| **Shareholder Rights** | Respect and protect shareholder interests; mechanisms for engagement and voting |
| **Culture and Ethics** | Boards foster an ethical corporate culture and set the tone for behaviour |

## 1.5 ⭐ Role of Corporate Governance (four contexts — a classic SAQ)

| Context | Why governance is needed |
|---|---|
| **Stock exchanges / public companies** | Companies are run by senior management **on behalf of shareholders**. Need to ensure senior management **do not act in a manner that benefits themselves at the expense of the public good** → **Enron scandal, 2001** |
| **Board of directors** | Appointed to **ensure accountability** and **define the objectives** of the organisation |
| **Private / non-public companies** | Ensure the company is run according to the **expectations of the stakeholders, especially its owners** |
| **Government agencies** | Board appointed to ensure the organisation **achieves its stated objectives as defined by the government** |

> ⭐ **The Enron anchor:** October 2001 → collapse → **Sarbanes-Oxley (SOX) Act**. This is the single most quoted example in Topics 1 and 2.

### Need for Governance (slide 15)
Governance ensures the enterprise is doing the **'right thing'** — achieving the aims of its owners while keeping stakeholders' interests intact.

Three key questions:
1. What is the 'right thing'?
2. Who are the owners and stakeholders?
3. How to ensure the 'right thing' is done?

## 1.6 ⭐ OECD Principles of Corporate Governance (6 — memorise the names)

| # | Principle | Substance |
|---|---|---|
| **I** | **Ensuring the basis for an effective corporate governance framework** | Framework should promote transparent and efficient markets, be consistent with the rule of law, clearly articulate division of responsibilities among supervisory, regulatory and enforcement authorities |
| **II** | **The rights of shareholders and key ownership functions** | Framework should protect and facilitate the exercise of shareholders' rights |
| **III** | **The equitable treatment of shareholders** | Equitable treatment of **all** shareholders, **including minority and foreign shareholders**; all shareholders should have opportunity for **effective redress** |
| **IV** | **The role of stakeholders in corporate governance** | Recognise rights of stakeholders established by law or mutual agreements; encourage active co-operation in creating wealth, jobs and sustainability |
| **V** | **Disclosure and transparency** | Timely and accurate disclosure on **all material matters** — financial situation, performance, ownership, governance |
| **VI** | **The responsibilities of the board** | Strategic guidance of the company, effective monitoring of management by the board, board's accountability to the company and shareholders |

> **Memory hook:** **F**ramework → **R**ights → **E**quitable → **S**takeholders → **D**isclosure → **B**oard. ("**F-R-E-S-D-B**" — or just remember it's the *lifecycle of a shareholder relationship*: the rules exist, you get rights, you're treated equally, others matter, you're told the truth, the board answers to you.)

### ⭐ The insider-trading question (Tutorial 1 Q7 — learn the reasoning, not just the answer)

> *Senior executives use confidential internal information to profit from trading the company's own shares. Which governance concept is most directly violated?*

**Answer: The equitable treatment of shareholders.**

**Why:** insider trading means insiders profit **at the expense of other shareholders** who don't have that information — that is *inequitable treatment* (Principle III), not merely a disclosure failure. "Disclosure and Transparency" (V) is the tempting distractor because it mentions information — but V is about the **company disclosing material matters to the market**, not about **insiders trading on what hasn't been disclosed**.

### ⭐ The scandal question (Tutorial 2 Q4)
**October 2001 → Enron collapse → Sarbanes-Oxley Act.**
- WorldCom → 2002 (also led to SOX strengthening, but the *trigger* was Enron)
- Lehman Brothers → 2008 (Global Financial Crisis)
- Madoff → 2008 (Ponzi scheme)

## 1.7 Why IT Governance matters (and what it does NOT promise)

| Situation | Consequence |
|---|---|
| Increased dependency on IT | **Failure of IT governance may mean business disruption or worse, failure** |
| Mild cases | Ineffective use of IT → **wastage and lost opportunities** |
| Important caveat ⭐ | **Lack of IT governance may NOT mean business failure or loss** |
| Driver | **Digitalization** today drives the increasing importance of IT governance |

> ⭐ **The "no guarantee" line (Tutorial 2 Q15):** IT governance does **NOT** guarantee pain points will never occur. What it promises is **"a better position to address and react to problems, with reduced risk and limited impact."**
> This is a favourite MCQ because every other option is an absolute ("zero incidents", "immediate elimination", "full compliance") — **absolutes are almost always wrong** in this module.

## 1.8 ⭐ Six Principles of Responsible AI

| Principle | Definition (slide wording) |
|---|---|
| **Fairness** | AI systems should treat all individuals **equitably** and **not perpetuate or amplify discrimination** |
| **Transparency** | How AI systems work and make decisions should be **explainable and understandable** |
| **Privacy & Security** | AI must respect **data privacy, consent**, and protect against **misuse and cybersecurity threats** |
| **Human Oversight** | **Humans must remain in control of consequential AI decisions** and systems must be **correctable** |
| **Accountability** | **Clear lines of responsibility** must exist for AI outcomes and harms |
| **Safety & Reliability** | AI systems must **perform as intended**, be **robust to adversarial inputs**, and **fail safely** |

> **Memory hook — "F-T-P-H-A-S"** → *"Five Terrific Principles Help AI Succeed."*

### ⭐ Distinguishing the principles (MCQ meat)

| If the scenario is about… | Answer |
|---|---|
| Hiring AI disadvantages women; facial recognition misidentifies minorities | **Fairness** |
| Model's decisions are unexplainable, even to its developers | **Transparency** |
| Training data used without consent; mass surveillance | **Privacy & Security** |
| Humans must remain in control; systems must be correctable | **Human Oversight** |
| Nobody can be held responsible for harm | **Accountability** |
| Model breaks under adversarial input; doesn't fail safely | **Safety & Reliability** |
| An AI that is *open-source and free to use regardless of gender or ethnicity* | ❌ **NOT fairness** — that's about cost/licensing, not equitable outcomes |
| An AI that provides 24/7 service without human intervention | ❌ That's the **opposite** of Human Oversight |
| An AI that processes applications faster than humans | ❌ That's **efficiency**, not fairness |

> **Trap:** "Fairness" traps always involve **speed, cost, or availability**. Real fairness is about **outcomes not varying by protected attribute** (gender, ethnicity, etc.).

## 1.9 ⭐ Six Risks of Ungoverned AI

| Risk | Real-world manifestation |
|---|---|
| **Algorithmic Bias** | Facial recognition misidentifies minorities at higher rates; hiring AI systematically disadvantages women |
| **Privacy Violations** | Training on personal data without consent; surveillance enabling mass monitoring |
| **Deepfakes & Misinformation** | Convincing fake audio/video/text at scale, weaponised for disinformation |
| **Autonomous Systems** | Self-driving accidents; AI trading **'flash crashes'** — risk of removing human oversight from critical systems |
| **Job Displacement** | Rapid AI deployment without transition planning → economic disruption and social instability |
| **Concentration of Power** | A small number of companies control foundational AI models → concerns about **access, dependency, and democratic oversight** |

> ⭐ **Classification trap (Tutorial 1 Q13):** Job displacement = **social and economic risk**. Not "algorithmic" (that's bias/fairness), not cybersecurity, not environmental.

> ⭐ **Concentration-of-power trap (Tutorial 1 Q11):** When a few companies control foundational models, the governance concern is **"concentration of power, access, dependency, and democratic oversight."** Not software patents, bandwidth, or employee IP.

## 1.10 Learning from past technology cycles

| Technology | Era | Lesson |
|---|---|---|
| **The Internet** | 1990s–2000s | Deployed globally **before** content moderation, privacy standards or monopoly regulation existed — we are still addressing harms today |
| **Social Media** | 2000s–2010s | Prioritised **engagement over wellbeing** → mental health crises, political manipulation, erosion of democratic discourse |
| **Genetic Engineering** | 1970s–present | **Asilomar Conference (1975)** paused research to establish safety norms — a model for **proactive** governance |

> ⭐ **The quotable line:** *"Move fast and break things" is **not** an acceptable governance philosophy for AI.*

## 1.11 ⭐ Building Trustworthy AI (six practical steps)

**AI Ethics Policy · Diverse Training Data · Human-in-the-Loop Review · Explainability Tools · Bias Testing & Auditing · Incident Response Plan**

## 1.12 ⭐ Sustainability — the three pillars

| Pillar | Components (slide wording) |
|---|---|
| **Environmental** | Carbon footprint reduction · Energy efficiency in IT · E-waste management · Sustainable hardware procurement · Green data centre design |
| **Social** | Digital inclusion & equity · Fair labour in tech supply chains · Community impact of AI decisions · Privacy and human rights · Workforce transition support |
| **Economic** | Long-term value creation · Circular economy principles · Responsible innovation investment · Sustainable business models · Regulatory compliance & risk |

> ⭐ **Do not confuse with ESG.** The **three pillars of sustainability** = Environmental / Social / **Economic**. **ESG** = Environmental / Social / **Governance**. Both are examined; mixing them is the classic error.

## 1.13 The environmental cost of technology (know these four numbers)

| Stat | Value |
|---|---|
| Global electricity used by data centres | **2–3%** |
| Global CO₂ from the ICT sector | **4%** |
| E-waste generated annually | **50M+ tonnes** |
| Energy to train a large AI model vs a car's lifetime CO₂ | **10×** |

**The Paradox:** technology is simultaneously our greatest tool for solving environmental challenges (smart grids, precision agriculture, carbon modelling) **and** one of our fastest-growing sources of environmental harm. **Governance is what determines which path we take.**

## 1.14 ⭐ ESG for technology organisations

**ESG** = a framework used by **investors, regulators, and stakeholders** to evaluate how organisations manage **environmental impact, social responsibility, and governance quality**.

For tech companies, ESG is shifting **from voluntary reporting to mandatory disclosure**, and is a key driver of:
- **Access to capital**
- **Regulatory compliance**
- **Brand reputation**
- **Talent attraction & retention**

| Letter | Tech sector priorities |
|---|---|
| **E** | Scope 1/2/3 emissions, renewable energy targets, water use, e-waste |
| **S** | Diversity & inclusion, employee wellbeing, community impact, supply chain ethics |
| **G** | Board diversity, executive pay, anti-corruption, data privacy, tax transparency |

## 1.15 ⭐ Green IT — six strategies

| Strategy | Content |
|---|---|
| **Data Centre Efficiency** | Improving **PUE (Power Usage Effectiveness)**, liquid cooling, AI-optimised energy management |
| **Circular Economy** | Device refurbishment, responsible recycling, extended hardware lifetimes, buy-back schemes |
| **Renewable Energy** | On-site solar/wind, **Power Purchase Agreements (PPAs)**, renewable energy certificates |
| **Cloud Optimisation** | Right-sizing workloads, serverless architecture, migrating to lower-emission cloud regions |
| **Carbon Accounting** | Measuring and reporting **Scope 1, 2, and 3** emissions across the IT value chain |
| **Sustainable Software Engineering** | Energy-efficient code, reducing computational complexity, green software practices |

## 1.16 AI and sustainability — both directions ⭐

| ⚠ AI's environmental COSTS | ✓ AI FOR sustainability |
|---|---|
| Training LLMs consumes as much energy as **hundreds of transatlantic flights** | Optimising **energy grids** to balance renewable supply and demand in real time |
| **Data centre water consumption** for cooling — AI accelerates demand | **Precision agriculture** reducing water and fertiliser use by **up to 25%** |
| Rapid hardware refresh cycles → **rare earth mining** | Accelerating **materials science and carbon capture** research |
| **Inference at scale** → continuous, growing energy demand | **Predictive maintenance** extending equipment lifetimes and reducing waste |

## 1.17 ⭐ The interconnection (Topic 1's closing argument)

| Combination | Result |
|---|---|
| **AI Ethics + IT Governance** | Responsible, **auditable, accountable** AI deployment |
| **Green IT + Governance** | **Policy-driven resource efficiency** and carbon accountability |
| **AI + Sustainability** | Using AI as a **tool for environmental and social good** |
| **All Three** | A **responsible digital future** for society |

## 1.18 Who is responsible? (six stakeholder groups)

| Stakeholder | Role |
|---|---|
| **Board & Executive Leadership** | Set strategic direction, approve governance frameworks, champion ethical and sustainable culture |
| **IT Leadership (CIO/CISO/CTO)** | Implement governance frameworks, manage risk, ensure technology aligns with ESG and ethical goals |
| **Data Scientists & AI Developers** | Build AI responsibly, document model decisions, test for bias, implement safety measures |
| **Legal & Compliance Teams** | Ensure regulatory adherence, manage risk exposure, liaise with regulators and auditors |
| **Employees & End Users** | Follow governance policies, report violations, participate in digital literacy and ethics training |
| **Governments & Regulators** | Set legal frameworks, enforce compliance, promote international standards and co-operation |

## 1.19 Emerging challenges

| Horizon | Challenge |
|---|---|
| **Now–2027** | **Agentic AI** — systems that act autonomously require new frameworks for **delegation, oversight, and liability** |
| **2027–2030** | **Quantum computing** — will break current encryption standards; governance must prepare for the quantum transition now |
| **Now–2030** | **Digital sovereignty** — nations asserting control over data and AI infrastructure; governance must navigate geopolitical fractures |
| **Now–2035** | **Climate tech urgency** — technology must accelerate net-zero; governance ensures effort is **genuine, not performative** |

### 🔴 Topic 1 — MCQ traps
1. **Four pillars** — "Software Development" is not one. "Risk Management" *is* (same as Risk Optimization).
2. **Code of Corporate Governance** — **MAS**, not SGX/IMDA/MDDI.
3. **Governance models** — "independent … different emphasis … similar objectives". Never "identical" or "interchangeable".
4. **Fairness** — about *outcomes by protected attribute*, not price/speed/availability.
5. **Transparency** — about *explainability*, not about publishing source code.
6. **Human Oversight** — "humans remain in control of **consequential** decisions", not "every decision reviewed by three employees".
7. **Sustainability pillars** = E/S/**Economic**. **ESG** = E/S/**Governance**.
8. **Job displacement** = **social and economic** risk.
9. **Concentration of power** = access, dependency, democratic oversight.

---

# TOPIC 2 — Framework for Governance of Enterprise IT (GEIT)

## 2.1 ⭐ The three players

| Player | Role (slide wording) |
|---|---|
| **Board of Directors** | Sets the **overall direction** of the company. **Accountable to the shareholders.** Meets regularly to deliberate company matters |
| **CEO & Executive Management** | Includes CEO and immediate subordinates (**CFO, CIO, COO**). **Executes the operational tasks** based on direction set by the board |
| **Employees** | Do the actual work as set out by CEO & Executive Management. **Responsible for the work done to CEO & Executive Management** |

## 2.2 ⭐ ISACA definition of enterprise governance (learn verbatim)

> "Enterprise governance is a set of **responsibilities and practices** exercised by the **board and executive management** with the goal of:
> 1. providing **strategic direction**,
> 2. ensuring that **objectives are achieved**,
> 3. ascertaining that **risks are managed appropriately**, and
> 4. verifying that the enterprise's **resources are used responsibly**."

**Memory hook — "D-O-R-R": Direction, Objectives, Risk, Resources.**

## 2.3 ⭐ Conformance & Performance (IFAC, October 2003)

| Dimension | Focus |
|---|---|
| **Conformance** | Addresses **corporate structure, roles and executive remuneration** |
| **Performance** | Focus on **strategy and value creation**. Enhance **efficiency through managing risk appetite** |

> ⭐ **This is the highest-probability "pair" question in Topic 2.** The trap options are "Compliance and Reporting", "Strategy and Execution", "Governance and Management". The actual IFAC pair is **Conformance and Performance**.

## 2.4 ⭐ Six key assets (Weill & Ross, 2004)

**Human · Financial · Physical · IP · Information & IT · Relationship**

> **Source:** Weill, Peter; Jeanne Ross: *IT Governance: How Top Performers Manage IT Decision Rights for Superior Results*, Harvard Business School Press, 2004.
> **Trap:** "Reputational assets" is the favourite wrong option (Tutorial 2 Q3). Reputation is *not* one of the six.

## 2.5 ⭐ GEIT frameworks — which does what

| Framework | Category | Covers |
|---|---|---|
| **COBIT** (ISACA) | **Governance** of enterprise IT | The overarching framework |
| **ISO 38500** | **Governance** of enterprise IT | **Governance of IT within organisations** |
| **CMMI** | **Management** of enterprise IT | Capability Maturity Model Integration |
| **ISO 27001** | **Management** | **Information security** |
| **ISO 9000** | **Management** | **Quality management** |
| **ISO/IEC 20000** | **Management** | **IT service management** |
| **ISO 31000:2009** | **Management** | **Risk management** standard |
| **TOGAF** | Management / architecture | The Open Group Architecture Framework |
| **M_o_R** | Management | Management of Risk |
| **ITIL** | Management | **IT Infrastructure Library** — management of IT **infrastructure and services** |

> ⭐ **The ISO number-matching question is almost guaranteed.** Learn: 38500=governance of IT · 27001=infosec · 9000=quality · 20000=IT service management · 31000=risk. (Mnemonic: **"38.5k governs, 27k secures, 9k assures quality, 20k serves, 31k manages risk."**)

### ⭐ Why COBIT can be the *overarching* framework
**"COBIT aligns with the other relevant standards and frameworks at a high level. This means COBIT can be used as the overarching framework for the governance and management of enterprise IT."**

> **Trap:** it does **not** replace other frameworks, is **not** mandated by law, and is **not** the cheapest. It is **integrative** — other frameworks plug into it.

## 2.6 Why frameworks matter (four points)

1. Frameworks represent the **'collected wisdom'** of the experts who developed them.
2. They provide the **best practices and know-how** so the system is developed optimally, with the **least amount of mis-spent resources** through mis-aligned actions.
3. Frameworks are **constantly reviewed and revised** to reflect current best practice, based on observed successes and lessons learnt.
4. ⭐ **The absence of frameworks does not mean that 'everyone will fail' — just that the rate of success would not be optimal.**

> That fourth point is a favourite MCQ ("absence of frameworks means all projects fail" = ✗).

## 2.7 ⭐ Business drivers — pain points vs trigger events

**Business drivers constitute the need for IT Governance.** Typical **pain points** or **trigger events** create the realisation that there is a need for improvement. IT governance then initiates **immediate action to solve or mitigate the pain points** and creates a platform for further future improvement.

### Definition difference (this is the examined distinction)

| | **Pain point** | **Trigger event** |
|---|---|---|
| What it is | **Awareness that something needs improvement** because of missed opportunities or negative impacts **already being felt** | An **internal or external event** that forces GEIT onto the agenda |
| Nature | A **symptom / ongoing condition** | A **discrete occurrence / change** |
| Example | Data loss incidents; hidden IT spending | New CIO; merger; new regulation |

### ⭐ Pain points (full list from the slides)

| # | Pain point |
|---|---|
| 1 | **Frustration with failed initiatives, rising IT costs and low business value** |
| 2 | **Significant incidents related to IT-related business risk** — e.g. data loss or project failure |
| 3 | **Outsourcing service delivery service levels not being met** |
| 4 | **Failure to meet regulatory requirements** |
| 5 | **IT limiting innovation capability and business agility** |
| 6 | **Regular audit findings of poor IT performance or quality of service** |
| 7 | **Hidden IT spending** |
| 8 | **Duplication or overlap between initiatives and wastage of resources** |
| 9 | **Insufficient IT resources, staff with inadequate skills, or dissatisfied employees** |
| 10 | **IT-enabled changes frequently failing to meet business needs, delivered late or over budget** |
| 11 | **Multiple and complex IT assurance efforts** |
| 12 | **Management reluctant to engage with IT, or lack of sponsors for IT projects** |
| 13 | **Complex IT operating models** — typically decentralized or federated |

### ⭐ Trigger events (full list)

| # | Trigger event |
|---|---|
| 1 | **Merger, acquisition or divestiture** |
| 2 | **Shift in market or competition position** |
| 3 | **New regulatory or compliance requirements** |
| 4 | **Initiation of an enterprise-wide governance project** |
| 5 | **New CIO, CFO, CEO or board member** |
| 6 | **External audit or consultant assessments** |
| 7 | **A new business strategy** |
| 8 | **Desire to significantly improve the value gained from IT** |

> ⭐⭐ **THE highest-value discrimination in Topic 2 (Tutorial 2 Q12 & Q13).**
> - "**Insufficient IT resources**" → **pain point**
> - "**Outsourcing service levels not met**" → **pain point**
> - "**Hidden IT spending**" → **pain point**
> - "**New regulatory or compliance requirements**" → **trigger event** ✔
> - "**IT limiting innovation capability and business agility**" → **pain point** (Tutorial 2 Q12's answer)
> **Rule of thumb:** if it's a *condition you're suffering*, it's a pain point. If it's an *event or change*, it's a trigger.

### ⭐ Third-party review and success factors
- **Engaging a third party to obtain a review may increase buy-in** (independent validation).
- **Success of GEIT initiatives depends on participation of everyone in the enterprise.**
- **Trap:** a consultant does **NOT** remove board responsibility, does **NOT** guarantee government approval, and is **NOT** a mandatory COBIT step.

## 2.8 ⭐ GEIT Components — COBIT's seven

> **Components** = "anything that can help achieve the objectives of the enterprise." They **interact with one another** to support a **comprehensive governance and management system** for GEIT.

| # | Component |
|---|---|
| 1 | **Principles, policies and frameworks** |
| 2 | **Processes** |
| 3 | **Organizational structures** |
| 4 | **Culture, ethics and behaviour** |
| 5 | **Information** |
| 6 | **Services, infrastructure and applications** |
| 7 | **People, skills and competencies** |

> **Memory hook:** **P-P-O-C-I-S-P** → *"Proper Processes Organise Culture, Information, Systems and People."*
> ⭐ **Key to successful implementation = a HOLISTIC approach toward the interaction between the components.** Not implementing them one at a time.

## 2.9 ⭐ IT Strategy — SWOT and BCG

**IT strategy must be aligned to the enterprise's mission, vision and values.** Techniques to identify strategy: **SWOT** and **BCG Matrix**.

### SWOT

| Element | What you do with it |
|---|---|
| **Strengths** | **Continue to develop them** |
| **Weaknesses** | **Mitigate them** |
| **Opportunities** | **Develop them into future strengths** |
| **Threats** | **Address them before they become a more serious issue** |

> **Trap:** SWOT is used to *identify* strategy — it is **not** a portfolio tool, a maturity model, or a benefits-calculation technique.

### ⭐ BCG Matrix (four quadrants)

| Quadrant | Resources needed | Returns | What to do |
|---|---|---|---|
| **Stars** | **Require large cash flows** | **Generate a lot of returns**, most benefit to the organisation | **Maintain or develop further to become cash cows** |
| **Cash Cow** | **Does not take up a lot of resources currently** | **Producing a lot of returns** | ⭐ **"This is the best area to be in."** |
| **Question Mark** | Needs **sufficient investment** | Not generating a lot of benefits **yet** | **Has potential to become cash cows** |
| **Dog** | **Does not take up a lot of resources** | **Neither generates a lot of benefits** | Low priority |

> ⭐ **The BCG MCQ is almost always "which is the best area to be in?" → Cash Cow.** And "which needs heavy cash but returns a lot?" → Star.

## 2.10 Organizational structures & roles

**Effective GEIT requires IT-related decisions to be made in a transparent manner, and effective communication between business and IT management.** Organizational structures ensure this. Organizational structure is specified as an **enabler in COBIT**.

| Role | Definition |
|---|---|
| **Board** | Most senior executives and/or non-executive directors, accountable for the **governance of the enterprise**, overall control of its resources |
| **CEO** | Highest-ranking officer in charge of the **total management** of the enterprise |
| **CFO** | Most senior official accountable for **all aspects of financial management**, including financial risk and controls, reliable and accurate accounts |
| **COO** | Most senior official accountable for the **operation** of the enterprise |
| **CRO** | Most senior official accountable for **all aspects of risk management** across the enterprise (an IT risk officer may oversee IT-related risk) |
| **CIO** | Most senior official responsible for **aligning IT and business strategies**, and accountable for **planning, resourcing and managing the delivery of IT services and solutions** |
| **CISO** | Most senior official accountable for the **security of enterprise information in all its forms** |
| **Business Executive** | Senior management individual accountable for the **operation of a specific business unit or subsidiary** |

> ⭐ **The CIO vs CISO vs CRO distinction is examinable.** CIO = alignment + delivery. CISO = security of information. CRO = risk across the enterprise.

## 2.11 ⭐ RACI

**RACI = Responsible, Accountable, Consulted, Informed.**

- A RACI chart shows **the assignment of various governance responsibilities to various roles** in the organisation, linking a **process** to **roles**.
- ⭐ **Effective governance depends on comprehensive allocation of responsibilities to provide END-TO-END coverage of all governance activities.**
- Not all roles need to be present as positions — but a person/position should be able to **identify with** each role.

**The Responsibility Poem (Charles Osgood)** — the point: *when everybody assumes somebody else will do it, nobody does it, and everybody blames somebody.* This is the argument for **explicit** RACI allocation.

### 🔴 Topic 2 — MCQ traps
1. **ISO numbers** — 38500 ≠ 27001. Governance ≠ security.
2. **Conformance & Performance** — not "compliance and reporting".
3. **Six assets** — "Reputational" is not one.
4. **COBIT** — *aligns with* other frameworks; does not replace them.
5. **Pain point vs trigger event** — regulation is a **trigger**; resourcing is a **pain point**.
6. **Frameworks absent** — success not optimal, **not** guaranteed failure.
7. **Seven components** — includes **culture, ethics and behaviour** (people forget this one) and **information**.
8. **BCG** — Cash Cow is the best area; Stars need heavy cash.
9. **RACI** — end-to-end coverage; "Accountable" is the one who answers for it.

---

# TOPIC 3 — Strategic Management

## 3.1 ⭐ What strategic management is

> **"Strategic management aims to achieve STRATEGIC ALIGNMENT between business and IT."**

It involves **2 key questions**:
1. **How is IT aligned with the business?**
2. **How is the business aligned with IT?**

> ⭐ **The #1 Topic 3 MCQ:** "Strategic management in IT primarily aims to achieve…" → **strategic alignment between business and IT.** Not cost reduction, not faster deployment, not standardisation.

## 3.2 ⭐ Strategic Alignment Model (SAM)

SAM recognises the need to consider **both the external and internal domain**.

| Domain | Contents |
|---|---|
| **External domain** | **IT strategy** and **business strategy** — issues dealing with the external aspect of the enterprise |
| **Internal domain** | **Key business processes, policies, guidelines and procedures** |

**Cross-alignment** between:
- **Business Strategy ↔ IT Infrastructure & Processes**
- **IT Strategy ↔ Organization Infrastructure & Processes**

…reflects how the Business and IT domains interact. **Business Strategy can affect how IT processes are organised, and IT Strategy can affect how organisational processes are designed — and vice versa.**

> ⭐ **The two-way relationship (Tutorial 3 Q3):** "Business and IT alignment is a two-way relationship because **IT can offer new opportunities that impact business strategy, just as business strategy shapes IT**." This exact phrasing recurs in Topic 3 (slide 15) and Topic 4. **Learn it once, use it three times.**

## 3.3 ⭐ Strategic Planning Process

**Process by which business strategy is defined, from which IT strategy is developed.**

It takes into account:

| Factor type | Examples |
|---|---|
| **External factors** | **Market, industry, geopolitics** |
| **Internal factors** | **Culture, organisation, appetite** |

> **Trap (Tutorial 3 Q2):** the options "financial/human", "technical/regulatory", "short-term/long-term" all sound plausible. The slide pair is **external (market, industry, geopolitics)** and **internal (culture, organisation, appetite)**.

## 3.4 ⭐⭐ COBIT Goals Cascade (the single most examined diagram in the module)

### The sequence — memorise this chain

```
Stakeholder DRIVERS
        ↓  (influence)
Stakeholder NEEDS
        ↓  (cascade)
ENTERPRISE GOALS
        ↓  (cascade)
ALIGNMENT GOALS
        ↓  (cascade)
GOVERNANCE & MANAGEMENT OBJECTIVES
        ↓
IT GOALS
```

> ⭐ **Tutorial 3 Q6 is literally this list.** The four traps are all plausible-sounding arrows (budget→projects→deliverables→benefits; business strategy→financial→HR→IT; IT strategy→processes→controls→audits).

### The four steps (learn the numbering)

| Step | Content |
|---|---|
| **Step 1** | **Stakeholder drivers influence stakeholder needs.** Stakeholder needs are influenced by drivers, e.g. **strategy changes, changing business and regulatory environment, new technologies** |
| **Step 2** | **Stakeholder needs cascade to enterprise goals.** Stakeholder needs can be related to a set of **generic enterprise goals** |
| **Step 3** | **Enterprise goals cascade to alignment goals.** From the identified enterprise goals, COBIT 5 defines various alignment goals to each of the enterprise goals |
| **Step 4** | **Alignment goals to Governance & Management Objectives.** Specific goals are defined in governance & management objectives |

> ⭐ **What INITIATES the cascade (Tutorial 3 Q5):** **Stakeholder drivers that influence stakeholder needs.** *Not* enterprise goals, not budget requests, not regulation. Enterprise goals are step 2 — a classic "off-by-one" trap.

### ⭐⭐ The two-way relationship (both directions must be stated)

1. **Top-down:** effective identification of IT goals **from stakeholder needs** enhances IT governance.
2. **Bottom-up:** IT goals **get linked to their source** — stakeholder drivers and needs.

This **2-way relationship** ensures **IT goals are tightly linked to the organisation's mission and objectives** *(A Tutorial 3 Q7 answer)* **and traceable back to stakeholder drivers.**

### ⭐ Value of the Goals Cascade (three points)

1. **Defines relevant and tangible goals and objectives at various levels of responsibility.**
2. **Filters knowledge in COBIT to provide relevant guidance for projects.**
3. **Clearly identifies and communicates how governance & management objectives are important to achieve enterprise goals.**

Plus the framing sentence: *"Goals cascade allows the definition of enterprise IT governance based on the objectives of the enterprise and related risk. This is an essential step in strategic management."*

## 3.5 Changes in business strategy ⭐

- The **dynamic nature of business** means there will be **constant revisions** to business strategy.
- **IT needs to continually readjust** to align with business.
- **Failure to do that → mis-alignment of IT with business objectives → systemic failures in governance.**
- Conversely, in today's digital world **IT may offer new opportunities which can impact business strategy** → hence a **2-way relationship**.

> ⭐ **Tutorial 3 Q15:** when business goals change, the correct response is to **"ensure the IT strategy is evolved and realigned to reflect the new business direction"** — **not** wait for the annual cycle, **not** replace all systems, **not** outsource strategy.

## 3.6 ⭐ Agility

> **Agility = the enterprise's ability to adapt quickly to changes in the environment.**

- Requires enterprises to **constantly assess strategic business changes and their impact on their IT environment**.
- ⭐ **Agility is an on-going process, NOT a one-time effort with a begin and end stage.**

> **Trap:** "agility" in this module is **NOT** about delivery speed, staff flexibility, or system scalability. It is **organisational adaptiveness to environmental change**.

## 3.7 ⭐⭐ The three Agility Loops

| Loop | Name | Focus |
|---|---|---|
| **Loop 1** | **Monitoring and deciding** | **Environmental monitoring and responsive decision making.** ⭐ *"Often, the most profitable opportunities for better alignment of IT and business arise from agile responses to new or unexpected events."* |
| **Loop 2** | **Improving existing processes** | Improving **existing operations**, often through **automation** and **enhancement of reliability** |
| **Loop 3** | **Creating new processes** | **Creating new operations to deliver effectiveness.** The IT organisation **senses changes and responds** by creating new processes and **retiring old obsolete ones** |

**Inputs to Loops 2 and 3** usually involve **non-standard inputs (information)**, which could result from:
- **Errors in the input data or system operations**, or
- **Input data that is correct but represents a new trend or event**

> ⭐ **The Loop 1 MCQ:** "Which best describes Agility Loop 1?" → **"Monitoring the environment and making responsive decisions."** The traps ("creating entirely new business processes", "improving existing IT processes through automation", "retiring obsolete systems") are **Loops 3, 2 and 3** respectively — the examiner is testing whether you can tell the three loops apart.

> ⭐ **Loop 2 vs Loop 3 boundary:** Loop 2 **improves what exists** (automate, make reliable). Loop 3 **creates what doesn't exist** and **retires** what's obsolete. When improving existing processes is **insufficient**, you must go to Loop 3.

## 3.8 ⭐⭐ Three barriers to strategic alignment

| Barrier | Definition (slide wording) | What it looks like |
|---|---|---|
| **Expression barrier** | **Inability by senior management in communicating business strategy to operational management** | Strategy exists in the boardroom but operational managers never hear it clearly |
| **Specification barrier** | **Lack of IT involvement in strategy development**, resulting in **IT and business having 2 different strategies** | IT builds its own roadmap because it wasn't in the room |
| **Implementation barrier** | **Difficulties in implementing the strategy due to the current IT portfolio** — e.g. **legacy systems** | The strategy is right but the estate can't support it |

> **Memory hook — the story arc:** you can't **say** it (Expression) → you didn't **design** it together (Specification) → you can't **build** it (Implementation).
> **Trap:** "Technical, financial and human barriers" and "Planning, execution and review barriers" are the plausible wrong answers. The correct trio is **Expression / Specification / Implementation**.

## 3.9 Policies and procedures

- Necessary in **supporting business and IT alignment**.
- **Reflect management guidance**, and so doing, **business and IT strategies**.
- **Tools with which strategic management provides guidance and direction.**

> ⭐ **Tutorial 3 Q4:** policies/procedures matter because they **"reflect management guidance and embody both business and IT strategies, providing direction to staff."** They are **not** legally required by all regulators, and they do **not** reduce the need for oversight.

## 3.10 ⭐ Communication — the CIO's central role

- To **not lose sight of business strategy**, ensure **continuous communication to IT personnel** of business and IT objectives.
- ⭐ **The CIO's role is central to this key activity.**
- The CIO needs to **explain the IT strategy to IT personnel and make them supporters of the strategy**.
- **When business goals change, the CIO needs to ensure the new IT strategy is evolved as well.**

> ⭐ **Tutorial 3 Q14:** continuous communication is important because it **"ensures IT personnel do not lose sight of business objectives and remain aligned with strategic direction"** — not because of regulatory documentation, not to reduce performance management, not to eliminate project management methodologies.

### 🔴 Topic 3 — MCQ traps
1. **Purpose of strategic management** = alignment between business and IT.
2. **Goals cascade initiator** = **stakeholder drivers** (not enterprise goals).
3. **Loop 1 / 2 / 3** — don't mix up monitoring, improving, creating.
4. **Barriers** = Expression / Specification / Implementation.
5. **Agility** = organisational adaptiveness, ongoing, not a project.
6. **Policies** = embody both strategies (not a legal requirement).
7. **CIO** = the communication linchpin.

---

# TOPIC 4 — Benefits Realization

## 4.1 ⭐ Definition / objective (three bullets — learn all three)

The objective of benefits realization is to ensure that:
1. **IT-enabled business investments achieve the promised benefits and deliver business value**
2. **Required capabilities are delivered on time and within budget**
3. **IT services and other IT assets continue to contribute to business value**

⭐ **Why the focus exists:** **many high expenditures on IT-related initiatives are NOT realizing their expected business benefits.**

> **Trap:** "IT departments receive adequate funding", "projects are delivered using agile", "systems are upgraded regularly" — all ✗. Benefits realization is about **value**, not funding, methodology or maintenance.

## 4.2 ⭐ The Business Case

- A **comprehensive business case is critical** to the outcome of any project involving IT.
- A business case contains **assumptions on how value will be created** — and these assumptions **should be well tested** to ensure expected outcomes are achieved.
- ⭐ **A business case is the PRIMARY TOOL for designing and articulating the expected benefits** that may result from the project.

## 4.3 ⭐ Program / Project Management

> **Realizing value requires the effective use of IT in conjunction with associated changes in:**
> 1. **the business process**
> 2. **individual's work**
> 3. **organizational structures**

Effective program/project management requires **constant focus on**:
1. **Desired business outcomes**
2. **The relationship between various initiatives**
3. **How the initiatives contribute to the ultimate business value**

> ⭐ **The point being made:** technology alone delivers nothing — you must also change **process, work and structure**. This is a favourite SAQ phrase.

## 4.4 ⭐⭐ Business benefits vs Intermediate benefits

| | **Business benefits** | **Intermediate benefits** |
|---|---|---|
| Definition | **Create value in that they increase the company's profits** | **Do NOT directly create value**, although they **benefit one or more groups of stakeholders** |
| Example | Higher revenue, lower cost, increased profit | **Improvement in customer service that does not contribute to increased profits** |
| Relationship | The ultimate target | **Must be made to contribute to business benefits** |

> ⭐ **Benefits realization "also helps to ensure that INTERMEDIATE benefits CONTRIBUTE TO BUSINESS benefits."** That is the linking discipline — intermediate benefits are not useless, but they must eventually be tied to profit or they're just activity.

> ⭐ **Tutorial 4 Q3 / trap:** "Business benefits are financial; intermediate benefits are always non-financial" is **wrong** — the defining difference is **value creation (profit)**, not financial vs non-financial.

### Additional guarantee
Benefits realization further ensures that **the realization of business benefits is unfolding at levels of return SUFFICIENT TO MERIT THE RESOURCES being expended** to achieve the benefits.

### ⭐⭐ The absence of benefits realization
**"In the absence of benefits realization, optimal value will not be created or, worse, value may be eroded or destroyed."**
> Learn this exact sentence — it is the answer to "what happens without benefits realization?" and every distractor is wrong.

## 4.5 ⭐⭐ Full Economic Life Cycle (five phases, in order)

> **The main issue with managing programs is LACK OF CONTINUITY in the program plan after delivering the required business and IT capabilities.** In general, **benefits and expected value will NOT be realised until after some time** — so the program must be **seen through its full economic life cycle**.

| # | Phase | What happens |
|---|---|---|
| **1** | **Investment** | **Developing** the necessary capabilities |
| **2** | **Adoption** | **Implementing** the capabilities |
| **3** | **Value creation** | **Achieving the expected level of performance** and **moving the delivered capabilities into the active service portfolio** |
| **4** | **Value sustainment** | **Assuring that the assets resulting from the investment continue to create value** — may well include **additional investments** required to sustain value |
| **5** | **Retirement** | **Decommissioning** the resulting assets |

> **Memory hook — "I-A-V-V-R":** **I**nvest, **A**dopt, **V**alue-create, **V**alue-sustain, **R**etire.

### ⭐⭐ The scenario question (Tutorial 4 Q15 — expect a variant of this)

> *Government agency invests SGD 50m. Platform delivered on time, within budget, all technical tests passed. Two years later citizens still use paper processes and the platform sits largely unused. What failed?*

**Answer: the ADOPTION phase.** The capabilities were **delivered but not implemented into active use**, so **value creation never occurred**.

**Why the distractors are wrong:**
- **Investment phase** ✗ — it succeeded; capabilities were developed on time and on budget.
- **Retirement phase** ✗ — you can't retire before you've adopted; the old paper systems are still in use because adoption failed, not the other way round.
- **Business case** ✗ — the money spent isn't the failure; the failure is that the delivered capability never entered service.

> **The examinable logic:** *Investment = build it. Adoption = get people actually using it. Value creation = hit the expected performance level and put it in the active service portfolio.* A project can pass phases 1 and 2 (delivered) and still die at the adoption→value-creation boundary. **"Delivered" ≠ "realised".**

## 4.6 ⭐ Portfolio & Portfolio Management

| Term | Definition |
|---|---|
| **Portfolio** | **A collection of programs, projects and/or operations managed as a group.** ⭐ The components **may not necessarily be interdependent or even related** — but they are managed together **to achieve strategic objectives** |
| **Portfolio management** | **The centralized management of one or more portfolios**, which includes **identifying, prioritizing, authorizing, managing, and controlling** projects, programs and other related work to achieve **specific strategic business objectives** |

> ⭐ **Tutorial 4 Q9 trap:** a portfolio is **not** "a collection of IT assets owned by the IT department", and **not** "a financial investment portfolio managed by the CFO". It's about **managing work as a group toward strategic objectives**, and the components **need not be related**.

### Aim of portfolio management
**To ensure that an enterprise secures OPTIMAL VALUE across its portfolio of IT-enabled investments.**

### What it helps enterprises do (five)
1. **Establish and manage resource portfolio**
2. **Define investment thresholds**
3. **Evaluate, prioritize, and select, defer, or reject new investments**
4. **Manage and optimize the overall investment portfolio**
5. **Monitor and report on portfolio performance**

### ⭐ Programs in the portfolio need to be:
**Clearly defined → Evaluated → Prioritized → Selected → Managed actively throughout their full economic life cycle.**

> That is a **five-step sequence**, and it is a direct MCQ ("which of the following…" → all five, in that order).

## 4.7 ⭐⭐ COBIT's five portfolio management processes

| # | Process | What it involves |
|---|---|---|
| **1** | **Establish target investment mix** | Review and ensure the investment mix — based on **cost, alignment with strategies and financial measures such as cost and ROI** — is **optimal** |
| **2** | **Determine the availability and sources of funds** | Find **funding source** and the **implications of the fund source on return expectations** |
| **3** | **Evaluate and select programs to fund** | Based on the **overall investment portfolio mix requirements**: **evaluate and prioritize program business cases, decide on investment proposals, allocate funds, and initiate programs** |
| **4** | **Monitor, optimise and report on investment portfolio performance** | **On a regular basis**, monitor and optimize the performance of the **investment portfolio and individual programs** throughout the **entire investment life cycle** |
| **5** | **Manage benefits achievement** | Monitor the benefits of providing and maintaining appropriate IT services and capabilities, **based on the agreed-on and current business case** |

> **Memory hook:** **MIX → MONEY → SELECT → MONITOR → BENEFITS.** (What mix do we want? Where's the money? Which programs? How are they doing? Did we get the benefit?)

## 4.8 ⭐ Benefits of portfolio management

1. **Provides a HOLISTIC approach** towards achievement of enterprise objectives by **considering a group of activities together**.
2. **Promotes sharing, economies of scale, and mutual benefits** where it would have been **impossible to achieve without portfolio management**.
3. **Allows management to allocate resources according to the relative importance (and urgencies) of each portfolio.**

> ⭐ **Tutorial 4 Q13:** economies of scale come from **"grouping programs and projects together, enabling resource sharing, specialisation, and synergies that would be impossible to achieve individually."** **Not** from negotiating volume discounts with vendors.

## 4.9 ⭐ Three ways to organise portfolios

| Way | Grouping basis | Benefit |
|---|---|---|
| **Categories** | Programs/projects **belonging to the same category** | **Synergies** between projects → **resource sharing and specialization** |
| **Product or service** | Programs/projects contributing to a **particular category of service or product** | **Timely realization of benefits** when the service/product is **launched or delivered to customers** |
| **Resource usage** | Programs/projects that **utilize or depend on common resources** — **raw materials, parts, or expertise** | **Specialization and economies of scale**; innovations from the resources used |

> ⭐ **Tutorial 4 Q14:** "resource usage" = **"utilise or depend on common resources such as raw materials, parts, or expertise."** Not "same project manager", not "same life-cycle phase", not "same financial period".

## 4.10 ⭐ Benefit calculation techniques

**Examples of benefit calculation techniques:**

**Breakeven analysis · Cost-benefit analysis (CBA) · Payback period · Return on investment (ROI) · Service life cycle**

### ⭐ Financially-oriented CBA (quantifiable — preferred)

| Technique | Definition (slide wording) | Formula |
|---|---|---|
| **Payback period** | Measures **the time period necessary to RECOUP the initial investment**. Used to evaluate an investment or **compare a set of mutually exclusive investments** | Initial investment ÷ annual net cash inflow |
| **ROI** | A relatively **simple calculation providing decision-making information in terms of a ratio**. **The ratio of expected profit to the initial investment cost is compared to the opportunity cost of capital.** **If return is greater, the greater the likelihood the investment is undertaken** | (Net benefit ÷ initial investment) × 100% |

> ⭐ **Why financially-oriented techniques are preferred: they provide ABSOLUTE VALUES to measure benefit** (based on quantifiable values).

**Worked example (possible SAQ):**
> A system costs **$300,000** to build and delivers **$75,000** of net benefit per year.
> - **Payback period** = 300,000 ÷ 75,000 = **4 years**
> - **ROI** (5-year view, total net benefit $375,000) = (375,000 − 300,000) ÷ 300,000 = **25%**
> - **Decision rule:** if the opportunity cost of capital is **10%**, 25% > 10% → **undertake the investment**.

### ⭐ Non-financially-oriented CBA

- Tries to **overcome the problem of financial ROI by finding a SURROGATE MEASURE for intangible costs or benefits**.
- Used when there is an issue with **quantifying the value of benefits**, or **difficulty identifying benefits or costs which do not have a ready market value**.
- Useful when **benefits are largely intangible**.

| Technique | Meaning |
|---|---|
| **Organizational flexibility** | The **ability of the organization to respond and its ease of responding** — viewed as a **source of competitive advantage** |
| **Information economics** | The notion that **information has economic value** |

## 4.11 ⭐ Process and service measurement

> **Measurement of performance is essential in benefits realization.** Management needs to have an idea of **how well benefits are being realized** through the initiatives.

| Technique | What it does |
|---|---|
| **Balanced Scorecard** | Allows for the **evaluation of IT from the USER'S perspective** |
| **Maturity model** (based on **ISO 15504**) | Evaluates the **capability of the organization against SIX levels of maturity or capability** (0–5) |

### ⭐⭐ The six maturity levels (0–5) — learn in order

| Level | Name | Definition |
|---|---|---|
| **0** | **Incomplete process** | The process is **not implemented or fails to achieve its process purpose**. Little or no evidence of any **systematic achievement** of the process purpose |
| **1** | **Performed process** | The implemented process **achieves its process purpose** |
| **2** | **Managed process** | The performed process is implemented in a **managed fashion**, and its **work products are appropriately established, controlled and maintained** |
| **3** | **Established process** | The performed process is implemented using a **defined process** that is capable of achieving its process outcomes |
| **4** | **Predictable process** | The process now **operates within defined limits** to achieve its process outcomes |
| **5** | **Optimizing process** | The process is **continuously improved** to meet relevant **current and projected business goals** |

**Key rules:**
- ⭐ **Each level includes ALL the previously described attributes** (cumulative).
- **Capability maturity measures the level of 'maturity' of the process.**

> **Memory hook — "I P M E P O":** **I**ncomplete, **P**erformed, **M**anaged, **E**stablished, **P**redictable, **O**ptimizing.
> **Trap:** Level 4 is **Predictable** (operates within defined limits); **Optimizing** is level **5** (continuously improved). The exam swaps these two constantly.

### 🔴 Topic 4 — MCQ traps
1. **Business vs intermediate benefits** — the difference is **value creation / profit**, not financial vs non-financial.
2. **Life-cycle phase order** — Investment → Adoption → Value creation → Value sustainment → Retirement.
3. **Delivered but unused** → **Adoption failure** (not investment, not retirement).
4. **Portfolio components need not be related.**
5. **Economies of scale** — from **grouping**, not vendor discounts.
6. **Maturity level 4 = Predictable, 5 = Optimizing.**
7. **Payback period** = time to recoup; **ROI** = ratio of expected profit to initial cost vs opportunity cost of capital.
8. **Balanced Scorecard** = IT from the **user's perspective**.

---

# 5. Cross-topic synthesis (where the SAQ marks hide)

These four topics are one story. If you can recite this paragraph, you can answer any integrative question:

> **Corporate governance** (MAS Code, OECD principles) sets the mission and holds the board accountable. **IT governance** (COBIT, ISO 38500) is the system by which IT is **directed and controlled** to achieve that mission — and it has **four pillars**: **strategic management, benefits realization, risk optimization, resource optimization**. **Strategic management** (Topic 3) delivers the **alignment** half, using the **COBIT goals cascade** to trace **stakeholder drivers → needs → enterprise goals → alignment goals → G&M objectives → IT goals**. **Benefits realization** (Topic 4) delivers the **value** half, managing investments across the **full economic life cycle** through **portfolio management**. **AI governance** sits inside IT governance and adds the **six Responsible AI principles**. **Sustainability** adds the environmental, social and economic dimension, and **ESG** makes it reportable.

| Confusable pair | Distinguishing test |
|---|---|
| Corporate vs IT vs AI governance | **Whole company** vs **role of IT** vs **AI within IT** — independent, different emphasis, similar objectives |
| Risk Optimization (pillar) vs Risk Management (framework) | Pillar = governance concern; ISO 31000 = the standard |
| Conformance vs Performance | **Structure/roles/remuneration** vs **strategy/value creation** |
| Pain point vs Trigger event | **Condition you suffer** vs **event that happens** |
| Goals cascade: initiator vs step 2 | **Drivers** initiate; **enterprise goals** are step 2 |
| Agility Loop 1 vs 2 vs 3 | **Monitor/decide** vs **improve existing** vs **create new/retire old** |
| Expression vs Specification vs Implementation barrier | **Can't say it** vs **didn't co-design it** vs **can't build it (legacy)** |
| Business vs Intermediate benefit | **Increases profit** vs **benefits stakeholders, no direct profit** |
| Investment vs Adoption vs Value creation | **Build** vs **get people using** vs **hit performance level + enter active service portfolio** |
| Portfolio vs Program vs Project | **Group toward strategic objectives** vs **related projects** vs **single deliverable** |
| Maturity 4 vs 5 | **Predictable (within limits)** vs **Optimizing (continuously improved)** |
| Three pillars of sustainability vs ESG | **E/S/Economic** vs **E/S/Governance** |

---

# 6. SAQ bank — 12 likely questions with model answers

> The real test has **2–3 SAQs worth 10 marks total**. These are the questions the slide emphasis and tutorial coverage make most likely. Practise writing them **in bullet form under time pressure** — 4 marks ≈ 4 distinct points, not 4 paragraphs.

---

### SAQ 1 — Define IT governance and its four pillars. (4 marks)
**(a) [1] Define IT governance. (b) [3] Name and briefly explain the four pillars.**

**Model answer**

(a) IT governance is **the system by which the use of IT within an organisation is directed and controlled**, ensuring **alignment with business strategy, management of risk, and delivery of value**. *(1)*

(b) *(¾ each)*
1. **Strategic Management** — achieving **alignment between business and IT**, so IT goals trace back to stakeholder needs.
2. **Benefits Realization** — ensuring IT-enabled investments **achieve the promised benefits and deliver business value**.
3. **Risk Optimization** — **identifying, assessing and mitigating** IT risk before it becomes a crisis.
4. **Resource Optimization** — ensuring IT **resources (people, infrastructure, information) are used efficiently** to meet objectives.

---

### SAQ 2 — Relationship between corporate, IT and AI governance. (3 marks)

**Model answer**
- They are **independent models** — one is not a subset step of another, and they are not interchangeable. *(1)*
- They have **different emphases but similar objectives**: corporate governance manages **the whole corporation**, IT governance manages **the role of IT in the corporation**, AI governance manages **AI within IT governance**. *(1)*
- All three ultimately serve the **same objective** — ensuring the entity is **run to achieve its mission and meet stakeholders' needs**, with **accountability, transparency and value creation**. *(1)*

---

### SAQ 3 — Why digitalization increases the importance of IT governance. (4 marks)

**Model answer**
- Companies now **depend far more heavily on IT** — IT underpins operations, customer channels and decision-making. *(1)*
- Therefore **a failure of IT governance may mean business disruption or, worse, business failure** — not just an IT inconvenience. *(1)*
- In **milder cases**, poor IT governance means **ineffective use of IT → wastage and lost opportunities**. *(1)*
- **However**, lack of IT governance **does not automatically mean business failure or loss** — and even with governance, **pain points will still occur**. What governance promises is **a better position to address and react to problems, with reduced risk and limited impact**. *(1)*

---

### SAQ 4 — The six OECD principles of corporate governance. (6 marks)
*Name each and state its substance in one line.*

**Model answer** *(1 each)*
1. **Ensuring the basis for an effective corporate governance framework** — transparent, efficient markets consistent with the rule of law, with clear division of responsibilities among authorities.
2. **The rights of shareholders and key ownership functions** — protect and facilitate the exercise of shareholders' rights.
3. **The equitable treatment of shareholders** — equitable treatment of **all** shareholders including **minority and foreign** shareholders, with **effective redress**.
4. **The role of stakeholders in corporate governance** — recognise stakeholder rights established by law or agreement, and encourage co-operation.
5. **Disclosure and transparency** — **timely and accurate disclosure on all material matters** (financial situation, performance, ownership, governance).
6. **The responsibilities of the board** — **strategic guidance**, **effective monitoring of management**, and **board accountability** to the company and shareholders.

---

### SAQ 5 — Apply the six Responsible AI principles to a bank's AI credit-scoring system. (6 marks)

**Model answer** *(1 per principle, correctly applied)*
- **Fairness** — test that the model does **not disadvantage applicants by gender, ethnicity, age or other protected attributes**, and does not **amplify historical bias** in lending data.
- **Transparency** — the bank must be able to **explain how a credit decision was reached**, both to regulators and to the applicant.
- **Privacy & Security** — customer financial data used **with consent**, protected against **misuse and cyber threats**.
- **Human Oversight** — a **human remains in control of consequential decisions** (e.g. loan refusal or account closure), and the decision must be **correctable** on appeal.
- **Accountability** — **clear lines of responsibility** for the model's outcomes and harms — a named owner, not "the algorithm".
- **Safety & Reliability** — the model **performs as intended**, is **robust to adversarial inputs** (e.g. manipulated application data), and **fails safely** rather than silently approving bad credit.

---

### SAQ 6 — Conformance and performance. (3 marks)

**Model answer**
- Identified by the **International Federation of Accountants (IFAC)** in its **October 2003** report, as the **two dimensions of enterprise governance**. *(1)*
- **Conformance** — addresses **corporate structure, roles and executive remuneration**; it is about **how the company is governed and held to account**. *(1)*
- **Performance** — focuses on **strategy and value creation**, and **enhancing efficiency through managing risk appetite**; it is about **what the company achieves**. *(1)*

---

### SAQ 7 — The seven GEIT components, and why a holistic approach matters. (4 marks)

**Model answer**

The seven COBIT components *(worth 3 of the 4 marks — award 3 for all seven, 2 for five or six)*:
1. **Principles, policies and frameworks**
2. **Processes**
3. **Organizational structures**
4. **Culture, ethics and behaviour**
5. **Information**
6. **Services, infrastructure and applications**
7. **People, skills and competencies**

Why holistic *(1)*: the components **interact with one another** to support a **comprehensive governance and management system**; implementing them in isolation (e.g. writing policies without changing culture or skills) fails, so **success depends on a holistic approach to their interaction**.

---

### SAQ 8 — Pain points vs trigger events. (4 marks)

**Model answer**
- **Pain point** — the **awareness that something needs improvement**, arising from **missed opportunities or negative impacts** already being felt. *(1)*
- **Trigger event** — an **internal or external event** that causes the organisation to focus on GEIT. *(1)*
- **Two pain point examples** *(1)*: **hidden IT spending**; **failure to meet regulatory requirements** / **outsourcing service levels not met** / **IT limiting innovation capability and business agility**.
- **Two trigger event examples** *(1)*: **merger, acquisition or divestiture**; **new CIO, CFO, CEO or board member** / **new regulatory or compliance requirements** / **external audit or consultant assessment**.

---

### SAQ 9 — The COBIT goals cascade. (5 marks)
**(a) [4] Describe the four steps. (b) [1] Why is the two-way relationship valuable?**

**Model answer**

(a)

- **Step 1 — Stakeholder drivers influence stakeholder needs.** Drivers include **strategy changes, changing business and regulatory environments, and new technologies**. *(1)*
- **Step 2 — Stakeholder needs cascade to enterprise goals.** Needs are related to a set of **generic enterprise goals**. *(1)*
- **Step 3 — Enterprise goals cascade to alignment goals.** COBIT defines **various alignment goals for each enterprise goal**. *(1)*
- **Step 4 — Alignment goals cascade to governance and management objectives**, where **specific goals are defined**. *(1)*

(b) Because IT goals are **linked back to their source (stakeholder drivers and needs)** as well as forward to enterprise objectives, the relationship **ensures IT goals are tightly linked to the organisation's mission and objectives and traceable back to stakeholder drivers** — so IT can demonstrate *why* it is doing what it is doing, and governance becomes **definable based on enterprise objectives and related risk**. *(1)*

---

### SAQ 10 — The three barriers to strategic alignment. (4 marks)
*Name and explain each. (b) Suggest one remedy.*

**Model answer** *(1 each + 1 for remedies)*
- **Expression barrier** — **inability by senior management to communicate business strategy to operational management**. *Remedy: structured, repeated communication cascades; the CIO translating strategy for IT staff.*
- **Specification barrier** — **lack of IT involvement in strategy development**, so **IT and business end up with two different strategies**. *Remedy: put the CIO in the strategy-formulation team, not just the delivery team.*
- **Implementation barrier** — **difficulty implementing the strategy because of the current IT portfolio**, e.g. **legacy systems**. *Remedy: portfolio management / staged modernisation of the legacy estate.*

---

### SAQ 11 — The full economic life cycle. (5 marks)
**(a) [4] Name the five phases in order and describe each. (b) [1] Why must a program be seen through its full life cycle?**

**Model answer**

(a)

1. **Investment** — **developing** the necessary capabilities. *(¾)*
2. **Adoption** — **implementing** the capabilities. *(¾)*
3. **Value creation** — **achieving the expected level of performance** and **moving the delivered capabilities into the active service portfolio**. *(1)*
4. **Value sustainment** — **assuring the assets continue to create value**, which may include **additional investment** to sustain value. *(¾)*
5. **Retirement** — **decommissioning** the resulting assets. *(¾)*

(b) Because **benefits and expected value are generally not realised until some time after delivery**, and the main risk is **lack of continuity in the program plan after the capabilities are delivered** — without continuity through the full cycle, **value is never captured**. *(1)*

---

### SAQ 12 — Business vs intermediate benefits + a scenario. (4 marks)
**(a) [2] Distinguish the two. (b) [2] A hospital invests in a new patient-records portal. Patient satisfaction rises but revenue and cost are unchanged. Classify the benefit and explain what benefits realization must do next.**

**Model answer**

(a) **Business benefits CREATE VALUE by increasing the company's profits.** **Intermediate benefits do NOT directly create value**, although they **benefit one or more groups of stakeholders** (e.g. improved customer service that does not increase profits). *(2)*

(b) The satisfaction rise is an **intermediate benefit** — real, stakeholder-facing, but **not yet profit** *(1)*. Benefits realization must ensure **intermediate benefits are made to CONTRIBUTE TO business benefits** — e.g. by using the portal to **reduce re-admission rates or administrative cost**, and it must confirm the return is **sufficient to merit the resources expended** *(1)*.

---

# 7. Tutorial answer key (all 60 questions)

> The tutorial files are quiz exports **without answers**. These are derived from the slides — they are your best predictor of the real paper, so check any you got wrong.

## Tutorial 1 — Topic 1

| Q | Answer |
|---|---|
| 1 | The system by which the use of IT within an organisation is directed and controlled |
| 2 | **Software Development** (not a pillar) |
| 3 | Independent but related models with different emphases but similar objectives |
| 4 | **The Monetary Authority of Singapore (MAS)** |
| 5 | Ensure accountability and define organisational objectives on behalf of shareholders |
| 6 | Companies depend more heavily on IT, so IT failures now risk business disruption or failure |
| 7 | **The equitable treatment of shareholders** |
| 8 | Ensure the organisation achieves its stated government-defined objectives |
| 9 | A hiring AI tested to ensure it does not disadvantage applicants based on gender or ethnicity |
| 10 | Humans must remain in control of consequential AI decisions and systems must be correctable |
| 11 | Concentration of power, access, dependency, and democratic oversight |
| 12 | **Transparency** |
| 13 | **Social and economic risk** |
| 14 | Transparency, accountability, robustness, safety, and human rights |
| 15 | The computational energy required can be equivalent to the lifetime CO₂ emissions of multiple cars |

## Tutorial 2 — Topic 2

| Q | Answer |
|---|---|
| 1 | A set of responsibilities and practices exercised by the board and executive management to provide strategic direction, manage risks, and ensure resources are used responsibly |
| 2 | **Conformance and Performance** |
| 3 | **Reputational assets** (not one of the six) |
| 4 | **Enron collapse** |
| 5 | **The shareholders** |
| 6 | **Governance of IT within organisations** |
| 7 | **Management of IT infrastructure and services** |
| 8 | Aligns with other relevant standards and frameworks, allowing them to be integrated alongside COBIT |
| 9 | Awareness that something needs improvement because of missed opportunities or negative impacts on the enterprise |
| 10 | Data loss incidents and failure to meet regulatory requirements |
| 11 | Represents untracked or unapproved expenditure that wastes resources and reduces earnings |
| 12 | **A pain point** |
| 13 | **New regulatory or compliance requirements** (trigger event) |
| 14 | Can increase buy-in from internal stakeholders through independent validation |
| 15 | A better position to address and react to problems, with reduced risk and limited impact |

## Tutorial 3 — Topic 3

| Q | Answer |
|---|---|
| 1 | **Strategic alignment between business and IT** |
| 2 | External factors (market, industry, geopolitics) and internal factors (culture, organisation, appetite) |
| 3 | IT can offer new opportunities that impact business strategy, just as business strategy shapes IT |
| 4 | Reflect management guidance and embody both business and IT strategies, providing direction to staff |
| 5 | **Stakeholder drivers that influence stakeholder needs** |
| 6 | Stakeholder needs → Enterprise goals → Alignment goals → Governance & Management Objectives → IT goals |
| 7 | IT goals are tightly linked to the organisation's mission and objectives, and also traceable back to stakeholder drivers |
| 8 | Strategy changes, changing business and regulatory environments, and new technologies |
| 9 | The enterprise's ability to adapt quickly to changes in the environment |
| 10 | **Monitoring the environment and making responsive decisions** |
| 11 | The business environment continuously changes, requiring continuous IT adaptation and realignment |
| 12 | Agile responses to new or unexpected events detected through environmental monitoring |
| 13 | **Expression, specification, and implementation barriers** |
| 14 | It ensures IT personnel do not lose sight of business objectives and remain aligned with strategic direction |
| 15 | Ensure the IT strategy is evolved and realigned to reflect the new business direction |

## Tutorial 4 — Topic 4

| Q | Answer |
|---|---|
| 1 | IT-enabled business investments achieve the promised benefits and deliver business value |
| 2 | Many high-expenditure IT-related initiatives fail to realize their expected business benefits |
| 3 | Business benefits create value by increasing company profits; intermediate benefits do not directly create value although they benefit one or more stakeholder groups |
| 4 | Optimal value will not be created, or worse, value may be eroded or destroyed |
| 5 | **Investment phase** |
| 6 | **Value creation phase** |
| 7 | **Retirement phase** |
| 8 | Because benefits and expected value are generally not realised until after some time, and continuity is required to capture those benefits |
| 9 | A collection of programs, projects and/or operations managed as a group to achieve strategic objectives |
| 10 | Defining investment thresholds and evaluating, prioritising, selecting, deferring, or rejecting new investments |
| 11 | Clearly defined, evaluated, prioritised, selected, and managed actively throughout their full economic life cycle |
| 12 | Evaluating and prioritising program business cases, deciding on investment proposals, allocating funds, and initiating programs |
| 13 | Grouping programs and projects together, enabling resource sharing, specialisation, and synergies that would be impossible to achieve individually |
| 14 | Utilise or depend on common resources such as raw materials, parts, or expertise |
| 15 | **The adoption phase** — capabilities were delivered but not implemented into active use, so value creation never occurred |

---

# 8. Rapid-fire recall (cover the right column)

| # | Prompt | Answer |
|---|---|---|
| 1 | IT governance definition | System by which the use of IT is **directed and controlled** |
| 2 | Four pillars | Strategic Management, Benefits Realization, Risk Optimization, Resource Optimization |
| 3 | Code of Corporate Governance publisher | **MAS** |
| 4 | Enron year | **2001** (→ SOX) |
| 5 | OECD principles (6) | Framework, Shareholder rights, Equitable treatment, Stakeholders, Disclosure, Board |
| 6 | Responsible AI principles (6) | Fairness, Transparency, Privacy & Security, Human Oversight, Accountability, Safety & Reliability |
| 7 | AI risks (6) | Bias, Privacy violations, Deepfakes, Autonomous systems, Job displacement, Concentration of power |
| 8 | Sustainability pillars (3) | Environmental, Social, Economic |
| 9 | ESG | Environmental, Social, **Governance** |
| 10 | Data centres' share of global electricity | **2–3%** |
| 11 | ICT share of global CO₂ | **4%** |
| 12 | E-waste per year | **50M+ tonnes** |
| 13 | Training a large AI model vs a car's lifetime CO₂ | **10×** |
| 14 | AI for sustainability: precision agriculture water/fertiliser saving | **up to 25%** |
| 15 | ISACA enterprise governance goal (4) | Direction, Objectives, Risk, Resources |
| 16 | IFAC 2003 dimensions | **Conformance & Performance** |
| 17 | Conformance covers | Corporate structure, roles, executive remuneration |
| 18 | Performance covers | Strategy and value creation; efficiency via risk appetite |
| 19 | Six key assets (Weill & Ross 2004) | Human, Financial, Physical, IP, Information & IT, Relationship |
| 20 | ISO 38500 | **Governance of IT** |
| 21 | ISO 27001 | Information **security** |
| 22 | ISO 9000 | **Quality** management |
| 23 | ISO/IEC 20000 | **IT service management** |
| 24 | ISO 31000:2009 | **Risk management** |
| 25 | ITIL | IT **infrastructure and services** management |
| 26 | Why COBIT is overarching | It **aligns with** other standards/frameworks |
| 27 | Absence of frameworks means | Success **not optimal** — not guaranteed failure |
| 28 | Pain point definition | **Awareness** something needs improvement |
| 29 | Trigger event definition | **Internal/external event** that triggers GEIT |
| 30 | COBIT components (7) | Principles/policies/frameworks; Processes; Org structures; Culture/ethics/behaviour; Information; Services/infrastructure/apps; People/skills/competencies |
| 31 | IT strategy techniques | **SWOT**, **BCG matrix** |
| 32 | BCG best area | **Cash Cow** |
| 33 | BCG needs heavy cash, high return | **Star** |
| 34 | RACI | Responsible, Accountable, Consulted, Informed |
| 35 | Strategic management aims at | **Strategic alignment between business and IT** |
| 36 | Two alignment questions | How is IT aligned to business? How is business aligned to IT? |
| 37 | SAM domains | **External** (IT strategy, business strategy); **Internal** (processes, policies, guidelines, procedures) |
| 38 | Planning factors | External (market, industry, geopolitics); Internal (culture, organisation, appetite) |
| 39 | Goals cascade (5 levels) | Drivers → Needs → Enterprise goals → Alignment goals → G&M objectives (+ IT goals) |
| 40 | Goals cascade initiator | **Stakeholder drivers** |
| 41 | Agility definition | Ability to **adapt quickly to changes in the environment** |
| 42 | Agility Loop 1 | **Monitoring and deciding** |
| 43 | Agility Loop 2 | **Improving existing processes** |
| 44 | Agility Loop 3 | **Creating new processes** (and retiring obsolete) |
| 45 | Three alignment barriers | **Expression, Specification, Implementation** |
| 46 | Expression barrier | Senior mgmt can't **communicate** strategy to operational mgmt |
| 47 | Specification barrier | **Lack of IT involvement** in strategy development |
| 48 | Implementation barrier | Unable to implement due to **current IT portfolio / legacy** |
| 49 | Communication linchpin | **CIO** |
| 50 | Benefits realisation objective | Investments **achieve promised benefits and deliver business value** |
| 51 | Business benefit definition | **Increases company profits** |
| 52 | Intermediate benefit definition | **No direct value**, but benefits stakeholders |
| 53 | Without benefits realisation | **Optimal value not created; value eroded or destroyed** |
| 54 | Life cycle (5, in order) | Investment → Adoption → Value creation → Value sustainment → Retirement |
| 55 | Value creation phase | Achieve expected performance + **move capabilities into active service portfolio** |
| 56 | Portfolio definition | Collection of programs/projects/operations **managed as a group** for strategic objectives |
| 57 | COBIT portfolio processes (5) | Target investment mix; sources of funds; evaluate & select; monitor/optimise/report; manage benefits achievement |
| 58 | Portfolio organisation (3) | **Categories, Product/service, Resource usage** |
| 59 | Payback period | Time to **recoup the initial investment** |
| 60 | Maturity levels 4 and 5 | **4 = Predictable, 5 = Optimizing** (ISO 15504, 6 levels 0–5) |

---

# 9. One-page cheat sheet (print this)

```
FOUR PILLARS        Strategic Mgt · Benefits Realization · Risk Optimization · Resource Optimization
GOVERNANCE HIERARCHY Corporate ⊃ IT ⊃ AI   (independent models, different emphasis, similar objectives)
SG CODE             MAS (Monetary Authority of Singapore), publicly-listed cos
ENRON               2001 → Sarbanes-Oxley
OECD (6)            Framework · Shareholder rights · Equitable treatment · Stakeholders · Disclosure · Board
AI PRINCIPLES (6)   Fairness · Transparency · Privacy&Security · Human Oversight · Accountability · Safety&Reliability
AI RISKS (6)        Bias · Privacy · Deepfakes · Autonomous systems · Job displacement · Concentration of power
SUSTAINABILITY (3)  Environmental · Social · Economic          ESG = Environmental · Social · GOVERNANCE
GREEN IT (6)        PUE/data centre · Circular economy · Renewables/PPA · Cloud optimisation · Carbon accounting · Sustainable SW eng
STATS               2–3% electricity · 4% CO₂ · 50M+ t e-waste · 10× model energy · 25% precision-ag saving

ISACA ENT GOV       Direction · Objectives · Risk · Resources
IFAC 2003           CONFORMANCE (structure, roles, remuneration) vs PERFORMANCE (strategy, value creation)
SIX ASSETS          Human · Financial · Physical · IP · Information&IT · Relationship   (NOT reputational)
ISO NUMBERS         38500=gov of IT | 27001=infosec | 9000=quality | 20000=IT svc mgmt | 31000=risk | 15504=maturity
COBIT               aligns with others → OVERARCHING. Absence ⇒ success not optimal, NOT failure
PAIN POINT          a condition you suffer      TRIGGER EVENT  an event that happens
COBIT 7 COMPONENTS  Principles/policies/frameworks · Processes · Org structures · Culture/ethics/behaviour ·
                    Information · Services/infrastructure/apps · People/skills/competencies   (= HOLISTIC)
BCG                 Star (cash-hungry, high return) · Cash Cow (BEST) · Question mark (potential) · Dog (neither)

STRATEGIC MGT       aim = ALIGNMENT business ↔ IT (two-way)
GOALS CASCADE       drivers → needs → enterprise goals → alignment goals → G&M objectives → IT goals
AGILITY LOOPS       1 Monitor & decide · 2 Improve existing (automate/reliability) · 3 Create new (retire old)
BARRIERS            Expression (can't say) · Specification (didn't co-design) · Implementation (legacy)
CIO                 explains IT strategy, makes staff supporters, realigns when business goals change

BENEFITS REAL.      investments achieve promised benefits & deliver business value
BUSINESS BENEFIT    increases PROFIT          INTERMEDIATE    benefits stakeholders, no direct profit
LIFE CYCLE          Investment → Adoption → Value creation → Value sustainment → Retirement
PORTFOLIO           components need NOT be related; managed as a group for strategic objectives
COBIT PM (5)        mix → funds → evaluate&select → monitor/optimise/report → manage benefits
PORTFOLIO ORG (3)   Categories · Product/service · Resource usage
PAYBACK             initial investment ÷ annual net benefit
ROI                 (net benefit ÷ initial investment) vs opportunity cost of capital
MATURITY (ISO15504) 0 Incomplete · 1 Performed · 2 Managed · 3 Established · 4 Predictable · 5 Optimizing
BALANCED SCORECARD  evaluates IT from the USER's perspective
```

---

*Study guide generated from Topics 1–4 lecture decks (117 slides) and Tutorials 1–4 (60 questions). Tutorial answers are derived from the slides — the exported tutorials contained no answer key.*
