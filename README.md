# Snippetbox

## Setup

### Set up local `mysql` database

```bash
sudo apt install mysql-server
sudo systemctl start mysql # starts the mysql service if not already running
mysql -u root -p
```

### Create a new UTF-8 `snippetbox` database

```sql
CREATE DATABASE snippetbox CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
-- Switch to using the `snippetbox` database.
USE snippetbox;
```

### Create a snippets table

```sql
CREATE TABLE snippets (
    id INTEGER NOT NULL PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    content TEXT NOT NULL,
    created DATETIME NOT NULL,
    expires DATETIME NOT NULL
);
-- Add an index on the created column.
CREATE INDEX idx_snippets_created ON snippets(created);
```

### Create a new user

```sql
CREATE USER 'web'@'localhost';
GRANT SELECT, INSERT, UPDATE, DELETE ON snippetbox.* TO 'web'@'localhost';
-- Important: Make sure to swap 'password' with a password of your own choosing.
ALTER USER 'web'@'localhost' IDENTIFIED BY 'password';
```
