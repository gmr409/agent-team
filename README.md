# Agent Team Architect

A prompt that designs a small team of AI agents to handle a task you repeat often.

You describe the task. The prompt asks a few questions, designs the team, and gives you everything you need to build it in one week: instructions for each agent, a flowchart, a test plan, and a day-by-day schedule.

The prompt lives in [`agent-team.md`](agent-team.md).

---

## The Short Version

Think about a small neighborhood restaurant.

The **Chef** runs the kitchen. She designs the menu, decides how each dish should taste, and cooks the most demanding dishes herself. She doesn't do everything, though. A few cooks work alongside her, and each one owns a station. One handles the grill. One handles sauces. One makes desserts. Each cook knows their station well and doesn't wander into someone else's.

Orders reach the kitchen on **tickets**. Every ticket follows the same format: table number, dish, changes, allergies. Because the format never changes, no cook has to guess what an order means.

Some work needs no cook at all. The dishwasher cleans plates. The ticket printer prints orders. The oven timer beeps on schedule. Nobody pays a cook to do a machine's job.

Before a plate leaves the kitchen, someone checks it at the pass. When the Chef adds a new dish, she tastes it herself before it goes on the menu. Then a server carries the finished meal to the table.

Good chefs also keep the kitchen lean. If someone has no job to do during service, the Chef asks them to step out. Extra people in a kitchen don't speed things up. They get in the way, cost money, and cause mistakes.

This prompt designs a kitchen like that for your work. The Chef is you. The cooks are AI agents. The meal is the finished result of your workflow. The prompt answers four questions:

1. **Which tasks need a cook at all?** Tasks that follow fixed rules go to plain automation, the way plates go to the dishwasher. AI agents handle tasks that need judgment or writing.
2. **How many cooks does the kitchen need?** As few as possible. The prompt questions every agent the way a chef questions every person in the kitchen: if the work runs fine without you, step out.
3. **How does work move between stations?** Every handoff follows a defined format, like an order ticket, so the next agent knows exactly what it's receiving.
4. **Where does the Chef stay in charge?** The prompt marks every point where you must review or approve the work before it goes out.

Then it writes a recipe card for each agent and gives you a schedule to open the kitchen in seven days.

### What about the expediter?

Busy restaurants often have an **expediter**, a person who calls out orders, keeps stations in sync, and makes sure dishes for the same table finish together. In an AI system, the matching role is a coordinating agent that manages the others.

The prompt treats this role as **optional**. A food truck with two cooks runs fine without an expediter, because the handoffs are simple and everyone sees the whole operation. Many AI workflows work the same way: fixed handoffs, no manager needed. The prompt adds a coordinating agent only when the workflow has enough moving parts to justify one. If you find yourself adding a manager agent by habit, ask whether the kitchen needs it.

---

## What the Prompt Does

You give the prompt a description of one workflow. It gives you back a build guide containing:

- Every task in your workflow, sorted into four groups: plain automation, AI agent, AI agent with human review, or human only
- A recommended team of 1 to 5 agents, with a reason for each one
- A cost estimate per run and per month
- A flowchart showing how work moves from start to finish
- A "contract" for every handoff, listing the exact fields one agent passes to the next
- A map of which data each agent is allowed to access
- Ready-to-use instructions (system prompts) for every agent
- A 7-day build plan that starts with creating a test set
- Metrics for measuring whether the system works, plus rules for when to take a task away from an agent

---

## How It Works

The prompt guides the AI through the same steps a chef follows when opening a new kitchen.

