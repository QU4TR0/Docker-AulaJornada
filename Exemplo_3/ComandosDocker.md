# Comandos Docker
Iniciar contâiner PostgreSQL
```bash
# Iniciar contêiner PostgreSQL
docker run --name postgres-dados -e POSTGRES_PASSWORD=segredo -e POSTGRES_USER=analista -e POSTGRES_DB=datawarehouse -p 5432:5432 -d postgres:14.8
```
Verificar status do contêiner
```bash
# Verificar status do contêiner
docker ps
```
Acessar o banco de dados
```bash
# Executar o cliente psql dentro do contêiner
docker exec -it postgres-dados psql -U analista -d datawarehouse

# No exemplo isolado, o banco começa vazio
# No Docker Compose, será preenchido com dados iniciais e através da API
```
Gerenciar o contêiner
```bash
# Parar o contêiner
docker stop postgres-dados

# Reiniciar o contêiner
docker start postgres-dados
```

## Persistência
Executar PostgreSQL com volume
```bash
# Executar PostgreSQL com volume para persistência
docker run --name postgres-dados \
  -e POSTGRES_PASSWORD=segredo \
  -e POSTGRES_USER=analista \
  -e POSTGRES_DB=datawarehouse \
  -v postgres_data:/var/lib/postgresql/data \
  -p 5432:5432 \
  -d postgres:14.8
```
Conexão externa
```bash
# Acessar usando ferramentas externas
# Host: localhost
# Port: 5432
# User: analista
# Password: segredo
# Database: datawarehouse
```
Backup e restauração
```bash
# Criar backup do banco de dados
docker exec -t postgres-dados pg_dump -U analista -d datawarehouse > backup.sql

# Restaurar backup (para um contêiner novo)
# 1. Criar novo contêiner
docker run --name postgres-dados-novo -e POSTGRES_PASSWORD=segredo -e POSTGRES_USER=analista -e POSTGRES_DB=datawarehouse -v postgres_data_novo:/var/lib/postgresql/data -p 5433:5432 -d postgres:14.8

# 2. Restaurar dados
cat backup.sql | docker exec -i postgres-dados-novo psql -U analista -d datawarehouse
```
