# 🔐 Documentação – Usuários <img align="right" src="https://github.com/MorpphAI/platform.Morph/blob/main/images/morphTrans.png" alt="Logo Morph" width="60">

Nesta página estão documentadas as functions relacionadas à **Usuários **. 

---

## 📘 Função: `get_user_data`

- **Rota:** `POST /rest/v1/rpc/get_user_data`
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/get_user_data`
- **Tipo de requisição:** `POST`
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

### 📝 Parâmetros esperados (request)

```json
{
  "p_user_id": "ad8df596-6d25-4a8f-a958-8eb45ad3b2b9"
}
```

| Campo       | Tipo   | Obrigatório | Descrição                        |
| ----------- | ------ | ----------- | -------------------------------- |
| `p_user_id` | string | Sim         | UUID do usuário a ser consultado |

### 📝 Parâmetros esperados 📤 Exemplo de resposta (response)

```json
{
  "user": {
    "id": "ad8df596-6d25-4a8f-a958-8eb45ad3b2b9",
    "nome": "Adilson Junior",
    "cargo": "Consultor de RH",
    "plano": "paying",
    "telefone": "11994598801",
    "num_vagas": "26–50",
    "thread_id": "thread_ch9lZkEI8ihjWuJyU4TbXpmh",
    "created_at": "2025-04-18T15:57:00",
    "first_date": "2025-04-18",
    "nome_empresa": "morph "
  },
  "status": "200 OK"
}
```
### 💬 Descrição
Essa função retorna os dados completos de um usuário cadastrado, com base no seu user_id.
É usada principalmente após o login, para carregar as informações do usuário logado no painel.

***
---

## 📘 Função: `get_auth_user_data`

- **Rota:** `POST /rest/v1/rpc/get_auth_user_data`
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/get_auth_user_data`
- **Tipo de requisição:** `POST`
- **Autenticação:** ✅ (Requer token JWT válido)

### 📝 Parâmetros esperados (request)

```json
{
  "p_user_id": "ad8df596-6d25-4a8f-a958-8eb45ad3b2b9"
}
```
| Campo       | Tipo   | Obrigatório | Descrição                        |
| ----------- | ------ | ----------- | -------------------------------- |
| `p_user_id` | string | Sim         | UUID do usuário no Supabase Auth |

```json
{
  "status": "200 OK",
  "auth_user": {
    "id": "ad8df596-6d25-4a8f-a958-8eb45ad3b2b9",
    "role": "authenticated",
    "email": "adilson.juniorcomunicacao@gmail.com",
    "phone": null,
    "created_at": "2025-04-18T18:57:08.991479+00:00",
    "user_metadata": {
      "sub": "ad8df596-6d25-4a8f-a958-8eb45ad3b2b9",
      "email": "adilson.juniorcomunicacao@gmail.com",
      "email_verified": true,
      "phone_verified": false
    },
    "last_sign_in_at": "2025-05-12T22:50:45.982819+00:00"
  }
}
```

### 💬 Descrição
Essa função retorna os dados brutos de autenticação do usuário, diretamente da tabela do Supabase Auth.

É útil para obter informações como:

E-mail e status de verificação

Data de criação do usuário

Último login

Metadados adicionais do usuário autenticado

---

## 📘 Função: `check_user_job_limit`

- **Rota:** `POST /rest/v1/rpc/check_user_job_limit`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/check_user_job_limit`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_user_id": "ad8df596-6d25-4a8f-a958-8eb45ad3b2b9"
}
```
| Campo       | Tipo   | Obrigatório | Descrição                        |
| ----------- | ------ | ----------- | -------------------------------- |
| `p_user_id` | string | Sim         | UUID do usuário a ser verificado |

---

### 📤 Exemplo de resposta (response)

#### ✅ Caso o plano seja válido:

```json
{
  "status": "200 OK",
  "message": "Verificação de limite concluída.",
  "jobs": 12,
  "plan": "free",
  "can_create_more_jobs": true
}
```
#### ❌ Caso o plano seja inválido ou não reconhecido:

```json
{
  "status": "400 Bad Request",
  "message": "Plano inválido para este usuário."
}
```
---

### 💬 Descrição

Essa função verifica se um usuário pode criar novas vagas com base no plano atual (`free` ou `paying`):

- **Plano `free`**: pode criar até 25 vagas.
- **Plano `paying`**: criação ilimitada de vagas.
- Caso o plano do usuário esteja indefinido ou incorreto, uma mensagem de erro é retornada.

---

### 🔁 Lógica Interna

1. O plano do usuário é buscado da tabela `users`.
2. Conta-se quantas vagas o usuário já criou na tabela `jobs`.
3. Com base no plano:
   - `free`: é permitido criar até 25 vagas.
   - `paying`: criação ilimitada.
4. Retorna um JSON com os dados relevantes.

<p align="left"> <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/content/functions.md">⬅ Voltar para o índice de endpoints</a> </p> 

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/README.md"> Ver login endpoints</a>
</p>
