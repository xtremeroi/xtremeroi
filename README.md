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

Reusable Claude skills that carry out approved recommendations in an ad management tool's web interface, build new campaigns from client creatives and stop before launch, and publish client reports. A separate planning agent proposes changes and waits for approval.

### Rooms: people and agents in one conversation

A standalone shared-room service where staff and their AI assistants work together. Messages from other people or agents are treated as information only. An agent acts only on its own user's approved instruction.

### Private voice and local models

- Push-to-talk dictation for the Mac, transcribed on our own hardware so nothing leaves the network
- A local model stack on in-house GPU machines, with sandboxed coding agents and a task router
- A private benchmark site where every model is tested before it gets a job

### Small utilities

- A screen sharing switcher for a fleet of Macs and PCs (menu bar and iPhone)
- A session tracker that shows every open AI work session and which ones are waiting on a person
- Cost, backup and security watchers that report to the Command Center
- Home and office controls with signed requests and owner-only approvals

### Websites and pitch apps

Interactive pitch apps for prospects, landing pages, and full small-business websites, each built and deployed in days.

## Built with

Claude Code, Claude skills and MCP connectors, Cloudflare Workers (KV, D1, R2, Durable Objects, Access), Next.js, three.js, Swift and SwiftUI, Electron, Python, and local models served on in-house hardware. We also use OpenAI Codex and open-weight models where they fit, and test them side by side.

## Public repositories

- [sns-desk](https://github.com/xtremeroi/sns-desk): macOS menu bar punch clock and activity tracker

## Work with us

If you run a small business and want to know which parts of it an agent could take over, start with a conversation: [xtremeroi.com](https://xtremeroi.com)
