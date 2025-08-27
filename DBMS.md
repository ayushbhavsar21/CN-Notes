# DBMS

A *DBMS* is software that manages databases. It provides an efficient way to store, retrieve, and update data while ensuring security, consistency, and reliability. It supports features like data abstraction, reduced redundancy, query processing, and multi-user access. Examples include *MySQL, Oracle, and MongoDB*.

---

## Data vs Information

- *Data*: Raw facts  
- *Information*: Processed, organized data

---

## DBMS Architecture

DBMS architecture can be described in two ways:

1. *System Architecture*: 1-tier, 2-tier, or 3-tier, depending on how client, server, and application layers interact.  
2. *Three-Schema Architecture*: External schema (user views), conceptual schema (logical structure), and internal schema (physical storage).

This separation ensures *data abstraction, security, and flexibility*.

---

### 1. Types of Architecture

#### 1-Tier  
- User interacts directly with the database.  
- Mostly used by developers for testing.

#### 2-Tier  
- Client communicates with the database server directly.  
- Example: simple applications using *JDBC/ODBC*.  
  - *ODBC*: Open Database Connectivity (Microsoft, C)  
  - *JDBC*: Java Database Connectivity

#### 3-Tier  
- Adds an *application server* between client and DB server.  
- Improves *scalability, security, and abstraction*.  
- Common in *web applications*.

---

### 2. Three-Schema Architecture (Most Asked in Interviews)

1. *External Level (View Level):* Describes how end users see the data. Multiple user views possible.  
2. *Conceptual Level (Logical Level):* Describes structure of the database as a whole. Defines entities, relationships, constraints.  
3. *Internal Level (Physical Level):* Defines how data is physically stored using indexes, files, and storage structures.

---

## ER Diagram

### Definition  
An *ER (Entity–Relationship) Diagram* is a visual representation of the data model of a system.  
It shows entities (objects), their attributes, and the relationships between them.  
It is used in database design to map real-world requirements into a structured database schema.

---

### Key Components of ER Diagram

#### 1. Entity  
- Object or concept that stores data.  
- *Strong Entity*: Has its own primary key (e.g., Student, Employee).  
- *Weak Entity*: Cannot be uniquely identified without another entity (e.g., OrderItem depends on Order).

#### 2. Attributes  
- Properties of entities.  
- *Simple Attribute*: Cannot be divided (Name, Age).  
- *Composite Attribute*: Can be split (FullName → FirstName + LastName).  
- *Derived Attribute*: Value can be derived from others (Age from DOB).  
- *Multivalued Attribute*: Can have multiple values (Phone Numbers).

#### 3. Relationship  
- Association between entities.  
- *Types*: One-to-One (1:1), One-to-Many (1:N), Many-to-Many (M:N).  
- Represented using *diamonds* in ER diagrams.

#### 4. Keys  
- *Primary Key*: Unique identifier of an entity.  
- *Foreign Key*: Attribute that links entities.
<img width="1592" height="784" alt="image" src="https://github.com/user-attachments/assets/c361e368-b4fb-43e5-b82f-e182cdeef27f" />

---

## Relational Model

- Proposed by *E.F. Codd (1970)*.  
- Represents data as *tables (relations)* with rows (tuples) and columns (attributes).  
- Each table has *constraints* to ensure data integrity.  
- Relationships between tables are defined using *keys*.

---

### Types of Keys in Relational Model

1. *Super Key*  
   - A set of one or more attributes that can uniquely identify a tuple.  
   - Example: {StudentID}, {StudentID, Name}.

2. *Candidate Key*  
   - Minimal super key (no unnecessary attributes).  
   - Example: StudentID or Email.

3. *Primary Key*  
   - One chosen candidate key.  
   - Cannot be NULL or duplicate.  
   - Example: StudentID.

4. *Alternate Key*  
   - Candidate keys not chosen as primary key.  
   - Example: If Email is not chosen as primary key, it becomes an alternate key.

5. *Foreign Key*  
   - Attribute in one relation that references the primary key in another relation.  
   - Maintains *referential integrity*.  
   - Example: CourseID in Enrollment table referencing Course table.

6. *Composite Key*  
   - Key formed by combining two or more attributes.  
   - Example: (StudentID, CourseID) in Enrollment table.

7. *Unique Key*  
   - Similar to primary key but allows one NULL.  
   - Example: PhoneNumber in Student table (unique but may be NULL).

---

**Nessacary condition for a candidate key to be a primary key**
> Any attribute of the Primary key can not contain a NULL value.
  While in the Candidate key, any attribute can contain a NULL value.

## Integrity & Consistency

- *Integrity* in DBMS is maintained using constraints like primary key, foreign key, domain rules, and business rules.  
- *Consistency* is ensured through *ACID properties* of transactions.  
- Together, they prevent invalid, duplicate, or conflicting data.

---

## Types of SQL Commands – Interview Answer

SQL commands are grouped into categories based on what they do with the database.

---

### **1. DDL (Data Definition Language)**

Used to define and manage database structure.

* **CREATE** → Creates objects (table, database).

  ```sql
  CREATE TABLE Student (
      StudentID INT PRIMARY KEY,
      Name VARCHAR(50),
      Age INT
  );
  ```
* **ALTER** → Modifies an existing object.

  ```sql
  ALTER TABLE Student ADD Email VARCHAR(100);
  ```
* **DROP** → Deletes an object.

  ```sql
  DROP TABLE Student;
  ```
* **TRUNCATE** → Removes all rows but keeps structure.

  ```sql
  TRUNCATE TABLE Student;
  ```

---

### **2. DML (Data Manipulation Language)**

Used to manipulate data inside tables.

* **INSERT**

  ```sql
  INSERT INTO Student (StudentID, Name, Age) VALUES (1, 'Ayush', 21);
  ```
* **UPDATE**

  ```sql
  UPDATE Student SET Age = 22 WHERE StudentID = 1;
  ```
* **DELETE**

  ```sql
  DELETE FROM Student WHERE StudentID = 1;
  ```

---

### **3. DQL (Data Query Language)**

Used to query and fetch data.

* **SELECT**

  ```sql
  SELECT Name, Age FROM Student WHERE Age > 20;
  ```

---

### **4. DCL (Data Control Language)**

Used for permissions and access control.

* **GRANT** → Gives user privileges.

  ```sql
  GRANT SELECT, INSERT ON Student TO user1;
  ```
* **REVOKE** → Removes privileges.

  ```sql
  REVOKE INSERT ON Student FROM user1;
  ```

---

### **5. TCL (Transaction Control Language)**

Used to manage transactions.

* **COMMIT** → Save changes permanently.

  ```sql
  COMMIT;
  ```
