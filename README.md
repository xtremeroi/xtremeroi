# XTREME ROI

We help small businesses put AI agents to work in their day-to-day operations.

We did it to our own company first. XTREME ROI is an Amazon advertising agency, and over the past year we rebuilt how the agency runs around AI agents: reporting, account monitoring, client deliverables, time tracking, invoicing, lead generation and internal communication. Everything below is software we built with Claude Code and other AI coding tools, and that our team uses every working day.

Most of the code is private because it carries client data. This page describes what exists and how it works. We are glad to walk through any of it live.

## What we do for clients

- **Find the work worth automating.** We map a business's recurring tasks and pick the ones where an agent saves real hours without adding risk.
- **Build the workflow.** Agents that read your data, draft the work, and hand it to a person for approval before anything goes out or changes.
- **Connect your tools.** We build connectors (MCP servers) so an AI assistant can work with your own systems, with access limited per person.
- **Train the team.** Seat-by-seat rollout, written guides, and reusable skills so staff can run the workflows themselves.
- **Keep sensitive work in-house.** For data that should not leave the building, we set up and benchmark local models on your own hardware.

## How we build

A few rules run through everything here:

1. **People approve, agents prepare.** Anything client-facing, money-related or hard to undo waits for a named person's yes.
2. **Numbers come from code, words come from the model.** Reports calculate figures in tested code and use AI only for the narrative.
3. **Every claim is checked.** An independent auditor compares what our tools say against source data.
4. **Access is per person.** Each teammate and each agent sees only the accounts they are assigned.
5. **Unattended jobs are watched.** Scheduled agents report in, and a watcher raises an alert when one misses a run.

## Case studies

### Stats & Strats: an agency operating system

The platform our team works in all day. It ingests advertising data for every client, produces the weekly analysis and a prioritized action plan, and drafts each client's weekly strategy brief for a manager to approve and publish to a client portal.

- Account Watchdog that flags problems and wins across all accounts
- Live intraday signals per client and a fleet board for managers
- A data auditor ("The Judge") and a verification layer that check each KPI against its sources
- Time tracking, timesheets, payroll support and invoicing in the same app
- Direct API connections in place of hand-downloaded reports:
  - Amazon Ads API for scheduled reporting, live budget and serving status every five minutes, invoices, and approved bid, budget and keyword changes
  - Amazon Marketing Stream for hourly performance pushed by Amazon
  - Amazon Selling Partner API (Brand Analytics) for Seller Central sales and traffic
  - Perpetua's data feed, delivered to our own cloud storage bucket
  - Data Dive for market and competitor research
  - Google Drive for client files, plus connections to accounting and chat tools
- One credential rule: the advertising keys live only inside the server. No agent, script or prompt is ever handed them. Agents get a read-only feed, a gated write path, or the connector below.
- Python scripts that run outside the platform as a second line of defense: a nightly backup of everything that cannot be rebuilt, a dead-man's switch that checks from the outside whether the weekly data job produced its files, a completeness check that learns each client's expected files from that client's own history, and a helper that turns agent answers into clean import files
- An MCP connector so Claude can read the analysis, generate reports and make approved ad changes
- Companion apps: a macOS menu bar punch clock, a Chrome extension, and iPhone apps for staff time and manager approvals

Next.js on Cloudflare Workers. 660+ commits.

### XROI Command Center: seeing your agents work

A 3D office in the browser where each AI agent has a desk and a job. It shows what every agent, machine and scheduled job is doing, and gives the owner one place to assign tasks, read results and approve requests.

- Wiring and flow maps of how data moves between systems
- Rooms where people and agents talk, with an approval gate before any agent acts on a request
- A single desk for mail, calendar and to-dos across accounts
- Revenue, usage and cost boards
- One-key health check across connectors, machines and services
- iPhone and Apple Watch companions

three.js on Cloudflare Workers. 1,850+ commits.

### Lead generation on autopilot, with a human gate

A Worker that scouts freelance marketplaces for matching jobs, drafts proposals for each team member's profile, and applies within set rules. New leads post to the team's chat within minutes.

### Channel attribution for a DTC brand

A weekly dashboard that reconciles two attribution vendors against platform-direct data for a subscription brand spending across many ad channels, so the owner can see where the tools disagree and where spend is past the point of return.

### Agents that operate ad platforms

Reusable Claude skills that carry out approved recommendations in Perpetua's web interface, build new campaigns from client creatives and stop before launch, and publish client reports. A separate planning agent proposes changes and waits for approval.

### Rooms: people and agents in one conversation

A standalone shared-room service where staff and their AI assistants work together. Messages from other people or agents are treated as information only. An agent acts only on its own user's approved instruction.

### Local models on two NVIDIA DGX Sparks

For work that should never leave the building, we run open-weight models on our own hardware: two DGX Sparks and a small fleet of Macs on a private network.

- **Setup and serving.** Both Sparks configured headless, serving large open models through vLLM and llama.cpp, each on its own or joined to run one larger model across the pair. Endpoints are reachable only on the private network, with keys held by a relay so no agent ever sees them.
- **Benchmarks before trust.** Every model runs a fixed suite of public tests (IFEval, IFBench, SimpleQA Verified, BFCL and others) before it is given a job. Results go to a private site with a live board of tests in progress, and a daily scout proposes newer tests for the owner to authorize.
- **Real jobs moved off the cloud.** Scheduled mail sweeps, daily reviews, report drafting and question answering now run on local models. A watcher alerts when a job misses its run.
- **Sandboxed agents.** Local coding agents work inside NVIDIA OpenShell sandboxes with a written network policy. We measured the cost: about 0% overhead for a single agent and about 5% with four running at once. Their output is reviewed before it is staged.
- **Operations.** Memory guards, scheduled model swaps, and one status card showing what each machine is serving.

