# Ingesting data

Download the dataset from `data/source/data.txt`.

Create an EC2 instance / Docker host, then spin up the Legacy MSSQL Server:

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=FdeEnterprisePass123!" \
  -p 1433:1433 --name legacy-mssql \
  -d mcr.microsoft.com/mssql/server:2022-latest
```

Connect with sqlcmd:

```bash
docker exec -it legacy-mssql /opt/mssql-tools18/bin/sqlcmd \
  -S localhost -U sa -P 'FdeEnterprisePass123!' -C
```
 
sqlcmd -S localhost,1433 -U sa -P 'FdeEnterprisePass123!'

# Then activate the env and run ingestion:

```bash
conda activate FDE_ENV
python scripts/ingest_legacy_data.py
```


We need to query the database
Download: https://github.com/microsoft/azuredatastudio
-https://learn.microsoft.com/en-us/previous-versions/azure-data-studio/
download-azure-data-studio?
tabs-win-install%2Cwin-user-install%2Credhat-install%2Cwindows-uninstall%2Cre
dhat-uninstall
The recommendation is to use VS code extension: "SQL Server (mssql)" by
microsoft
I


SELECT COUNT(*) AS total_rows FROM dbo.TBL_SC_FLEET_HIST_RAW;