
## ODBC Setup

### 1. Install OBDC driver from Google:
Make sure download 64-bit version

[Download link](https://cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers)

### 2. Credentials 

#### BigQuery service account:

Retrieve the credential from BigQuery admin to get the service account with:
- principal (which is email address that BigQuery provide after create a service account or in the json file below)
- The access key which is the json file
#### Setup OBDC

- Open OBDC driver that installed on the first step

- Select System DSN -> Add -> Simba ODBC Driver for Google BigQuery:
	- Data Source Name: BigQuery_DSN
	- Authentication: Service Authentication
	- Email: the principal above
	- Key File Path: the location of the access key (json file)

- Click Catalog to test if the setup/credential is correct. If yes, there are a projects to select.

- Then click test and ok if success.

### 3. MSSQL Server Management

Open MSSQL Server Management (Make sure SQL Server Express is installed)

Connect to the local host database using Windows Authentication

Open query and run:

```sql
EXEC sp_addlinkedserver   
    @server = N'BigQuery_Link',  
    @srvproduct = N'BigQuery',  
    @provider = N'MSDASQL',  
    @datasrc = N'BigQuery_DSN';
```

```sql
EXEC sp_addlinkedsrvlogin   
    @rmtsrvname = N'BigQuery_Link',  
    @useself = 'FALSE',  
    @locallogin = NULL,  
    @rmtuser = '',  
    @rmtpassword = '';
```

If successful test out the connection:

```sql
EXEC sp_testlinkedserver N'BigQuery_Link';
```

Done