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

%% Theme configuration
%% Uses Mermaid's dark foundation so titles and labels remain readable.
%% Edge labels use a medium charcoal rather than near-black.
%%{init: {
    "theme": "dark",
    "themeVariables": {
        "textColor": "#e6edf3",
        "titleColor": "#e6edf3",
        "lineColor": "#9ca3af",
        "edgeLabelBackground": "#242424"
    }
}}%%

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

    %% Theme: Carbon Glow v2.1
    %% Dark charcoal surfaces with restrained semantic neon accents.
    %% Subtle tinted fills add depth while preserving the README's dark card aesthetic.
    %% Brighter typography keeps labels readable against GitHub's dark background.

    %% Node styles
    %% Green = entry / successful completion
    classDef input fill:#142018,stroke:#39d353,color:#f0f0f0,stroke-width:1.5px
    classDef output fill:#142018,stroke:#39d353,color:#f0f0f0,stroke-width:1.5px

    %% Blue = context / active information state
    classDef context fill:#141c24,stroke:#58a6ff,color:#f0f0f0,stroke-width:1.5px

    %% Purple = model / intelligence
    classDef model fill:#1d1726,stroke:#a371f7,color:#f0f0f0,stroke-width:1.5px

    %% Amber = tool execution / action
    classDef tool fill:#211a0d,stroke:#f0a000,color:#f0f0f0,stroke-width:1.5px

    %% Gray = retrieval / infrastructure / persistence
    classDef retrieval fill:#1c1c1c,stroke:#8b949e,color:#e0e0e0,stroke-width:1px
    classDef storage fill:#181818,stroke:#8b949e,color:#e0e0e0,stroke-width:1px

    %% Apply node styles
    class User input
    class RAG retrieval
    class CW context
    class LLM model
    class TE tool
    class WorkSpace storage
    class FinalAnswer output

    %% Connector styles
    %% Brighter silver keeps arrows clearly visible without becoming dominant
    linkStyle default stroke:#9ca3af,stroke-width:1.15px

    %% Container styles
    %% Outer harness uses a brighter dashed architectural boundary
    style Harness fill:#1c1c1c08,stroke:#8b949e,stroke-width:1.25px,stroke-dasharray:5 5

    %% Inner ReAct loop is subtle but remains clearly visible
    style Loop fill:#1c1c1c05,stroke:#666666,stroke-width:1px
```

<details>
<summary><strong>How it works</strong></summary>
The diagram illustrates a modern agent harness workflow in which a user prompt is first enriched through context retrieval using search, grep, or RAG. That context enters a ReAct loop, where the model evaluates the available context, decides whether to invoke tools, and receives the resulting observations back into its context window for further reasoning.

Tool execution can interact with a persistent workspace or file system, allowing the agent to read, modify, and operate on external state. This cycle can repeat as needed until the model has enough information to produce the final response to the user.
</details>
