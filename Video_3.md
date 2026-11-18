# Restoring a Sample PostgreSQL Database

## Introduction

In the previous lesson, we learned how to create a database and connect
to it using pgAdmin, psql, and DBeaver.

This lesson explains how to create a database and restore a sample
database backup using those three tools. The sample database in the
video is **DVD Rental**.

A database backup is a saved copy of database information. Restoring a
backup loads the saved database objects and information into a database.

The video uses a backup file that has already been downloaded. It says
the download link is provided in the video description.

---

## 1. Restore a Database Using pgAdmin

### 1.1 Create a New Database

First, create an empty database to hold the backup.

1.  Open pgAdmin and connect to your PostgreSQL server.
2.  Find the **Databases** section.
3.  Right-click **Databases**.
4.  Select **Create**, then **Database**.
5.  Enter a name for the database.
6.  Click **Save**.

The video creates a database for the DVD Rental sample.

### 1.2 Open the Restore Tool

After creating the database:

1.  Find the new database under **Databases**.
2.  Right-click the database.
3.  Select **Restore**.

The Restore window lets you choose the backup file and its format.

### 1.3 Choose the Backup Format and File

In the Restore window, select the format that matches your backup file.
The video uses the **Custom or Tar** format.

Next, choose the backup file:

1.  Open the file browser beside the filename field.
2.  Find the downloaded backup file.
3.  If the `.backup` file does not appear, change the file filter to
    **All Files**.
4.  Select the backup file.
5.  Click **Open**.

Changing the file filter allows the file browser to show files that are
not included in its current filter.

### 1.4 Restore and Verify the Database

Start the restore process and wait for it to finish.

To verify the restore, expand the database in pgAdmin and look through
its contents. The video checks that the database now contains tables and
views. Before the restore, the new database was empty. After the
restore, the tables and views from the backup appear.

This confirms that the backup was restored.

---

## 2. Restore a Database Using psql and the Command Prompt

This method uses two tools:

- **psql**, to create the database and later connect to it.
- **Windows Command Prompt**, to run the `pg_restore` program.

### 2.1 Create the Database in psql

Open psql and connect to your PostgreSQL server.

Run this SQL statement:

```sql
CREATE DATABASE dvdrental;
```

`CREATE DATABASE` tells PostgreSQL to create a database. `dvdrental` is
the name used in this example.

### 2.2 Check That the Database Exists

In psql, enter:

```text
\l
```

This command lists the databases on the server. Check the list for
`dvdrental`.

### 2.3 Open the Windows Command Prompt

Open Windows Command Prompt.

The `pg_restore` program is stored in PostgreSQL's `bin` folder. The
folder location depends on where PostgreSQL was installed.

Use the `cd` command to move to that folder:

```bat
cd "PATH_TO_POSTGRESQL_BIN_FOLDER"
```

Replace `PATH_TO_POSTGRESQL_BIN_FOLDER` with the actual path to the
`bin` folder on your computer. You need to use the folder that contains
the `pg_restore` application.

### 2.4 Run pg_restore

The `pg_restore` program loads a database backup into a database.

Use this command structure:

```bat
pg_restore -h localhost -d dvdrental -U postgres -p PORT_NUMBER "PATH_TO_BACKUP_FILE"
```

Replace the placeholders with the correct values for your computer:

---

Part Meaning

---

`pg_restore` Runs PostgreSQL's restore program.

`-h localhost` Connects to the PostgreSQL server
on the local computer.

`-d dvdrental` Selects `dvdrental` as the database
where the backup will be restored.

`-U postgres` Uses the `postgres` username.

`-p PORT_NUMBER` Specifies the port used by your
PostgreSQL server.

`PATH_TO_BACKUP_FILE` The location and name of the
downloaded backup file.

---

Use the port number configured for your PostgreSQL installation and the
actual location of your backup file. Keep quotation marks around the
file path if it contains spaces.

Press Enter to run the command.

### 2.5 Enter the Password

The command asks for the password belonging to the `postgres` user.

Enter the password you set for that user and press Enter. The restore
process will load the backup into the `dvdrental` database.

### 2.6 Connect to the Restored Database

After the restore finishes, return to psql.

