# Documentação do Endpoint de Login

Esta documentação explica como utilizar o endpoint de login para verificar usuários na base de dados utilizando o Supabase. O endpoint realiza a busca por email e senha para autenticar um usuário.

---

## Informações Básicas

- **Base URL:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/users`
- **Método:** `GET`
- **Autenticação:** É necessário utilizar a API Key e o Bearer Token.

---

## Configuração do Endpoint

### URL de Requisição

```text
https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/users?email=eq.{email}&senha=eq.{senha}
```

- Substitua `{email}` pelo email do usuário que deseja autenticar.
- Substitua `{senha}` pela senha do usuário.

### Headers

Os headers necessários para realizar a requisição são:

```json
{
  "apikey": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh3YmR2YXFnZ2NkZmdzcW54aWNvIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MzQzNjEwNTksImV4

