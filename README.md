# Database Architecture and Concepts Notes

## 1. Introduction to Databases
A **database** is a structured collection of data that can be easily accessed, managed, and updated. Databases are used in almost every modern software application to store data efficiently and consistently.

- **DBMS (Database Management System):** Software that handles the creation, retrieval, updating, and management of data in databases. Examples include MySQL, PostgreSQL, Oracle, and MongoDB.
- Databases are the backbone of applications such as banking systems, online stores, mobile apps, and more.

---

## 2. CRISP-DM (Cross Industry Standard Process for Data Mining)
CRISP-DM is a widely used methodology that guides the process of carrying out data mining or data science projects. It provides a structured framework consisting of six phases:

### 1. Business Understanding
- Focuses on understanding project objectives and requirements from a business perspective.
- Determines business success criteria and defines project scope.

### 2. Data Understanding
- Involves initial data collection and familiarization.
- Helps identify data quality issues and discover first insights.

### 3. Data Preparation
- The most time-consuming phase where raw data is cleaned, integrated, and transformed.
- Includes tasks like handling missing values, encoding categorical variables, and formatting data.

### 4. Modeling
- Selecting and applying appropriate modeling techniques such as decision trees, clustering, regression, etc.
- Often involves tuning model parameters to optimize performance.

### 5. Evaluation
- Assessing the model's accuracy, precision, recall, or business value.
- Determines whether the model meets the business goals.

### 6. Deployment
- Putting the model or insights into practical use.
- Can involve creating dashboards, applications, or reporting tools.

### Supporting Activities:
- **Documentation**: Should be maintained throughout the project to record steps, decisions, and assumptions.
- **Presentation**: Often includes summaries, charts, or slides to convey findings to stakeholders.
- **Maintenance**: In deployment, set up monitoring systems and plan for periodic updates and retraining.

---

## 3. Terminologies in Databases

### Types of Data
| Type               | Description                                     | Examples                    |
|--------------------|-------------------------------------------------|-----------------------------|
| Structured         | Organized data in fixed fields, like tables     | SQL tables, Excel sheets    |
| Semi-Structured    | Partially organized with tags or keys           | JSON, XML, YAML             |
| Unstructured       | No predefined structure                         | Images, videos, PDFs        |

### Types of Databases
| Type                    | Description                                       | Common Tools                |
|-------------------------|---------------------------------------------------|-----------------------------|
| Relational (SQL)        | Uses tables with fixed schemas                    | MySQL, PostgreSQL, Oracle   |
| NoSQL                   | Flexible structure for varied data formats        | MongoDB, Cassandra, Redis   |
| Time-Series             | Optimized for time-stamped data                  | InfluxDB, TimescaleDB       |
| Graph                   | Stores data as nodes and relationships           | Neo4j, ArangoDB             |
| NewSQL                  | Hybrid of SQL's structure and NoSQL scalability  | Google Spanner, CockroachDB |

---

## 4. SQL vs NoSQL

| Feature             | SQL                              | NoSQL                               |
|---------------------|-----------------------------------|--------------------------------------|
| Structure           | Table-based with rows and columns| Document, key-value, graph, etc.     |
| Schema              | Predefined and fixed             | Dynamic and flexible                 |
| Scalability         | Vertical (scale up)              | Horizontal (scale out)               |
| Use Case            | Structured data, financial apps  | Big data, social networks, IoT       |
| Examples            | MySQL, Oracle, SQLite            | MongoDB, Cassandra, Firebase         |

---

## 5. OLTP vs OLAP

| Category                   | OLTP (Online Transaction Processing) | OLAP (Online Analytical Processing) |
|---------------------------|--------------------------------------|-------------------------------------|
| Goal                      | Manage day-to-day transactions       | Support complex analytical queries  |
| Users                     | Clerks, admin staff, customers       | Business analysts, decision-makers |
| Query Type                | Simple reads and writes              | Aggregations, joins, drill-down     |
| Data Volume               | Low to medium                        | High                                |
| Schema Design             | Highly normalized                    | Denormalized (star/snowflake)      |
| Examples                  | Banking systems, shopping carts      | Sales dashboards, BI tools         |

---

