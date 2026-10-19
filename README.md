<div align="center">

# GALAXY CORE · AI-SPM

**AI Security Posture Management with a live galaxy-graph command console.**

Every prompt from a user or AI agent passes through a full security pipeline. Every decision, alert and enforcement action appears as a particle moving through the system in real time.

![Status](https://img.shields.io/badge/status-private%20beta-FF1A1A?style=flat-square&labelColor=0A0F24)
![Open source](https://img.shields.io/badge/open%20source-community%20vote-FF4D4D?style=flat-square&labelColor=0A0F24)
![MITRE ATLAS](https://img.shields.io/badge/MITRE-ATLAS-B30000?style=flat-square&labelColor=0A0F24)
![Backend](https://img.shields.io/badge/backend-zero%20dependencies-E2E8F0?style=flat-square&labelColor=0A0F24)

![Galaxy Core console](docs/images/01-galaxy-core.jpg)

▶️ **[Watch the 60-second launch video](media/galaxy-core-launch.mp4)**

</div>

> **This is the public showcase.** The source code is in a private beta. Whether Galaxy Core becomes open source is being decided by a community poll on LinkedIn. To join the beta, [open an issue](../../issues/new?title=Beta%20access%20request) or comment on the launch post.

---

## Why Galaxy Core

Organisations are deploying AI agents, models and MCP servers faster than security teams can see them. Galaxy Core answers four questions:

1. **What AI do we have?** It keeps an inventory of models, agents, MCP servers and data sources, including *shadow AI* that nobody registered.
2. **How exposed is it?** It scores the posture of every asset, detects configuration drift, and checks compliance against OWASP LLM Top 10, NIST AI RMF, the EU AI Act and ISO/IEC 42001.
3. **Is someone attacking it right now?** Every prompt is scored and decided in about a millisecond, and every attack is mapped to MITRE ATLAS techniques.
4. **Can we respond?** Alerts roll up into cases, a threat hunter sweeps the telemetry, and a freeze controller is a kill switch for any user, agent or tenant.

---

## Feature highlights

### 🌌 Live galaxy graph
A floating map of all 17 services, with **Galaxy Core** (the policy decider) at its centre. Each particle is a real event: cool gray when allowed, neon red when flagged, and alert red when blocked. Nodes heat up with load. Hover any service for live stats, or click it to see the events flowing through it.

![Analytics](docs/images/02-analytics.jpg)

### ⚡ Runtime playground with stage-by-stage trace
Send any prompt as any agent and watch it move through **gateway → prompt guard → CEP → risk fusion → policy → memory → tools → LLM → output guard**, with each stage's verdict, timing and evidence.

| Attack blocked at the policy stage | PII redacted from a tool result |
|---|---|
| ![Blocked](docs/images/03-runtime-blocked.jpg) | ![Redaction](docs/images/04-runtime-redaction.jpg) |

### 🛡️ Multi-layer detection
- **Three-pass signal extraction:** raw text, evasion-normalised text (zero-width characters and hyphen-split words removed), and decoded base64 payloads.
- **Eight signal families:** prompt injection, jailbreak, exfiltration, tool abuse, privilege escalation, indirect injection, social engineering and obfuscation.
- **Harm-category guard model** (malware, credential theft, violence, fraud) that returns an allow, flag or block verdict.
- **Complex event processing:** detects bursts, sustained volume and intent drift for each principal.
- **Risk fusion** into one posture score, mapped to **MITRE ATLAS** techniques (AML.T0051, T0054, T0048, T0029 and more).

### 📦 AI inventory and shadow-AI discovery
Models, agents, MCP servers and data sources are tracked with owner, scopes, tools, egress and live runtime risk. Every configuration change is recorded as **drift**, with before and after evidence.

![Inventory](docs/images/05-inventory.jpg)

### 📊 Posture and compliance
Each asset gets a health score explained by its risk drivers. Live control checks cover **OWASP LLM Top 10, NIST AI RMF, the EU AI Act and ISO/IEC 42001**.

![Posture](docs/images/06-posture.jpg)

### 📜 Policy engine with monitor mode
An ordered, versioned rule chain. Switch any rule between **Enforce** and **Monitor** (record what it would have decided without blocking), with hit counters and versions. Thresholds: allow below 0.30, hold for review from 0.30 to 0.70, block at 0.70 and above.

![Policies](docs/images/07-policies.jpg)

### 🚨 Threats: alerts → cases → auto-freeze
Alerts come from policy, CEP, the output guard, drift and threat hunting, and roll up into **cases per principal** with a timeline, assignee, notes and one-click freeze. Repeat attackers are automatically frozen at the gateway with **HTTP 423**.

| Alert triage | Case investigation |
|---|---|
| ![Threats](docs/images/08-threats.jpg) | ![Case](docs/images/09-case.jpg) |

### 🔎 Threat hunting
Nine collectors sweep telemetry and posture on a schedule or on demand: posture, shadow AI, anomaly, data leakage, tool misuse, injection campaigns, privilege escalation, CEP and compliance gaps.

![Hunting](docs/images/10-hunting.jpg)

### 🧪 Red-team simulation
Seven probe suites (21 attacks) run through the real pipeline in dry-run mode, reporting the attack block rate and false-positive rate. In the demo estate: **100% blocked, 0% false positives**.

![Simulation](docs/images/11-simulation.jpg)

### 🧬 Session lineage
Follow any session request by request through every service it touched.

![Lineage](docs/images/12-lineage.jpg)

### ❄️ Enforcement
Freeze a user, agent or whole tenant for a set time or until lifted.

![Enforcement](docs/images/13-enforcement.jpg)

### 📱 Desktop to phone
The dark-mode console adapts down to 375px screens, and the graph reflows into a portrait layout.

<p align="center"><img src="docs/images/14-mobile.jpg" width="300" alt="Mobile view"></p>

---

## How a request flows

```
 User / Agent ──▶ API Gateway ──▶ Prompt Guard ──▶ CEP Engine ──▶ Risk Fusion
                  freeze · rate     3-pass signals    burst · volume   score 0…1
                  limit · identity  harm categories   intent drift     + ATLAS TTPs
                                                                          │
                       ┌──────────────── block / review ◀── GALAXY CORE ◀─┘
                       ▼                                    (policy chain)
          Orchestrator → alerts → cases → auto-freeze            │ allow
                                                                 ▼
                      Memory → LLM ⇄ Tool sandbox → Output Guard → Response

   Every stage publishes to the event bus → live graph · threat hunter · lineage · metrics
```

---

## Under the hood

| | |
|---|---|
| **Backend** | Node.js, zero runtime dependencies, modular services on a tenant-scoped event bus |
| **Console** | React + Vite, canvas graph driven by Server-Sent Events |
| **Integrations** | REST API · SSE event stream · Prometheus `/metrics` · optional Claude LLM backend |
| **Run it** | Requires Node 20+ and one command. No database, Docker, Kafka or Java |
| **Quality** | 14 end-to-end acceptance tests on the real pipeline |

---

## Get involved

- 🗳️ **Vote in the LinkedIn poll** on whether Galaxy Core should be open source.
- 🔑 **Request beta access:** [open an issue](../../issues/new?title=Beta%20access%20request) in this repo.
- ⭐ **Star this repo** to get notified when the source is released.

---

<sub>Architecture inspired by [dshapi/AI (Apache-2.0) and independently implemented. MITRE ATLAS™ is a trademark of The MITRE Corporation.</sub>
