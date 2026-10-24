# Enterprise HRM, Asset & Case Management

A Salesforce Developer Edition project built to practise Salesforce administration: data model, security, Service Cloud, Flow automation, reports and dashboards, and data quality.

## Project status
- [ ] Phase 1: Data model
- [ ] Phase 2: Security
- [ ] Phase 3: Service Cloud
- [ ] Phase 4: Automation
- [ ] Phase 5: Reports and dashboards
- [ ] Phase 6: Data quality
- [ ] Phase 7: Lightning app and UI
- [ ] Phase 8: Documentation and demo video

## Folders
- docs: screenshots, data model diagram, security matrix
- data: dummy CSV files used with Data Loader

## Built by
Kavish Muthusamy Karthi, Salesforce Certified Administrator

## Architecture Diagram


```mermaid
erDiagram

    EMPLOYEE {
        autonumber Employee_ID PK
        text Employee_Name
        picklist Department
        picklist Status
        email Work_Email
        date Start_Date
        lookup Manager FK
    }

    IT_ASSET {
        autonumber Asset_Tag PK
        text Serial_Number
        picklist Asset_Type
        picklist Status
        date Warranty_End
        lookup Assigned_To FK
    }

    ASSET_ASSIGNMENT {
        autonumber Assignment_No PK
        masterdetail Employee FK
        masterdetail IT_Asset FK
        date Assigned_Date
        date Returned_Date
    }

    ASSET_REQUEST {
        autonumber Request_No PK
        masterdetail Requested_By FK
        picklist Asset_Type
        picklist Status
        lookup Allocated_Asset FK
    }

    ACCOUNT {
        text Name PK
    }

    ENTITLEMENT {
        text Name PK
        lookup Account FK
    }

    CASE {
        autonumber Case_Number PK
        picklist Priority
        lookup Employee FK
        lookup Related_Asset FK
        lookup Entitlement FK
    }

    %% Relationships & Cardinalities
    EMPLOYEE ||--o{ EMPLOYEE : "manages"
    EMPLOYEE ||--o{ IT_ASSET : "assigned to"
    EMPLOYEE ||--|| ASSET_ASSIGNMENT : "master-detail"
    IT_ASSET ||--|| ASSET_ASSIGNMENT : "master-detail"
    EMPLOYEE ||--|| ASSET_REQUEST : "master-detail"
    IT_ASSET ||--o| ASSET_REQUEST : "allocated"
    EMPLOYEE ||--o{ CASE : "raised by"
    IT_ASSET ||--o{ CASE : "related to"
    ACCOUNT ||--o{ ENTITLEMENT : "has"
    ENTITLEMENT ||--o{ CASE : "governs SLA"

```
