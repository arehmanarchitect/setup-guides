# MySQL 5.7 – Local Docker Setup

## 1. What is it?

A local MySQL 5.7 database running inside Docker.

- **Image:** MySQL 5.7
- **Container:** `mysql-local`
- **Database:** `appdb`
- **Port:** `3306`
- **Persistent storage:** Docker volume `mysql_data`
- **Platform:** Linux AMD64 (runs on Apple Silicon through emulation if required)

Your database data persists even when you stop or remove the container, provided you retain the Docker volume.

## 2. Download and Run

Save the configuration as `docker-compose.yml`.
Open Terminal in the directory containing the file.

* Run the docker-compose: `bash docker compose up -d`
* Check container status: `bash docker compose ps `

* View logs: ` bash docker compose logs -f mysql `

**Check MySQL startup:**

```bash
docker exec -it mysql-local mysqladmin -uroot -proot123456 ping
```

Expected output:

```text
mysqld is alive
```

## 3. Database Credentials

| Setting | Value |
|---|---|
| Host | `localhost` |
| Port | `3306` |
| Root username | `root` |
| Root password | `root123456` |
| Database | `appdb` |
| Application username | `appuser` |
| Application password | `app123456` |
| JDBC URL | `jdbc:mysql://localhost:3306/appdb` |

## 4. Connect to MySQL

**Connect as root:**

```bash
docker exec -it mysql-local mysql -uroot -p
```

Enter password: `root123456`

**Connect as application user:**

```bash
docker exec -it mysql-local mysql -uappuser -p appdb
```

Enter password: `app123456`

**Connect from your Mac terminal (if MySQL client is installed):**

```bash
mysql -h 127.0.0.1 -P 3306 -uappuser -p appdb
```

## 5. Useful MySQL Commands

```sql
SHOW DATABASES;

USE appdb;

SHOW TABLES;

SELECT VERSION();

CREATE TABLE test (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);

INSERT INTO test (name) VALUES ('Hello MySQL');

SELECT * FROM test;

EXIT;
```

## 6. Start, Stop and Restart

Run these commands from the directory containing `docker-compose.yml`.

| Operation | Command |
|---|---|
| Start | `docker compose start` |
| Stop | `docker compose stop` |
| Restart | `docker compose restart` |
| Start (create if missing) | `docker compose up -d` |
| Stop and remove container | `docker compose down` |
| Check status | `docker compose ps` |
| View logs | `docker compose logs -f mysql` |

## 7. Remove MySQL Completely

**Remove container and network:**

```bash
docker compose down
```

**Remove container, network and database volume (PERMANENT DATA LOSS):**

```bash
docker compose down -v
```

The `-v` option deletes `mysql_data`, including all stored databases and tables.

## 8. Important Notes

- Use `docker compose up -d` to download the image automatically if it is not already available.
- Data is persisted in the Docker volume `mysql_data`.
- Stopping or restarting the container does not delete your database.
- Port `3306` must be free on your Mac.
- Use `appuser` for application development rather than the root account.
- These credentials are for local development only, not production.
