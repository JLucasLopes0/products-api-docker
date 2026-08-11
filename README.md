# Products API Docker

API REST enxuta para revisar e praticar containerização com Docker e Docker Compose em um backend ASP.NET Core integrado ao PostgreSQL.

## Tecnologias

- .NET 8
- ASP.NET Core Web API
- Entity Framework Core
- PostgreSQL 16
- Docker
- Docker Compose
- Swagger/OpenAPI

## Como executar com Docker Compose

Na raiz do projeto, execute:

```bash
docker compose up --build
```

A API fica disponível em:

```text
http://localhost:8080/swagger
```

O PostgreSQL é exposto no host em:

```text
localhost:5433
```

Credenciais locais do banco:

```text
Database: productsdb
Username: postgres
Password: postgres
```

Ao iniciar, a API aplica as migrations do Entity Framework automaticamente. Isso permite subir o ambiente em um volume novo sem criar as tabelas manualmente.

## Endpoints principais

```http
GET /products
GET /products/{id}
POST /products
```

Exemplo de criação de produto:

```json
{
  "name": "Notebook Gamer",
  "price": 7500
}
```

## Como executar localmente sem Docker

Suba um PostgreSQL local compatível com a connection string de `src/ProductsApi/appsettings.json`:

```json
"Host=localhost;Port=5433;Database=productsdb;Username=postgres;Password=postgres"
```

Depois execute:

```bash
dotnet restore
dotnet run --project src/ProductsApi/ProductsApi.csproj
```

## Estrutura

```text
.
├── docker-compose.yml
├── src/
│   └── ProductsApi/
│       ├── Controllers/
│       ├── Data/
│       ├── Migrations/
│       ├── Models/
│       ├── Dockerfile
│       └── Program.cs
└── backup.sql
```

## Objetivo do projeto

Este repositório demonstra a containerização de uma API .NET com banco PostgreSQL usando Docker Compose, incluindo build multi-stage, rede entre containers, volume persistente e execução local reproduzível.
