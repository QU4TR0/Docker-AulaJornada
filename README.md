# Docker-AulaJornada
Este repositório são arquivos de estudo desenvolvidos na aula da jornada de Dados sobre Docker. Foram realizados 4 exemplos de containerização e os mesmos estão contemplados abaixo:

## [Exemplo 1](https://github.com/QU4TR0/Docker-AulaJornada/Exemplo_1)
Criar arquivo com dependências
```bash
# Criar o arquivo requirements.txt
echo "streamlit==1.44.0
pandas==2.2.3
matplotlib==3.10.1" > requirements.txt
```
Construir imagem Docker
```bash
# Construir a imagem Docker
docker build -t dashboard-vendas .
```
Executar o contâiner
```bash
# Executar o contêiner
docker run -p 8501:8501 -d --name streamlit-app dashboard-vendas

# Acessar o dashboard
# Abra seu navegador em http://localhost:8501
```
Benefícios neste exemplo:

- Dashboard de visualização de dados pronto para uso em qualquer ambiente
- Sem necessidade de instalar Python, Streamlit ou outras dependências no host
- Portabilidade para compartilhar facilmente com a equipe
- Ambiente isolado com versões específicas das bibliotecas


## [Exemplo 2](https://github.com/QU4TR0/Docker-AulaJornada/Exemplo_2)
Criar arquivo com dependências

```bash
# Criar o arquivo requirements.txt
echo "fastapi==0.115.12
uvicorn==0.34.0
pandas==2.2.3
pydantic==2.11.1" > requirements.txt
```

Construir imagem Docker

```bash
# Construir a imagem Docker
docker build -t api-vendas .
```

Executar o contâiner e testar API

```bash
# Executar o contêiner
docker run -p 8000:8000 -d --name fastapi-app api-vendas

# Testar a API
# Acesse http://localhost:8000/docs para ver a documentação interativa
```
Benefícios neste exemplo:

- API de dados pronta para consumo por outras aplicações
- Documentação interativa automática com Swagger UI
- Isolamento de dependências e versões específicas
- Fácil implantação em qualquer ambiente que tenha Docker

## [Exemplo 3](https://github.com/QU4TR0/Docker-AulaJornada/Exemplo_3)
[Comandos Docker](https://github.com/QU4TR0/Docker-AulaJornada/Exemplo_3/ComandosDocker.md)

Benefícios neste exemplo:

- Banco de dados para análise pronto para uso em segundos
- Persistência de dados com volumes Docker
- Isolamento completo do sistema host
- Fácil backup e restauração
- Possibilidade de executar múltiplas versões do PostgreSQL no mesmo sistema

## [Exemplo 4](https://github.com/QU4TR0/Docker-AulaJornada/Exemplo_4)
[Comandos](https://github.com/QU4TR0/Docker-AulaJornada/Exemplo_4/Comandos.md)

### Benefícios neste exemplo:

- Stack completa de análise de dados orquestrada com um único comando
- Comunicação entre serviços usando a rede interna do Docker
- Fluxo de dados bidirecional: inserção de dados via dashboard → API → banco de dados
- Atualização em tempo real dos gráficos após inserção de novos dados
- Persistência de dados com volumes Docker
- Pipeline de dados completo com feedback circular

### Fluxo completo de dados:

1. Usuário insere dados no dashboard Streamlit
2. Dashboard envia dados para a API FastAPI
3. API persiste dados no PostgreSQL
4. Dashboard consulta API para atualizar visualizações
5. API obtém dados do PostgreSQL
