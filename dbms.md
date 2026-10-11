# ============================================================
# DBMS ASSIGNMENT
# ============================================================


# Comparative Study of Relational, Hierarchical and Network Data Models


# Introduction

Database Management System (DBMS) is an essential part of modern computing used to store, organize, manage and retrieve data efficiently. Different data models, such as relational, hierarchical and network models, provide different methods of organizing and representing data. At the same time, database security plays a vital role in protecting stored information from unauthorized access, data theft and loss. Understanding database models and security measures helps in designing reliable, efficient and secure database systems.


# 1. Relational Data Model

The relational data model represents data in the form of tables, also called relations. Each table consists of rows and columns. Rows are called tuples, and columns are called attributes. Relationships between tables can be established using primary keys and foreign keys.

**Example:** A student database may contain a table with student ID, name and department.

## Advantages

- Simple and easy to understand.
- Reduces data redundancy through proper database design.
- Supports flexible data retrieval using SQL.
- Provides data integrity and security features.

## Disadvantages

- Complex queries involving many tables may require more processing.
- Not always suitable for highly interconnected data without careful design.


# 2. Hierarchical Data Model

The hierarchical data model organizes data in the form of a tree structure. It consists of parent and child records. Each child record generally has only one parent, while a parent can have multiple children. Data is accessed by following predefined paths through the hierarchy.

**Example:** In a college database, a college may have several departments, and each department may have multiple students.

## Advantages

- Simple structure for data with clear parent-child relationships.
- Efficient access when relationships follow a fixed hierarchy.
- Suitable for representing organizational structures.

## Disadvantages

- Difficult to represent many-to-many relationships.
- Changes to the structure can be complicated.
- Accessing data outside predefined paths may be difficult.


# 3. Network Data Model

The network data model represents data using a graph-like structure. Unlike the hierarchical model, a child record can have multiple parent records. It supports one-to-one, one-to-many and many-to-many relationships.

**Example:** In a college database, one student can enrol in several courses, and each course can have many students.

## Advantages

- Supports complex relationships between records.
- Handles many-to-many relationships effectively.
- Can provide efficient access through predefined links.

## Disadvantages

- More complex to design and maintain.
- Users may need to understand the links between records.
- Changes to the database structure can be difficult.


# Comparative Table

| Feature | Relational Model | Hierarchical Model | Network Model |
|---|---|---|---|
| Structure | Tables | Tree | Graph |
| Relationship | Through keys | Parent-child | Linked records |
| Multiple parents | Supported through relationships between tables | Generally not supported | Supported |
| Many-to-many relationships | Supported through related tables | Difficult to represent | Supported directly |
| Complexity | Relatively simple | Simple for hierarchical data | More complex |
| Data access | Queries using SQL | Traversal through a tree | Traversal through linked records |
| Common use | Business and student databases | Hierarchical data structures | Complex interconnected records |


# Database Security: Issues and Solutions


## Major Database Security Issues

### 1. Unauthorized Access

Unauthorized users may access confidential information without permission.

### 2. Data Theft and Leakage

Sensitive information, such as personal details, passwords and financial records, may be stolen or exposed.

### 3. SQL Injection

Attackers may insert malicious SQL commands through vulnerable applications to access or modify database information.

### 4. Data Modification

Unauthorized changes to records can affect the accuracy and reliability of the database.

### 5. Malware and Ransomware

Malicious software can damage database files, steal information or make data inaccessible.

### 6. Insider Threats

Employees or other authorized users may misuse their access privileges to steal, disclose or modify data.


## Solutions to Database Security Issues

### 1. Authentication

Use strong passwords and multi-factor authentication to verify the identity of users before allowing access.

### 2. Authorization and Access Control

Assign permissions according to users' responsibilities. Users should access only the data required for their work.

### 3. Data Encryption

Encrypt sensitive data both when it is stored and when it is transmitted over a network.

### 4. Regular Backup and Recovery

Maintain regular backups and test recovery procedures to restore data after accidental deletion, system failure or cyberattacks.

### 5. Software Updates

Regularly update the DBMS, operating system and related applications to fix known security vulnerabilities.

### 6. Protection Against SQL Injection

Use parameterized queries or prepared statements, validate inputs and avoid constructing SQL queries directly from untrusted user input.


# Conclusion

In conclusion, database models and database security are important aspects of database management. Relational, hierarchical and network models offer different ways to organize data according to application requirements. Proper security measures, such as authentication, access control, encryption and regular backups, help protect databases from various threats. Therefore, selecting a suitable data model and implementing effective security practices are essential for maintaining the efficiency, reliability and safety of database systems.


# ============================================================
# END OF ASSIGNMENT
# ============================================================
