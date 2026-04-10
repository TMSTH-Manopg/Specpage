# 06. Save Premium Database

```mermaid
sequenceDiagram
    participant P as Premium Process
    participant DB as Premium DB

    P->>DB: Insert / Update
    DB-->>P: Commit
```
