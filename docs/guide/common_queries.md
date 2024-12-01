# Common Queries

This section provides a list of commonly used SQL queries to interact with the database.

---

## Users

### Find User by Email

Search for a specific user by their email address.

```sql
SELECT * FROM users WHERE email = 'example@example.com';
```

### Get Users Without Any Projects

Retrieve users who have not created any projects.

```sql
SELECT users.*
FROM users
LEFT JOIN projects ON users.id = projects.user_id
WHERE projects.id IS NULL;
```

### Get Users with the Number of Projects They Own

List users along with the total number of projects they have created.

```sql
SELECT users.full_name, COUNT(projects.id) AS total_projects
FROM users
LEFT JOIN projects ON users.id = projects.user_id
GROUP BY users.id;
```

## Projects

### Get Projects Without Any Activities

Retrieve all projects that do not have any associated activities.

```sql
SELECT projects.*
FROM projects
LEFT JOIN activities ON projects.id = activities.project_id
WHERE activities.id IS NULL;
```

### Get Projects with the Most Activities

List projects along with the total number of activities they contain, sorted in descending order.

```sql
SELECT projects.name, COUNT(activities.id) AS total_activities
FROM projects
LEFT JOIN activities ON projects.id = activities.project_id
GROUP BY projects.id
ORDER BY total_activities DESC;
```

## Activities

### Get Critical Path Activities for a Project

Retrieve all activities that are part of the critical path for a specific project.

```sql
SELECT activities.*
FROM activities
JOIN calculations ON activities.project_id = calculations.project_id
WHERE POSITION(activities.label IN calculations.critical_path) > 0
AND activities.project_id = 1;
```

### Find Projects with Slack Time Less Than a Threshold

Retrieve projects where any activity has slack time below a specified threshold.

```sql
SELECT DISTINCT projects.*
FROM projects
JOIN activities ON projects.id = activities.project_id
WHERE activities.slack < 5;
```

## Advanced Queries

### Get Users, Their Projects, and the Number of Activities Per Project

Retrieve a detailed view of users, their projects, and the number of activities in each project.

```sql
SELECT users.full_name AS user_name, 
       projects.name AS project_name, 
       COUNT(activities.id) AS total_activities
FROM users
JOIN projects ON users.id = projects.user_id
LEFT JOIN activities ON projects.id = activities.project_id
GROUP BY users.id, projects.id;
```

## Notes

- Replace placeholders (e.g., 1, 5) with your specific values.
- Always test queries in a development environment before running them in production.
