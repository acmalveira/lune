# LUNE 🌙

**AI-supported customer discovery and lead qualification pipeline.**

> **Protect your time.**

LUNE is an intelligent pipeline designed to help service businesses discover, qualify, and advance the opportunities that have the strongest potential for a successful relationship.

## What is LUNE?

LUNE supports the early stages of the relationship between a business and a potential client.

Instead of investing time in opportunities that may not fit the business, LUNE uses Customer Discovery, ICP-based Lead Scoring, Generative AI, and workflow automation to identify compatibility earlier and help the right opportunities move forward.

The goal is simple:

**protect the time of both sides of the relationship.**

## How it works

LUNE combines three main AI-supported agents:

1. **Qualification and Diagnosis Agent**  
   Conducts the initial interaction, gathers information about the potential client, identifies needs and context, and evaluates the opportunity.

2. **Auxiliary Proposal Agent**  
   Uses the information collected during discovery to support the creation of a structured visual proposal.

3. **Presentation and Closing Agent**  
   Presents the proposal, records the client's decision, and supports closing or follow-up.

The agents are connected through independent automation workflows and communicate using structured data and webhooks.

## Technology

The proof of concept integrates:

- Generative AI
- Customer Discovery
- ICP-based Lead Scoring
- iPaaS automation
- Webhooks
- Structured JSON
- Google Sheets
- Google Drive
- Gmail
- Cloudinary

The automation layer uses independent workflows implemented with Make, Pipedream, and Activepieces.

## Architecture

LUNE follows a modular architecture in which the components can be replaced or extended without requiring a single central orchestration layer.

The current proof of concept consists of five independent webhook-based workflows connecting the AI agents, automation platforms, data storage, communication, and proposal generation.

## Research origin

LUNE originated as the technological artifact developed and evaluated in a master's research project based on **Design Science Research (DSR)**.

The research combines Customer Discovery, Lead Scoring, Customer Success, Generative AI, and iPaaS-based automation to investigate how AI-supported pipelines can improve the qualification of opportunities in service businesses.

## Status

**Functional proof of concept / research-derived software.**

The repository is maintained separately from the open-science research repository associated with the project.

## Intellectual property

This repository is associated with software developed in the context of research at the **Federal University of Itajubá (UNIFEI)**.

Intellectual-property ownership, authorship, licensing, and distribution terms are being handled separately through the appropriate institutional processes.

**No open-source license is granted at this stage.**

## Security

Do not commit:

- API keys
- passwords
- access tokens
- webhook secrets
- personal data
- production credentials
- private configuration files

Production secrets must be stored using the appropriate environment or platform-specific secret management mechanisms.

---

🌙 **LUNE**

*Protect your time.*
