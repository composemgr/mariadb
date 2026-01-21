## 👋 Welcome to mariadb 🚀

MariaDB - Drop-in MySQL replacement relational database

## 📋 Description

MariaDB is a community-developed, commercially supported fork of MySQL. Designed as a drop-in replacement for MySQL with more features, improved performance, and better licensing (GPL).

## 🚀 Services

- **db**: MariaDB 11 (`mariadb:11`)

## 📦 Installation

### Using curl
```shell
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/mariadb/main/docker-compose.yaml" | docker compose -f - up -d
```

### Using git
```shell
git clone "https://github.com/composemgr/mariadb" ~/.local/srv/docker/mariadb
cd ~/.local/srv/docker/mariadb
docker compose up -d
```

### Using composemgr
```shell
composemgr install mariadb
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York

# Root credentials
MYSQL_ROOT_PASSWORD=changeme_root_password

# Optional: Create database and user
MYSQL_DATABASE=myapp
MYSQL_USER=myapp
MYSQL_PASSWORD=changeme_user_password
```

## 🌐 Access

- **MariaDB**: localhost:3306 (from Docker host)
- **Connection String**: `mysql://user:password@localhost:3306/database`

## 📂 Volumes

- `./rootfs/db/mariadb/mariadb` - Database files

## 🔐 Security

- Change default root password
- Create app-specific users (don't use root)
- Use strong passwords
- Limit remote access
- Regular security updates

### Create Application User
```sql
CREATE USER 'myapp'@'%' IDENTIFIED BY 'secure_password';
CREATE DATABASE myapp_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
GRANT ALL PRIVILEGES ON myapp_db.* TO 'myapp'@'%';
FLUSH PRIVILEGES;
```

## 🔍 Logging

```shell
docker compose logs -f db
```

## 🛠️ Management

### Connect to MySQL shell
```shell
docker compose exec db mysql -u root -p
```

### Run SQL commands
```shell
docker compose exec db mysql -u root -p -e "SHOW DATABASES;"
```

## 🔄 Backup & Restore

### Backup
```shell
# Single database
docker compose exec db mysqldump -u root -p mydb > mydb-backup.sql

# All databases
docker compose exec db mysqldump -u root -p --all-databases > all-backup.sql
```

### Restore
```shell
cat mydb-backup.sql | docker compose exec -T db mysql -u root -p mydb
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+
- 256MB+ RAM minimum

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
