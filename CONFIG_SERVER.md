For MailSlurper to run correctly it must be configured. In the [Getting Started](Getting-Started) section we walked you through a basic setup. This section here will detail the configuration options of **config.json**. First let's see that configuration file again.

```js
{
	"wwwAddress": "127.0.0.1",
	"wwwPort": 8080,
	"serviceAddress": "127.0.0.1",
	"servicePort": 8085,
	"smtpAddress": "127.0.0.1",
	"smtpPort": 2500,
	"dbEngine": "SQLite",
	"dbHost": "",
	"dbPort": 0,
	"dbDatabase": "./mailslurper.db",
	"dbUserName": "",
	"dbPassword": "",
	"maxWorkers": 1000,
	"keyFile": "",
	"certFile": "",
	"adminKeyFile": "",
	"adminCertFile": "",
	"authenticationScheme": "",
	"authSecret": "",
	"authSalt": "",
	"authTimeoutInMinutes": 120,
	"credentials": {}
}
```

Let's get a breakdown of what each line is for.

* **wwwAddress** and **wwwPort** - This is the address and port to bind the user interface to. This is the address you will put in your browser to use MailSlurper
* **serviceAddress** and **servicePort** - MailSlurper runs an HTTP service that does things like get emails from your database, delete them, etc... This needs an address and port to run on.
* **smtpAddress** and **smtpPort** - This is the address and port to run the mail server on. The port for the average mail server is usually port 25.
	* For most Linux and Mac OSX systems, port 25 is restricted, and you must run MailSlurper as an administrator to bind to port 25
	* This address and port is what you would use for a mail server setting in your application, or application server. For example:
		* The mail server setting in the ColdFusion administrator
		* SMTP connection information in a .NET ```Web.config``` file
		* SMTP connection information in your ```php.ini``` file
* **dbEngine** - Specifies the database engine used to store captured emails. Options are: SQLite, MySQL, MSSQL
* **dbHost** and **dbPort** - Address and port to your SQL server. This is not used for SQLite
	* Microsoft SQL Server (MSSQL) runs on port 1433 in a default installation
	* MySQL runs on port 3306 in a default installation
* **dbDatabase** - Name of the database where emails will be stored. Recommend using ```mailslurper```
	* For SQLite this should be a path and file name. The default is ```./mailslurper.db``` which is a database file in the same directory where MailSlurper lives
* **dbUserName** and **dbPassword** - Credentials used to access your SQL server. This is not used for SQLite
* **maxWorkers** - Defines the maximum number of email processors. **1000** is usually plenty for most setups. For really high volume, on a server with plenty of resources (read RAM), you can set this higher
	* A single worker processes a single incoming email
* **keyFile** - Private key file. Used for running MailSlurper's SMTP server and services over SSL. Optional
* **certFile** - SSL certificate file. Used for running MailSlurper's SMTP server and services over SSL. Optional
* **adminKeyFile** - Private key file. Used for running the MailSlurper Admin over SSL. Optional
* **adminCertFile** - SSL certificate file. Used for running the MailSlurper Admin over SSL. Optional
* **authenticationScheme** - Instructs MailSlurper to enable authentication to access the administrator. Valid values are: **basic**. See [Configure Basic Authentication](Configure-Basic-Authentication) for more information
* **authSecret** - Password secret used to secure cookies and JWT tokens. Only required if authenticationScheme is configured. See [Configure Basic Authentication](Configure-Basic-Authentication) for more information
* **authSalt** - Password salt to increase encryption security. Only required if authenticationScheme is configured. See [Configure Basic Authentication](Configure-Basic-Authentication) for more information
* **authTimeoutInMinutes** - Timeout expiration for user session when authenticationScheme is configured. Time is measured in minutes. See [Configure Basic Authentication](Configure-Basic-Authentication) for more information
* **credentials** - A map of user names whose values are hashed passwords. Only required if authenticationScheme is configured. See [Configure Basic Authentication](Configure-Basic-Authentication) for more information

By default the **config.json** file comes ready to run locally using SQLite, which is quite sufficient for simple usage. See [Using a SQL Server](Using-A-SQL-Server) for more information on how to setup and use a SQL server.

### Running Over SSL
MailSlurper supports running the HTTP services, web application, and SMTP server over SSL for secure communication. To do this you must provide a PEM certificate file and PEM-formatted key file (with either a *.key* or *.pem* extension). This can be a certificate purchased by a trusted certificate authority, or a self-signed certificate. Below is an example BASH script which will generate the above files as a self-signed certificate. There are *many* resources available on the internet for more information on obtaining or generating certificates.

```bash
openssl genrsa -out mailslurper-key.pem 1024
openssl req -new -key mailslurper-key.pem -out mailslurper.csr
openssl x509 -req -in mailslurper.csr -signkey mailslurper-key.pem -out mailslurper-cert.pem
```

Here is an example configuration file that makes use of the certificate files generated by the above script.

```js
{
	"wwwAddress": "127.0.0.1",
	"wwwPort": 8080,
	"serviceAddress": "127.0.0.1",
	"servicePort": 8888,
	"smtpAddress": "127.0.0.1",
	"smtpPort": 25,
	"dbEngine": "SQLite",
	"dbHost": "",
	"dbPort": 0,
	"dbDatabase": "./mailslurper.db",
	"dbUserName": "",
	"dbPassword": "",
	"maxWorkers": 1000,
	"keyFile": "./mailslurper-key.pem",
	"certFile": "./mailslurper-cert.pem",
	"adminKeyFile": "./mailslurper-key.pem",
	"adminCertFile": "./mailslurper-cert.pem",
	"authenticationScheme": "",
	"authSecret": "",
	"authSalt": "",
	"authTimeoutInMinutes": 120,
	"credentials": {}
}
```
