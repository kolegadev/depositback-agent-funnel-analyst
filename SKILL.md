# Funnel Analyst

> **Agent**: `depositback-agent-funnel-analyst`  
> **Group**: Analytics  
> **Product**: DepositBack — Security Deposit Demand Letter Service

## Purpose

Monitors visitor→form start (>15%), form start→complete (>60%), form complete→payment (>40%), payment→completion. Uses PostHog session replay to identify abandonment points.

## DepositBack Context

DepositBack is a single-page, no-signup transactional product for US renters seeking to recover security deposits. The entire customer journey fits on one URL: landing page → 6-question form → Revolut payment → PDF emailed. Conversion rate target: **4% visitor-to-purchase minimum**.

## Inputs

- PostHog events
- Revolut webhooks from operations/purchase-orchestrator
- UTM data

## Outputs

- Funnel reports → landing-page-optimizer inbox
- Drop-off alerts → operations/escalation

## Human Escalation Points 🛑

- Conversion rate drops below 4%
- Payment failure rate >30%
- Form field sensitivity issues

## Skills

| Skill | Description | Status |
|-------|-------------|--------|
| `noop` | Health check / pipeline verification | ✅ Active |
| `execute` | Primary function for this agent | 🔧 Planned |

## Workflow

1. Poll `data/inbox/` for task manifests from upstream agents.
2. Resolve required skills (local `skills/` or ClawHub fallback).
3. Execute workflow.
4. Write artifacts to `data/outbox/`.
5. Update `data/state.json`.

## Runtime

```bash
pip install -r requirements.txt
python runtime/main.py
```
