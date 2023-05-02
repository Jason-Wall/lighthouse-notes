# W05

## PostgreSQL

Have to `startpostgres` on each restart.\
Run postgres in the folder of choice using `psql`.\
Make a new database? `CREATE DATABASE <databasename>`\
`\c <database_name>` to connect to a database.

To create a new db with username/pass:

```bash
CREATE ROLE labber WITH LOGIN password 'labber';
CREATE DATABASE midterm OWNER labber;
```

### Workflow:

Create a database in the working folder: `CREATE DATABASE <database_name>;`\
Open the database: `\c <database_name>`\
Create tables using sql. Append to the database: `\i <folder>/<table_maker>.sql`\
Load data into the tables using sql: `\i <folder>/<data>.sql`\
Run queries `\i <folder>/<queries>.sql`

### [Alter Tables](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-alter-table/)

`ALTER TABLE table_name action;`

### Foreign Keys

must match the data type of the corresponding primary (ie. integer).

```sql
CREATE TABLE pets (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  owner_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE
);
```

```sql
-- Insert data intot table.
INSERT INTO TABLE_NAME (column1, column2, column3,...columnN)
VALUES (value1, value2, value3,...valueN);

-- Update row data.
UPDATE table_name
SET column1 = value1, column2 = value2...., columnN = valueN
WHERE [condition];


```

**[Postgres Tutorials](https://www.postgresqltutorial.com/)**

## Database Best Practices:

- Primary key column:
  - Use the name id and then SERIAL PRIMARY KEY.
- Foreign key columns:
  - Add \_id to the singular name of the column you are referencing.
  - If the primary key is SERIAL, then the foreign key should be INTEGER.
  - You also should create the foreign key with REFERENCES table_name(id) ON DELETE CASCADE.
- Names, emails, usernames and passwords can all be stored as VARCHAR(255).
- Dates would use the DATE type. If we needed date and time, use TIMESTAMP.
- Numbers:
  - We will use INTEGER to represent most numbers. There are other sizes of integers as well.
  - SMALLINT -32,768 to 32,767 (thirty-two thousand)
  - INTEGER -2,147,483,648 to 2,147,483,647 (two billion)
  - BIGINT -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (nine quintillion)
  - SERIAL 1 to 2,147,483,647 (auto incrementing)
- Dates, Phone Numbers & Currency
  - ISO 8601 date formatting standard. The string '2018-02-12' uses this format to represent 'February 12th, 2018'. Year, month and then day. Dates should be stored consistently. Apply timezones and formatting when displayed to the user.
  - Store phone numbers as VARCHAR, there are so many possible formats. The number 214 748 3647 hits our INTEGER limit.
  - Store currency as an integer representing cents. Use a BIGINT if you need values over $21 million dollars.

## SQL

### Joins

All `JOIN` have a an `ON` associated with them that characterize the relationship between the tables. Example:\

```sql
FROM students JOIN cohorts ON cohorts.id = cohort_id
```

`INNER JOIN` or just plain `JOIN` will return all items where a full match is found.\
Outer Joins - `LEFT, RIGHT, and FULL` will return the entire table of the specified direction. Left of Join returns all the left entries, even if they don't match with the right table.

## [Node-Postgress](https://node-postgres.com/)

`npm install pg`

Insert the following into .js to create a new connection instance:

```js
const { Client, Pool } = require('pg');

const pool = new Pool({
  // We generally want to use pool.
  user: 'vagrant',
  password: '123',
  host: 'localhost',
  database: 'bootcampx',
});
```

queries are promises:

```js
pool
  .query(
    `
SELECT id, name, cohort_id
FROM students
LIMIT 5;
`
  )
  .then((res) => {
    console.log(res);
  })
  .catch((err) => console.error('query error', err.stack));

// Response data comes back as an object.
res.rows; //is where the actual data lives.
```

## Git Workflow

One person creates a repo other people work on it.\
Commit before pulling if you don't want to overwrite your work.

## Express Router
