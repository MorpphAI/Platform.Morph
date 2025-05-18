## 📘 Função: `login` (Autenticação de usuário)

- **Rota:** `POST /auth/v1/token?grant_type=password`
- **URL completa:**  
  `https://xwbdvaqggcdfgsqnxico.supabase.co/auth/v1/token?grant_type=password`
- **Tipo de requisição:** `POST`
- **Autenticação:** ❌ (Endpoint público para login)

---

### 📝 Parâmetros esperados (request)

```json
{
  "email": "adilson.juniorcomunicacao@gmail.com",
  "password": "adilson1234"
}
```

| Campo      | Tipo   | Obrigatório | Descrição               |
| ---------- | ------ | ----------- | ----------------------- |
| `email`    | string | Sim         | E-mail do usuário       |
| `password` | string | Sim         | Senha usada no cadastro |

```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6...",
  "token_type": "bearer",
  "expires_in": 3600,
  "refresh_token": "y9xKf4s95...",
  "user": {
    "id": "ad8df596-6d25-4a8f-a958-8eb45ad3b2b9",
    "email": "adilson.juniorcomunicacao@gmail.com"
  }
}
```

### 💬 Descrição
Esse endpoint é utilizado para autenticar o usuário com e-mail e senha, retornando um JWT (access_token) e um refresh_token, que serão usados em chamadas autenticadas aos serviços do Supabase (como funções protegidas e acesso a dados).

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/README.md">⬅ Voltar para o menu principal</a>
</p>

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/content/Supabase/users/functions.md"> ver os endpoints de redefinir senha </a>
</p>