* **ROLLBACK** → Undo changes before commit.

  ```sql
  ROLLBACK;
  ```
* **SAVEPOINT** → Create a point to rollback to.

  ```sql
  SAVEPOINT sp1;
  ROLLBACK TO sp1;
  ```

---

**Query Language (DQL)**

- *DQL* mainly has the *SELECT* statement.  
- Clauses: *WHERE, ORDER BY, GROUP BY* are used to refine and structure queries.


## 📌 **Normalization in DBMS**
---
### 🔹 **Definition**

Normalization is the **process of organizing data** in a database to reduce **redundancy (duplication)** and improve **data integrity**.
It transforms large, complex tables into smaller, related ones.

---

### 📌 **Normal Forms (NFs)**

There are several normal forms (rules). The most common ones used are:

---

#### 1️⃣ **First Normal Form (1NF)**

**Rule**:

* Data must be in **tabular format** (rows & columns).
* Each cell must hold **atomic (indivisible)** values (no repeating groups, no arrays).
* Each record must be unique.

**How to achieve 1NF**:

* Remove repeating groups.
* Break down multivalued attributes into separate rows.

---

#### 2️⃣ **Second Normal Form (2NF)**

**Rule**:

* Must already be in **1NF**.
* No **partial dependency**: Non-key attributes must depend on the **whole primary key**, not part of it.
  *(Applies only if composite key exists)*

**How to achieve 2NF**:

* If non-key attributes depend on only part of the composite key → move them to a new table with that part as primary key.

---

#### 3️⃣ **Third Normal Form (3NF)**

**Rule**:

* Must already be in **2NF**.
* No **transitive dependency**: Non-key attributes must not depend on another non-key attribute.

**How to achieve 3NF**:

* Remove attributes that depend on other non-key attributes into a separate table.

---

#### 4️⃣ **Boyce-Codd Normal Form (BCNF)**

**Rule**:

* A stronger version of 3NF.
* For every functional dependency (X → Y), **X should be a super key**.

---

#### 4️⃣ **Fourth Normal Form (4NF)**

**Rule**:

* Must already be in **BCNF**.
* No **multi-valued dependencies** (MVDs).
* A multi-valued dependency means one attribute can determine multiple independent sets of values.

**Example (Before 4NF):**

| Student | Hobby    | Language |
| ------- | -------- | -------- |
| Alice   | Chess    | English  |
| Alice   | Chess    | French   |
| Alice   | Painting | English  |
| Alice   | Painting | French   |

Here, **Hobbies** and **Languages** are independent of each other but are stored together → redundancy.

**Solution (After 4NF):**

* Split into two tables:

**Student–Hobby**

| Student | Hobby    |
| ------- | -------- |
| Alice   | Chess    |
| Alice   | Painting |

**Student–Language**

| Student | Language |
| ------- | -------- |
| Alice   | English  |
| Alice   | French   |

✅ Now no multi-valued dependency → in **4NF**.

---

#### 5️⃣ **Fifth Normal Form (5NF or PJNF – Project Join Normal Form)**

**Rule**:

* Must already be in **4NF**.
* No **join dependency** — data should not be decomposable into multiple tables that need to be recombined with joins unnecessarily.
* In other words - It cannot be further decomposed into smaller tables without losing information.
* In short: avoid redundancy that occurs due to complex relationships.


✅ **5NF ensures** the table cannot be split further without losing data or introducing redundancy.

---
### 📌 **Summary of All Normal Forms**

| Normal Form | Removes                             | Example Issue Solved                       |
| ----------- | ----------------------------------- | ------------------------------------------ |
| **1NF**     | Repeating groups, non-atomic values | Multiple values in one cell                |
| **2NF**     | Partial dependency                  | Non-key depending on part of composite key |
| **3NF**     | Transitive dependency               | Non-key depending on another non-key       |
| **BCNF**    | More strict FDs                     | Every determinant must be superkey         |
| **4NF**     | Multi-valued dependency             | Independent multi-valued attributes        |
| **5NF**     | Join dependency                     | Complex redundancy from joins              |
| **6NF**     | Temporal / advanced join deps       | Time-dependent attributes                  |

---

✅ **In real-world systems**:

* **3NF/BCNF** is usually enough for OLTP (transactional DBs).
* **4NF/5NF** for advanced enterprise DBs with complex relationships.
* **6NF** for data warehouses & temporal DBs.
---
### **📌 In normalization we break table to remove redundency , but how breaking table removes redundency ?**
- "Normalization removes redundancy by decomposing a large table into smaller tables based on functional dependencies. This ensures that each fact is stored only once. Instead of repeating data (like student names or course names) across multiple rows, we store them in separate tables and use keys to establish relationships. This avoids anomalies and maintains data consistency."

- **Eg**
🔹 1. Start with the Problem (Redundancy)

* In an unnormalized table, **the same information is repeated many times**.
* Example:

  ```
  StudentID | StudentName | Course | Instructor
  1         | Alice       | DBMS   | Prof. John
  2         | Bob         | DBMS   | Prof. John
  ```

  Here, *“Prof. John”* is repeated for every student in DBMS.

👉 Repetition = redundancy → wastes space, and causes **update anomalies** (if Prof. John changes phone number, we must update multiple rows).

🔹 2. Explain the Solution (Breaking Tables)

* By splitting into **separate tables**, we **store each fact only once**.
* Example after normalization:

**Student Table**

```
StudentID | StudentName
1         | Alice
2         | Bob
```

**Course Table**

```
Course | Instructor
DBMS   | Prof. John
```

**Enrollment Table**

```
StudentID | Course
1         | DBMS
2         | DBMS
```
👉 Now *“Prof. John”* is stored **once**, linked through `Course`.

🔹 3. Why This Removes Redundancy

* Instead of repeating the same instructor name in every row, we keep it in **one place (Course table)**.
* Any update is done once → **no anomalies** (Update, Insert, Delete).
* Tables store **atomic, non-redundant facts**, and relationships are captured with **foreign keys**.
  
---

## 📌 Functional Dependency (FD)

### 🔹 **Definition**

> *A functional dependency means one attribute uniquely determines another. For example, StudentID determines StudentName. They can be trivial, non-trivial, full, partial, transitive, or multivalued. Each type is important because they guide normalization steps — partial dependencies violate 2NF, transitive dependencies violate 3NF, and multivalued dependencies violate 4NF.*

---

A **functional dependency** exists when the value of one attribute (or a set of attributes) in a relation **uniquely determines** the value of another attribute.

👉 Formally:
If `X → Y`, then for every two rows in a table, if the values of **X** are the same, the values of **Y** must also be the same.

**Example**:

