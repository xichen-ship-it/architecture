# System Architecture

Below is our 3-tier architecture (active/active servers, SQL cluster):

```mermaid
flowchart TD
    User[End User] --> WebUI[Web UI: HTML/CSS/JS/C#]
    WebUI --> Services[C# Services on IIS]
    Services --> DBPrimary[Primary SQL Server DB]
    Services --> DBSecondary[Secondary SQL Server DB]
    Services --> DBReporting[Reporting SQL Server DB]

    subgraph WindowsServer1[Windows Server 1]
        WebUI
        Services
    end

    subgraph WindowsServer2[Windows Server 2]
        WebUI2[Web UI: HTML/CSS/JS/C#]
        Services2[C# Services on IIS]
    end
    User --> WebUI2
    WebUI2 --> Services2
    Services2 --> DBPrimary
    Services2 --> DBSecondary
    Services2 --> DBReporting
