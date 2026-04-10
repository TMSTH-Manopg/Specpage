# SmileyQuote ↔ Premium Integration (Step-by-Step)

## 1. Overall Sequence Diagram
```mermaid
sequenceDiagram
    participant SQ as SmileyQuote (.NET API)
    participant PA as Premium API (SOAP)
    participant PR as Premium Process (Progress)
    participant DB as Premium DB
    participant WH as SmileyQuote Webhook

    SQ->>PA: 1. Publish Campaign (SOAP)
    PA-->>SQ: 2. Response Accepted (ReferenceNo)
    PA->>PR: 3. Start Async Process
    PR->>PR: 4. Export File
    PR->>PR: 5. Validate Data
    PR->>DB: 6. Save Premium
    PR->>WH: 7. Callback Result (Webhook)
    WH-->>PR: 8. ACK
```

---

## 2. Process 1: Publish Campaign (.NET → Premium SOAP)

### Step-by-Step
1. Client เรียก `.NET API /api/publish/premium`
2. .NET Validate Request
3. .NET แปลงข้อมูลเป็น SOAP Payload
4. เรียก Premium SOAP Service
5. Premium Return ReferenceNo
6. .NET Save Status = SENT

### Mermaid
```mermaid
sequenceDiagram
    participant Client
    participant API as .NET API
    participant SOAP as Premium SOAP

    Client->>API: POST Publish Campaign
    API->>SOAP: SOAP Request
    SOAP-->>API: ReferenceNo
    API-->>Client: SENT
```

---

## 3. Process 2: Premium Receive & Accept

### Responsibility (Progress)
- Parse JSON / XML
- Generate ReferenceNo
- Save Incoming Log
- Return Accepted

### Mermaid
```mermaid
sequenceDiagram
    participant API as .NET API
    participant SOAP as Premium SOAP

    API->>SOAP: Campaign Data
    SOAP->>SOAP: Log + Generate Ref
    SOAP-->>API: Accepted
```

---

## 4. Process 3: Export File (Progress)

### Step-by-Step
1. Load Temp-Table
2. Map Data
3. Write File (CSV/XML)
4. If Error → Error File

### Mermaid
```mermaid
sequenceDiagram
    participant PR as Premium Process

    PR->>PR: Load Data
    PR->>PR: Export File
    PR->>PR: Handle Error (if any)
```

---

## 5. Process 4: Validate Process

### Validation Rules
- Mandatory Field
- Duplicate Check
- Business Rule

### Mermaid
```mermaid
sequenceDiagram
    participant PR as Premium Process

    PR->>PR: Validate Mandatory Field
    PR->>PR: Validate Business Rule
    PR->>PR: Set PASS / FAIL
```

---

## 6. Process 5: Save Premium Database

### Step-by-Step
1. Begin Transaction
2. Insert / Update Premium Table
3. Commit
4. On Error → Rollback

### Mermaid
```mermaid
sequenceDiagram
    participant PR as Premium Process
    participant DB as Premium DB

    PR->>DB: Insert Premium
    DB-->>PR: OK
```

---

## 7. Process 6: Callback Webhook (Progress → .NET)

### Step-by-Step
1. Prepare Result JSON
2. Add API Key Header
3. POST to Webhook
4. Wait ACK

### Mermaid
```mermaid
sequenceDiagram
    participant PR as Premium Process
    participant WH as .NET Webhook

    PR->>WH: POST Result
    WH->>WH: Update Status
    WH-->>PR: ACK
```

---

## 8. Status Mapping
| Step | Status |
|---|---|
| Publish | SENT |
| Processing | PROCESSING |
| Success | SUCCESS |
| Error | FAIL |

---

## 9. Key Design Notes
- SOAP = Accept & Return Quickly
- Process = Async Only
- Webhook = Idempotent (ReferenceNo)
- Logging ทุก Step

---

## End of Document
