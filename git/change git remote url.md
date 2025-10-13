
```bash
git remote set-url origin <new-url>
```

```
psql -U postgres -d worklenz_db -f database/sql/0_extensions.sql

psql -U postgres -d worklenz_db -f database/sql/1_tables.sql

psql -U postgres -d worklenz_db -f database/sql/indexes.sql

psql -U postgres -d worklenz_db -f database/sql/4_functions.sql

psql -U postgres -d worklenz_db -f database/sql/triggers.sql

psql -U postgres -d worklenz_db -f database/sql/3_views.sql

psql -U postgres -d worklenz_db -f database/sql/2_dml.sql

psql -U postgres -d worklenz_db -f database/sql/5_database_user.sql
```