To connect to the restored database, enter:

```text
\c dvdrental
```

The `\c` command connects psql to the database named after it. In this
example, it connects to `dvdrental`.

### 2.7 Check the Restored Tables

To list the tables in the connected database, enter:

```text
\dt
```

This command displays the tables in the current database. The video
shows tables from the DVD Rental database in the results. This confirms
that the backup was loaded.

### 2.8 Drop the Database

The video also demonstrates how to remove the database after testing the
restore.

You cannot drop a database while you are connected to that same
database. First, connect to a different database.

In psql, connect to the `postgres` database:

```text
\c postgres
```

Now run this SQL statement:

```sql
DROP DATABASE dvdrental;
```

`DROP DATABASE` removes the database named `dvdrental`.

To check that it was removed, list the databases again:

```text
\l
```

The `dvdrental` database should no longer appear in the list.

---

## 3. Restore a Database Using DBeaver

### 3.1 Connect to PostgreSQL

Open DBeaver and connect to your PostgreSQL server. The video already
has a PostgreSQL connection, so it uses that existing connection.

### 3.2 Create a New Database

1.  Expand or select the PostgreSQL connection.
2.  Find the **Databases** section.
3.  Right-click **Databases**.
4.  Select **Create New Database**.
5.  Enter the database name, `dvdrental`.
6.  Create the database.

### 3.3 Check the Empty Database

Expand the new `dvdrental` database.

The video checks its `public` schema and **Tables** section. These are
empty before the backup is restored.

### 3.4 Open the Restore Tool

1.  Right-click the `dvdrental` database.
2.  Open **Tools**.
3.  Select **Restore**.

The Restore window allows you to choose the backup format and file.

### 3.5 Select the Backup File

1.  Select the format that matches the backup file.
2.  Check the backup file selection.
3.  If needed, use the browse option to find the file.
4.  If the file is not visible, change the file filter to **All Files**.
5.  Select the backup file.

### 3.6 Start the Restore

Start the restore process.

DBeaver displays a warning that restoring may affect the database. Since
the video created an empty database for this restore, it confirms the
warning by clicking **Yes**.

Wait for the restore process to finish. DBeaver displays a notification
when it is complete.

### 3.7 Verify the Restored Database

Close the restore window and refresh the database view.

Expand the `dvdrental` database and look inside its `public` schema. The
video shows that the tables and views from the backup are now present.
This confirms that the database was restored.

### 3.8 Drop the Database

To remove the database in DBeaver:

1.  Right-click the `dvdrental` database.
2.  Select **Delete**.
3.  Confirm by clicking **Yes**.

This removes the database.

---

## 4. Summary

This lesson demonstrated how to create a database, restore a sample
backup, check the restored contents, and remove the database using
different PostgreSQL tools.

### pgAdmin

1.  Create a database.
2.  Right-click it and select **Restore**.
3.  Choose the backup format and file.
4.  Start the restore.
5.  Check that the tables and views appear.

### psql and Windows Command Prompt

1.  Create the database with `CREATE DATABASE`.
2.  Check that it exists with `\l`.
3.  Open Command Prompt and move to PostgreSQL's `bin` folder.
4.  Run `pg_restore` with the server, database, username, port, and
    backup file information.
5.  Enter the PostgreSQL user's password.
6.  Connect to the restored database with `\c`.
7.  Check its tables with `\dt`.
8.  Connect to a different database before removing it with
    `DROP DATABASE`.

### DBeaver

1.  Create a database.
2.  Open **Tools** and select **Restore**.
3.  Choose the backup format and file.
4.  Confirm the restore warning and wait for the process to finish.
5.  Check that the tables and views appear.
6.  To remove the database, right-click it, select **Delete**, and
    confirm.

### Important Commands

```sql
CREATE DATABASE dvdrental;

DROP DATABASE dvdrental;
```

```text
\l
\c dvdrental
\c postgres
\dt
```

```bat
pg_restore -h localhost -d dvdrental -U postgres -p PORT_NUMBER "PATH_TO_BACKUP_FILE"
```

Remember that the database must exist before restoring the backup into
it. Also, when using psql, connect to a different database before
attempting to drop the database you want to remove.
