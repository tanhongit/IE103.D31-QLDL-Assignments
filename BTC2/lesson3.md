Entities:

- Member: MemberID, Name, GroupID (FK to Group)
- Group: GroupID, GroupName, TeamLeaderID (FK to Member)
- Job: JobID, Description, JobCost, MemberID (FK to Member)
- Contract: ContractID, ContractDate, LicensePlate, TotalCost, ExpectedDeliveryDate, ActualDeliveryDate, CustomerID (FK to Customer)
- Customer: CustomerID, Name, Address, PhoneNumber

---

Relationships:

- Group - Member (1-n): A group has many members (GroupID in Member is a FK).
- Member - Group (1-1): Each member belongs to only one group.
- Group - Member (1-1, TeamLeader): Each group has one team leader (TeamLeaderID is a FK).
- Contract - Job (1-n): A contract can have multiple jobs (ContractID in JobContract is a FK).
- Job - Contract (n-1): A job belongs to one contract (ContractID in Job is a FK).
- Member - Job (1-n): Each job is performed by one mechanic (MemberID in Job is a FK).
- Customer - Contract (1-n): A customer can have multiple contracts (CustomerID in Contract is a FK).
- Contract - Customer (n-1): A contract belongs to one customer (CustomerID in Contract is a FK).

ERD (Entity Relationship Diagram):

```mermaid
erDiagram
    MEMBER ||--o{ GROUP : BelongTo
    GROUP ||--o{ MEMBER : Has
    GROUP ||--o{ MEMBER : TeamLeader
    JOB ||--o{ MEMBER : AssignedTo
    JOB ||--o{ CONTRACT : BelongTo
    CONTRACT ||--o{ JOB : Has
    CUSTOMER ||--o{ CONTRACT : Has
    CONTRACT ||--o{ CUSTOMER : BelongTo
    CUSTOMER ||--o{ CONTRACT : Has
    
    CUSTOMER {
        int CustomerID PK
        string Name
        string Address
        string PhoneNumber
    }
    CONTRACT {
        int ContractID PK
        date ContractDate
        string LicensePlate
        float TotalCost
        date ExpectedDeliveryDate
        date ActualDeliveryDate
        int CustomerID FK
    }
    JOB {
        int JobID PK
        string Description
        float JobCost
        int MemberID FK
        int ContractID FK
    }
    MEMBER {
        int MemberID PK
        string Name
        int GroupID FK
    }
    GROUP {
        int GroupID PK
        string GroupName
        int TeamLeaderID FK
    }
```

CD:

```mermaid
classDiagram
    CUSTOMER "1" --o "n" CONTRACT : "has"
    CONTRACT "n" --o "1" CUSTOMER : "belongs_to"
    CONTRACT "1" --o "n" JOB : "includes"
    JOB "n" --o "1" MEMBER : "performed_by"
    MEMBER "n" --o "1" GROUP : "belongs_to"
    GROUP "1" --o "n" MEMBER : "has_members"
    GROUP "1" --o "1" MEMBER : "TeamLeader"

    class CUSTOMER {
        +int CustomerID
        +string Name
        +string Address
        +string PhoneNumber
    }

    class CONTRACT {
        +int ContractID
        +date ContractDate
        +string LicensePlate
        +float TotalCost
        +date ExpectedDeliveryDate
        +date ActualDeliveryDate
        +int CustomerID
    }

    class JOB {
        +int JobID
        +string Description
        +float JobCost
        +int MemberID
        +int ContractID
    }

    class MEMBER {
        +int MemberID
        +string Name
        +int GroupID
    }

    class GROUP {
        +int GroupID
        +string GroupName
        +int TeamLeaderID
    }
```
