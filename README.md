```mermaid
graph TD

    %% USER LAYER
    subgraph User_Layer [User Layer]
        A[Developer UI (Web / Gradio Interface)]
    end

    %% AGENTIC AI LAYER
    subgraph Agentic_AI_Layer [Agentic AI Layer]
        B1[UI Agent\nUser access, authentication, request handling]
        B2[Scheduler Agent\nPredictive scheduling, idle detection]
        B3[Health Agent\nService validation pre/post operations]
        B4[Cost Agent\nUsage tracking, cost forecasting]
        B5[Policy Agent\nAccess control, exception handling]
        B6[Orchestrator Agent\nMain coordinator, workflow engine]
    end

    %% INTEGRATION LAYER
    subgraph Integration_Layer [Integration Layer]
        C1[Oracle Cloud API\nInstance start/stop/status]
        C2[Jenkins Pipeline (Legacy Control)\nFallback automation layer]
        C3[Monitoring + Logging\nGrafana / ELK / CloudWatch]
    end

    %% DATA LAYER
    subgraph Data_Layer [Data Layer]
        D1[Telemetry DB\nMetrics, activity logs, health data]
        D2[Knowledge Store\nPolicy memory, agent reasoning traces]
    end

    %% PRIMARY DATA FLOWS
    A -->|User action| B1
    B1 -->|Request| B6
    B6 -->|Schedules & signals| B2
    B6 -->|Health validation| B3
    B6 -->|Cost optimization| B4
    B6 -->|Policy enforcement| B5
    B6 -->|Execution commands| C1
    B6 -->|Fallback| C2

    %% MONITORING & FEEDBACK
    B3 -->|Metrics| C3
    C3 -->|Alerts| B6
    B4 -->|Utilization reports| D1
    B2 -->|Predictions| D1
    B5 -->|Governance logs| D2
    C1 -->|VM telemetry| D1

    %% FEEDBACK LOOPS
    D1 -->|Insights| B4
    D1 -->|Usage trends| B2
    D2 -->|Policies| B5
    B5 -->|Approval signals| B6

    %% LATENCY ANNOTATIONS
    classDef fastFlow fill:#a9dfbf,stroke:#27ae60,stroke-width:2px,color:#000;
    classDef slowFlow fill:#f5b7b1,stroke:#c0392b,stroke-width:2px,color:#000;

    A-->B1:::fastFlow
    B1-->B6:::fastFlow
    B6-->C1:::fastFlow
    B3-->C3:::fastFlow
    D1-->B4:::slowFlow
    D1-->B2:::slowFlow
    D2-->B5:::slowFlow
```
