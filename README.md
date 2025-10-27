# CodeAid : An Agentic AI for Repository-Wide Code Understanding, Error Detection, and Repair

## Overview
CodeAid is an intelligent multi-agent system designed to autonomously scan, analyze, and improve entire code repositories.  
It detects bugs, suggests optimal fixes, verifies them in sandboxed environments, and explains the reasoning behind each correction — acting as a **“Grammarly for code.”**

## Objectives
- Enable **full-repository understanding** rather than snippet-based code assistance.  
- Automate **bug detection, repair, and validation** using AI agents.  
- Provide **human-readable explanations** for detected issues and fixes.  
- Continuously learn and improve from developer feedback and benchmark datasets.

## System Architecture

```mermaid
flowchart TD
    %% MAIN ENTRY
    A[🗂 Repository Loader] --> B[📘 Code Parser & AST Builder]
    B --> C[🔍 Scanner Agent]
    
    %% VECTOR STORE INTEGRATION
    B --> D[(🧬 Vector Store - FAISS/Chroma)]
    D <---> G[(📚 CodeXGLUE Datasets)]
    G --> C

    %% SCANNER FLOW
    C -->|Detects Bug| E[🧩 Repair Agent]
    E -->|Retrieves similar fixes| D
    E --> F[🧪 Verifier Agent]
    F_text(Generates Fix: CodeT5) --> F

    %% VERIFICATION
    F -->|Runs Sandbox Tests| H[✅ Verified Fix / ❌ Failed Fix]
    F --> I[💬 Explainability Agent]
    
    %% EXPLANATION FLOW
    I -->|Summarizes Bug & Fix| J[📊 Developer Dashboard]

    %% DASHBOARD INTERACTION
    J -->|Feedback / Approve| E

    %% CONNECTIONS
    G -. Provides training & benchmarks .-> C
    G -. Provides repair examples .-> E
    G -. Provides summarization data .-> I

    %% STYLES
    style A fill:#b3d9ff,stroke:#003366,stroke-width:1px
    style B fill:#c2e0ff,stroke:#003366,stroke-width:1px
    style C fill:#fff2cc,stroke:#ff9900,stroke-width:1px
    style E fill:#ffe6cc,stroke:#cc6600,stroke-width:1px
    style F fill:#d5e8d4,stroke:#008000,stroke-width:1px
    style I fill:#f4cccc,stroke:#cc0000,stroke-width:1px
    style J fill:#e1d5e7,stroke:#660099,stroke-width:1px
    style D fill:#f0f0f0,stroke:#666666,stroke-width:1px,stroke-dasharray: 5 5
    style G fill:#f0f0f0,stroke:#666666,stroke-width:1px,stroke-dasharray: 5 5

****
