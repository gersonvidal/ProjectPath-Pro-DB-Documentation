# Project Documentation

This repository contains the MkDocs-based documentation for the **ProjectPath-Pro Database**. It includes detailed sections about the database schema, common queries, setup instructions, and more to help developers understand and interact with the system efficiently.

---

## Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Getting Started](#getting-started)

---

## About the Project

The **ProjectPath-Pro Database Documentation** provides a comprehensive guide for developers working with the PostgreSQL database schema for the ProjectPath-Pro application. This documentation is built using [MkDocs](https://www.mkdocs.org/) and designed for easy navigation and readability.

---

## Features

- **Database Schema**: Detailed breakdown of tables, relationships, and constraints.
- **Common Queries**: Predefined SQL queries for efficient database interactions.
- **Getting Started**: Step-by-step instructions for setting up the database.
- **Troubleshooting**: Solutions to common setup and usage problems.

---

## Getting Started

To view the documentation locally:

1. **Clone the Repository**:

```bash
git clone https://github.com/gersonvidal/ProjectPath-Pro-DB-Documentation
```

2. **Install MkDocs** 

Ensure you have Python 3.12 installed, then install MkDocs.

First create the virtual environment:

```bash
python -m venv venv_mkdocs
```

Then activate it:

```bash
source venv_mkdocs/Scripts/activate
```

> [!NOTE]  
> This command changes for Windows.

Finally, install from the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

3. **Build the documentation**

From the project directory, run: 

```bash
mkdocs build
```

The static files will be created in the `site/` directory.

4. **Open the documentation** 

You can open the documentation just by opening the `index.html` file.