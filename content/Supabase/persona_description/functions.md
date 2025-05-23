
## 📘 Função: `get_persona_description`

- **Rota:** `POST /rest/v1/rpc/get_persona_description`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/get_persona_description`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_job_id": "uuid-da-vaga"
}
```

| Campo      | Tipo | Obrigatório | Descrição                   |
|------------|------|-------------|-----------------------------|
| `p_job_id` | uuid | Sim         | ID da vaga relacionada à persona |

---

### 📤 Exemplo de resposta (response)

#### ✅ Persona encontrada:

```json
{
  "status": "200 OK",
  "message": "Persona encontrada.",
  "descricao": "Perfil ideal de candidato para projetos internacionais..."
}
```

#### ℹ️ Nenhuma persona encontrada:

```json
{
  "status": "200 OK",
  "message": "Nenhuma persona encontrada para esta vaga."
}
```

---

### 💬 Descrição

Essa função retorna a descrição da persona ideal associada a uma vaga (via `job_id`) na tabela `persona_descriptions`.  
Caso não exista descrição, retorna um status `200 OK` com uma mensagem informativa.

---

## 📘 Função: `create_persona_description`

- **Rota:** `POST /rest/v1/rpc/create_persona_description`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/create_persona_description`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_job_id": "uuid-da-vaga",
  "p_descricao": "Perfil desejado: proatividade, experiência em projetos ágeis, boa comunicação..."
}
```

| Campo         | Tipo | Obrigatório | Descrição                                  |
|---------------|------|-------------|--------------------------------------------|
| `p_job_id`    | uuid | Sim         | ID da vaga para a qual será criada a persona |
| `p_descricao` | text | Sim         | Conteúdo da descrição da persona           |

---

### 📤 Exemplo de resposta (response)

```json
{
  "status": "201 Created",
  "message": "Persona cadastrada com sucesso."
}
```

---

### 💬 Descrição

Essa função insere uma nova descrição de persona na tabela `persona_descriptions`, associada a um `job_id`.

---

## 📘 Função: `update_persona_description`

- **Rota:** `POST /rest/v1/rpc/update_persona_description`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/update_persona_description`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_job_id": "uuid-da-vaga",
  "p_description": "Nova descrição da persona com perfil atualizado.",
  "p_user_id": "uuid-do-usuario"
}
```

| Campo           | Tipo | Obrigatório | Descrição                                       |
|-----------------|------|-------------|-------------------------------------------------|
| `p_job_id`      | uuid | Sim         | ID da vaga cuja persona será atualizada        |
| `p_description` | text | Sim         | Nova descrição da persona                      |
| `p_user_id`     | uuid | Sim         | ID do usuário responsável pela atualização     |

---

### 📤 Exemplo de resposta (response)

#### ✅ Atualização bem-sucedida:

```json
{
  "status": "200 OK",
  "message": "Descrição da persona atualizada com sucesso."
}
```

#### ❌ Nenhuma persona encontrada:

```json
{
  "status": "404 Not Found",
  "message": "Nenhuma descrição encontrada para atualizar."
}
```

---

### 💬 Descrição

Essa função atualiza a descrição da persona associada a um `job_id`.  
Além da atualização, um log é automaticamente registrado na tabela `activity_logs` contendo os detalhes da modificação, incluindo o `job_name`, `user_id`, valor anterior e novo valor.
