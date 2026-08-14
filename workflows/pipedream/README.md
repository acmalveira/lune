# Pipedream Workflows

This directory contains the two Pipedream workflows used in the LUNE pipeline.

## Workflows

### 1. Agente Auxiliar de Apresentação

Pipedream workflow responsible for the auxiliary presentation stage of the LUNE pipeline.

[Open shared workflow](https://pipedream.com/new?h=tch_jPf0Ll)

### 2. infos-do-lead-apresentação

Pipedream workflow used to provide lead information to the presentation stage.

[Open shared workflow](https://pipedream.com/new?h=tch_7Jfyne)

## Role in the LUNE architecture

Pipedream operates as an integration and processing layer between independent components of LUNE.

The workflows communicate with other components through webhooks and structured data, supporting the presentation stage of the pipeline.

LUNE uses Pipedream together with Make and ActivePieces as independent automation platforms.

## Security

The shared workflow links above are provided for reference to the configured workflows.

Production credentials, API keys, access tokens, webhook secrets, private data, and other sensitive configuration must not be committed to this repository.

Production secrets remain managed within the Pipedream environment.

## Status

**Functional proof of concept / research-derived software.**
