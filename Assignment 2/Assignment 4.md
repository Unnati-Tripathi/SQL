# Assignment - 4

# Proublem Statement

Collaborative Schema Design + ER Diagram
	- As a team, pick any company or domain you find interesting and build its database together. Each intern owns one table.
	Each intern delivers: their table design with correct data types and constraints, justification for every constraint, foreign key linking to at least one teammate's table, realistic dummy data, and an ER diagram with their name as table owner.
	As a group: all tables should connect, run clean on a fresh PostgreSQL database, and end with one meaningful business query joining all tables together.

## Table Owner
Name: Unnati Tripathi  
Owned Table: Project

## Domain
Company/Organization Management System

The database is designed for an organization where employees work in departments, departments handle projects, clients give projects, and employees are assigned tasks related to those projects.

---

# My Table: Project

The `project` table stores all important details about projects handled by the organization.  
Each project belongs to one client and one department. This helps the company track which client requested the project and which department is responsible for completing it.

---

# Project Table Design

```sql
CREATE TABLE project (
    project_id SERIAL PRIMARY KEY,

    project_name VARCHAR(100) NOT NULL,

    client_id INT NOT NULL,
    department_id INT NOT NULL,

    start_date DATE,
    end_date DATE,

    budget NUMERIC(12,2),

    status VARCHAR(20),

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_project_client
        FOREIGN KEY (client_id)
        REFERENCES clients(client_id),

    CONSTRAINT fk_project_department
        FOREIGN KEY (department_id)
        REFERENCES department(department_id),

    CONSTRAINT chk_project_dates
        CHECK (end_date IS NULL OR end_date >= start_date),

    CONSTRAINT chk_project_budget
        CHECK (budget IS NULL OR budget >= 0)
);

![alt text](image.png)