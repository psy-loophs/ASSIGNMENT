📚 Comparative Study of Relational, Hierarchical and Network Data Models

«Subject: Database Management System (DBMS)
Topic: Comparative Study of Data Models and Database Security»

---

📑 Table of Contents

- "1. Introduction" (#-1-introduction)
- "2. Relational Data Model" (#-2-relational-data-model)
- "3. Hierarchical Data Model" (#-3-hierarchical-data-model)
- "4. Network Data Model" (#-4-network-data-model)
- "5. Comparative Study" (#-5-comparative-study)
- "6. Database Security: Issues and Solutions" (#-6-database-security-issues-and-solutions)
- "7. Conclusion" (#-7-conclusion)

---

🔰 1. Introduction

A Database Management System (DBMS) is an essential part of modern computing used to store, organize, manage, and retrieve data efficiently.

Different data models provide different methods of organizing and representing information. The three important data models are:

- 🟦 Relational Data Model — Organizes data into tables.
- 🌳 Hierarchical Data Model — Organizes data into a tree structure.
- 🕸️ Network Data Model — Organizes data through interconnected records.

At the same time, database security plays a vital role in protecting stored information from unauthorized access, data theft, and loss.

Understanding these models and security measures helps in designing reliable, efficient, and secure database systems.

---

🟦 2. Relational Data Model

The relational data model represents data in the form of tables, also called relations. Each table consists of rows and columns.

- Rows: Known as tuples.
- Columns: Known as attributes.
- Primary Key: Uniquely identifies each record in a table.
- Foreign Key: Establishes a relationship between tables.

💡 Example

A student database may contain the following table:

Student ID| Name| Department
101| Arun| Computer Science
102| Anjali| Commerce
103| Rahul| Mathematics

✅ Advantages

- Simple and easy to understand.
- Reduces data redundancy through proper database design.
- Supports flexible data retrieval using Structured Query Language (SQL).
- Provides data integrity and security features.

❌ Disadvantages

- Complex queries involving multiple tables may require more processing.
- Highly interconnected data may require careful database design.

«Key Point: The relational model is widely used in business applications, banking systems, and student databases.»

---

🌳 3. Hierarchical Data Model

The hierarchical data model organizes data in the form of a tree structure consisting of parent and child records.

- A parent can have multiple children.
- Each child generally has only one parent.
- Data is accessed by following predefined paths through the hierarchy.

💡 Example

In a college database, a college may have several departments, and each department may contain multiple students.

                    COLLEGE
                       |
             +---------+---------+
             |                   |
        DEPARTMENT A         DEPARTMENT B
             |                   |
         +---+---+           +---+---+
         |       |           |       |
      STUDENT  STUDENT    STUDENT  STUDENT
        101      102        103      104

✅ Advantages

- Has a simple structure for parent-child relationships.
- Provides efficient access when relationships follow a fixed hierarchy.
- Suitable for representing organizational structures.

❌ Disadvantages

- Difficult to represent many-to-many relationships.
- Changes to the structure can be complicated.
- Accessing data outside predefined paths may be difficult.

«Key Point: The hierarchical model is suitable for data that naturally follows a tree-like structure.»

---

🕸️ 4. Network Data Model

The network data model represents data using a graph-like structure in which records are connected through links.

Unlike the hierarchical model, a child record can have multiple parent records.

It supports:

- One-to-one relationships
- One-to-many relationships
- Many-to-many relationships

💡 Example

In a college database, one student can enroll in several courses, and each course can have many students.

       STUDENT A -------- COURSE 1
           |                  |
           |                  |
           +-------------- COURSE 2
                              |
       STUDENT B -------------+
           |
           +-------------- COURSE 1

✅ Advantages

- Supports complex relationships between records.
- Handles many-to-many relationships effectively.
- Can provide efficient access through predefined links.

❌ Disadvantages

- More complex to design and maintain.
- Users may need to understand the links between records.
- Changes to the database structure can be difficult.

«Key Point: The network model is useful when records have complex and interconnected relationships.»

---

📊 5. Comparative Study

The following table highlights the major differences between the three data models.

Feature| Relational Model| Hierarchical Model| Network Model
Structure| Tables| Tree| Graph
Relationships| Through keys| Parent-child| Linked records
Multiple parents| Represented through relationships between tables| Generally not supported| Supported
Many-to-many relationships| Supported through related tables| Difficult to represent| Supported directly
Complexity| Relatively simple| Simple for hierarchical data| More complex
Data access| Queries using SQL| Traversal through a tree| Traversal through linked records
Flexibility| Flexible querying| Limited by the hierarchy| Supports complex connections
Common uses| Business and student databases| Hierarchical data structures| Complex interconnected records

📝 Summary

- Relational Model: Best known for its tabular structure and SQL-based querying.
- Hierarchical Model: Organizes records in a parent-child tree structure.
- Network Model: Connects records through links and supports multiple relationships.

---

🔐 6. Database Security: Issues and Solutions

Database security refers to the methods and practices used to protect databases from unauthorized access, misuse, data loss, and cyberattacks.

Effective database security helps maintain the three important principles of information security:

Principle| Meaning
🔒 Confidentiality| Ensures that information is accessible only to authorized users.
🛡️ Integrity| Ensures that data remains accurate and is not modified without authorization.
⚡ Availability| Ensures that authorized users can access data when needed.

⚠️ 6.1 Major Database Security Issues

1. 🚫 Unauthorized Access

Unauthorized users may access confidential information without permission, potentially exposing sensitive data.

2. 🗃️ Data Theft and Leakage

Sensitive information, such as personal details, passwords, and financial records, may be stolen or exposed.

3. 💻 SQL Injection

Attackers may insert malicious SQL commands through vulnerable applications to access, modify, or delete database information.

4. ✏️ Unauthorized Data Modification

Unauthorized changes to records can affect the accuracy and reliability of the database.

5. 🦠 Malware and Ransomware

Malicious software can damage database files, steal information, or make data inaccessible.

6. 👤 Insider Threats

Employees or other authorized users may misuse their access privileges to steal, disclose, or modify data.

---

🛡️ 6.2 Solutions to Database Security Issues

1. 🔑 Authentication

Use strong passwords and multi-factor authentication (MFA) to verify the identity of users before allowing access.

2. 👮 Authorization and Access Control

Assign permissions according to users' responsibilities. Users should access only the data required for their work.

3. 🔒 Data Encryption

Encrypt sensitive data both when it is stored (data at rest) and when it is transmitted over a network (data in transit).

4. 💾 Regular Backup and Recovery

Maintain regular backups and test recovery procedures to restore data after accidental deletion, system failure, or cyberattacks.

5. 🔄 Software Updates

Regularly update the DBMS, operating system, and related applications to fix known security vulnerabilities.

6. 🛠️ Protection Against SQL Injection

Use parameterized queries or prepared statements, validate inputs, and avoid constructing SQL queries directly from untrusted user input.

📌 Database Security Best Practices

- [x] Use strong authentication mechanisms.
- [x] Apply appropriate access controls.
- [x] Encrypt sensitive information.
- [x] Maintain regular database backups.
- [x] Install security updates promptly.
- [x] Protect applications against SQL injection.

---

🎯 7. Conclusion

In conclusion, database models and database security are important aspects of database management.

The relational model organizes data into tables, the hierarchical model organizes data into a tree structure, and the network model represents data through interconnected records. Each model has its own advantages and limitations depending on the application requirements.

Similarly, implementing security measures such as authentication, access control, encryption, and regular backups helps protect databases from various threats.

Therefore, selecting a suitable data model and implementing effective security practices are essential for maintaining the efficiency, reliability, integrity, and safety of database systems.

---

<div align="center">📘 END OF ASSIGNMENT

Database Management System (DBMS)

</div>
