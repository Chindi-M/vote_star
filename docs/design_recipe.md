# Design Recipe



## 1. Design and create the Table

```
# USER STORIES:


```

```
Nouns:

posts, title, tags, name
```

## 2. Infer the Table Name and Columns

Put the different nouns in this table. Replace the example with your own nouns.

| Record                | Properties          |
| --------------------- | ------------------  |
| posts                 | title, content
| tags                  | name

1. Name of the first table (always plural): `posts` 

    Column names: `title`, `content`

2. Name of the second table (always plural): `tags` 

    Column names: `name`

## 3. Decide the column types.



```
# EXAMPLE:

Table: posts
id: SERIAL
title: text
content: text

Table: tags
id: SERIAL
name: text
```

## 4. Design the Many-to-Many relationship

Make sure you can answer YES to these two questions:

1. Can one [TABLE ONE] have many [TABLE TWO]? (Yes/No)
2. Can one [TABLE TWO] have many [TABLE ONE]? (Yes/No)

```
# EXAMPLE

1. Can one tag have many posts? YES
2. Can one post have many tags? YES
```

_If you would answer "No" to one of these questions, you'll probably have to implement a One-to-Many relationship, which is simpler. Use the relevant design recipe in that case._

## 5. Design the Join Table

The join table usually contains two columns, which are two foreign keys, each one linking to a record in the two other tables.

The naming convention is `table1_table2`.

```
# EXAMPLE

Join table for tables: posts and tags
Join table name: posts_tags
Columns: post_id, tag_id
```

## 6. Write the SQL.

```sql
-- EXAMPLE
-- file: posts_tags.sql


CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  title text,
  content text
);

-- Create the second table.
CREATE TABLE tags (
  id SERIAL PRIMARY KEY,
  name text
);

-- Create the join table.
CREATE TABLE posts_tags (
  post_id int,
  tag_id int,
  constraint fk_post foreign key(post_id) references posts(id) on delete cascade,
  constraint fk_tag foreign key(tag_id) references tags(id) on delete cascade,
  PRIMARY KEY (post_id, tag_id)
);

```

## 7. Create the tables.

```bash
psql -h 127.0.0.1 database_name < posts_tags.sql
```




```

Table: students

Columns:
id | name | cohort_name
```

## 2. Create Test SQL seeds


```sql
-- EXAMPLE
-- (file: spec/seeds_{table_name}.sql)



TRUNCATE TABLE students RESTART IDENTITY; -- replace with your own table name.

-- Below this line there should only be `INSERT` statements.
-- Replace these statements with your own seed data.

INSERT INTO students (name, cohort_name) VALUES ('David', 'April 2022');
INSERT INTO students (name, cohort_name) VALUES ('Anna', 'May 2022');
```


```bash
psql -h 127.0.0.1 your_database_name < seeds_{table_name}.sql
```

## 3. Define the class names



```python
# EXAMPLE
# Table name: students

# Model class
# (in lib/student.py)
class Student


# Repository class
# (in lib/student_repository.py)
class StudentRepository

```

## 4. Implement the Model class



```python
# EXAMPLE
# Table name: students

# Model class
# (in lib/student.py)

class Student:
    def __init__(self):
        self.id = 0
        self.name = ""
        self.cohort_name = ""

        # Replace the attributes by your own columns.


```

## 5. Define the Repository Class interface


```python
# EXAMPLE
# Table name: students

# Repository class
# (in lib/student_repository.py)

class StudentRepository():

    # Selecting all records
    # No arguments
    def all():
        # Executes the SQL query:
        # SELECT id, name, cohort_name FROM students;

        # Returns an array of Student objects.

        # Gets a single record by its ID
        # One argument: the id (number)
    def find(id):
        # Executes the SQL query:
        # SELECT id, name, cohort_name FROM students WHERE id = $1;

        # Returns a single Student object.

        # Add more methods below for each operation you'd like to implement.

    # def create(student)
    # 

    # def update(student)
    # 

    # def delete(student)
    # 

```

## 6. Write Test Examples


```python

```

Encode this example as a test.


## 7. Test-drive and implement the Repository class behaviour

