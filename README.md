# r_db

A simple, easy to use database access lib.

```
r_sqlite_conn conn("test.db", true);
conn.exec("CREATE TABLE worker_bees(sesa_id TEXT, name TEST, id INTEGER PRIMARY KEY AUTOINCREMENT);");
conn.exec("INSERT INTO worker_bees(sesa_id, name) VALUES('120129', 'Tony Di Croce');");
auto pk = conn.last_insert_id();
RTF_ASSERT(pk == "1");
auto results = conn.exec("SELECT * FROM worker_bees;");
RTF_ASSERT(results.size() == 1);
RTF_ASSERT(results[0]["sesa_id"] == "120129");
RTF_ASSERT(results[0]["name"] == "Tony Di Croce");
RTF_ASSERT(results[0]["id"] == "1");
```
