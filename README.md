<div align="center">

<p align="center">
  <img src="https://github-readme-stats-fast.vercel.app/api?username=amir0ff&show_icons=true&theme=dark&hide_border=true" alt="GitHub Stats" />
</p>

<p align="center">
  <img src="https://github-readme-stats-fast.vercel.app/api/streak/?username=amir0ff&theme=dark&hide_border=true" alt="GitHub Streak" />
</p>

</div>

```mermaid
---
title: Agent Harness Architecture
---
graph TD
    User("User Prompt") --> RAG

    subgraph Harness["Agent Harness"]
        RAG("Context Retrieval<br/>Search · Grep · RAG") --> CW

        subgraph Loop["Agent ReAct Loop"]
            CW("Context Window")
            LLM("LLM / Model")
            TE("Tool Execution")

            CW -->|"1 · Context + History"| LLM
            LLM -->|"2a · Tool Call"| TE
            TE -->|"3 · Observation"| CW
        end

        TE --> WorkSpace[("Workspace / File System")]
    end

    %% Lengthened arrow keeps final output visually separated
    LLM ---->|"2b · Final Response"| FinalAnswer("Final Output to User")
    WorkSpace ~~~ FinalAnswer

    %% Node styles
    classDef input fill:#2563eb,stroke:#3b82f6,color:#ffffff,stroke-width:1.5px
    classDef context fill:#0369a1,stroke:#0ea5e9,color:#ffffff,stroke-width:1.5px
    classDef model fill:#6d28d9,stroke:#8b5cf6,color:#ffffff,stroke-width:1.5px
    classDef tool fill:#b45309,stroke:#f59e0b,color:#ffffff,stroke-width:1.5px
    classDef retrieval fill:#1e293b,stroke:#475569,color:#e2e8f0,stroke-width:1px
    classDef storage fill:#111827,stroke:#475569,color:#cbd5e1,stroke-width:1px
    classDef output fill:#15803d,stroke:#22c55e,color:#ffffff,stroke-width:1.5px

    %% Apply node styles
    class User input
    class RAG retrieval
    class CW context
    class LLM model
    class TE tool
    class WorkSpace storage
    class FinalAnswer output

    %% Container styles
    style Harness fill:#0f172a10,stroke:#64748b,stroke-width:1.5px,stroke-dasharray:5 5
    style Loop fill:#0f172a08,stroke:#94a3b8,stroke-width:1px
```
