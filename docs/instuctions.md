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

Then activate the env and run ingestion:

```bash
conda activate FDE_ENV
python scripts/ingest_legacy_data.py
```