* In `Student(StudentID, Name, Department)`:

  * `StudentID → Name` (StudentID uniquely determines Name).
  * `Department → HOD` (Department uniquely determines Head of Department).
---

### 📌 Types of Functional Dependencies

---

#### 1️⃣ **Trivial Functional Dependency**

* Dependency where the right-hand side is a subset of the left-hand side.
* Example: `{StudentID, Name} → Name` (trivial because Name is already in LHS).
---

#### 2️⃣ **Non-Trivial Functional Dependency**

* Dependency where RHS is **not** part of LHS.
* Example: `StudentID → Name` (Name not in LHS).
---

#### 3️⃣ **Completely (Fully) Functional Dependency**

* If `X → Y` and removing any attribute from X means dependency no longer holds.
* Example: `(StudentID, CourseID) → Grade`

  * Grade depends on both StudentID and CourseID (composite key).
---

#### 4️⃣ **Partial Functional Dependency**

* If `X → Y` but Y depends on only part of a **composite key**.
* Example: `(StudentID, CourseID) → StudentName`

  * StudentName depends only on StudentID, not on CourseID.
* ❌ Violates **2NF**.
---

#### 5️⃣ **Transitive Dependency**

* When `X → Y` and `Y → Z`, then `X → Z` indirectly.
* Example: `StudentID → Department` and `Department → HOD` ⇒ `StudentID → HOD`.
* ❌ Violates **3NF**.
---

#### 6️⃣ **Multivalued Dependency (MVD)**

* Special case where one attribute determines a **set of values** for another attribute, independent of other attributes.
* Example: `Student → {Hobby, Language}` (a student can have multiple hobbies and multiple languages, independent).
* ❌ Violates **4NF**.
---

### 📌 Summary Table

| Type           | Definition                             | Example                    |
| -------------- | -------------------------------------- | -------------------------- |
| Trivial FD     | RHS ⊆ LHS                              | {ID, Name} → Name          |
| Non-Trivial FD | RHS not in LHS                         | ID → Name                  |
| Fully FD       | Whole composite key needed             | (ID, Course) → Grade       |
| Partial FD     | Only part of composite key             | (ID, Course) → StudentName |
| Transitive FD  | X → Y and Y → Z ⇒ X → Z                | ID → Dept, Dept → HOD      |
| Multivalued FD | One attr → set of values independently | Student → Hobby            |

---

## Transaction in DBMS

### **Definition**

A **transaction** is a single logical unit of work in a database. It may consist of one or multiple CRUD (Create, Read, Update, and Delete) (queries, updates, insertions, deletions) operations that are executed as a whole. A transaction ensures that the database moves from one **consistent state** to another, even in the presence of failures.

Example: In a **bank transfer**, deducting money from one account and adding it to another must either both happen or none happen.

---

### **Properties of Transactions (ACID)**

1. **Atomicity** → All operations in a transaction execute completely or none at all.

   * Example: Debit succeeds but credit fails → rollback entire transaction.
2. **Consistency** → Database must remain in a valid state before and after the transaction.

   * Example: Total balance in system remains same after transfer.
3. **Isolation** → Concurrent transactions execute independently without interfering.

   * Example: Two users booking the same seat → DBMS ensures only one succeeds.
4. **Durability** → Once committed, changes are permanent, even if system crashes.

---

### **Transaction States**

* **Active** → When execution is in progress.
* **Partially Committed** → After the last statement executed but before changes are made permanent.
* **Committed** → Successfully completed and changes saved.
* **Failed** → Error occurs, cannot proceed.
* **Aborted** → Rolled back to previous consistent state.

<img width="910" height="415" alt="image" src="https://github.com/user-attachments/assets/bcd5a661-4357-4bcb-ae52-4a15947b3ad6" />


---

### **Control Commands (TCL)**

* `BEGIN TRANSACTION` → Start.
* `COMMIT` → Save changes.
* `ROLLBACK` → Undo changes.
* `SAVEPOINT` → Set a point to rollback to.

---
## How is ACID properties are incorporated in Transaction
---

### 1. **Atomicity**

* **Meaning**: A transaction is treated as a single, indivisible unit. Either all operations succeed, or none do.
* **Implementation in DBMS**:

  * **Undo/rollback logs**: If part of a transaction fails, changes are rolled back using logs.
  * **Write-ahead logging (WAL)**: Before any data is changed, the intended update is recorded in a log. This ensures rollback is possible.
  * Example: If money is transferred between two accounts, either debit and credit both happen, or neither.

---

### 2. **Consistency**

* **Meaning**: The database must move from one valid state to another valid state, preserving all rules (constraints, triggers, cascades).
* **Implementation in DBMS**:

  * **Constraints**: Primary keys, foreign keys, unique, not-null, check constraints ensure rules are not violated.
  * **Referential integrity**: Ensures relationships between tables remain valid.
  * Example: You cannot insert an order with a customer ID that doesn’t exist.

---

### 3. **Isolation**

* **Meaning**: Transactions execute independently of each other. Intermediate states of a transaction are not visible to others.
* **Implementation in DBMS**:

  * **Locking protocols**: Shared locks, exclusive locks prevent conflicts.
  * **Isolation levels**: Read Uncommitted, Read Committed, Repeatable Read, Serializable (ANSI SQL levels).
  * **Concurrency control**: Techniques like 2-Phase Locking (2PL), Multiversion Concurrency Control (MVCC).
  * Example: While one transaction is transferring money, another transaction cannot read a half-updated balance.

---

### 4. **Durability**

* **Meaning**: Once a transaction is committed, its changes are permanent—even in case of crash or power loss.
* **Implementation in DBMS**:

  * **Write-ahead logs** ensure committed transactions are stored on disk.
  * **Checkpointing**: Periodically saves database state.
  * **Replication & backups**: Extra measures for ensuring data survives failures.
  * Example: If you book a ticket and system crashes, the booking should still be confirmed when it comes back online.

---
✅ **In summary**:

* **Atomicity** → via transaction logs & rollbacks
* **Consistency** → via constraints & rules
* **Isolation** → via locks & concurrency control
* **Durability** → via logs, checkpoints, and recovery mechanisms

### Check Keyword
> “`CHECK` is a declarative constraint that validates a Boolean rule on every row at write time (Insert or update ). It enforces domain and business rules like ranges, enums, and cross-column conditions, is cheaper and safer than triggers for row invariants, and works with `NOT NULL` and other constraints to keep the data valid.”

**How it works**

* If the predicate is `TRUE` the row is accepted.
* If `FALSE` the statement fails.
* If `UNKNOWN` due to `NULL`, most engines treat it as pass. Use `NOT NULL` to block `NULL`s.

**Syntax**

