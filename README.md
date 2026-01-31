# TicketSystem

## Creating the SQL Schema

### Users Table

* id => Primary Key
* username => Unique Key
* email => Unique Key
* password_hash => Not Null
* role -- "admin", "user"
* created_at

```[SQL]
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    role VARCHAR(20) NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);
```

### Ticket Table

* id => Primary Key
* title => Not Null
* description
* status => default "open"
* priority => default "low"
* created_by => references user_id
* assigned_to => references user_id
* created_at
* updated_at

```[SQL]
CREATE TABLE tickets (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    status VARCHAR(20) DEFAULT 'open'
    priority VARCHAR(10) DEFAULT 'low',
    created_by INT REFERENCES users(id),
    assigned_to INT REFERENCES users(id),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

### Attachments

* id => Primary Key
* ticket_id references ticket_id, on delete cascade
* file_path => Not Null
* uploaded_at

```[SQL]
CREATE TABLE attachments (
    id SERIAL PRIMARY KEY,
    ticket_id INT REFERENCES tickets(id) ON DELETE CASCADE,
    file_path VARCHAR(255) NOT NULL,
    uploaded_at TIMESTAMP DEFAULT NOW()
);
```
