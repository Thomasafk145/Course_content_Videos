# Connecting to a PostgreSQL Database

## Introduction

PostgreSQL is a database system. To work with a PostgreSQL database, you
need a tool that can connect to its server.

This chapter explains how to connect to PostgreSQL using three tools:

1.  **pgAdmin** --- a graphical tool included with PostgreSQL.
2.  **psql** --- a command-line tool included with PostgreSQL.
3.  **DBeaver** --- a free, third-party tool that can connect to
    different database systems.

The examples assume PostgreSQL has already been installed. The video
refers to a separate installation tutorial and does not show the
installation process.

---

## 1. Before Connecting

After PostgreSQL is installed, you should have access to pgAdmin and
psql.

You will also need the password that you created during the PostgreSQL
installation. The password is used when connecting to the server.

The examples in the video use:

- A local PostgreSQL server.
- The default maintenance database, named `postgres`.
- The `postgres` username.
- The default port number configured during installation.

The video does not state the numerical value of the default port.

---

## 2. Connecting with pgAdmin

### 2.1 Open pgAdmin

Open pgAdmin after installing PostgreSQL.

If the installation was successful, a server entry should appear under
**Servers**. The entry may show the installed PostgreSQL version.

Select the server and enter the password you created during
installation. If the password is correct, pgAdmin connects to the
server.

### 2.2 Create a Server Group

If a server entry does not appear automatically, you can create a
connection yourself.

A server group is used to organize server connections in pgAdmin.

1.  Right-click **Servers**.
2.  Select **Register**.
3.  Select **Server Group**.
4.  Enter a name for the group, such as `My Local Server`.
5.  Save the group.

### 2.3 Register a Server

After creating the group, add a server connection inside it.

1.  Right-click the server group.
2.  Select **Register**.
3.  Select **Server**.
4.  Enter a name for the server, such as `Local Server`.
5.  Open the **Connection** settings.

Enter the connection details:

---

Setting Example or value Purpose

---

Host name/address `localhost` The computer hosting
PostgreSQL. In the
video, PostgreSQL is
running on the same
computer.

Port Default port The port configured for
PostgreSQL during
installation.

Maintenance database `postgres` The database used for
this connection.

Username `postgres` The PostgreSQL username
used in the example.

Password Your installation The password for that
password PostgreSQL user.

---

`localhost` means the local computer. If your PostgreSQL server is
hosted somewhere else, you would enter that server's address instead.

After entering the settings, click **Save**. If the connection details
are correct, pgAdmin connects to the server.

---

## 3. Create a Sample Table in pgAdmin

The video creates a table to confirm that the connection works.

### 3.1 Open the SQL Editor

After connecting:

1.  Expand the database and its `public` schema.
2.  Select **Tables** if you want to view the tables already there.
3.  Open the SQL Editor.

The SQL Editor lets you write and run SQL statements.

### 3.2 Create the Table

The example table is named `emp`. It has two columns:

- `id`, which uses the `INTEGER` data type.
- `name`, which uses the `VARCHAR` data type.

Run this SQL statement:

```sql
CREATE TABLE emp (
    id INTEGER,
    name VARCHAR
);
```

What each part means:

- `CREATE TABLE` tells PostgreSQL to make a new table.
- `emp` is the table's name.
- `id` and `name` are the column names.
- `INTEGER` is a data type for whole numbers.
- `VARCHAR` is a data type for text.

The video mentions specifying a length for the `VARCHAR` column but does
not give a particular length in its example. PostgreSQL also allows
`VARCHAR` without a length limit.

### 3.3 Confirm That the Table Was Created

After running the statement, refresh the `public` schema's **Tables**
list.

The `emp` table should appear. Expand it to see the `id` and `name`
columns.

Seeing the table in pgAdmin confirms that PostgreSQL created it.

---

## 4. Connecting with psql

### 4.1 What Is psql?

`psql` is a command-line tool that comes with PostgreSQL. Instead of
using a graphical interface, you type commands to connect to the
database and work with it.

### 4.2 Open psql and Enter the Connection Details

Open the SQL Shell (psql). It asks for connection information.

The video uses these values:

Prompt Example or value

---

Server `localhost`
Database `postgres`
Port The default port used during installation
Username `postgres`
Password Your installation password

Enter the values when prompted. If the displayed default value is
correct, you can accept it.

After entering the password, press Enter. If the details are correct,
psql connects to PostgreSQL.

### 4.3 Test the Connection

To check that the connection works, run:

```sql
SELECT 1 + 1 AS sum;
```

This statement asks PostgreSQL to calculate `1 + 1`. The `AS sum` part
gives the result column the name `sum`.

The expected result is `2`. Getting this result shows that psql is
connected and can run SQL statements.

### 4.4 List the Databases

To see the databases on the server, enter this psql command:

```text
\l
```

The video shows the default databases:

- `postgres`
- `template0`
- `template1`

The video says these databases will be explained in more detail in a
later lesson. For this example, the connection uses the `postgres`
database.

### 4.5 List the Tables

To see the tables in the currently connected database, enter:

```text
\dt
```

The output should include the `emp` table created earlier.

The listing includes information such as:

- **Schema** --- the schema containing the table.
- **Name** --- the table's name.
- **Type** --- the kind of database object; in this example, it is a
  table.
- **Owner** --- the PostgreSQL user who owns the table.

The `\l` and `\dt` commands are psql commands. They are not ordinary SQL
statements.

---

## 5. Connecting with DBeaver

### 5.1 What Is DBeaver?

DBeaver is a free, third-party database tool. It is useful because it
provides a graphical interface for connecting to different database
systems, including PostgreSQL.

The video assumes DBeaver has already been downloaded and installed.

### 5.2 Create a PostgreSQL Connection

1.  Open DBeaver.
2.  Click the plus (**+**) icon to create a connection.
3.  Select **PostgreSQL** from the database list.
4.  Click **Next**.

### 5.3 Enter the Connection Details

Enter the information for your PostgreSQL server:

Setting Example or value

---

Database `postgres`
Username `postgres`
Password Your installation password

DBeaver also displays connection information such as the URL. The video
uses the local PostgreSQL installation and shows that the PostgreSQL
client is detected automatically.

Review the settings and click **Finish**. DBeaver should connect to the
server if the information is correct.

### 5.4 Confirm the Connection

Expand the connection in DBeaver and navigate to the `public` schema.

Open the **Tables** section. The `emp` table should appear.

This confirms that DBeaver is connected to the same PostgreSQL server
where the table was created.

---

## 6. Summary

This chapter covered three ways to connect to a PostgreSQL server:

- **pgAdmin** provides a graphical interface for connecting to
  PostgreSQL and running SQL statements.
- **psql** provides a command-line interface. The `\l` command lists
  databases, and `\dt` lists tables in the current database.
- **DBeaver** provides a graphical interface that can connect to
  PostgreSQL and other database systems.

The chapter also demonstrated how to create a table in pgAdmin and
verify that the same table could be seen through psql and DBeaver.

The sample SQL statement was:

```sql
CREATE TABLE emp (
    id INTEGER,
    name VARCHAR
);
```
