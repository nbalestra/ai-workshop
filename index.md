---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: Introduction
nav_enabled: true
nav_order: 1
---

**Welcome to the MuleSoft AI Workshop: Building Actionable, Data-Grounded Intelligent Agents**

Today, we'll explore how MuleSoft empowers you to rapidly build powerful AI agents that are not just intelligent, but also deeply integrated into your business operations. We aim to move beyond generic AI, creating agents that are:

* **Grounded in Your Business Data:** Leveraging your company's unique knowledge and information.
* **Capable of "Action":** Interacting with your existing enterprise systems to perform tasks and trigger processes.

MuleSoft acts as the critical integration backbone, connecting AI capabilities to your real-world data and systems. We will focus on two key architectural patterns:

**1. Tooling (Function Calling): Enabling AI to Act within Your Enterprise**

* **What it is:** This approach allows a Large Language Model (LLM) to intelligently decide when to use external "tools" to fulfill a user's request. These "tools" are essentially APIs that connect to your existing systems.
* **How it works:**
    1.  A user makes a request in natural language (e.g., "What's my order status?").
    2.  The LLM identifies the need for an external system and selects the appropriate pre-defined "tool" (e.g., an `getOrderStatus` function).
    3.  This "tool" then invokes a **MuleSoft API**, which securely connects to your backend systems (like an order database or CRM).
    4.  MuleSoft retrieves the necessary data, which the LLM then uses to formulate a helpful, actionable response.
* **MuleSoft's Role:** You'll leverage an existing **MuleSoft API** to allow the AI agent to query for customer orders using natural language. This demonstrates how MuleSoft makes your current API investments AI-ready, enabling AI to take concrete actions based on real-time enterprise data.

**2. Retrieval Augmented Generation (RAG): Grounding AI with Your Specific Knowledge**

* **What it is:** RAG enhances LLM responses by providing them with relevant, specific information from your private data sources – information the LLM wasn't originally trained on.
* **How it works:**
    1.  Your enterprise documents (e.g., PDFs, knowledge bases) are processed and stored in a searchable format (often a vector database) that captures their meaning. **MuleSoft can automate this data ingestion pipeline.**
    2.  When a user asks a question (e.g., "What is our internal policy on X?"), the RAG system first retrieves the most relevant snippets from your document store.
    3.  This retrieved context is then combined with the user's original query and sent to the LLM. **MuleSoft can orchestrate this entire flow:** receiving the query, fetching context, and calling the LLM.
    4.  The LLM generates an answer that is "grounded" in your specific information, making it more accurate and relevant.
* **MuleSoft's Role:** We will use the content of a PDF to ground user prompts. **MuleSoft facilitates the process** of making this private knowledge available to the LLM, effectively "enriching" its understanding so it can answer questions based on information exclusive to your organization. This significantly reduces the chance of the LLM providing generic or incorrect answers.

By the end of this workshop, you'll understand how MuleSoft's API-led connectivity and integration capabilities are essential for building practical, effective, and enterprise-grade AI solutions.

Let's get started!
