# 04. Export File Process (Progress)

```mermaid
sequenceDiagram
    participant P as Premium Process

    P->>P: Load Data
    P->>P: Export File
    alt Error
        P->>P: Write Error File
    end
```
