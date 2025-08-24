# Codtech-task-4-Database_Backup_And_Recovery

# 🗄️ Database Backup and Recovery (Task-4)

This project demonstrates **database backup and recovery** as part of CodTech Internship **Task 4**.

---

## 🚀 Features
- Backup MySQL database using `mysqldump`
- Restore database from SQL file
- Scripts for automation
- Sample test database

---

## 📜 Scripts

### 🔹 `backup.sh`
```bash
#!/bin/bash

# Database Credentials
DB_USER="root"
DB_PASSWORD="yourpassword"
DB_NAME="yourdatabase"
BACKUP_DIR="./backups"
DATE=$(date +%F_%H-%M-%S)

# Create backup directory if not exists
mkdir -p $BACKUP_DIR

# Run backup command
mysqldump -u $DB_USER -p$DB_PASSWORD $DB_NAME > $BACKUP_DIR/${DB_NAME}_$DATE.sql

# Confirmation message
if [ $? -eq 0 ]; then
  echo "✅ Backup successful! File saved at $BACKUP_DIR/${DB_NAME}_$DATE.sql"
else
  echo "❌ Backup failed!"
fi


🔹 restore.sh

#!/bin/bash

# Database Credentials
DB_USER="root"
DB_PASSWORD="yourpassword"
DB_NAME="yourdatabase"
BACKUP_FILE=$1

# Usage check
if [ -z "$BACKUP_FILE" ]; then
  echo "Usage: ./restore.sh <backup_file.sql>"
  exit 1
fi

# Restore database
mysql -u $DB_USER -p$DB_PASSWORD $DB_NAME < $BACKUP_FILE

# Confirmation message
if [ $? -eq 0 ]; then
  echo "✅ Database restored successfully from $BACKUP_FILE"
else
  echo "❌ Restore failed!"
fi

🔹 scripts/mysql_backup.sql

-- Sample database schema & data for testing backup and restore
CREATE DATABASE IF NOT EXISTS yourdatabase;
USE yourdatabase;

CREATE TABLE IF NOT EXISTS employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50),
    role VARCHAR(50),
    salary DECIMAL(10,2)
);

INSERT INTO employees (name, role, salary) VALUES
('Alice', 'Developer', 60000),
('Bob', 'Manager', 75000),
('Charlie', 'Tester', 50000);

⚙️ Usage & Output

1️⃣ Setup

Install MySQL

Update database credentials in backup.sh & restore.sh



---

2️⃣ Create Sample Database

mysql -u root -p < scripts/mysql_backup.sql

✅ Output in MySQL

Query OK, 1 row affected
Query OK, 0 rows affected
Query OK, 3 rows affected


---

3️⃣ Take Backup

./backup.sh

✅ Output

✅ Backup successful! File saved at ./backups/yourdatabase_2025-08-24_12-30-45.sql

(A backup file with timestamp will be created inside the backups/ folder.)


---

4️⃣ Restore Database

./restore.sh ./backups/yourdatabase_2025-08-24_12-30-45.sql

✅ Output

✅ Database restored successfully from ./backups/yourdatabase_2025-08-24_12-30-45.sql


---

5️⃣ Verify Data

mysql -u root -p -e "SELECT * FROM yourdatabase.employees;"

✅ Output

+----+---------+-----------+----------+
| id | name    | role      | salary   |
+----+---------+-----------+----------+
|  1 | Alice   | Developer | 60000.00 |
|  2 | Bob     | Manager   | 75000.00 |
|  3 | Charlie | Tester    | 50000.00 |
+----+---------+-----------+----------+


---

📌 Deliverables

✅ Backup Script (backup.sh)

✅ Restore Script (restore.sh)

✅ Documentation (README.md)

✅ Test SQL file (scripts/mysql_backup.sql)

