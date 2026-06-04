
[[dev-notes]]


## Basic SQL
```sql

SELECT * 
FROM testing 
WHERE id > 1
ORDER BY name
LIMIT 1
OFFSET 10
;


```

```sql
INSERT INTO Artist (name) VALUES ('Radiohead');
SELECT * from Artist WHERE name = 'Radiohead';
```

```sql
UPDATE Artist SET name = 'Daft Punk' WHERE name = 'Radiohead';
SELECT * from Artist WHERE name = 'Daft Punk';
```


```sql
UPDATE Artist SET name = 'Justice' WHERE name = 'Daft Punk' RETURNING *;
```

```sql
ALTER TABLE table ADD COLUMN image TEXT;
ALTER TABLE table DROP COLUMN image TEXT;
```

```sql
ALTER TABLE table ADD COLUMN name TEXT NOT NULL DEFAULT 'john';

```

must declare foreign keys on each connection
now sqlite will respect foreign keys
```sql
PRAGMA foreign_keys=on;
```

aggregation functions
aggregation happens after the where clause
```sql
SELECT COUNT(*) FROM table;
SELECT COUNT(DISTINCT GenreId) FROM Track;

SELECT MAX(*) FROM table;
SELECT MIN(*) FROM table;
```

aggregation happens after the where clause
cannot use agg functions in the where clause,
use them in HAVING
```sql
SELECT trackid, count(genreid) 
FROM tracks 
WHERE something > 1
GROUP BY genreid
HAVING COUNT(genreid) > 300;
```

create view to reuse sql queries easily
this can be dangerous on performance and usage if
the view query is big
```sql
CREATE VIEW
easy_tracks
AS
SELECT
  t.TrackId as id,
  ar.Name as artist,
  al.Title as album,
  t.Name as track
FROM
  Track t

JOIN
  Album al
ON
  t.AlbumId = al.AlbumId

JOIN
  Artist ar
ON
  ar.ArtistId = al.ArtistId;

-- now you can do this
SELECT * FROM easy_tracks LIMIT 15;

```

```sql
EXPLAIN <query statement>
EXPLAIN QUERY PLAN<query statement>
.eqp on
```

shows the indexed column
sqlite automatically indexed foreign keys
```sql
PRAGMA index_list(table);
CREATE INDEX idx_track_name ON TrackTable (Name);

```


```sql
DROP VIEW IF EXISTS easy_tracks;
```

FTS5
full text search
research bm25() for nearest match / fuzzy find search
```sql
-- incomplete
CREATE VIRTUAL TABLE track_search USING FTS5(content="easy_tracks", content_rowid='id')

```

```sql

```
```sql

```

```sql

```
```sql

```




## SQLITE

```Bash
sudo apt install sqlite3
```

---

Types
 - INTEGER
 - TEXT
 - BLOB
 - REAL
 - NUMERIC

---

creates a new db from command line
```
sqlite3 test.db
```

- stores booleans as integers 0 and 1
- does not enforce types
```sql
.mode csv

.import

.ouput ./outputFile.csv
- queries will append to this file by default

.headers on
-- Bash Commands 
-- apt install sqlite3
-- sqlite3 FILENAME
-- sqlite3 sample.sqlite3 

.quit

.tables
--shows tables

.schema
-- shows the past table declaration details

.mode csv 
-- changes import/output method to csv

.import FILE table
-- imports file into table

.mode column
-- outputs normal columns in the terminal

`.mode csv

`.import

`.ouput ./outputFile.csv
- queries will append to this file by default

`.headers on
----------------------------------------------------------------

CREATE TABLE modelData2;
```




```
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```
# SQL Commands

```sql
CREATE TABLE IF NOT EXISTS playing_with_neon(id SERIAL PRIMARY KEY, name TEXT NOT NULL, value REAL);
INSERT INTO playing_with_neon(name, value)
  SELECT LEFT(md5(i::TEXT), 10), random() FROM generate_series(1, 10) s(i);
SELECT * FROM playing_with_neon;
```