```sql
-- column-level
CREATE TABLE employee (
  emp_id INT PRIMARY KEY,
  salary NUMERIC(12,2) CHECK (salary >= 0),       -- domain rule
  rating INT CHECK (rating BETWEEN 1 AND 5)       -- 1..5 inclusive
);

-- table-level (can use multiple columns)
CREATE TABLE booking (
  id INT PRIMARY KEY,
  start_at TIMESTAMP NOT NULL,
  end_at   TIMESTAMP,
  CHECK (end_at IS NULL OR end_at >= start_at)    -- cross-column rule
);

-- named constraints
CREATE TABLE order_hdr (
  id INT PRIMARY KEY,
  status TEXT NOT NULL,
  paid_at TIMESTAMP,
  CONSTRAINT chk_paid_when_status_paid
    CHECK (status <> 'PAID' OR paid_at IS NOT NULL)
);
```
**CONSTRAINT keyword (CONSTRAINT name) above is used so errors are readable and maintainable.**

| Aspect          | **CONSTRAINT**                                                                                                                                                                                                       | **CHECK**                                                                                                    |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Definition**  | A **keyword** used to define rules (integrity constraints) on a table. It is a **general mechanism** to apply different types of restrictions like `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `CHECK`, `NOT NULL`, etc. | A **specific type of constraint** used to validate data against a **Boolean condition** (e.g., salary > 0).  |
| **Scope**       | Umbrella term – covers **all constraints** (PK, FK, UNIQUE, CHECK, NOT NULL, DEFAULT).                                                                                                                               | Only enforces a **condition on values** in a column or across multiple columns.                              |
| **Usage**       | Used when **defining any rule** on a table/column.                                                                                                                                                                   | Used when **validating data** against a logical expression.                                                  |
| **Example**     | `sql CREATE TABLE Employee ( emp_id INT CONSTRAINT pk_emp PRIMARY KEY, emp_name VARCHAR(50) CONSTRAINT nn_name NOT NULL ); `                                                                                         | `sql CREATE TABLE Product ( product_id INT, price DECIMAL(10,2) CONSTRAINT chk_price CHECK (price >= 0) ); ` |
| **Flexibility** | Can define multiple different constraint types.                                                                                                                                                                      | Only checks whether inserted/updated data satisfies the given condition.                                     |
| **Purpose**     | To **enforce data integrity** at table/column level (structural + relational).                                                                                                                                       | To **restrict data values** using logical conditions.                                                        |

## 📌 **Indexing in DBMS**

### 🔹 **Definition**

Indexing is a **data structure technique** used to quickly locate and access data in a database. It works like an index in a book → speeds up searches instead of scanning every record (full table scan).

Indexing is used to optimise the performance of a database by minimising the number of disk accesses required when a query is processed.

---

### 🔹 **Why Indexing?**

* **Faster query execution** (search, update, delete).
* **Improves performance** of `WHERE`, `ORDER BY`, `JOIN`.
* **Reduces disk I/O**.
* **Drawback**: Takes extra storage & overhead for updates (insert/delete must update index too).

---

### 🔹 **Types of Indexing**

### 1. **Primary Index**

* Built automatically on **primary key**.
* One index per table.
* Records are stored in **sorted order of primary key**.

### 2. **Secondary Index**

* Created manually on **non-primary attributes**.
* Allows **multiple indexes per table**.
* Supports searching on non-key columns.

### 3. **Clustered Index**

* **Sorts and stores** rows physically in table based on index key.
* Only **one clustered index** per table (since data can be stored one way).

### 4. **Non-Clustered Index**

* Separate structure; stores **pointers to data** instead of actual rows.
* Multiple non-clustered indexes can exist.
### 5. **Multilevel Index**
* Uses multiple levels of indexing (like B+ trees) for large datasets.
---
### **Dense vs Sparse Index**

* **Dense Index** → Every record has an entry in index. (Fast lookup, more space).
* **Sparse Index** → Only some records have index entries. (Less space, slightly slower).


### 🔹 **Index Data Structures**

1. **B-Tree Index**

   * Balanced tree; keeps data sorted.
   * Good for range queries.

2. **B+ Tree Index** (Most used)

   * Leaf nodes hold actual data pointers.
   * Supports **range & equality** queries efficiently.

3. **Hash Index**

   * Uses hashing function.
   * Good for **equality search** (e.g., `WHERE id = 10`).
   * Not suitable for range queries.

---

### 🔹 **Advantages**

* Very fast search, retrieval, and join.
* Reduces I/O operations.
* Makes sorting and grouping faster.

### 🔹 **Disadvantages**

* Extra space required.
* Slows down **insert, update, delete** (index must be updated).
* Poor choice for small tables.

---

### 🔹 **When to Use Indexing**

✅ Large tables.
✅ Columns used frequently in `WHERE`, `JOIN`, `GROUP BY`, `ORDER BY`.
✅ High read operations.

❌ Not useful for small tables.
❌ Columns with high updates.
❌ Columns with very low selectivity (like gender = M/F).

---
### ✅ **In Short**

* **Index = Shortcut to data**.
* **Types** → Primary, Secondary, Clustered, Non-clustered, Dense, Sparse.
* **Structures** → B-Tree, B+Tree, Hash.
* **Trade-off** → Fast reads 🔄 Slower writes & extra space.
* 
---
### 📌 **Types of Indexing in DBMS (with Examples)**

###3 1️⃣ **Primary Index**

* Automatically created on the **primary key**.
* Table rows are stored in **sorted order** of the primary key.

**Example**

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Dept VARCHAR(20)
);
```

👉 Oracle/MySQL automatically creates a **primary index** on `StudentID`.

---

#### 2️⃣ **Secondary Index**

* Created manually on a **non-primary column** to speed up queries.

**Example**

```sql
CREATE INDEX idx_student_dept 
ON Students(Dept);
```

👉 Useful if queries like `SELECT * FROM Students WHERE Dept = 'CSE';` are frequent.

---

#### 3️⃣ **Clustered Index**

* Data rows are **physically stored** in the order of the index key.
* Only **one clustered index per table** (because rows can be ordered in one way).

**Example (SQL Server / MySQL InnoDB)**

```sql
CREATE CLUSTERED INDEX idx_student_name 
ON Students(Name);
```

👉 Table rows will be physically ordered by `Name`.

---

#### 4️⃣ **Non-Clustered Index**

* Stores a **separate index structure** with pointers to the data.
* Multiple non-clustered indexes can exist on a table.

**Example**

```sql
CREATE NONCLUSTERED INDEX idx_student_name 
ON Students(Name);
```

👉 Index stores (Name + RowPointer), and pointer refers back to actual row.

