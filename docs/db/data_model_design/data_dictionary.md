# Data Dictionary

## `users` Table
Stores user information.

| Column         | Data Type      | Constraints             | Description                                    |
|----------------|----------------|-------------------------|------------------------------------------------|
| `id`           | BIGINT         | Primary Key             | Unique identifier for the user.               |
| `full_name`    | VARCHAR(255)   | Not Null                | Full name of the user.                        |
| `username`     | VARCHAR(30)    | Not Null                | Username for the account.                     |
| `email`        | VARCHAR(254)   | Unique, Not Null        | User's email address.                         |
| `password`     | TEXT           | Not Null                | Hashed password for the account.                     |
| `date_of_birth`| DATE           | Not Null                | User's date of birth.                         |

---

## `projects` Table
Stores information about projects.

| Column       | Data Type | Constraints             | Description                                    |
|--------------|-----------|-------------------------|------------------------------------------------|
| `id`         | BIGINT    | Primary Key             | Unique identifier for the project.            |
| `name`       | TEXT      | Not Null                | Name of the project.                          |
| `description`| TEXT      |                         | Description of the project.                   |
| `user_id`    | BIGINT    | Foreign Key (`users.id`)| Identifier for the user owning the project.   |

---

## `activities` Table
Stores information about activities within projects.

Note that `close_start`, `distant_start`, `close_finish`, `distant_finish` and `slack` default to `null` because they are later calculated by the API.

| Column          | Data Type | Constraints                | Description                                    |
|-----------------|-----------|----------------------------|------------------------------------------------|
| `id`            | BIGINT    | Primary Key                | Unique identifier for the activity.           |
| `name`          | TEXT      | Not Null                   | Name of the activity.                         |
| `label`         | TEXT      | Not Null                   | Label for the activity. Format: A...Z, AA...ZZ, AAA...ZZZ, etc.   |
| `predecessors`  | TEXT      |                            | List of predecessors, comma-separated. For example: "A,B,C,D"        |
| `days_duration` | INT       | Not Null                   | Duration of the activity in days.             |
| `close_start`   | INT       | Default: NULL              | Closest possible start in days.               |
| `distant_start` | INT       | Default: NULL              | Latest possible start in days.                |
| `close_finish`  | INT       | Default: NULL              | Closest possible finish in days.              |
| `distant_finish`| INT       | Default: NULL              | Latest possible finish in days.               |
| `slack`         | INT       | Default: NULL              | Slack time in days.                           |
| `project_id`    | BIGINT    | Foreign Key (`projects.id`)| Identifier for the associated project.        |

---

## `calculations` Table
Stores calculated project data.

| Column             | Data Type | Constraints                | Description                                    |
|--------------------|-----------|----------------------------|------------------------------------------------|
| `id`               | BIGINT    | Primary Key                | Unique identifier for the calculation.        |
| `critical_path`    | TEXT      | Not Null                   | Critical path in hyphen-separated format. For example: "L-M-N-O-P"     |
| `estimated_duration`| INT      | Not Null                   | Estimated project duration in days.           |
| `project_id`       | BIGINT    | Foreign Key (`projects.id`)| Identifier for the associated project.        |

---

## `tokens` Table
Stores authentication tokens for users.

| Column      | Data Type     | Constraints                | Description                                    |
|-------------|---------------|----------------------------|------------------------------------------------|
| `id`        | BIGINT        | Primary Key                | Unique identifier for the token.              |
| `token`     | TEXT          | Unique, Not Null           | The token string used for authentication.     |
| `token_type`| TOKEN_TYPE    | Not Null                   | Type of token.                                |
| `is_revoked`| BOOL          | Not Null                   | Indicates whether the token is revoked.       |
| `is_expired`| BOOL          | Not Null                   | Indicates whether the token is expired.       |
| `user_id`   | BIGINT        | Foreign Key (`users.id`)   | Identifier for the associated user.           |

---

## `token_type` Enum
Defines the type of token used in the `tokens` table.

| Value   | Description       |
|---------|-------------------|
| `BEARER`| Token for authentication purposes. |