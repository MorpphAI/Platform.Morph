# Documentação do Endpoint de Login

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
}
```

### Params

Também é possivel passar a key por parametro no corpo de url, seria algo assim: 

```text
https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/users?apikey=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh3YmR2YXFnZ2NkZmdzcW54aWNvIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MzQzNjEwNTksImV4cCI6MjA0OTkzNzA1OX0.SQFXuWYP4p6LA5HLko691Gkkpetnu_Zq7YSCb8sVzD8
```