---

#### 5️⃣ **Unique Index**

* Ensures all values in the column are **unique**.
* Created automatically on **PRIMARY KEY** and **UNIQUE** constraints.

**Example**

```sql
CREATE UNIQUE INDEX idx_student_email 
ON Students(Email);
```

👉 Guarantees no two students have the same Email.

---

#### 6️⃣ **Dense vs Sparse Index**

* **Dense Index** → Every record has an entry.
* **Sparse Index** → Only some records have entries (common with primary indexes).

**Example**

* **Dense**: Index has every student’s `StudentID`.
* **Sparse**: Index only has first `StudentID` of each block/page.

---

#### 7️⃣ **B-Tree Index**

* Default in most RDBMS (Oracle, MySQL, SQL Server).
* Balanced tree → good for **range queries**.

**Example**

```sql
CREATE INDEX idx_student_btree 
ON Students(StudentID);
```

---

#### 8️⃣ **Bitmap Index (Oracle-specific)**

* Uses **bitmaps** instead of row pointers.
* Best for **low-cardinality columns** (like Gender, Yes/No).

**Example (Oracle)**

```sql
CREATE BITMAP INDEX idx_student_gender 
ON Students(Gender);
```

---

#### 9️⃣ **Hash Index**

* Uses a **hash function** → great for equality search (`=`), not ranges.
* Common in **NoSQL** and some RDBMS (like PostgreSQL).

**Example (PostgreSQL)**

```sql
CREATE INDEX idx_student_hash 
ON Students USING HASH(StudentID);
```

---


## 📌 **NoSQL Databases**

### 🔹 **Definition**

* **NoSQL (Not Only SQL)** databases are **non-relational databases** designed for **scalability, flexibility, and high performance**.
* They do not strictly follow relational DBMS principles (tables, schemas, joins).
* They are schema-less or have dynamic schema and can handle **unstructured / semi-structured data** (JSON, XML, key-value).



### 🔹 **Why NoSQL?**

* Handle **Big Data** (huge volume, variety, velocity).
* **Scalable**: Easily distribute data across servers (horizontal scaling).
* **Flexible**: No fixed schema; data model can evolve easily.
* **Fast**: Optimized for specific use cases (key lookups, document queries, graphs).
* Used in **social media, IoT, real-time apps, e-commerce, recommendation systems**.

1. **Key-Value Stores**

* Data stored as key–value pairs.
* Very fast lookups, simple schema.
* **Examples:**
  * Redis
  * Amazon DynamoDB
  * Riak KV
  * Oracle NoSQL Database
  * Aerospike
  * Berkeley DB
  * Voldemort

2. **Document Stores**

* Data stored as documents (JSON, BSON, XML).
* Flexible schema: each document can have different structure.
* **Examples:**
  * MongoDB
  * CouchDB
  * Couchbase
  * Amazon DocumentDB
  * RethinkDB
  * RavenDB
  * MarkLogic
  * ArangoDB (multi-model, supports documents)
 
 3. **Column-Oriented Stores**

* Store data in **columns instead of rows**.
* Optimized for analytical queries and large datasets.
* **Examples:**
  * Apache Cassandra
  * HBase (Hadoop ecosystem)
  * ScyllaDB
  * Google Bigtable
  * Hypertable
  * Accumulo

 4. **Graph Databases**
* Store data as **nodes (entities)** and **edges (relationships)**.
* Best for social networks, recommendations, fraud detection.
* **Examples:**
  * Neo4j
  * Amazon Neptune
  * OrientDB (multi-model, strong graph support)
  * ArangoDB
  * Titan / JanusGraph
  * AllegroGraph
  * TigerGraph

5. **Multi-Model Databases**
* Support more than one NoSQL model (document + graph + key-value).
* **Examples:**
  * ArangoDB (document + graph + key-value)
  * OrientDB (document + graph)
  * Cosmos DB (Microsoft, supports key-value, column, document, graph)
  * MarkLogic

6. **Time-Series Databases**
* Specialized for **time-stamped data** (IoT, monitoring, finance).
* Optimized for high write throughput and time-range queries.
* **Examples:**
  * InfluxDB
  * TimescaleDB (SQL + time-series)
  * OpenTSDB
  * KairosDB

7. **Object-Oriented Databases**
* Store data as **objects** (like in OOP languages).
* Objects persist with attributes and methods.
* **Examples:**
  * db4o
  * ObjectDB

### 🔹 **Features of NoSQL**

* **Schema-less / flexible schema**.
* **Horizontal scaling** (add more machines instead of upgrading one).
* **Replication & partitioning** for high availability.
* **Eventual consistency** (CAP theorem → often prefer Availability + Partition tolerance over strict Consistency).
* Supports **real-time analytics**.



### 🔹 **Advantages**

✅ Handles massive, varied, unstructured data.
✅ Scales horizontally (cloud-friendly).
✅ High performance for read/write operations.
✅ Flexible schema → easy to adapt.

### 🔹 **Disadvantages**

❌ Weaker consistency compared to SQL (many follow **BASE**: Basically Available, Soft-state, Eventually consistent).
❌ No standard query language (varies by DB).
❌ Limited complex transaction support (compared to SQL ACID).
❌ Learning curve.

### 🔹 **When to Use NoSQL**

* Applications with **Big Data** (e.g., Facebook, Netflix, Amazon).
* Systems needing **fast reads/writes**.
* **Real-time apps** (chat apps, recommendation engines).
* **Flexible/ evolving schema** requirements.



### ✅ **In Short**

* **NoSQL = Not Only SQL** → non-relational, schema-less, distributed DB.
* **Types** → Key-Value, Document, Column, Graph.
* **Trade-off** → High scalability & speed 🔄 Weaker consistency & transactions.
* Popular DBs → MongoDB, Cassandra, Redis, Neo4j, CouchDB, DynamoDB.

## **BASE in NoSQL**

### **Definition**

In NoSQL databases, **BASE** is an alternative to the strict **ACID** model of relational databases. It relaxes consistency requirements to achieve high availability and scalability in distributed systems.

**BASE stands for:**

* **Basically Available** → System guarantees availability, even if parts fail.
* **Soft State** → Data may be temporarily inconsistent, as updates propagate asynchronously.
* **Eventual Consistency** → The system will become consistent over time, if no new updates are made.



### **Why BASE instead of ACID?**

* ACID ensures strict consistency, reliability, and correctness.
* In distributed environments (e.g., large-scale web apps), strict ACID limits performance and scalability.
* BASE sacrifices **immediate consistency** for **availability and partition tolerance**, aligning with the **CAP theorem**.

 ## **CAP vs ACID/BASE mapping**

### **1. ACID (SQL / RDBMS)**

