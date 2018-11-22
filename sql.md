## Sql Docker Scripts
#### For quick startup

```
// Pulls new 2017 sql server
sudo docker pull mcr.microsoft.com/mssql/server:2017-latest

// Creates sql db instance
$ docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=yourStrong(!)Password' -p 1433:1433 --name chopper-db -d microsoft/mssql-server-linux:2017-latest

// Change password
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'

// Connect to root
sudo docker exec -it sql1 "bash"

// Login 
/opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>' // this uses the changed password
```