# Practical 8 — Python & SQLite

Connects Python to a SQLite database using the built-in `sqlite3` module, creates a `students` table and inserts a record.

## Files

| File            | Purpose                                                                 |
|-----------------|-------------------------------------------------------------------------|
| `main.py`       | Connects to `students.db`, creates the table, inserts a record          |
| `sqlconnect.py` | Same flow, plus saving changes and closing the connection               |
| `students.db`   | SQLite database created by running the scripts                          |

## Table schema

```sql
CREATE TABLE IF NOT EXISTS students (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    roll_no TEXT UNIQUE NOT NULL,
    marks REAL CHECK(marks >= 0 AND marks <= 100)
)
```

- `roll_no` must be unique and non-null
- `marks` must be between 0 and 100

## Run

Requires Python 3.8+ (no external packages).

```bash
python3 main.py
```

Output:

```
Database connected successfully!
Student record added successfully!
```

`sqlconnect.py` additionally prints `Students table created successfully!`.

## Notes

- Values are inserted with `?` placeholders (parameterised queries), which prevents SQL injection.
- The scripts insert the same roll number (`39`), so running a second script against the same `students.db` raises `sqlite3.IntegrityError: UNIQUE constraint failed: students.roll_no`. Delete `students.db` to start fresh.

## Inspect the data

```bash
sqlite3 students.db "SELECT * FROM students;"
```
