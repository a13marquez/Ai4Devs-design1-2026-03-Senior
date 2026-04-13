# LTI-AMJ: Learning Tools Interoperability Platform v1

**Version:** 1.0  
**Date:** 2026-04-13  
**Status:** Architecture Specification Document

---

## 1. Product Overview

LTI-AMJ (Advanced Learning Tools Interoperability) is a next-generation LTI-compliant platform designed to provide seamless integration between external learning tools and Learning Management Systems (LMS) such as Canvas, Moodle, and Blackboard.

### Added Value for the EdTech Ecosystem

- **Unified Integration Framework:** Single API surface for connecting diverse learning tools across multiple LMS platforms
- **Standardized Data Exchange:** Full compliance with 1EdTech LTI Advantage specification
- **Enhanced Security:** OAuth2/OIDC based authentication with JWT token validation
- **Real-time Analytics:** Built-in usage tracking and learning outcome metrics

### Competitive Advantages

| Advantage | Description |
|-----------|-------------|
| Security | Platform-level OAuth2/OIDC flow with nonce validation and signature verification |
| Ease of Integration | Pre-built launch handlers and standardized registration workflows |
| Data Analytics | Native Grade Passback, Deep Linking, and Names and Roles Provisioning Services |
| Scalability | Cloud-native microservices architecture with horizontal scaling |
| Compliance | Full LTI 1.3 / LTI Advantage support |

---

## 2. Core Functionality

### LTI Advantage Support

LTI-AMJ implements all three LTI Advantage services:

1. **Assignment and Grade Services (AGS):** Enables reading, creating, and updating line items and scores
2. **Names and Role Provisioning Services (NRPS):** Provides membership data sync between LMS and tools
3. **Deep Linking (DL):** Allows instructors to select and configure content from external tools

### Deep Linking Workflow

1. LMS sends a Deep Linking Request with JWT containing launch context
2. LTI-AMJ validates the request and presents available resources
3. User selects resources and submits selections
4. LTI-AMJ returns selected items as a Deep Linking Response
5. LMS creates corresponding Tool Links in the course

### Grade Passback

1. External tool collects assessment data
2. LTI-AMJ receives score submission via AGS API
3. Platform validates score against configured grading schema
4. Score is pushed back to LMS gradebook via Line Item endpoint
5. Student sees synchronized grade in their LMS

---

## 3. Lean Canvas

```mermaid
flowchart LR
    subgraph Problem
        P1[LMS silos learning tools]
        P2[Complex OAuth integration]
        P3[Manual grade synchronization]
    end
    
    subgraph Solution
        S1[Unified LTI 1.3 Platform]
        S2[Automated Grade Passback]
        S3[Deep Linking Content Selection]
    end
    
    subgraph UniqueValue
        UV1[Single integration for all LMS]
        UV2[Real-time analytics dashboard]
        UV3[Compliance-first architecture]
    end
    
    subgraph Metrics
        M1[Active tool launches/day]
        M2[Grade sync latency]
        M3[Registration success rate]
    end
    
    subgraph Channels
        C1[1EdTech Certified Directory]
        C2[Canvas Commons]
        C3[Direct LMS Integration]
    end
    
    subgraph Cost
        CO1[Cloud infrastructure]
        CO2[Security audits]
        CO3[Partner integrations]
    end
    
    subgraph Revenue
        R1[Per-seat licensing]
        R2[Premium analytics add-ons]
        R3[Enterprise SLA contracts]
    end
```

---

## 4. Use Cases

### Use Case 1: Instructor Tool Setup

**Description:** An instructor configures an external tool (e.g., a coding assessment platform) within their LMS course using Deep Linking.

```mermaid
sequenceDiagram
    participant I as Instructor
    participant LMS as Learning Management System
    participant LTI as LTI-AMJ Platform
    participant DB as Tool Registry

    I->>LMS: Opens course configuration
    LMS->>LTI: Initiates Deep Linking Request
    LTI->>DB: Validates tool registration
    DB-->>LTI: Returns tool configuration
    LTI-->>LMS: Renders content selection UI
    I->>LTI: Selects assessment modules
    LTI->>DB: Stores selection preferences
    LTI-->>LMS: Deep Linking Response (Tool Links)
    LMS->>I: Displays configured tool links
```

