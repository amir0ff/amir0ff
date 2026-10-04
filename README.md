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

    %% Theme: Carbon Glow
    %% Dark charcoal surfaces with restrained semantic neon accents.
    %% Designed to visually match dark GitHub stats/streak/language cards.

    %% Node styles
    %% Green = entry / successful completion
    classDef input fill:#1c1c1c,stroke:#39d353,color:#f0f0f0,stroke-width:1.5px
    classDef output fill:#1c1c1c,stroke:#39d353,color:#f0f0f0,stroke-width:1.5px

    %% Blue = context / active information state
    classDef context fill:#1c1c1c,stroke:#58a6ff,color:#f0f0f0,stroke-width:1.5px

    %% Purple = model / intelligence
    classDef model fill:#1c1c1c,stroke:#a371f7,color:#f0f0f0,stroke-width:1.5px

    %% Amber = tool execution / action
    classDef tool fill:#1c1c1c,stroke:#f0a000,color:#f0f0f0,stroke-width:1.5px

    %% Gray = retrieval / infrastructure / persistence
    classDef retrieval fill:#1c1c1c,stroke:#8b949e,color:#c9c9c9,stroke-width:1px
    classDef storage fill:#1c1c1c,stroke:#8b949e,color:#c9c9c9,stroke-width:1px

    %% Apply node styles
    class User input
    class RAG retrieval
    class CW context
    class LLM model
    class TE tool
    class WorkSpace storage
    class FinalAnswer output

    %% Container styles
    %% Outer harness uses a brighter dashed boundary
    style Harness fill:#1c1c1c08,stroke:#8b949e,stroke-width:1.5px,stroke-dasharray:5 5

    %% Inner ReAct loop stays more subtle
    style Loop fill:#1c1c1c05,stroke:#555555,stroke-width:1px
```
<details>
<summary><strong>How it works</strong></summary>

The diagram illustrates a modern agent harness workflow in which a user prompt is first enriched through context retrieval using search, grep, or RAG. That context enters a ReAct loop, where the model evaluates the available context, decides whether to invoke tools, and receives the resulting observations back into its context window for further reasoning.

Tool execution can interact with a persistent workspace or file system, allowing the agent to read, modify, and operate on external state. This cycle can repeat as needed until the model has enough information to produce the final response to the user.

</details>
