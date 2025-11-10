graph TD

    subgraph User Layer
        A["Developer UI<br/>(Web / Gradio Interface)"]
    end

    subgraph Agentic AI Layer
        B1["UI Agent<br/>User access, authentication, request handling"]
        B2["Scheduler Agent<br/>Predictive scheduling, idle detection"]
        B3["Health Agent<br/>Service validation pre/post operations"]
        B4["Cost Agent<br/>Usage tracking, cost forecasting"]
        B5["Policy Agent<br/>Access control, exception handling"]
        B6["Orchestrator Agent<br/>Main coordinator, workflow engine"]
    end

    subgraph Integration Layer
        C1["Oracle Cloud API<br/>Instance start/stop/status"]
        C2["Jenkins Pipeline<br/>(Legacy Control)"]
        C3["Monitoring + Logging<br/>Grafana / ELK / CloudWatch"]
    end

    subgraph Data Layer
        D1["Telemetry DB<br/>Metrics, activity logs, health data"]
        D2["Knowledge Store<br/>Policy memory, agent reasoning traces"]
    end

    %% Primary data flows
    A -->|User action| B1
    B1 -->|Request| B6
    B6 -->|Schedules & signals| B2
    B6 -->|Health validation| B3
    B6 -->|Cost optimization| B4
    B6 -->|Policy enforcement| B5
    B6 -->|Execution commands| C1
    B6 -->|Fallback| C2

    %% Monitoring & feedback
    B3 -->|Metrics| C3
    C3 -->|Alerts| B6
    B4 -->|Utilization reports| D1
    B2 -->|Predictions| D1
    B5 -->|Governance logs| D2
    C1 -->|VM telemetry| D1

    %% Feedback loops
    D1 -->|Insights| B4
    D1 -->|Usage trends| B2
    D2 -->|Policies| B5
    B5 -->|Approval signals| B6

    %% Latency annotations
    classDef fastFlow fill:#a9dfbf,stroke:#27ae60,stroke-width:2px,color:#000;
    classDef slowFlow fill:#f5b7b1,stroke:#c0392b,stroke-width:2px,color:#000;

    A --> B1:::fastFlow
    B1 --> B6:::fastFlow
    B6 --> C1:::fastFlow
    B3 --> C3:::fastFlow
    D1 --> B4:::slowFlow
    D1 --> B2:::slowFlow
    D2 --> B5:::slowFlow

    %% Styling
    style A fill:#fef9e7,stroke:#f5b041,stroke-width:2px
    style B1 fill:#ebf5fb,stroke:#5dade2,stroke-width:2px
    style B2 fill:#ebf5fb,stroke:#5dade2,stroke-width:2px
    style B3 fill:#ebf5fb,stroke:#5dade2,stroke-width:2px
    style B4 fill:#ebf5fb,stroke:#5dade2,stroke-width:2px
    style B5 fill:#ebf5fb,stroke:#5dade2,stroke-width:2px
    style B6 fill:#d6eaf8,stroke:#2874a6,stroke-width:2px
    style C1 fill:#e8f8f5,stroke:#1abc9c,stroke-width:2px
    style C2 fill:#e8f8f5,stroke:#1abc9c,stroke-width:2px
    style C3 fill:#e8f8f5,stroke:#1abc9c,stroke-width:2px
    style D1 fill:#fdebd0,stroke:#f39c12,stroke-width:2px
    style D2 fill:#fdebd0,stroke:#f39c12,stroke-width:2px
