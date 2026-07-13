<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0EA5E9,45:7C3AED,100:EC4899&height=230&section=header&text=OpenLeash&fontSize=58&fontColor=ffffff&fontAlignY=38&desc=Agent%20Control%20Layer&descSize=20&descAlignY=58" width="100%" />

<p>
  <a href="https://openleash.com"><img src="https://img.shields.io/badge/Website-openleash.com-0EA5E9?style=for-the-badge&logo=googlechrome&logoColor=white" /></a>
  <a href="https://docs.openleash.com"><img src="https://img.shields.io/badge/Docs-docs.openleash.com-7C3AED?style=for-the-badge&logo=readthedocs&logoColor=white" /></a>
  <a href="https://github.com/open-leash?q=plugin-"><img src="https://img.shields.io/badge/Plugins-events%20%2B%20capabilities-EC4899?style=for-the-badge&logo=typescript&logoColor=white" /></a>
</p>

<p>
  <a href="https://github.com/orgs/open-leash/repositories"><img src="https://img.shields.io/badge/Star-our%20repositories-F59E0B?style=for-the-badge&logo=github&logoColor=white" /></a>
  <a href="https://github.com/open-leash"><img src="https://img.shields.io/badge/Follow-OpenLeash-181717?style=for-the-badge&logo=github&logoColor=white" /></a>
</p>

<h2>Explore the repositories</h2>

<p><strong>⭐ Star the repositories you find useful and follow OpenLeash for new releases, plugins, and project updates.</strong></p>

</div>

---

## Core platform

