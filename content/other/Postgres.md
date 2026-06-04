
[[dev-notes]]

```bash
sudo apt install postgresql
```

```bash
#log into psql cli
sudo -u postgres psql

#psql commands
\dt shows tables
\q quit
```

```sql

postgres=# ALTER USER postgres PASSWORD 'mynewpassword';

CREATE TABLE monies (entry_id serial PRIMARY KEY,date date,  amount FLOAT, description VARCHAR(255));

INSERT INTO monies (date, amount, description) VALUES('11/12/2024', 444.44, 'tanners bday');

```

```javascript
     pool = new Pool({
        host: 'localhost',
        database: 'postgres',
        user:'postgres',
        password:'mynewpassword',
        port: 5432
    });
```