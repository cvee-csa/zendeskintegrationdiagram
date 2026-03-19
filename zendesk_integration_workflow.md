# Zendesk Integration Workflow Diagram

This diagram illustrates how the `zendeskopenticketreport` and `zendeskmcp` workflows operate and interact with Zendesk data and other services.

---

```mermaid
flowchart TD
    subgraph OpenTicketReport[zendeskopenticketreport Workflow]
        A1[Start: GitHub Actions Trigger or Manual Run]
        A2[Set up Python Environment]
        A3[Install Dependencies]
        A4[Run Report Script]
        A5[Fetch Open Tickets from Zendesk API]
        A6[Apply Heuristics & Analyze Tickets]
        A7[Generate Excel Report]
        A8[Upload Report as Artifact or to Google Drive]
        A9[End]
        A1 --> A2 --> A3 --> A4 --> A5 --> A6 --> A7 --> A8 --> A9
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
- `zendeskopenticketreport` is focused on automated reporting and ticket analysis, triggered by GitHub Actions or manually.
- `zendeskmcp` runs as a server, providing API endpoints for ticket management, analysis, and integration with tools like Claude.

