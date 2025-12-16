# 🚧 System Limitations & Production Roadmap

This project is a functional **Proof of Concept (PoC)** designed to demonstrate the architecture of an Agentic RAG system. It is **not** yet intended for production deployment.

## Current Limitations (Prototype Status)

### 1. Memory & Context Management
* **Current State:** Uses **Simple Memory (Window Buffer)**.
    * *Behavior:* The agent retains the last 5 turns of conversation to provide context.
    * *Limitation:* This memory is volatile and stored in the active execution RAM. If the n8n instance restarts or the specific workflow execution concludes, the user's conversational history is lost.
* **Production Requirement:** Implementation of persistent conversational memory using **Redis** or **PostgreSQL** (Zep/LangChain Checkpointers) to allow users to resume conversations days later.

### 2. Security & Authentication
* **Current State:** The "Approver" workflow relies on obfuscated URL parameters in the email link.
* **Production Requirement:** A production version would require **OAuth2 / SSO (Single Sign-On)** verification to ensure only authorized personnel can approve tickets.

### 3. Data Persistence
* **Current State:** Uses **Google Sheets** as a mock database for ticket storage.
* **Production Requirement:** Integration with an enterprise ITSM tool like **ServiceNow**, **Jira Service Management**, or **Zendesk** via REST API.

### 4. Concurrency
* **Current State:** The n8n instance is self-hosted locally (Community Edition).
* **Production Requirement:** Deployment to a **Kubernetes** cluster with n8n worker nodes to handle concurrent user requests without blocking.