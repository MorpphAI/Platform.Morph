## 📘 Função: `signup` (Criação de usuário com supanase auth)

- **Rota:** `POST /auth/v1/signup`
- **URL completa:**  
  `https://xwbdvaqggcdfgsqnxico.supabase.co/auth/v1/signup?apikey=<YOUR_API_KEY>`
- **Tipo de requisição:** `POST`
- **Autenticação:** ❌ (Acesso público)

### 📝 Parâmetros esperados (request)

```json
{
  "email": "geyiga9833@hikuhu.com",
  "password": "adilson1234"
}
```
| Campo      | Tipo   | Obrigatório | Descrição                            |
| ---------- | ------ | ----------- | ------------------------------------ |
| `email`    | string | Sim         | E-mail do usuário a ser cadastrado   |
| `password` | string | Sim         | Senha do usuário (mín. 6 caracteres) |


### 📤 Exemplo de resposta (response)
```json
{
  "user": {
    "id": "uuid-gerado",
    "aud": "authenticated",
    "email": "geyiga9833@hikuhu.com",
    "created_at": "2025-05-13T19:20:00.000Z"
  },
  "session": {
    "access_token": "jwt-token",
    "token_type": "bearer",
    "expires_in": 3600,
    "refresh_token": "refresh-token",
    "user": {
      "id": "uuid-gerado",
      "email": "geyiga9833@hikuhu.com"
    }
  }
}
```

### 💬 Descrição
Esse endpoint realiza o cadastro de um novo usuário na base do Supabase Auth.
Ao ser chamado com um email e password válidos, o usuário é criado e já recebe um token de autenticação (JWT) e um refresh token.
A confirmação de e-mail pode ser exigida, dependendo da configuração do seu projeto no Supabase.

---

## 📘 Endpoint: `Criar perfil de usuário` (`/rest/v1/users`)

- **Rota:** `POST /rest/v1/users`
- **URL completa:**  
  `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/users`
- **Tipo de requisição:** `POST`
- **Autenticação:** ✅ (Requer token JWT do usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "id": "beabcb17-c361-4720-85a2-0bd48b336303",
  "nome": "Adilson Júnior",
  "nome_empresa": "Comunicação X",
  "first_date": "2025-01-06",
  "cargo": "diretor-de-rh"
}
```

| Campo          | Tipo   | Obrigatório | Descrição                                           |
| -------------- | ------ | ----------- | --------------------------------------------------- |
| `id`           | string | Sim         | UUID do usuário (deve ser o mesmo do Supabase Auth) |
| `nome`         | string | Sim         | Nome completo do usuário                            |
| `nome_empresa` | string | Sim         | Nome da empresa vinculada                           |
| `first_date`   | string | Sim         | Data do primeiro acesso ou cadastro (formato ISO)   |
| `cargo`        | string | Sim         | Cargo ou função do usuário dentro da empresa        |


### 📤 Exemplo de resposta (response)
```json
{
  "id": "beabcb17-c361-4720-85a2-0bd48b336303",
  "nome": "Adilson Júnior",
  "nome_empresa": "Comunicação X",
  "first_date": "2025-01-06",
  "cargo": "diretor-de-rh"
}
```

### 💬 Descrição
Esse endpoint é utilizado para criar o perfil de um usuário na tabela users logo após ele ser cadastrado via Supabase Auth (/auth/v1/signup).

A ligação entre as duas tabelas é feita pelo campo id, que deve ser o mesmo do Supabase Auth (auth.users.id = users.id), garantindo consistência e permitindo recuperar dados adicionais posteriormente.

É um passo essencial no processo de onboarding da Morph IA.

<p align="left"> <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/content/functions.md">⬅ Voltar para o índice de endpoints</a> </p> 

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/content/Supabase/users/Onboarding/Login/functions.md"> Ver login endpoints</a>
</p>
