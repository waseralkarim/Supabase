## **Use `pg_dump` / `pg_restore` (Logical Backup)**

This is the **official PostgreSQL-safe** and **Supabase-recommended** method.

It avoids file-level corruption, works across PostgreSQL versions, and integrates perfectly with Docker and Supabase.

## **Backup (Logical Dump)**

A **logical backup** captures **schemas, data, roles, and extensions**.

1. **Run backup inside the container**:

```bash
docker exec -t <POSTGRES_CONTAINER_NAME> \
pg_dump -U <POSTGRES_USER> -d <POSTGRES_DB> -F c -f /tmp/db_backup.dump
```

- `<POSTGRES_CONTAINER_NAME>` — your Postgres container (e.g., `supabase_db_yourprojectname`)
- `<POSTGRES_USER>` — Postgres user (usually `postgres`)
- `<POSTGRES_DB>` — Database name (usually `postgres`)
- `F c` — Creates a compressed dump
1. **Copy the backup to your host machine**:

```bash
docker cp <POSTGRES_CONTAINER_NAME>:/tmp/db_backup.dump ./db_backup.dump

```

Now you have a portable `db_backup.dump` on your host.

---

## **Restore (Safe + Version-Independent)**

1. **Copy backup file into the target container**:

```bash
docker cp ./db_backup.dump <POSTGRES_CONTAINER_NAME>:/tmp/db_backup.dump

```

1. **Run restore**:

```bash
docker exec -it <POSTGRES_CONTAINER_NAME> \
pg_restore -U <POSTGRES_USER> -d <POSTGRES_DB> -c /tmp/db_backup.dump

```

- `c` = clean (drops existing objects before restoring)
- This safely restores schemas, data, roles, and extensions
1. **Verify restore**:

```bash
docker exec -it <POSTGRES_CONTAINER_NAME> \
psql -U <POSTGRES_USER> -d <POSTGRES_DB> -c "\dt"

```
