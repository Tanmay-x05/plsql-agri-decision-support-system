
#  PL/SQL Agricultural Decision Support System

A PL/SQL-based Decision Support System that models crop–climate–fertilizer relationships and assists in sustainable agricultural planning. Built on Oracle Database, the system integrates climate conditions, crop varieties, fertilizers, herbicides, biopesticides, and market pricing into a unified relational schema with automated cost analysis and audit tracking.

---

##  Features

* Models relationships between climate zones, crop varieties, fertilizers, herbicides, and biopesticides.
* Computes fertilizer and herbicide costs for specific crop breeds using stored functions.
* Tracks government subsidy and open-market pricing differences.
* Maintains audit trails for updates and deletions through database triggers.
* Enforces data integrity with validation rules and constraints.

---

##  System Capabilities

### Cost Analysis

* Calculate total fertilizer cost per crop breed.
* Calculate total herbicide cost per crop breed.
* Analyze subsidy versus market price differences.

### Audit Logging

* Record all market price modifications.
* Archive deleted fertilizer records.
* Archive deleted herbicide records.

### Data Validation

* Prevent invalid market price entries.
* Ensure subsidy prices remain lower than open-market prices.

---

##  Database Schema

| Table                      | Purpose                                            |
| -------------------------- | -------------------------------------------------- |
| `login`                    | User authentication                                |
| `user_farmer`              | Farmer profiles, land size, region, farming type   |
| `climate`                  | Climate zones, rainfall, soil condition, sea level |
| `crops_climate`            | Maps crop breeds to suitable climate conditions    |
| `crops_vegetable`          | Crop breed information and seasons                 |
| `crop_fertilizers`         | Fertilizers associated with crop breeds            |
| `biofertilizers`           | Fertilizer details and pricing                     |
| `herbs`                    | Herbicide information                              |
| `herbs_t1`                 | Crop-herbicide mapping                             |
| `herbs_t2`                 | Herbicide classification data                      |
| `biopesticides`            | Biopesticide records                               |
| `market`                   | Government subsidy and market prices               |
| `market_history`           | Audit log for market price updates                 |
| `crop_fertilizers_history` | Archive of deleted fertilizer records              |
| `herbs_history`            | Archive of deleted herbicide records               |

---

##  Stored Functions & Procedures

### Functions

#### `GetTotalFertilizerCost(breed_id)`

Returns the total fertilizer cost for a crop breed.

#### `GetTotalHerbicideCost(breed_id)`

Returns the total herbicide cost for a crop breed.

#### `GetMarketPriceDifference(breed_id)`

Returns the difference between government subsidy price and open-market price.

### Procedures

#### `UpdateMarketPrices(breed_id, subsidy_price, open_market_price)`

Updates market pricing information for a crop breed.

#### `DeleteCropFertilizersByBreed(breed_id)`

Deletes fertilizer records associated with a crop breed.

#### `DeleteHerbsByBreed(breed_id)`

Deletes herbicide records associated with a crop breed.

---

##  Database Triggers

| Trigger                          | Event                             | Purpose                                   |
| -------------------------------- | --------------------------------- | ----------------------------------------- |
| `After_Update_Market_Prices`     | AFTER UPDATE ON market            | Logs old and new prices in market_history |
| `Before_Delete_Crop_Fertilizers` | BEFORE DELETE ON crop_fertilizers | Archives deleted fertilizer records       |
| `After_Delete_Herbs`             | AFTER DELETE ON herbs_t1          | Archives deleted herbicide records        |
| `Before_Insert_Market`           | BEFORE INSERT ON market           | Validates subsidy price constraints       |

---

##  Setup & Usage

### Run the Database Script

```sql
@dbms-project.sql
```

### Execute a Function

```sql
SELECT GetTotalFertilizerCost('12A')
FROM dual;
```

### Call a Procedure

```sql
BEGIN
    UpdateMarketPrices(
        '12A',
        1200.50,
        1500.00
    );
END;
/
```

### View Audit History

```sql
SELECT *
FROM market_history
WHERE breed_id = '12A';
```

---

## 🛠️ Technology Stack

* Oracle Database
* PL/SQL
* DDL & DML Operations
* Stored Functions
* Stored Procedures
* Triggers
* Cursors

---

##  Future Enhancements

* Develop a web-based dashboard for farmers and administrators.
* Incorporate seasonal price fluctuation analysis.
* Implement role-based access control (RBAC).
* Integrate weather forecasting data for smarter crop recommendations.
* Migrate to PostgreSQL (PL/pgSQL) for open-source deployment.

---

##  Learning Outcomes

* Relational database design and normalization.
* PL/SQL programming with functions and procedures.
* Trigger-based auditing and logging.
* Data validation and integrity enforcement.
* Agricultural decision-support system modeling.


Computer Science Engineering Student

Oracle PL/SQL • Database Systems • Agricultural Informatics