The two-Spark model builds follow community recipes, credited to their authors.

### Private voice

Push-to-talk dictation for the Mac, transcribed on our own hardware so nothing leaves the network. The same service transcribes recorded calls into meeting notes.

### Guardrails for a high-stakes agent: a trading sandbox

A personal research project, included here for its controls. It is not a service we offer, and we publish no positions or results.

An open-weight model on the Sparks writes and maintains strategy code for the owner's own accounts on a regulated exchange. The question we built it to answer: how do you let a model write code that touches real money without trusting the model?

- **The model never holds credentials.** It works in a sandbox whose only exits are the model endpoint and a single gate. Direct access to the exchange, the internet, package registries and local secrets was tested and confirmed blocked.
- **Proposals are hashed.** Each change is a packet of a written proposal plus code. The site shows the owner the exact text and fingerprints the exact bytes.
- **Independent review.** Three different models must each approve the same fingerprinted packet, and tests must pass against it. A conditional yes, a missing answer or a review of an earlier version does not count.
- **Two owner decisions.** Approving a strategy does not authorize deploying it. Each is a separate signed decision on a private, authenticated site.
- **The gate checks everything again.** Before deploying, it confirms the receipt is the owner's, unused, unexpired and matches the current bytes, and that no later hold or rejection exists. Any edit after approval voids the approval.
- **Failure reverts.** The gate applies the change as a patch, runs the packet's tests and confirms the service restarted. Any failure rolls it back.
- **Read-only where possible.** Brokerage data is a read-only snapshot. Every decision and deployment is written to a ledger.

The same pattern fits any agent whose mistakes are expensive: payments, payroll, pricing, or changes to customer records.

### Small utilities

- A screen sharing switcher for a fleet of Macs and PCs (menu bar and iPhone)
- A session tracker that shows every open AI work session and which ones are waiting on a person
- Cost, backup and security watchers that report to the Command Center
- Home and office controls with signed requests and owner-only approvals

### Contractor invoicing and payout approvals

A portal where a company's contractors submit invoices and expenses and admins approve them for payment by ACH, Zelle or Wise. Built for two separate businesses from one design. The portal tracks and approves payouts; the money itself moves through the bank or payment service.

- **Invite only.** Admins issue single-use activation codes that expire.
- **Verified before paid.** A contractor cannot invoice until an admin has their tax form on file and has set them up as a payee.
- **Changes re-lock the account.** Editing payout details pauses invoicing until an admin verifies them again.
- **Two people on every payment.** One admin approves an item and a different admin marks it paid.
- **No bank numbers stored.** The portal records the payout method only. Account details are collected separately.
- **Batch exports.** Approved items download as files ready for each payment method.

### Bookkeeping across several companies at once

Custom QuickBooks connectors (MCP servers) built for a business that runs as several related legal entities, each with its own set of books. Claude can work across all of the entities' books in one conversation, instead of a bookkeeper signing in and out of each company file in turn.

### talkandtext.ai: booking by text

Our own product for local service businesses. Customers text the business, pick a service and a time, and get a confirmation back, with no phone call and no app. It is the booking layer on the Pro MBL site below.

### Client websites

**[mbldetail.com](https://mbldetail.com/)**: Pro MBL Auto Detail, a mobile detailing and ceramic coating business in San Diego. A full site that replaced a template builder page: an AI concierge that answers visitor questions, a button that drafts the customer's booking text for them, booking by text message through our own talkandtext.ai, real pricing by vehicle size, a before-and-after slider, and a gallery of the shop's own work.

**[jardininfusions.com](https://jardininfusions.com/pages/lavender-cocktails)**: Jardin Infusions, a botanical drink elixir brand. Landing pages inside the brand's Shopify store for its Pinterest campaigns. Each pin opens the page on the exact recipe the visitor clicked, with the product and a multi-pack offer beside it. We also built design directions for the storefront for the owner to review.

**[simpletics.com](https://simpletics.com/)**: Simpletics, a men's hair care brand. Ongoing AI development: connecting Claude to the brand's advertising platforms through the platforms' official connectors, under a dedicated account with its own limited access, with a person approving any budget or spend change. Also landing page concepts built for testing.

### Pitch apps

Interactive pitch apps and private growth plans for prospects, each a small gated site built around that prospect's own numbers.

## Built with

Claude Code, Claude skills and MCP connectors, Cloudflare Workers (KV, D1, R2, Durable Objects, Access), Next.js, three.js, Swift and SwiftUI, Electron, Python, and open-weight models served with vLLM, llama.cpp and Ollama on NVIDIA DGX Sparks and Apple silicon. We also use OpenAI Codex and open-weight models where they fit, and test them side by side.

## Public repositories

- [sns-desk](https://github.com/xtremeroi/sns-desk): macOS menu bar punch clock and activity tracker

## Work with us

If you run a small business and want to know which parts of it an agent could take over, start with a conversation: [xtremeroi.com](https://xtremeroi.com)