| Repository | What it does |
|---|---|
| [`desktop-client`](https://github.com/open-leash/desktop-client) | Installed tray app, local API, and hook installer for connecting developer agents to OpenLeash. |
| [`client-api`](https://github.com/open-leash/client-api) | Client-facing API for hooks, evaluation, enrollment, mobile approvals, and updates. |
| [`dashboard-api`](https://github.com/open-leash/dashboard-api) | Admin API for organization setup, users, policy, plugins, audit, and usage. |
| [`dashboard-web`](https://github.com/open-leash/dashboard-web) | Organization dashboard for identity, deployment, policies, plugins, and audit history. |
| [`mobile-client`](https://github.com/open-leash/mobile-client) | iOS and Android companion for reviewing and responding to approval requests. |
| [`local-proxy`](https://github.com/open-leash/local-proxy) | Local AI-agent traffic proxy and policy-enforcement relay. |
| [`provider-puller`](https://github.com/open-leash/provider-puller) | Scheduler that discovers and normalizes agent activity from hosted enterprise providers. |
| [`shared`](https://github.com/open-leash/shared) | Shared TypeScript contracts, event schemas, and plugin types used across OpenLeash. |
| [`docs-web`](https://github.com/open-leash/docs-web) | Source for the public OpenLeash documentation site. |

## First-party plugins

| Repository | What it does |
|---|---|
| [`plugin-blast-radius`](https://github.com/open-leash/plugin-blast-radius) | Guards destructive tool calls and operations that affect broad sets of data. |
| [`plugin-code-scanner`](https://github.com/open-leash/plugin-code-scanner) | Scans AI-generated code for security risks and reports structured findings. |
| [`plugin-data-leakage-prevention`](https://github.com/open-leash/plugin-data-leakage-prevention) | Detects and masks sensitive data before it is sent in agent prompts. |
| [`plugin-mcp-scanner`](https://github.com/open-leash/plugin-mcp-scanner) | Inventories MCP servers, tools, and calls for visibility and audit. |
| [`plugin-rules-enforcer`](https://github.com/open-leash/plugin-rules-enforcer) | Evaluates agent activity against user- and organization-defined rules. |
| [`plugin-sensitive-access`](https://github.com/open-leash/plugin-sensitive-access) | Detects secret access, environment-file reads, and possible exfiltration attempts. |
| [`plugin-siem-exporter`](https://github.com/open-leash/plugin-siem-exporter) | Exports OpenLeash events and logs to SIEM destinations. |
| [`plugin-skill-scanner`](https://github.com/open-leash/plugin-skill-scanner) | Reviews agent skills and reports suspicious or risky behavior. |
| [`plugin-token-saver`](https://github.com/open-leash/plugin-token-saver) | Reduces prompt token usage before model calls to lower cost and latency. |

---

## What OpenLeash Is

OpenLeash is the agent control layer for AI agents.

It gives teams and builders one place to observe agent activity, shape prompts, reduce token cost, scan tools and skills, route approvals, enforce policy, and add new capabilities through plugins.

An agent does something: submits a prompt, calls a tool, starts a session, changes a skill, produces a response, or touches an MCP server. OpenLeash catches that moment, turns it into an event, runs the plugins subscribed to that event, and returns a result when the agent needs one.

```text
agent action
  -> OpenLeash observes it
  -> OpenLeash emits a normalized event
  -> matching plugins run in order
  -> OpenLeash returns allow, deny, ask, transformed prompt, inventory, audit, or metadata
```

That makes OpenLeash bigger than a security product. Security is one important use case, but the same pipeline also handles token compression, prompt shaping, MCP inventory, skill scanning, audit context, approvals, policy decisions, and future community-built agent features.

---

## Real Examples

```text
User submits a long prompt
  -> event: prompt.beforeSubmit
  -> token-saver reduces token cost
  -> data-leakage-prevention checks the final prompt
  -> sensitive-access checks secret exposure and exfiltration risk
```

```text
Agent calls a tool or MCP server
  -> event: tool.beforeUse
  -> sensitive-access checks secret access
  -> blast-radius checks destructive scope
  -> rules-enforcer checks policy
  -> mcp-scanner records inventory and audit context
  -> OpenLeash returns allow, ask, or deny
```

```text
OpenLeash detects a new agent skill
  -> event: skill.changed
  -> skill-scanner reviews the skill
  -> OpenLeash stores the finding or asks for review
```

```text
Agent finishes work
  -> event: agent.response
  -> response-aware plugins can evaluate output, add audit context, or trigger follow-up workflows
```

---

## Why It Exists

Agents are leaving the chat box.

They read repos, edit files, call tools, run shell commands, browse SaaS apps, touch tickets, inspect databases, interact with MCP servers, and work across local and cloud environments.

The hard problem is not only "block dangerous things." It is:

- What did the agent try to do?
- Which tools and MCP servers did it use?
- What context did it send?
- Which plugin changed or checked the request?
- Was a human asked?
- What should happen next?

OpenLeash is built to make those answers clear, programmable, and auditable.

---

## The Plugin Model

Plugins are small, focused features that subscribe to OpenLeash events.

Each plugin has:

- a manifest with name, version, events, permissions, settings, effects, and ordering
- a handler that receives event input
- stable primitive capabilities for evaluator LLM calls, plugin-scoped storage, notifications, signals, usage, logs, audit, and reviewed host context
- typed results that OpenLeash merges into the final agent response

Plugins do not import OpenLeash internals. They own their detection logic, prompts, schemas, parsing, and fallbacks. OpenLeash provides primitive capabilities and decides how those primitives are fulfilled in OpenLeash Cloud or Private Cloud.

Start with any first-party plugin repo under the `open-leash/plugin-*` pattern.

---

## First-Party Plugins

| Plugin | Event | What it does |
|---|---|---|
| [`plugin-token-saver`](https://github.com/open-leash/plugin-token-saver) | `prompt.beforeSubmit` | Reduces prompt size before downstream checks. |
| [`plugin-data-leakage-prevention`](https://github.com/open-leash/plugin-data-leakage-prevention) | `prompt.beforeSubmit` | Masks or blocks sensitive data in prompts. |
| [`plugin-sensitive-access`](https://github.com/open-leash/plugin-sensitive-access) | prompts, tools, responses | Detects secret-file reads, env dumps, and exfiltration attempts. |
| [`plugin-blast-radius`](https://github.com/open-leash/plugin-blast-radius) | `tool.beforeUse` | Guards destructive tool and data operations. |
| [`plugin-rules-enforcer`](https://github.com/open-leash/plugin-rules-enforcer) | prompts, tools, responses | Evaluates user and agent rules. |
| [`plugin-mcp-scanner`](https://github.com/open-leash/plugin-mcp-scanner) | `tool.beforeUse`, `tool.afterUse` | Inventories MCP tool usage for audit and review. |
| [`plugin-skill-scanner`](https://github.com/open-leash/plugin-skill-scanner) | startup, agent detected, skill changed | Reviews agent skills and records findings. |

---

## Who It Is For

### Developers using coding agents

Use OpenLeash to understand and shape what agents do across prompts, tools, shell commands, files, MCP servers, and code workflows.

### Teams adopting agents at work

Use OpenLeash to configure plugins, route approvals, track usage, review audit history, and roll out agent controls through OpenLeash Cloud or Private Cloud.

### Security and platform teams

Use OpenLeash to make agent behavior visible and enforceable without banning the tools people actually want to use.

### Plugin builders

Build focused pipeline features: cost reducers, prompt transforms, approval workflows, MCP inventory plugins, policy packs, session analyzers, data classifiers, and more.

---

## Product Shape

OpenLeash has two backend-backed deployment paths:

- **OpenLeash Cloud**: hosted by OpenLeash for individuals and organizations.
- **Private Cloud**: customer-hosted open-source core for organizations that need their own API, dashboard, database, identity, logs, and operational controls.

The desktop client still receives local hooks first at `127.0.0.1`, but account state, plugin settings, policy, approvals, audit, and evaluation come from the configured backend.

---

## What We Believe

Agents should be useful, fast, and connected.

Humans should still understand what happened.

Teams should be able to adopt agents without turning every workflow into blind trust or blanket denial.

OpenLeash is the middle layer: observable, configurable, extensible, and open.

---

<div align="center">

### Start Here

<a href="https://openleash.com"><img src="https://img.shields.io/badge/Visit-openleash.com-0EA5E9?style=for-the-badge&logo=googlechrome&logoColor=white" /></a>
<a href="https://docs.openleash.com"><img src="https://img.shields.io/badge/Read-docs.openleash.com-7C3AED?style=for-the-badge&logo=readthedocs&logoColor=white" /></a>
<a href="https://github.com/open-leash?q=plugin-"><img src="https://img.shields.io/badge/Build-plugins-EC4899?style=for-the-badge&logo=typescript&logoColor=white" /></a>

<br/>
<br/>

<strong>Support OpenLeash</strong>

<br/>
<br/>

<a href="https://github.com/orgs/open-leash/repositories"><img src="https://img.shields.io/badge/Star-the%20repos%20you%20use-F59E0B?style=for-the-badge&logo=github&logoColor=white" /></a>
<a href="https://github.com/open-leash"><img src="https://img.shields.io/badge/Follow-OpenLeash-181717?style=for-the-badge&logo=github&logoColor=white" /></a>

<br/>
<br/>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0EA5E9,50:7C3AED,100:EC4899&height=120&section=footer" width="100%" />

</div>