* **Strong Consistency** → Always correct and reliable.
* Fits best with **CP** in CAP theorem:

  * **C**: Consistency maintained
  * **P**: Partition tolerance required in distributed systems
  * **A**: Availability sometimes sacrificed (e.g., if nodes are partitioned, system may reject requests to preserve consistency).
* **Example**: Traditional RDBMS (PostgreSQL, Oracle, MySQL with strict transactions).

### **2. BASE (NoSQL / Distributed DBs)**

* **Eventual Consistency** → Availability prioritized, consistency relaxed.
* Fits best with **AP** in CAP theorem:

  * **A**: High availability guaranteed
  * **P**: Partition tolerance ensured
  * **C**: Consistency is eventual, not immediate
* **Example**: Cassandra, DynamoDB, Riak.

### **3. Hybrid Systems**

Some modern databases allow **tunable consistency** → user chooses C vs A per operation.

* **Examples**: MongoDB, Cosmos DB.

### **Interview-Ready Summary Table**

| Model      | Philosophy                                            | CAP Mapping                                                            | Example DBs                        |
| ---------- | ----------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------- |
| **ACID**   | Strong consistency, reliable transactions             | **CP** (Consistency + Partition tolerance, may sacrifice Availability) | Oracle, MySQL (InnoDB), PostgreSQL |
| **BASE**   | Basically available, soft state, eventual consistency | **AP** (Availability + Partition tolerance, relaxed Consistency)       | Cassandra, DynamoDB, Riak          |
| **Hybrid** | Tunable consistency (choose per query)                | Can behave as CP or AP depending on config                             | MongoDB, Cosmos DB                 |


## 📌 **CAP Theorem in DBMS/NoSQL**

### 🔹 **Definition**

Proposed by **Eric Brewer**, CAP theorem states that in a **distributed database system**, you can only guarantee **two** of the following three properties at the same time:

1. **Consistency (C)**

   * Every read receives the **most recent write** (all nodes see the same data).
   * Example: If you update your profile picture, everyone should see the latest one instantly.

2. **Availability (A)**

   * Every request gets a **response**, even if it may not be the latest data.
   * Example: Even during server issues, your profile still loads (maybe old data).

3. **Partition Tolerance (P)**

   * System continues to work even if there is a **network partition** (communication failure between nodes).
   * Example: If servers in two regions cannot talk to each other, both should still keep working.

---

### 🔹 **CAP in Simple Words**

* In a distributed system, **network failures are inevitable**, so **Partition Tolerance (P)** is a must.
* That means databases must **choose between Consistency (C) and Availability (A)**.

---

### 🔹 **CAP Theorem & NoSQL**

#### 1. **CP (Consistency + Partition Tolerance)**

* Guarantees **correct data**, but might sacrifice **availability** during failures.
* Example: **HBase, MongoDB (in some configs), Redis (clustered)**.
* Use case: Banking, payments (must be consistent).

#### 2. **AP (Availability + Partition Tolerance)**

* Guarantees system is **always up**, but data may be **eventually consistent** (not always latest).
* Example: **Cassandra, DynamoDB, CouchDB, Riak**.
* Use case: Social media feeds, shopping carts, recommendation engines.

#### 3. **CA (Consistency + Availability)**

* Works well in a **single-node system** (not distributed).
* Not practical in large distributed systems, since partition failures are inevitable.
* Example: **Traditional RDBMS (Oracle, MySQL in standalone mode)**.

---

### 🔹 **Relation Between NoSQL & CAP**

* NoSQL databases are **distributed systems**, so **Partition Tolerance (P)** is mandatory.
* That forces a choice:

  * Some NoSQL DBs are **CP** (prefer consistency over availability).
  * Some NoSQL DBs are **AP** (prefer availability over consistency).
* Hence, **NoSQL design decisions are guided by CAP theorem**.

---

### ✅ **In Short**

* **CAP Theorem**: Only 2 of **Consistency, Availability, Partition Tolerance** can be achieved simultaneously.
* **NoSQL DBs**: Must choose between **CP** or **AP** (since P is required).
* **Trade-off**:

  * CP → Accurate but may be unavailable.
  * AP → Always available but may return stale data.

---
👉 Example to remember:

* **Banking app** → needs **CP** (accuracy > availability).
* **Instagram/Netflix** → needs **AP** (availability > strict accuracy, eventual consistency is fine).
---
### 📌 **Examples of Databases under CAP**

🔹 **CA (Consistency + Availability, No Partition Tolerance)**

* Works well only in **single-node** or tightly coupled systems (since real-world distributed systems must tolerate partitions).
* **Examples**:

  * **Traditional RDBMS (non-distributed)** → Oracle, PostgreSQL, MySQL (standalone mode).
  * They guarantee **consistency** and **availability** as long as no partition occurs.

---

🔹 **CP (Consistency + Partition Tolerance, sacrificing Availability)**

* Prioritizes **correct data** even if some nodes become unavailable.
* During a network partition, some requests may be denied (not available).
* **Examples**:

  * **HBase**
  * **MongoDB (default configs)**
  * **Redis (clustered, with strong consistency mode)**
* **Use case**: Banking systems, stock trading, payment gateways (where stale/wrong data is unacceptable).

---

🔹 **AP (Availability + Partition Tolerance, sacrificing Consistency)**

* Prioritizes **system uptime** → every request gets a response, even if data is slightly outdated.
* Uses **eventual consistency** (data becomes consistent over time).
* **Examples**:

  * **Cassandra**
  * **DynamoDB (Amazon)**
  * **CouchDB**
  * **Riak**
* **Use case**: Social media, shopping carts, recommendation systems (stale data is tolerable).
---

## View (Virtual Table)
  A **View** in DBMS is a **virtual table** based on the result of an SQL query. It does not store data itself but displays data stored in one or more base tables.

---

### 🔹 **Key Points (Interview Version)**

1. **Definition** – A view is a stored query that acts like a table. It shows data dynamically from underlying tables.
2. **Storage** – Only the query definition is stored, not the actual data (unless it is a materialized view).
3. **Types of Views**

   * **Simple View** → Based on a single table, no functions or group of data.
   * **Complex View** → Based on multiple tables, may contain joins, aggregations.
   * **Materialized View** → Stores actual data physically for faster access, needs refresh.
4. **Advantages**

   * Data security → Restrict access to specific columns/rows.
   * Simplifies complex queries → Users query the view instead of writing long SQL.
   * Logical independence → Underlying schema can change, but the view hides complexity.
5. **Limitations**

   * Some views are not updatable (especially those with joins, GROUP BY).
   * Performance overhead since query runs every time (except materialized views).

---