### Use Case 2: Student Tool Access

**Description:** A student launches an external tool from within their LMS course.

```mermaid
sequenceDiagram
    participant S as Student
    participant LMS as Learning Management System
    participant LTI as LTI-AMJ Platform
    participant Tool as External Learning Tool

    S->>LMS: Clicks tool link in course
    LMS->>LTI: LTI 1.3 Launch Request (id_token + state)
    LTI->>LTI: Validate JWT signature & nonce
    LTI->>LTI: Extract user context & roles
    LTI->>Tool: Forward launch with user context
    Tool-->>S: Render tool interface
    LTI->>LMS: Optional: NRPS membership sync
```

### Use Case 3: Automatic Grading

**Description:** An external tool submits assessment scores back to the LMS gradebook automatically.

```mermaid
sequenceDiagram
    participant S as Student
    participant Tool as External Learning Tool
    participant LTI as LTI-AMJ Platform
    participant LMS as Learning Management System

    S->>Tool: Completes assessment
    Tool->>LTI: Score submission request
    LTI->>LTI: Validate scoring permissions
    LTI->>LTI: Transform to AGS format
    LTI->>LMS: POST to Line Item /scores
    LMS->>LMS: Update gradebook
    LMS-->>LTI: Score submission confirmation
    LTI-->>Tool: Acknowledgment
    S->>LMS: Views grade in gradebook
```

---

## 5. Data Model

### Entities

| Entity | Attributes | Type | Constraints |
|--------|------------|------|-------------|
| **User** | id, lms_user_id, email, name, given_name, family_name, roles | UUID, String, String, String, String, String, String[] | PK, Unique per LMS |
| **Context** | id, lms_context_id, title, type, lms_id | UUID, String, String, String, UUID | PK, FK to LMS |
| **Tool** | id, client_id, deployment_id, name, description, public_key, jwks_url, initiator_oidc_url, target_link_uri | UUID, String, String, String, Text, String, String, String, String | PK, Unique (client_id + deployment_id) |
| **ResourceLink** | id, tool_id, context_id, resource_link_id, title, url, custom_params | UUID, UUID, UUID, String, String, String, JSON | PK, FK to Tool, Context |
| **Score** | id, resource_link_id, user_id, score_given, score_maximum, activity_progress, grading_progress, comment, timestamp, is_final | UUID, UUID, UUID, Decimal, Decimal, String, String, String, DateTime, Boolean | PK, FK to ResourceLink, User |
| **LineItem** | id, tool_id, context_id, line_item_id, label, score_maximum, resource_id, tag | UUID, UUID, UUID, String, String, Decimal, String, String | PK, FK to Tool, Context |
| **Membership** | id, context_id, user_id, status, roles | UUID, UUID, UUID, String, String[] | PK, FK to Context, User |

### Relationships

```mermaid
erDiagram
    Tool ||--o{ ResourceLink : "provides"
    Tool ||--o{ LineItem : "creates"
    Context ||--o{ ResourceLink : "contains"
    Context ||--o{ LineItem : "has"
    Context ||--o{ Membership : "includes"
    User ||--o{ Membership : "belongs to"
    User ||--o{ Score : "receives"
    ResourceLink ||--o{ Score : "generates"
```

---

## 6. High-Level System Design

### Architectural Approach

LTI-AMJ follows a **cloud-native microservices architecture** designed for horizontal scalability and high availability.

| Characteristic | Implementation |
|----------------|-----------------|
| Deployment | Kubernetes on AWS/GCP |
| Communication | REST APIs with async message queues |
| Database | PostgreSQL (relational), Redis (caching) |
| Authentication | OAuth2/OIDC with JWT |
| Observability | Prometheus, Grafana, ELK Stack |

### C1 System Context Diagram