| Step | What happens | Restaurant version |
|---|---|---|
| 0. Clarify | If your description has gaps, the AI asks up to 5 questions and waits for answers. | "How many covers on a Friday night? Any dietary restrictions on the menu?" |
| 1. Workflow audit | The AI identifies the real goal and where time gets wasted. | Tickets pile up at the grill while the dessert station sits idle. |
| 2. Task classification | Every task goes into one of four groups. Rule-based tasks go to plain automation, not AI. | Plates go to the dishwasher. The Chef keeps the signature dish. |
| 3. Team design | The AI picks the smallest team that gets the job done and decides which agents need the most capable (and most expensive) model. | Three cooks, not eight. The senior cook takes the sauté station, and a prep cook chops vegetables. |
| 4. Role definition | Each agent gets a job description: what it does, what it receives, what it produces, and what it must stay away from. | The pastry cook makes desserts and never touches the grill. |
| 5. Handoff contracts | Each handoff gets a defined format, and the receiving agent checks it before starting. | The order ticket: table, dish, changes, allergies, every time. |
| 6. Data boundaries | The AI maps which data goes where and flags anything sensitive. | Allergen rules. Peanuts never reach the station making the nut-free dish. |
| 7. Prompt writing | The AI writes the instructions for every agent. | A recipe card and station guide for each cook. |
| 8. QA and safety | The AI adds review steps and marks where a person must approve. | Plates get checked at the pass. The Chef tastes every new dish. |
| 9. Launch plan | A 7-day schedule. Day 1 builds a test set before anything else. | A soft opening for friends and family before the public arrives. |
| 10. Optimization | Metrics, cost controls, and "kill criteria" for when an agent isn't working. | Food cost per plate, ticket times, and pulling a dish off the menu ("86 it") when it keeps coming back. |

---

## Two Modes

The prompt runs in one of two modes. You choose in the `<mode>` block.

**Design-first (the default, and the recommended choice)**
The AI delivers the team design (sections 1 through 6), then stops and asks you to approve it. After you approve, it writes the agent prompts and the build plan.

Use this mode most of the time. A chef approves the menu and the station layout before anyone writes recipe cards. If you disagree with the team design, you find out before the AI writes instructions for agents you plan to cut.

**One-shot**
The AI delivers everything in one response. Use this mode when you know the workflow well and want the full guide at once. Expect a long response, often 6,000 to 10,000 words.

---

## How to Use It

1. Open [`agent-team.md`](agent-team.md) and copy its full contents.
2. Fill in every `{{placeholder}}` in the `<workflow>` block. Specific details produce better results.
3. Set the `<mode>` block to `design-first` or `one-shot`.
4. Paste the prompt into Claude (or another capable AI model) and send it.
5. Answer any clarifying questions.
6. In design-first mode, review the team design, request changes, and approve it.
7. Follow the 7-day plan.

---

## Filling In the Workflow Block

The `<workflow>` block is where you describe your task. The table below explains each field, using a small bakery that handles catering orders by email as the example.

| Field | What to write | Example |
|---|---|---|
| Business or team | Who you are and what you do | Two-person bakery that takes catering orders |
| Workflow to automate | The steps as they happen today, in order | A customer emails a request. We read it, check the calendar, price it, write a quote, and email it back. |
| Volume | How often the workflow runs | About 25 requests per week |
| Goal and KPIs | What success looks like, with numbers | Send quotes within 4 hours instead of 2 days |
| Bottlenecks | Where time or money gets lost | Pricing custom orders takes 30 minutes each |
| Constraints | Budget, rules, required approvals | Under $50 per month. The owner approves every quote over $500. |
| Data sensitivity | Types of data involved | Customer names, emails, phone numbers |
| Deployment stack | Tools you already have | Gmail, Google Sheets, Zapier, Claude API |

Describe the workflow steps the way you'd explain them to a new cook on their first shift. "We handle orders" gives the AI nothing to work with. "We read the email, check whether the date is open in Google Calendar, and look up prices in a spreadsheet" gives it a clear picture.

---

## What You Get Back

| # | Section | What it tells you |
|---|---|---|
| 1 | Assumptions | What the AI assumed about your situation, plus any questions |
| 2 | Executive summary | The whole plan in 5 sentences or fewer |
| 3 | Task classification | Every task and which of the four groups it belongs in |
| 4 | Agent team | Each agent, its job, its model tier, and the cost estimate |
| 5 | Workflow map and contracts | A flowchart plus the exact format of every handoff |
| 6 | Data boundaries | Which agent accesses which data, and what's off-limits |
| 7 | Agent blueprints | A full job description for each agent |
| 8 | Prompt pack | Copy-paste instructions for every agent |
| 9 | Tools and stack | What each tool does, plus lower-cost alternatives |
| 10 | QA and approvals | Every review step and every human checkpoint |
| 11 | 7-day plan | What to build each day, starting with a test set |
| 12 | Measurement and risks | Metrics, kill criteria, and how to recover when something breaks |
| 13 | Next steps | 3 to 5 things to do today |

