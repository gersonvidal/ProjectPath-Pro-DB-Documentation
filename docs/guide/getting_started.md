# Getting Started

This section explains how to set up the database using PostgreSQL 14 from the terminal. Follow these steps to clone the repository containing the `schema.sql` file and create the database.

---

## Prerequisites

Before starting, ensure you have the following installed on your machine:

- **[Git](https://git-scm.com/):** To clone the repository.
- **[PostgreSQL 14](https://www.postgresql.org/download/):** To create and manage the database.

---

## Steps to Set Up the Database

### 1. Clone the Repository
First, clone the repository that contains the `schema.sql` file.

```bash
git clone https://github.com/gersonvidal/ProjectPath-Pro-Database.git
```

This command will download the repository to your local machine. Navigate into the repository directory:

```bash
cd ProjectPath-Pro-Database
```
### 2. Start PostgreSQL Service

Make sure the PostgreSQL service is running. On Linux systems, you can start it using:

```bash
sudo systemctl start postgresql
```

On macOS or Windows, use the appropriate command for your setup or start it through the PostgreSQL application

### 3. Access PostgreSQL

Log in to the PostgreSQL shell using your database user. Typically, this user is postgres:

```bash
psql -U postgres
```

You will be prompted to enter the password for the postgres user. It typically it's also `postgres`.

### 4. Create the Database

Once inside the PostgreSQL shell, create a new database for your project:

```sql
CREATE DATABASE projectpath_pro;
```

You can verify that the database was created using:

```bash
\l
```

### 5. Connect to the Database

Switch to the newly created database:

```bash
\c projectpath_pro;
```

Now you can exit PostgreSQL shell using `\q`. 

### 6. Execute the Schema Script

Run the `schema.sql` script to create the tables and relationships defined in the database schema. Assuming you are in the ProjectPath-Pro-Database directory where the script is located, execute:

```bash
psql -U postgres -d projectpath_pro -f schema.sql
```

This command executes the SQL script in the `projectpath_pro` database.

### 7. Verify the Database Structure

After executing the script, verify that the tables and relationships were created successfully. From the PostgreSQL shell, list the tables:

```bash
\dt
```

You should see a list of all the tables (`users`, `projects`, `activities`, `calculations`, `tokens`).

## Troubleshooting 

- If you encounter a "permission denied" error, ensure your PostgreSQL user has sufficient privileges to create and modify the database.
- If the psql command is not found, ensure that PostgreSQL is correctly installed and added to your system's PATH.

Your database is now set up and ready to use!