```mermaid
graph TD
    subgraph External_Systems
        LMS[("LMS\nCanvas/Moodle/Blackboard")]
        ExternalTool[("External Learning\nTool")]
        JWKS[("JWKS Provider")]
    end

    subgraph LTI_AMJ_Platform
        API_GW[("API Gateway")]
        Auth_Module[("Authentication\nService")]
        Launch_Service[("Launch\nService")]
        AGS_Service[("Grade Passback\nService")]
        NRPS_Service[("Membership\nSync Service")]
        DL_Service[("Deep Linking\nService")]
        Tool_Registry[("Tool Registry\nService")]
        Analytics[("Analytics\nService")]
    end

    subgraph Data_Layer
        DB[(PostgreSQL)]
        Cache[(Redis)]
        Audit[("Audit Log")]
    end

    LMS -->|LTI 1.3 Launch| API_GW
    ExternalTool -->|Score Submission| API_GW
    API_GW --> Auth_Module
    Auth_Module -->|Verify JWT| JWKS
    Auth_Module -->|Launch Request| Launch_Service
    Launch_Service -->|Forward| ExternalTool
    ExternalTool -->|AGS Score| AGS_Service
    AGS_Service -->|Sync Grade| LMS
    LMS -->|NRPS Request| NRPS_Service
    LMS -->|Deep Link Request| DL_Service
    Launch_Service --> Tool_Registry
    Tool_Registry --> DB
    AGS_Service --> DB
    AllServices --> Cache
    AllServices --> Audit
```

---

## 7. C4 Diagram - Component Level

### LTI Provider Service (Authentication Module)

This component is the "heart" of LTI security, handling OAuth2/OIDC flow, JWT validation, and launch request processing.

```mermaid
graph TB
    subgraph LTI_AMJ_Platform
        subgraph Auth_Module["LTI Provider Service - Authentication Module"]
            direction TB
            OIDC_Handler["OIDC Handler"]
            JWT_Validator["JWT Validator"]
            Nonce_Manager["Nonce Manager"]
            Signature_Verifier["Signature Verifier"]
            Claim_Extractor["Claim Extractor"]
            Launch_Controller["Launch Controller"]
            Security_Config["Security Config"]
        end
        
        subgraph External
            LMS[("LMS")]
            JWKS[("JWKS Provider")]
        end
        
        subgraph Data
            ToolRegistry[("Tool Registry")]
            SessionStore[("Session Store")]
        end
    end

    LMS -->|1. OIDC Login Init| OIDC_Handler
    OIDC_Handler -->|2. Validate Client ID| ToolRegistry
    ToolRegistry -->|3. Return Tool Config| OIDC_Handler
    OIDC_Handler -->|4. Redirect to Authorize| LMS
    LMS -->|5. POST id_token| JWT_Validator
    JWT_Validator -->|6. Fetch JWKS| JWKS
    JWKS -->|7. Return Keys| JWT_Validator
    JWT_Validator -->|8. Verify Signature| Signature_Verifier
    Signature_Verifier -->|9. Check Nonce| Nonce_Manager
    Nonce_Manager -->|10. Store Nonce| SessionStore
    Signature_Verifier -->|11. Extract Claims| Claim_Extractor
    Claim_Extractor -->|12. Validate Claims| Security_Config
    Security_Config -->|13. Create Session| Launch_Controller
    Launch_Controller -->|14. Forward to Tool| LMS
```

### Component Responsibilities

| Component | Responsibility |
|-----------|---------------|
| OIDC Handler | Processes OIDC login initiation, validates client registration, generates authorization redirect |
| JWT Validator | Validates JWT structure, expiry, issuer, audience |
| Signature Verifier | Verifies JWT signature against JWKS from LMS |
| Nonce Manager | Manages one-time use nonces to prevent replay attacks |
| Claim Extractor | Extracts user identity, context, roles, and resource link from LTI claims |
| Launch Controller | Creates session, generates launch response, redirects to tool |
| Security Config | Enforces security policies (allowed domains, required scopes) |

---

## 8. Compliance & Standards

LTI-AMJ is designed for full compliance with:

- **LTI 1.3 / LTI Advantage** (1EdTech)
- **OAuth 2.0** (RFC 6749)
- **OpenID Connect Core** (RFC 8252)
- **JWT** (RFC 7519)
- **IMS Global Security Best Practices**

---

*Document Version: 1.0 | Architecture by Senior Software Architect*