In design-first mode, the AI stops after section 6 and waits for your approval.

---

## Tips for Good Results

- **Pick a workflow you know well.** The AI only knows what you tell it. If the steps aren't clear to you yet, write them down first.
- **Start with a small, repeating workflow.** A task you do 10 or more times a week gives the system enough runs to prove itself.
- **Clear the kitchen.** Review section 4 the way a chef looks around the line before service. For every agent, ask: "Would anything break if this one left?" If the answer is no, cut it.
- **Build the test set first.** Collect 10 to 20 real past examples along with the results you'd consider correct. Without them, you have no way to tell whether the system works.
- **Taste everything during the first week.** Review every output yourself. Reduce human review only after the numbers show the system holds up.

---

## Known Limits

This prompt gives you a strong starting point, not a guarantee. Keep these limits in mind.

- **Cost estimates are rough.** AI models lack reliable access to current pricing. For accurate numbers, add current per-token prices to your workflow block, or treat the estimate as a first guess and check it against your provider's pricing page.
- **The AI grades its own work.** The `<final_checks>` block asks the AI to review its answer before responding. It helps, but AI models tend to report that every check passed. Your own review of the team design matters more.
- **Long output.** One-shot mode produces a lot of text. Design-first mode keeps it manageable.
- **Flowcharts need a viewer.** The workflow map uses Mermaid, a text format for diagrams. It displays as a picture on GitHub, in Claude, and in many markdown editors, but appears as plain text in Word or Notepad.
- **Results vary.** The prompt follows sound multi-agent design practice, but output quality depends on your workflow description and the model you use.

---

## How to Tell If It Worked

After a run, ask yourself four questions:

1. Did the AI ask useful clarifying questions, or generic ones?
2. Would you cut any agent it recommended?
3. Did it assign a fixed, rule-based task to an AI agent instead of plain automation?
4. Would one of its agent prompts produce usable output if you handed it to an AI tool unchanged?

Good answers on all four mean the prompt did its job. A bad answer points to the section of the prompt to adjust.

---

## Customizing the Prompt

The prompt uses XML-style tags (like `<rules>` and `<output_format>`) to separate its parts. Claude reads these tags reliably, and they let you edit one section without touching the rest.

Common changes:

- **Fewer or more agents:** Change "1 to 5 agents" in step 3 of `<instructions>`.
- **Shorter output:** Remove sections from `<output_format>`, or reduce what `<analysis_depth>` asks for.
- **Different launch timeline:** Change the 7-day plan in step 9.
- **Stricter governance:** Add rules to `<rules>`, such as required approval before any external email or data export.

---

## Glossary

| Term | Definition | Restaurant version |
|---|---|---|
| Agent | An AI model given one job, a set of instructions, and access to specific tools | A cook assigned to one station |
| Workflow | A series of steps you repeat to get a result | Everything from taking an order to serving the meal |
| Automation | A fixed set of rules a computer follows the same way every time, with no AI involved | The dishwasher or the ticket printer |
| Coordinating agent | An optional agent that routes work between other agents and keeps them in sync | The expediter |
| Handoff | When one agent passes its finished work to the next agent | Passing a plate from the grill to the pass |
| Schema | The exact list of fields and formats in a handoff | The order ticket: table, dish, changes, allergies |
| System prompt | The standing instructions an agent follows every time it runs | A recipe card and station guide |
| Human-in-the-loop | A step where a person reviews or approves the work | The Chef tasting a new dish before it goes on the menu |
| Model tier | Which AI model an agent uses: a more capable, pricier one or a faster, cheaper one | A senior cook on sauté, a prep cook chopping onions |
| Test set | Real past examples with known correct results, used to check the system | Soft opening night |
| Kill criteria | Measurable rules for when to take a task away from an agent | Taking a dish off the menu ("86 it") |
| Hallucination | When an AI states something false as if it were true | A dish sent out with an ingredient the ticket never asked for |