## 6. Single-Tier and Multi-Tier Architecture

### Single-Tier Architecture
- All components (UI, business logic, and data access) reside on the same layer.
- Often used in local desktop applications.
- Direct interaction with the database is possible.

**Advantages:**
- Easy to develop  
- Fast data access for single users

**Disadvantages:**
- Not scalable  
- Difficult to manage security and maintenance

### Multi-Tier Architecture
In this model, the system is split into separate layers, each handling a specific responsibility.

#### 2-Tier Architecture
- The client handles the user interface.
- The server hosts the database.
- The application logic is either embedded in the client or database.

#### 3-Tier Architecture
- **Presentation Layer (Client):** Interface the user interacts with.
- **Application Layer (Server):** Contains the logic and rules.
- **Data Layer (Database):** Responsible for data storage and retrieval.

**Advantages:**
- Improves maintainability and security  
- Supports more users simultaneously

**Disadvantages:**
- Increased complexity  
- More network overhead

---

## 7. Client-Server Model

The client-server model is a fundamental network architecture where the **client** requests services, and the **server** responds.

### How It Works
- A client (e.g., a web browser) sends a request over a network.
- A server (e.g., a web server or database server) processes and responds with data or content.

### Characteristics
- Centralized system: data is stored and managed at the server.
- Clients are typically thin (do minimal processing).
- Scales well with proper infrastructure.

### Real-World Examples
- Web browsing (Chrome requests a page from a web server)
- Email (email client connects to mail server)
- Database queries (application sends SQL to a DB server)

### Client-Server vs Peer-to-Peer
| Feature         | Client-Server               | Peer-to-Peer (P2P)            |
|------------------|------------------------------|-------------------------------|
| Roles            | Separated (client & server)  | Equal roles for all nodes     |
| Central Server   | Required                     | Not required                  |
| Examples         | Web apps, cloud services     | File sharing, blockchain      |
| Scalability      | High with proper setup       | High but harder to control    |


## 8. Anomalies and the Need for Normalization

### 🔍 What are Anomalies?
Anomalies are problems that arise when data is not stored in a well-structured format. These typically occur in poorly designed relational database tables.

There are three main types:

#### 1. Insertion Anomaly
Occurs when we cannot insert a data item because of the absence of another.

**Example:**
- You cannot insert a new student record unless you also provide course details.

#### 2. Update Anomaly
Occurs when redundant data exists and updates to one part lead to inconsistencies.

**Example:**
- If an instructor’s email is stored in multiple rows and one is updated incorrectly, inconsistency occurs.

#### 3. Deletion Anomaly
Occurs when deletion of one piece of information unintentionally deletes related important data.

**Example:**
- Deleting the last student enrolled in a course may delete the course information entirely.

---

### 9. Why Normalization?
**Normalization** is the process of organizing data to reduce redundancy and improve data integrity.

**Goals of Normalization:**
- Eliminate redundant data
- Ensure data dependencies make sense (data is stored logically)
- Avoid anomalies in insert, update, and delete operations


| Normal Form | Rule / Condition | Purpose / Benefit | Example |
|-------------|------------------|-------------------|---------|
| **1NF**     | All attributes must be atomic (indivisible). No repeating groups or arrays. | Eliminates duplicate columns and ensures a unique value in each field. | A table with multiple phone numbers in one field violates 1NF. |
| **2NF**     | Must be in 1NF and every non-prime attribute should be fully functionally dependent on the entire primary key. | Removes partial dependencies (important for composite keys). | Student-Course table: StudentName depends only on StudentID, not on the combination of (StudentID, CourseID). |
| **3NF**     | Must be in 2NF and all non-prime attributes should not depend on other non-prime attributes (i.e., no transitive dependencies). | Avoids indirect relationships that can cause anomalies. | If a table stores StudentID → DepartmentID → DepartmentName, then DepartmentName should be in another table. |
| **BCNF**    | A stronger version of 3NF: For every functional dependency X → Y, X should be a super key. | Eliminates anomalies not handled by 3NF when there are overlapping candidate keys. | In a table where both {Course, Instructor} and {Instructor, Time} are keys, splitting is required if Instructor is not a super key. |



---


