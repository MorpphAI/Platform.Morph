
## 📘 Função: `get_job_description`

- **Rota:** `POST /rest/v1/rpc/get_job_description`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/get_job_description`  
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
| `p_job_id` | uuid | Sim         | ID da vaga que será buscada |

---

### 📤 Exemplo de resposta (response)

#### ✅ Descrição encontrada:

```json
{
  "status": "200 OK",
  "message": "Descrição encontrada.",
  "descricao": "Esta vaga é para atuação com projetos internacionais..."
}
```

#### ℹ️ Nenhuma descrição encontrada:

```json
{
  "status": "200 OK",
  "message": "Nenhuma descrição encontrada para esta vaga."
}
```

---

### 💬 Descrição

Essa função retorna o conteúdo do campo `descricao` da tabela `job_descriptions` referente ao `job_id` informado.  
Caso não exista descrição registrada para a vaga, a função ainda responde com status `200 OK`, porém com uma mensagem informativa.

---

## 📘 Função: `save_job_description`

- **Rota:** `POST /rest/v1/rpc/save_job_description`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/save_job_description`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_job_id": "uuid-da-vaga",
  "p_descricao": "Esta vaga exige experiência com projetos ágeis, liderança técnica e arquitetura backend."
}
```

| Campo         | Tipo | Obrigatório | Descrição                                     |
|---------------|------|-------------|-----------------------------------------------|
| `p_job_id`    | uuid | Sim         | ID da vaga para a qual a descrição será salva |
| `p_descricao` | text | Sim         | Conteúdo da descrição da vaga                 |

---

### 📤 Exemplo de resposta (response)

```json
{
  "status": "200 OK",
  "message": "Descrição da vaga salva com sucesso!",
  "description_id": "uuid-da-descricao"
}
```

---

### 💬 Descrição

Essa função salva (ou registra) uma descrição de vaga na tabela `job_descriptions`.  
Ela associa um texto descritivo a um `job_id` e retorna o `id` da nova descrição inserida.

---

## 📘 Função: `update_description_job`

- **Rota:** `POST /rest/v1/rpc/update_description_job`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/update_description_job`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_job_id": "uuid-da-vaga",
  "p_description": "Atualização da descrição com requisitos mais recentes da vaga."
}
```

| Campo           | Tipo | Obrigatório | Descrição                                        |
|-----------------|------|-------------|--------------------------------------------------|
| `p_job_id`      | uuid | Sim         | ID da vaga cuja descrição será atualizada       |
| `p_description` | text | Sim         | Novo conteúdo da descrição da vaga              |

---

### 📤 Exemplo de resposta (response)

#### ✅ Atualização bem-sucedida:

```json
{
  "status": "200 OK",
  "message": "Descrição da vaga atualizada com sucesso."
}
```

#### ❌ Nenhuma descrição encontrada:

```json
{
  "status": "404 Not Found",
  "message": "Nenhuma descrição encontrada para atualizar."
}
```

---

### 💬 Descrição

Essa função atualiza a descrição de uma vaga, caso ela já exista na tabela `job_descriptions`.  
Se não houver descrição registrada previamente para o `job_id` informado, a função retorna uma mensagem de erro `404`.

<p align="left"> <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/content/functions.md">⬅ Voltar para o índice de endpoints</a> </p> 

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/README.md"> Ver login endpoints</a>
</p>

