# 03. Premium SOAP Accept Process

```mermaid
sequenceDiagram
    participant API as .NET API
    participant SOAP as Premium SOAP

    API->>SOAP: Campaign Payload
    SOAP->>SOAP: Log + Generate Ref
    SOAP-->>API: Accepted
```
