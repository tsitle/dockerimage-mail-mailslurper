MailSlurper supports three database engines: SQLite, Microsoft SQL Server, and MySQL. This section will talk about how to configure Microsoft SQL Server and MySQL.

Prerequisites
-------------
To use either Microsoft SQL Server and MySQL you must first create a database. It is beyond the scope of this documentation to teach you how to do this. However, you will need a database to hold your MailSlurper data. Here are some links to get you started.

* [Create a MSSQL Database](https://msdn.microsoft.com/en-us/library/ms186312(v=sql.120).aspx)
* [Create a MySQL Database](http://dev.mysql.com/doc/refman/5.7/en/creating-database.html)

MSSQL Creation Script
---------------------
Once you have a database run the following script to create the schema.

```sql
/*
 * Mail Item
 */
CREATE TABLE mailitem (
	id VARCHAR(36) NOT NULL PRIMARY KEY,
	dateSent DATETIME,
	fromAddress VARCHAR(50) NOT NULL,
	toAddressList VARCHAR(1024) NOT NULL,
	subject VARCHAR(255),
	xmailer VARCHAR(50),
	body TEXT,
	contentType VARCHAR(50),
	boundary VARCHAR(255)
);

/*
 * Attachment
 */
CREATE TABLE attachment (
	id VARCHAR(36) NOT NULL PRIMARY KEY,
	mailItemId VARCHAR(36) NOT NULL,
	fileName VARCHAR(255),
	contentType VARCHAR(50),
	content TEXT
);
```

MySQL Creation Script
---------------------
Once you have a database run the following script to create the schema.

```sql
/*
 * Mail Item
 */
CREATE TABLE mailitem (
	id VARCHAR(36) NOT NULL PRIMARY KEY,
	dateSent DATETIME,
	fromAddress VARCHAR(50) NOT NULL,
	toAddressList VARCHAR(1024) NOT NULL,
	subject VARCHAR(255),
	xmailer VARCHAR(50),
	body TEXT,
	contentType VARCHAR(50),
	boundary VARCHAR(255)
) ENGINE=MyISAM;

/*
 * Attachment
 */
CREATE TABLE attachment (
	id VARCHAR(36) NOT NULL PRIMARY KEY,
	mailItemId VARCHAR(36) NOT NULL,
	fileName VARCHAR(255),
	contentType VARCHAR(50),
	content TEXT
) ENGINE=MyISAM;
```

Example Server Configurations
-----------------------------
Here are some sample **config.json** files to demonstrate using MSSQL and MySQL. These assume you have created a database named **mailslurper**, and have created a user named **mailslurperuser** with a password of **password** that has access to this database. PLEASE NOTE: Do ***not*** make a user account with a password as terrible as **password**. Always use strong passwords!!

### MSSQL Running Locally
In this sample MSSQL is running on your local machine and using the *default* instance.

```js
{
	"wwwAddress": "127.0.0.1",
	"wwwPort": 8080,
	"serviceAddress": "127.0.0.1",
	"servicePort": 8888,
	"smtpAddress": "127.0.0.1",
	"smtpPort": 25,
	"dbEngine": "MSSQL",
	"dbHost": "localhost",
	"dbPort": 1433,
	"dbDatabase": "mailslurper",
	"dbUserName": "mailslurperuser",
	"dbPassword": "password",
	"maxWorkers": 1000
}
```

### MSSQL Running Locally With a Named Instance
In this sample MSSQL is running on your local machine and running in an instance named *MSSQL2014*.

```js
{
	"wwwAddress": "127.0.0.1",
	"wwwPort": 8080,
	"serviceAddress": "127.0.0.1",
	"servicePort": 8888,
	"smtpAddress": "127.0.0.1",
	"smtpPort": 25,
	"dbEngine": "MSSQL",
	"dbHost": "localhost\\MSSQL2014",
	"dbPort": 1433,
	"dbDatabase": "mailslurper",
	"dbUserName": "mailslurperuser",
	"dbPassword": "password",
	"maxWorkers": 1000
}
```

### MSSQL Running Remotely
In this sample MSSQL is running on a remote machine named **DEVSERVER**. This sample assumes DNS is configured to resolve this name. It also assumes that you have configured your SQL server instance to accept remote connections over TCP.

```js
{
	"wwwAddress": "127.0.0.1",
	"wwwPort": 8080,
	"serviceAddress": "127.0.0.1",
	"servicePort": 8888,
	"smtpAddress": "127.0.0.1",
	"smtpPort": 25,
	"dbEngine": "MSSQL",
	"dbHost": "DEVSERVER",
	"dbPort": 1433,
	"dbDatabase": "mailslurper",
	"dbUserName": "mailslurperuser",
	"dbPassword": "password",
	"maxWorkers": 1000
}
```

### MySQL Running Locally
In this sample MySQL is running on your local machine.

```js
{
	"wwwAddress": "127.0.0.1",
	"wwwPort": 8080,
	"serviceAddress": "127.0.0.1",
	"servicePort": 8888,
	"smtpAddress": "127.0.0.1",
	"smtpPort": 25,
	"dbEngine": "MySQL",
	"dbHost": "localhost",
	"dbPort": 3306,
	"dbDatabase": "mailslurper",
	"dbUserName": "mailslurperuser",
	"dbPassword": "password",
	"maxWorkers": 1000
}
```

### MySQL Running Remotely
In this sample MySQL is running on a remote machine named **DEVSERVER**. This sample assumes DNS is configured to resolve this name. It also assumes that you have configured your SQL server instance to accept remote connections over TCP.

```js
{
	"wwwAddress": "127.0.0.1",
	"wwwPort": 8080,
	"serviceAddress": "127.0.0.1",
	"servicePort": 8888,
	"smtpAddress": "127.0.0.1",
	"smtpPort": 25,
	"dbEngine": "MySQL",
	"dbHost": "DEVSERVER",
	"dbPort": 3306,
	"dbDatabase": "mailslurper",
	"dbUserName": "mailslurperuser",
	"dbPassword": "password",
	"maxWorkers": 1000
}
```
