O [Microsoft SQL Server](https://pt.wikipedia.org/wiki/Microsoft_SQL_Server) é um sistema gerenciador de [[Relational|Banco de dados relacional]] desenvolvido pela Sybase em parceria com a Microsoft. Esta parceria durou até 1994, com o lançamento da versão para Windows NT e desde então a Microsoft mantém a manutenção do produto.

## Start Up
Starting a SQL Server and Adminer in [[Docker]]:
```yaml
services:
  db:
    container_name: MSSQL
    image: mcr.microsoft.com/mssql/server:2022-latest
    restart: unless-stopped
    environment:
      MSSQL_SA_PASSWORD: "dbPassword123!"
      ACCEPT_EULA: "Y"
      MSSQL_PID: "Developer"
    ports:
      - "1433:1433"
    volumes:
      - mssqldata:/var/opt/mssql
  adminer:
    image: adminer:4.8.1
    ports:
      - "8080:8080"
volumes:
	mssqldata:
```



