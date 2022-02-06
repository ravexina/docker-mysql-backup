# docker-mysql-backup

This compose file uses databack/mysql-backup to create preiodically backups from
mysql service.

I keep all the environment variables in an `.env` file like `example.env`. It's
well commented and gives the feeling of a config file.

```yaml
---
version: '3.1'

services:

  db-backup:
    image: databack/mysql-backup
    container_name: app_db_backup
    env_file:
      - ./example.env
    environment:
      DB_PASS_FILE: /run/secrets/database_password
    secrets:
      - database_password
    volumes:
      - ./backup/database/:/backup
    depends_on:
      - db
```
