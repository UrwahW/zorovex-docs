# ADR-009: AI Platform Architecture

**Status:** Accepted

**Date:** 2026-06-28

**Owner:** Platform Architecture

---

# Context

During Sprint 1, Zorovex introduced AI-powered functionality beginning with an AI Receptionist.

Initially, AI was planned as a Business module.

As the product vision evolved, it became clear that AI would eventually support multiple specialized capabilities including:

- AI Receptionist
- AI Voice Agent
- AI Sales Agent
- AI Marketing Assistant
- AI Customer Support
- AI Internal Assistant

Treating AI as a Business feature would tightly couple unrelated functionality and limit future growth.

---

# Decision

AI becomes its own platform.

A new top-level module named **AI Studio** is introduced.

Business Setup remains responsible only for preparing the business.

AI Studio becomes responsible for configuring every AI capability.

---

# Architecture

The platform is divided into two responsibilities.

## Business

Business configuration.

Examples

Business Profile

Business Hours

Services

Staff

Business Brain

Communication Channels

---

## AI Studio

AI configuration.

Examples

Agents

Behaviour

Goals

Knowledge Sources

Escalation Rules

Playground

Monitoring

Future Memory

---

# Runtime

Execution is handled by the AI Runtime.

AI Studio never executes conversations.

It only stores configuration.

---

# AI Agents

Every AI capability must be implemented as an AI Agent.

Examples

Receptionist

Voice

Sales

Marketing

Support

Internal

Future Custom Agents

No AI capability may bypass the AI Agent architecture.

---

# Prompt Philosophy

Business owners never write prompts.

Instead they configure business behaviour.

The platform generates prompts automatically.

Prompt generation is considered an internal implementation detail.

---

# Provider Independence

Business logic must remain independent from AI providers.

Supported providers may include:

OpenAI

Anthropic

Google Gemini

Azure OpenAI

OpenRouter

Local Models

Switching providers must not require application redesign.

---

# Tool Calling

AI Agents never access business data directly.

Every action must be performed through approved tools.

Business logic remains inside the CRM.

---

# Knowledge

AI retrieves business information from approved knowledge sources.

Examples

Business Brain

Services

Staff

Business Hours

Policies

Promotions

Future Customer Context

Knowledge retrieval remains independent from prompt generation.

---

# Security

AI Agents never receive:

Database Access

Provider Credentials

Infrastructure Secrets

Internal Configuration

Every capability must follow the platform permission system.

---

# Future Expansion

The architecture must support:

Multiple AI Agents

Conversation Memory

Voice Calling

Workflow Automation

Recommendation Engine

Analytics

Campaign Generation

External Integrations

Future AI Employees

without architectural redesign.

---

# Consequences

Positive

- Modular architecture
- Provider independence
- Easier testing
- Easier scaling
- Better security
- Reusable AI infrastructure

Trade-offs

- More initial architecture work
- More platform components
- Longer implementation time

These trade-offs are accepted.

---

# Alternatives Considered

## Option 1

Embed AI inside Business Setup.

Rejected.

Reason

AI is larger than onboarding.

---

## Option 2

Create separate AI systems for every capability.

Rejected.

Reason

Creates duplicated infrastructure.

---

## Option 3

Introduce AI Studio as a dedicated platform.

Accepted.

Reason

Provides a scalable foundation for every future AI capability.

---

# Related Documents

01_Product/AI_STUDIO.md

03_Backend/AI_RUNTIME.md

03_Backend/AGENT_ARCHITECTURE.md

03_Backend/TOOL_CALLING.md

---

# Decision Summary

Zorovex AI is a platform.

Business modules configure the business.

AI Studio configures AI.

The AI Runtime executes conversations.

AI Agents perform specialized tasks.

Tool Calling provides secure access to business functionality.

This architecture becomes the foundation for all future AI development.