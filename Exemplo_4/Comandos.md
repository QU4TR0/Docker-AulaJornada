# Comandos

Estrutura inicial do projeto
```bash
# Estrutura de diretórios
mkdir -p projeto-dados/{api,dashboard}
```
Script de inicialização do banco
```bash
# Criar script de inicialização do banco
cat > init.sql << 'EOF'
CREATE TABLE vendas (
    id SERIAL PRIMARY KEY,
    data_venda DATE NOT NULL,
    produto VARCHAR(100) NOT NULL,
    categoria VARCHAR(50) NOT NULL,
    valor DECIMAL(10,2) NOT NULL,
    quantidade INT NOT NULL
);

INSERT INTO vendas (data_venda, produto, categoria, valor, quantidade)
VALUES 
  ('2025-01-15', 'Curso Python', 'Educação', 197.00, 45),
  ('2025-01-20', 'Assinatura BI', 'Software', 89.90, 28),
  ('2025-02-05', 'Consultoria', 'Serviços', 1200.00, 3),
  ('2025-02-12', 'Curso SQL', 'Educação', 147.00, 52),
  ('2025-03-01', 'Licença Tableau', 'Software', 999.00, 15);
EOF
```
Configuração da API
```bash
# Criar Dockerfile para a API
cat > api/Dockerfile << 'EOF'
FROM python:3.12-slim

WORKDIR /app

# Copiar e instalar dependências
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiar código
COPY . .

# Expor porta para a API
EXPOSE 8000

# Iniciar API com Uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
EOF

# Requisitos para a API
cat > api/requirements.txt << 'EOF'
fastapi==0.115.12
uvicorn==0.34.0
pydantic==2.11.1
sqlalchemy==2.0.22
psycopg2-binary==2.9.9
EOF
```
Configuração do Dashboard
```bash
# Criar Dockerfile para o Dashboard
cat > dashboard/Dockerfile << 'EOF'
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["streamlit", "run", "app.py", "--server.address=0.0.0.0"]
EOF

# Requisitos para o Dashboard
cat > dashboard/requirements.txt << 'EOF'
streamlit==1.44.0
pandas==2.2.3
plotly==5.18.0
requests==2.31.0
EOF
```
Gerenciar Docker Compose
```bash
# Iniciar todos os serviços
docker-compose up -d

# Verificar logs dos serviços
docker-compose logs -f

# Parar todos os serviços
docker-compose down

# Parar e remover volumes (limpar dados)
docker-compose down -v
```