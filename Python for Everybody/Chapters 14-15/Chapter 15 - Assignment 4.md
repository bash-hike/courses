## Many Students in Many Courses

#### This assignment will be a Python program to build a set of tables using the Many-to-Many approach to store enrollment and role data.

### Instructions

This application will read roster data in JSON format, parse the file, and then produce an SQLite database that contains a User, Course, and Member table and populate the tables from the data file.

You can base your solution on this code: http://www.py4e.com/code3/roster/roster.py - this code is incomplete as you need to modify the program to store the **role** column in the **Member** table to complete the assignment.

Each student gets their own file for the assignment. Download [this file](/Python%20for%20Everybody/Chapters%2014-15/roster_data.json) and save it as `roster_data.json`. Move the downloaded file into the same folder as your `roster.py` program.

Once you have made the necessary changes to the program and it has been run successfully reading the above JSON data, run the following SQL command:

```sql
SELECT hex(User.name || Course.title || Member.role ) AS X FROM 
    User JOIN Member JOIN Course 
    ON User.id = Member.user_id AND Member.course_id = Course.id
    ORDER BY X
```

Find the **first** row in the resulting record set and enter the long string that looks like **53656C696E613333**. 

## 

### Turning in Assignment 

Code: *4161646974736933363430* ( (Hint: starts with 416))

Python Code:

```python
import json
import sqlite3

conn = sqlite3.connect('rosterdb.sqlite')
cur = conn.cursor()

# Do some setup
cur.executescript('''
DROP TABLE IF EXISTS User;
DROP TABLE IF EXISTS Member;
DROP TABLE IF EXISTS Course;

CREATE TABLE User (
    id     INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT UNIQUE,
    name   TEXT UNIQUE
);

CREATE TABLE Course (
    id     INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT UNIQUE,
    title  TEXT UNIQUE
);

CREATE TABLE Member (
    user_id     INTEGER,
    course_id   INTEGER,
    role        INTEGER,
    PRIMARY KEY (user_id, course_id)
)
''')

fname = input('Enter file name: ') or 'roster_data.json'
# Parse the JSON file
str_data = open(fname).read()
json_data = json.loads(str_data)

for entry in json_data:
    # Each entry in the JSON file is a list consisting of 
    # thrree items - name, course title, and role
    name = entry[0]
    title = entry[1]
    role = entry[2]

    # Insert a new name in the User table,
    # unless there's already a row with the same name.
    cur.execute('''INSERT OR IGNORE INTO User (name)
        VALUES ( ? )''', ( name, ) )
    cur.execute('SELECT id FROM User WHERE name = ? ', (name, ))
    # user_id goes in Member table, so we need that
    user_id = cur.fetchone()[0]

    cur.execute('''INSERT OR IGNORE INTO Course (title)
        VALUES ( ? )''', ( title, ) )
    cur.execute('SELECT id FROM Course WHERE title = ? ', (title, ))
    course_id = cur.fetchone()[0]

    cur.execute('''INSERT OR REPLACE INTO Member
        (user_id, course_id, role) VALUES ( ?, ?, ? )''',
        ( user_id, course_id, role ) )

    conn.commit()

# SQL query to get the code
sqlstr = '''
SELECT hex(User.name || Course.title || Member.role ) AS X FROM 
    User JOIN Member JOIN Course 
    ON User.id = Member.user_id AND Member.course_id = Course.id
    ORDER BY X
    '''

cur.execute(sqlstr)
print(cur.fetchone()[0])

cur.close()
```