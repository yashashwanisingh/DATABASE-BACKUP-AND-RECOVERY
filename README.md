# DATABASE-BACKUP-AND-RECOVERY

COMPANY: CodTech IT SOLUTIONS

NAME: YASHASHWANI SINGH

INTERN ID: CT06DR1311

DURATION: 6 WEEKS

MENTOR: NEELA SANTOSH

DESCRIPTION:

1. Documentation of the Process
A. Objective

To demonstrate how to back up a database and restore it in case of system failure.

B. Tools Used

MySQL (you can adapt this for PostgreSQL if needed)

Command line (mysqldump / mysql)

📌 2. Backup Process
A. Backup Using mysqldump
Backup Script (backup.sh)
#!/bin/bash

# Database details
DB_NAME="your_database_name"
USER="root"
PASSWORD="your_password"
OUTPUT_FILE="backup_$(date +%Y%m%d_%H%M%S).sql"

echo "Starting backup..."

mysqldump -u $USER -p$PASSWORD $DB_NAME > $OUTPUT_FILE

if [ $? -eq 0 ]; then
    echo "Backup successful! File created: $OUTPUT_FILE"
else
    echo "Backup failed!"
fi

B. How it Works

mysqldump exports your entire database into a .sql file.

The filename includes timestamp for versioning.

Script checks if backup succeeded.

📌 3. Recovery Process
A. Restore Using mysql
Recovery Script (restore.sh)
#!/bin/bash

# Database details
DB_NAME="your_database_name"
USER="root"
PASSWORD="your_password"
BACKUP_FILE="backup_file_to_restore.sql"

echo "Starting restoration..."

mysql -u $USER -p$PASSWORD $DB_NAME < $BACKUP_FILE

if [ $? -eq 0 ]; then
    echo "Database restored successfully from $BACKUP_FILE"
else
    echo "Database restoration failed!"
fi

B. How it Works

The script reads the backup .sql file and recreates all tables + data.

Useful after accidental delete, corruption, or system crash.

📌 4. Example Workflow
Step 1: Take backup
bash backup.sh


Output:

Backup successful! File created: backup_20250219_142000.sql

Step 2: Restore backup
bash restore.sh


Output:

Database restored successfully from backup_20250219_142000.sql