### 🔹 **Example**

```sql
-- Simple view showing only selected columns
CREATE VIEW Employee_View AS
SELECT emp_id, name, department
FROM Employees
WHERE department = 'IT';

-- Using the view
SELECT * FROM Employee_View;
```

This shows only IT employees without exposing the full `Employees` table.

---

## 📌 **Partitioning vs Sharding in DBMS**

---

### 🔹 1. Partitioning

**Definition**
Partitioning = **splitting a large table (or index) into smaller pieces (partitions)** within the **same database/server**.

* Logically: still one table.
* Physically: stored as multiple segments.

**Types of Partitioning**

* **Horizontal partitioning** → split rows (e.g., Orders by year).
* **Vertical partitioning** → split columns (e.g., Customer info vs Contact info).
* **Range / List / Hash / Composite partitioning**.

**Example**
Orders table split by year:

* Partition 1 → Orders\_2022
* Partition 2 → Orders\_2023

👉 Goal: **Performance optimization & manageability**.

---

### 🔹 2. Sharding

**Definition**
Sharding = **distributing partitions across multiple servers/nodes (databases)**.

* Each shard = an independent database with its own subset of data.
* Together, shards form the complete dataset.
* Common in distributed systems & NoSQL DBs (MongoDB, Cassandra, DynamoDB).

**Example**
Users table split by region:

* Shard 1 → Users from Asia
* Shard 2 → Users from Europe
* Shard 3 → Users from America

👉 Goal: **Horizontal scalability & high availability**.

---

### 🔹 3. Key Differences

| Feature        | Partitioning                                               | Sharding                                                       |
| -------------- | ---------------------------------------------------------- | -------------------------------------------------------------- |
| **Definition** | Splitting data within a single database instance           | Splitting data across multiple databases/servers               |
| **Level**      | **Database-internal** (DB engine manages it)               | **Application/distribution-level** (app or middleware decides) |
| **Management** | Centralized (one DB server)                                | Decentralized (many DB servers)                                |
| **Use Case**   | Performance optimization, easier query execution, archival | Scalability across machines, very large datasets, global apps  |
| **Example**    | Oracle/PostgreSQL Partitioned Tables                       | MongoDB/DynamoDB Shards                                        |

---

### 🔹 4. In Simple Words

* **Partitioning**: Cutting a big pizza into slices 🍕 (all slices still on one plate).
* **Sharding**: Putting slices on **different plates (servers)** and distributing them to people.

---

### ✅ **Interview-ready Answer**

> *“Partitioning splits a large table into smaller parts within the same database for performance and manageability, while sharding distributes those partitions across multiple servers for horizontal scalability. Partitioning is DB-internal, sharding is cross-server. For example, partitioning orders by year in one Oracle DB is partitioning, but storing customers by region on separate servers is sharding.”*

---
## Types of Decomposition
In **DBMS normalization**, decomposition means breaking a relation (table) into two or more relations.

### 🔹 **1. Lossless-Join Decomposition**

* The decomposed tables can be **joined back to get the original table without losing information**.
* Ensures no spurious tuples appear when relations are joined.
* **Condition:** Common attributes between decomposed relations must form a **key** in at least one relation.
* **Example:**

  ```
  R(A, B, C)
  Decompose into R1(A, B), R2(A, C)
  ```

  Here, `A` is a key → lossless.

---

### 🔹 **2. Lossy (Lossy-Join) Decomposition**

* When decomposition **loses some information** or produces **extra tuples** after joining.
* Not desirable in practice.
* **Example:**

  ```
  R(A, B, C)
  Decompose into R1(A, B), R2(B, C)
  ```

  If `B` is not a key → join may produce wrong results.

---

### 🔹 **3. Dependency-Preserving Decomposition**

* Ensures that all functional dependencies from the original relation are still enforceable after decomposition.
* Important for maintaining data integrity without needing costly joins.
* **Note:** A decomposition can be lossless but not dependency-preserving, or dependency-preserving but not lossless. Ideally, we want both.



✅ Example 1 – Dependency Preserved
```
R(A, B, C)
FDs: A → B, B → C
```
We decompose `R` into:

* `R1(A, B)`
* `R2(B, C)`

* In `R1`: A → B is preserved.
* In `R2`: B → C is preserved.

👉 Both dependencies are preserved **without joining** → This is **dependency-preserving decomposition**.

---

 ❌ Example 2 – Not Dependency Preserving
```
R(A, B, C)
FDs: A → B, B → C, A → C
```

Decompose into:

* `R1(A, B)`
* `R2(B, C)`

Now check FDs:

* `A → B` (preserved in R1 ✅)
* `B → C` (preserved in R2 ✅)
* `A → C` ❌ not present in either R1 or R2.

  * To check `A → C`, we’d need to join `R1` and `R2`.

👉 This decomposition is **lossless** (if `B` is a key in `R2`), but **not dependency-preserving**.

---

## 📌 Schedule 

> *“A schedule in DBMS is the sequence of operations from multiple transactions arranged by the system. It is needed to control concurrency, maintain consistency, and avoid problems like lost updates or dirty reads. By analyzing schedules, the DBMS ensures transactions follow a safe order and the outcome is equivalent to serial execution.”*

### 🔹 Definition

* A **schedule** is an **order (sequence) of operations** from one or more transactions arranged by the DBMS.
* Operations usually include:

  * **Read (R)**
  * **Write (W)**
  * **Commit (C)**
  * **Abort (A)**

👉 It tells us *how multiple transactions are executed together*.


---

### 📌 **Why is a Schedule Needed?**

#### 🔹 1. Concurrency Control

* In a multi-user system, **many transactions run at the same time**.
* If they all directly accessed data, it could lead to **conflicts and anomalies** (lost updates, dirty reads, uncommitted data).
* A **schedule defines the order** of execution, so DBMS can **detect and prevent conflicts**.

---

#### 🔹 2. Serializability

* The DBMS must ensure that a concurrent schedule is **equivalent to some serial execution** (one transaction after another).
* This ensures **consistency** and preserves **ACID properties**.

---

#### 🔹 3. Avoiding Anomalies

Without proper scheduling:

* **Lost Update** → Two transactions overwrite each other’s changes.
* **Dirty Read** → A transaction reads uncommitted data from another.
* **Inconsistent Read** → One transaction sees partial updates from another.

Schedules help DBMS **decide the safe order** to avoid these.

---


### **Serial Schedule**

   * Transactions execute one after another, no interleaving.
   * Always consistent, but poor concurrency.

### **Concurrent / Non-Serial Schedule**

   * Operations interleaved.
   * Needs concurrency control to avoid anomalies.

---
## **Types of schedules** by two ways:

