# Zendesk Integration Workflow Diagram

This diagram illustrates how the `zendeskopenticketreport` and `zendeskmcp` workflows operate and interact with Zendesk data and other services.

---

```mermaid
flowchart TD
    subgraph OpenTicketReport[zendeskopenticketreport Workflows]
        A0[Trigger: external cron dispatch or manual workflow_dispatch]
        A1[Check out repository]
        A2[Set up Python 3.11]
        A3[Install dependencies]
        A4[Run ESC/RARC report script]
        A5[Fetch open tickets from Zendesk API]
        A6[Analyze tickets and build report]
        A7[Generate Excel report]
        A8[Upload artifact or optional Google Drive upload]
        A9[End]
        A0 --> A1 --> A2 --> A3 --> A4 --> A5 --> A6 --> A7 --> A8 --> A9
    end

    subgraph MCPServer[zendeskmcp Workflow]
        B1[Start: MCP Server Launched]
        B2[Receive API Request from Claude or User]
        B3[Authenticate & Connect to Zendesk]
        B4[Fetch/Manage Tickets, Comments, Knowledge Base]
        B5[Process Request: Analysis, Draft, or Data]
        B6[Return Response to Client]
        B7[End]
        B1 --> B2 --> B3 --> B4 --> B5 --> B6 --> B7
    end

    %% Optional: Show Zendesk as a shared resource
    Zendesk[(Zendesk API)]
    A5 -- API Calls --> Zendesk
    B3 -- API Calls --> Zendesk
```

---

**Legend:**
- Both workflows interact with Zendesk via API calls.
- `zendeskopenticketreport` uses a GitHub Actions workflow: `zendeskreport_esc-rarc.yml`, which is triggered via `workflow_dispatch` and may be externally dispatched on a schedule.
- `zendeskmcp` runs as a server, providing API endpoints for ticket management, analysis, and integration with tools like Claude.

