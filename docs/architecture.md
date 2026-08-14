# LUNE Architecture

## Overview

LUNE is a modular AI-supported pipeline for customer discovery and lead qualification.

The architecture is distributed: each component performs a specific responsibility and communicates with the other components through structured webhooks and JSON data. There is no single central orchestrator.

The proof of concept is composed of three AI agents implemented through five independent automation workflows.

## Pipeline

The execution flow is:

Lead
↓
Agent 01 — Qualification & Diagnosis
↓
Make
↓
Agent 02 — Proposal
↓
Pipedream
↓
Agent 03 — Presentation & Closing
↓
ActivePieces
↓
Gmail

The proposal stage uses two automation workflows: Make and Pipedream.

The presentation and closing stage uses Pipedream and ActivePieces.

## Agents

### Agent 01 — Qualification & Diagnosis

**Purpose:** conduct customer discovery, qualify the lead, and produce a structured diagnosis.

**Platform:** Make

**Main output:** qualified lead information and structured diagnostic data.

The agent sends structured JSON data to the Make workflow through a webhook. Make checks whether the lead already exists, stores the lead information, and routes the qualified information to the next stage.

### Agent 02 — Proposal

**Purpose:** transform the lead diagnosis into a visual proposal.

**Platforms:** Make + Pipedream

The Make workflow retrieves and prepares the qualified lead information and sends the structured data to the proposal stage.

Pipedream processes the proposal-related information and integrates external services used for visual asset management.

The resulting proposal information and image URL are made available to the next stage of the pipeline.

### Agent 03 — Presentation & Closing

**Purpose:** present the personalized proposal, capture the lead's decision, and route the relationship to closing or follow-up.

**Platforms:** Pipedream + ActivePieces

Pipedream prepares and provides the proposal information required for presentation.

ActivePieces processes the lead's decision and routes the interaction according to the result, including closing or nurturing/follow-up.

## Workflow Architecture

The three agents are implemented through five independent workflows:

| Agent | Responsibility | Platform |
|---|---|---|
| Agent 01 | Qualification and diagnosis | Make |
| Agent 02 | Proposal | Make |
| Agent 02 | Proposal processing and visual integration | Pipedream |
| Agent 03 | Presentation and proposal data | Pipedream |
| Agent 03 | Closing and follow-up | ActivePieces |

## Communication

Communication between components is performed through webhooks using structured JSON payloads.

This approach allows each workflow to operate independently while exchanging only the information required by the next component.

## Data and External Services

The pipeline uses external services for persistence, document storage, visual asset management, and communication:

- **Google Sheets** — lead information and pipeline state.
- **Google Drive** — proposal and document storage.
- **Cloudinary** — visual asset storage and management.
- **Gmail** — communication with leads and internal recipients.

## Architectural Characteristics

- Modular architecture
- Distributed workflow execution
- No central orchestrator
- Five independent workflows
- Webhook-based communication
- Structured JSON data
- Low coupling between components
- Replaceable automation components
- Human-in-the-loop decision support

## Design Principle

The architecture separates the responsibilities of the AI agents from the automation infrastructure used to connect and execute them.

The agents provide the intelligence and interaction logic, while the iPaaS workflows provide integration, data movement, persistence, and communication between the components.

This separation allows individual components to be modified or replaced without requiring the entire pipeline to be redesigned.