1. **Correctness (Serializability)**
2. **Failure safety (Recoverability)**
---

### 1) On the basis of **Serializability**

#### A. Conflict-serializable (CSR)

**Idea:** The interleaved schedule is equivalent to some serial order after swapping only **non-conflicting** operations.

* **Conflicting pairs (same item, different txns):** `R–W`, `W–R`, `W–W`. (`R–R` never conflicts.)
* **Test (easy, exam favorite):** Build a **precedence graph**

  * Nodes = transactions, edge `Ti → Tj` if an op of `Ti` precedes and conflicts with one of `Tj`.
  * **Acyclic ⇒ conflict-serializable.** The topological order gives the equivalent serial order.
* **Why we like it:** Fast to check; most concurrency control (e.g., **Strict 2PL**) guarantees CSR.

**Mini example (CSR):**
`R1(X)  R2(X)  W1(X)  R2(Y)  W2(Y)  C1  C2` → graph has no cycle ⇒ equivalent to serial `T1 → T2`.

---

#### B. View-serializable (VSR)

**Idea:** Equivalent to some serial order if three **view conditions** match:

1. **Reads of initial values**: same txns read the “initial” value of each item.
2. **Reads-from**: if `Ti` reads a value written by `Tj` in one schedule, it must do so in the other.
3. **Final writer** of each item is the same.

* **Stronger vs. CSR?** **VSR ⊃ CSR** (there are VSR schedules that are **not** CSR).
* **Why not always used?** Testing VSR is computationally hard (classic result), so DBs target CSR.

**Classic VSR-but-not-CSR example (uses a “blind write”):**
`W1(X);  W2(X);  W1(X)`
Precedence graph has a cycle (`T1→T2` from the first two writes, `T2→T1` from `W2(X)` before the last `W1(X)`), so **not CSR**.
But it’s **view-equivalent** to serial `T2 → T1` (no reads; final writer is `T1` in both).

---

### 2) On the basis of **Recoverability**

Think “what happens if someone aborts?”

#### A. Recoverable

**Rule:** If `Ti` **reads** a value written by `Tj`, then **`Ti` must commit only after `Tj` commits**.

* Prevents committing based on data that might later be rolled back.

**Non-recoverable counterexample:**
`W1(X);  R2(X);  C2;  A1` → `T2` committed a value that `T1` later aborted ⇒ **unsafe**.

---

#### B. Cascadeless

**Rule:** A transaction **never reads uncommitted data** (no “dirty reads”).

* If `Ti` reads from `Tj`, then **`Tj` must have committed before that read**.
* Eliminates **cascading aborts** (where many dependents must abort because one writer aborts).
* **All cascadeless schedules are recoverable** (but not conversely).

**Cascadeless but not strict example (has a dirty write):**
`W1(X);  W2(X);  C1;  C2`
No one **reads** uncommitted data ⇒ cascadeless. But `T2` overwrote `X` while `T1` was uncommitted ⇒ **not strict**.

---

#### C. Strict

**Rule:** If `Ti` writes `X`, **no other txn may read or write `X` until `Ti` commits/aborts**.

* Forbids **dirty reads** *and* **dirty writes**.
* Easiest to recover: if `Ti` aborts, no one has seen or overwritten its uncommitted data.
* **Strict ⇒ Cascadeless ⇒ Recoverable** (proper subset chain).

**Typical way to get Strict:** **Strict 2-Phase Locking (S2PL)**—hold write locks till commit.

**Strict example:**
`W1(X);  C1;  R2(X);  W2(X);  C2`
`T2` touches `X` only after `T1` commits.

---

## The two families together (how they relate)

* **Serializability** = logical **correctness under concurrency**.
* **Recoverability** = **safety under failures/aborts**.

They’re orthogonal—but in practice many protocols give you both:

* **Strict 2PL** ⇒ **Conflict-serializable** **and** **Strict** (hence cascadeless & recoverable).
* **MVCC** systems (e.g., Read Committed/Serializable) avoid dirty reads; with proper write rules they provide cascadeless or strict behavior while ensuring serializability at chosen isolation levels.

---
##**Concurrency Control in DBMS**

> Concurrency control is the mechanism to ensure correct and consistent execution of multiple transactions running **concurrently**.

>Concurrency control = **set of protocols** that ensure safe, consistent, and efficient concurrent transaction execution by enforcing **serializability** and **recoverability**.

---

### 🔹 Why Concurrency Control?

* In a multi-user DBMS, many transactions run in parallel.
* Without control, problems like:

  1. **Lost Update** → Two transactions overwrite each other’s changes.
  2. **Dirty Read** → A transaction reads uncommitted data from another.
  3. **Unrepeatable Read** → A value read twice gives different results because another transaction modified it in between.
  4. **Phantom Read** → A re-executed query returns different results because another transaction inserted/deleted rows.

---

### 🔹 Goals

* Maintain **Isolation** (ACID property).
* Ensure **Serializability** of schedules.
* Avoid anomalies like cascading rollbacks.
* Maximize throughput and resource utilization.

---

### 🔹 Concurrency Control Techniques

#### 1. **Lock-based Protocols**

Transactions acquire locks before accessing data.

* **Binary Locks**: Lock = 0 (unlocked), 1 (locked).
* **Shared/Exclusive Locks (S/X locks)**:

  * Shared lock → multiple reads allowed.
  * Exclusive lock → only one writer.
* **Two-Phase Locking (2PL)**:

  * Growing phase: acquire locks.
  * Shrinking phase: release locks.
  * Guarantees conflict-serializability.
* **Strict 2PL**: Keeps write locks till commit → avoids cascading aborts.

---

#### 2. **Timestamp-based Protocols**

Each transaction gets a **timestamp**. Ordering of operations is based on timestamps.

* Ensures serializability by always executing as if transactions are in timestamp order.
* Uses **Read Timestamp (RTS)** and **Write Timestamp (WTS)** for each data item.

---

#### 3. **Validation-based Protocols (Optimistic Concurrency Control)**

* Assumes conflicts are rare.
* Execution divided into 3 phases:

  1. **Read Phase**: Transaction reads and stores updates locally.
  2. **Validation Phase**: Check if transaction conflicts with others.
  3. **Write Phase**: If valid, apply changes to DB.
* Works well in read-heavy workloads.

---

#### 4. **Multiversion Concurrency Control (MVCC)**

* Keeps multiple versions of data items.
* Readers access old versions without blocking writers.
* Used in PostgreSQL, Oracle, etc.

---
## 🔹 Concurrency Control and Schedule Types

* Ensures schedules are **serializable** (conflict/view).
* Ensures schedules are **recoverable** (recoverable, cascadeless, strict).

---
