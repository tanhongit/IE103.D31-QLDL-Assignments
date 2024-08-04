Relational Database Design:

- CUSTOMER (**CustomerID**, Name, PhoneNumber, Address)					
- DEALER (**DealerID**, Location)								
- VEHICLEINFO (**VehicleID**, **DealerID**, Manufacturer, EngineCapacity, VehicleType, NumberOfDoors, Color, FrameSize)						
- ADMINISTRATIVE_STAFF (**StaffID**, Name, **DealerID**, EducationLevel, Position)								
- TECHNICIAN (**TechnicianID**, **DealerID**, YearsOfExperience, Name, Position, Level)								
- CONTRACT (**ContractID**, Salesperson, Accountant, ContractDate, TotalAmount, DiscountRate, IsPaid, FirstPayment, SecondPayment, WarrantyPeriod, **DealerID**)								
- PAYMENT_SLIP (**SlipID**, **ContractID**, **DealerID**, **CustomerID**, PaymentDate, Receiver, Amount)						
- WARRANTY_SLIP (**WarrantyID**, **CustomerID**, **DealerID**, Technician, RepairCost, Reason)							
- WARRANTY_DETAIL (**WarrantyDetailID**, **WarrantyID**, PartName)


Relationships:

- CUSTOMER - CONTRACT (1-n)
- DEALER - VEHICLEINFO (1-n)
- DEALER - ADMINISTRATIVE_STAFF (1-n)
- DEALER - TECHNICIAN (1-n)
- DEALER - CONTRACT (1-n)
- CUSTOMER - PAYMENT_SLIP (1-n)
- CUSTOMER - WARRANTY_SLIP (1-n)
- WARRANTY_SLIP - WARRANTY_DETAIL (1-n)
- DEALER - WARRANTY_SLIP (1-n)
- DEALER - WARRANTY_DETAIL (1-n)
- TECHNICIAN - WARRANTY_SLIP (1-n)
- WARRANTY_SLIP - TECHNICIAN (1-n)
- WARRANTY_DETAIL - WARRANTY_SLIP (1-1)

---

ERD (Entity Relationship Diagram):

```mermaid
erDiagram
    CUSTOMER ||--o{ CONTRACT : Has
    DEALER ||--o{ VEHICLEINFO : Has
    DEALER ||--o{ ADMINISTRATIVE_STAFF : Has
    DEALER ||--o{ TECHNICIAN : Has
    DEALER ||--o{ CONTRACT : Has
    CUSTOMER ||--o{ PAYMENT_SLIP : Has
    CUSTOMER ||--o{ WARRANTY_SLIP : Has
    WARRANTY_SLIP ||--o{ WARRANTY_DETAIL : Has
    DEALER ||--o{ WARRANTY_SLIP : Has
    DEALER ||--o{ WARRANTY_DETAIL : Has
    TECHNICIAN ||--o{ WARRANTY_SLIP : Has
    WARRANTY_SLIP ||--o{ TECHNICIAN : Has
    WARRANTY_DETAIL ||--o{ WARRANTY_SLIP : Has

    CUSTOMER {
        int CustomerID PK
        string Name
        string PhoneNumber
        string Address
    }
    DEALER {
        int DealerID PK
        string Location
    }
    VEHICLEINFO {
        int VehicleID PK
        int DealerID FK
        string Manufacturer
        float EngineCapacity
        string VehicleType
        int NumberOfDoors
        string Color
        string FrameSize
    }
    ADMINISTRATIVE_STAFF {
        int StaffID PK
        string Name
        int DealerID FK
        string EducationLevel
        string Position
    }
    TECHNICIAN {
        int TechnicianID PK
        int DealerID FK
        int YearsOfExperience
        string Name
        string Position
        string Level
    }
    CONTRACT {
        int ContractID PK
        string Salesperson
        string Accountant
        date ContractDate
        float TotalAmount
        float DiscountRate
        bool IsPaid
        float FirstPayment
        float SecondPayment
        int WarrantyPeriod
        int DealerID FK
    }
    PAYMENT_SLIP {
        int SlipID PK
        int ContractID FK
        int DealerID FK
        int CustomerID FK
        date PaymentDate
        string Receiver
        float Amount
    }
    WARRANTY_SLIP {
        int WarrantyID PK
        int CustomerID FK
        int DealerID FK
        int Technician FK
        float RepairCost
        string Reason
    }
    WARRANTY_DETAIL {
        int WarrantyDetailID PK
        int WarrantyID FK
        string PartName
    }
```

CD

```mermaid
classDiagram
    CUSTOMER "1" --o "n" CONTRACT : "Has"
    DEALER "1" --o "n" VEHICLEINFO : "Has"
    DEALER "1" --o "n" ADMINISTRATIVE_STAFF : "Has"
    DEALER "1" --o "n" TECHNICIAN : "Has"
    DEALER "1" --o "n" CONTRACT : "Has"
    CUSTOMER "1" --o "n" PAYMENT_SLIP : "Has"
    CUSTOMER "1" --o "n" WARRANTY_SLIP : "Has"
    WARRANTY_SLIP "1" --o "n" WARRANTY_DETAIL : "Has"
    DEALER "1" --o "n" WARRANTY_SLIP : "Has"
    DEALER "1" --o "n" WARRANTY_DETAIL : "Has"
    TECHNICIAN "1" --o "n" WARRANTY_SLIP : "Has"
    WARRANTY_SLIP "1" --o "n" TECHNICIAN : "Has"
    WARRANTY_DETAIL "1" --o "1" WARRANTY_SLIP : "Has"

    class CUSTOMER {
        +int CustomerID
        +string Name
        +string PhoneNumber
        +string Address
    }
    class DEALER {
        +int DealerID
        +string Location
    }
    class VEHICLEINFO {
        +int VehicleID
        +int DealerID
        +string Manufacturer
        +float EngineCapacity
        +string VehicleType
        +int NumberOfDoors
        +string Color
        +string FrameSize
    }
    class ADMINISTRATIVE_STAFF {
        +int StaffID
        +string Name
        +int DealerID
        +string EducationLevel
        +string Position
    }
    class TECHNICIAN {
        +int TechnicianID
        +int DealerID
        +int YearsOfExperience
        +string Name
        +string Position
        +string Level
    }
    class CONTRACT {
        +int ContractID
        +string Salesperson
        +string Accountant
        +date ContractDate
        +float TotalAmount
        +float DiscountRate
        +bool IsPaid
        +float FirstPayment
        +float SecondPayment
        +int WarrantyPeriod
        +int DealerID
    }
    class PAYMENT_SLIP {
        +int SlipID
        +int ContractID
        +int DealerID
        +int CustomerID
        +date PaymentDate
        +string Receiver
        +float Amount
    }
    class WARRANTY_SLIP {
        +int WarrantyID
        +int CustomerID
        +int DealerID
        +int Technician
        +float RepairCost
        +string Reason
    }
    class WARRANTY_DETAIL {
        +int WarrantyDetailID
        +int WarrantyID
        +string PartName
    }
```
