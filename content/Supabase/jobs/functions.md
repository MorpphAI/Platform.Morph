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

---
## 📘 Função: `create__job`

- **Rota:** `POST /rest/v1/rpc/create__job`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/create__job`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_user_id": "uuid-do-usuario",
  "p_titulo_cargo": "Desenvolvedor Backend",
  "p_salario": 8000,
  "p_beneficios": "Plano de saúde, Vale alimentação",
  "p_regime_contratacao": "CLT",
  "p_localizacao": "São Paulo - SP",
  "p_observacoes": "Disponibilidade para início imediato",
  "p_arquivos": null,
  "p_escolaridade": "Superior completo",
  "p_certificacoes": "AWS, Scrum",
  "p_idiomas": "Inglês, Espanhol",
  "p_experiencia_profissional": "3 anos como dev backend",
  "p_horarios": "Segunda a Sexta, horário comercial",
  "p_habilidades_tecnicas": "Node.js, PostgreSQL",
  "p_habilidades_interpessoais": "Trabalho em equipe, Comunicação",
  "p_company_id": "uuid-da-empresa"
}
```
| Campo                         | Tipo     | Obrigatório | Descrição                                 |
|------------------------------|----------|-------------|-------------------------------------------|
| `p_user_id`                  | uuid     | Sim         | ID do usuário que está criando a vaga     |
| `p_titulo_cargo`             | text     | Sim         | Título do cargo                           |
| `p_salario`                  | numeric  | Sim         | Salário ofertado                          |
| `p_beneficios`               | text     | Não         | Benefícios adicionais                     |
| `p_regime_contratacao`       | text     | Sim         | Regime de contratação (CLT, PJ etc.)      |
| `p_localizacao`              | text     | Sim         | Local da vaga                             |
| `p_observacoes`              | text     | Não         | Observações adicionais                    |
| `p_arquivos`                 | text     | Não         | Arquivos relacionados (links, uploads)    |
| `p_escolaridade`             | text     | Não         | Nível de escolaridade exigido             |
| `p_certificacoes`            | text     | Não         | Certificações desejadas                   |
| `p_idiomas`                  | text     | Não         | Idiomas desejados                         |
| `p_experiencia_profissional` | text     | Não         | Experiência necessária                    |
| `p_horarios`                 | text     | Não         | Horário de trabalho                       |
| `p_habilidades_tecnicas`     | text     | Não         | Habilidades técnicas exigidas             |
| `p_habilidades_interpessoais`| text     | Não         | Soft skills esperadas                     |
| `p_company_id`               | uuid     | Sim         | ID da empresa associada                   |

---

### 📤 Exemplo de resposta (response)

```json
{
  "status": "200 OK",
  "message": "Vaga criada com sucesso!",
  "job_id": "b5989f4e-e0b7-4cd4-a43d-77b1ff934d6c",
  "job_name": "Desenvolvedor Backend"
}
```
---

### 💬 Descrição

Essa função insere uma nova vaga na tabela `jobs`, com base nas informações fornecidas pelo usuário autenticado. Após a criação da vaga, também registra automaticamente um log da atividade na tabela `activity_logs`, com o tipo de atividade `"Vaga Criada"`.

---

### 🔁 Lógica Interna

1. Insere uma nova vaga na tabela `jobs`.
2. Captura o `id` e `titulo_cargo` da vaga recém-criada.
3. Insere um registro de log em `activity_logs` informando a criação.
4. Retorna um JSON com o status da operação, `job_id` e `job_name`.

---

## 📘 Função: `get_job_by_id`

- **Rota:** `POST /rest/v1/rpc/get_job_by_id`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/get_job_by_id`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_job_id": "uuid-da-vaga"
}
```
| Campo       | Tipo   | Obrigatório | Descrição                     |
|-------------|--------|-------------|-------------------------------|
| `p_job_id`  | uuid   | Sim         | ID da vaga a ser consultada   |

---

### 📤 Exemplo de resposta (response)

#### ✅ Vaga encontrada:

```json
{
  "status": "200 OK",
  "message": "Vaga encontrada.",
  "job": {
    "id": "uuid-da-vaga",
    "user_id": "uuid-do-usuario",
    "titulo_cargo": "Analista de Dados",
    "salario": 7000,
    "beneficios": "VR, VT",
    ...
    "descricao": "Responsável por análises de BI e relatórios estratégicos"
  }
}
```
#### ❌ Vaga não encontrada:

```json
{
  "status": "404 NOT FOUND",
  "message": "Vaga não encontrada com o ID fornecido."
}
```
---

### 💬 Descrição

Essa função busca uma vaga específica a partir do seu `job_id`, unindo os dados da tabela `jobs` com o campo `descricao` da tabela `job_descriptions`.  
Se a vaga não for encontrada, retorna um erro 404 com mensagem personalizada.

---

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
| Campo       | Tipo   | Obrigatório | Descrição                   |
|-------------|--------|-------------|-----------------------------|
| `p_job_id`  | uuid   | Sim         | ID da vaga que será buscada |

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

## 📘 Função: `get_jobs_by_step`

- **Rota:** `POST /rest/v1/rpc/get_jobs_by_step`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/get_jobs_by_step`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_user_id": "uuid-do-usuario",
  "p_step": "draft"
}
```
| Campo       | Tipo   | Obrigatório | Descrição                                      |
|-------------|--------|-------------|------------------------------------------------|
| `p_user_id` | uuid   | Sim         | ID do usuário cujas vagas serão consultadas    |
| `p_step`    | text   | Sim         | Etapa da vaga (ex: draft, published, archived) |

---

### 📤 Exemplo de resposta (response)

#### ✅ Vagas encontradas:

```json
{
  "status": "200 OK",
  "message": "Vagas encontradas.",
  "jobs": [
    {
      "id": "uuid-da-vaga-1",
      "titulo_cargo": "Desenvolvedor Frontend",
      "step": "draft",
      ...
    },
    {
      "id": "uuid-da-vaga-2",
      "titulo_cargo": "Analista de Dados",
      "step": "draft",
      ...
    }
  ]
}
```
#### ℹ️ Nenhuma vaga encontrada:

```json
{
  "status": "200 OK",
  "message": "Nenhuma vaga encontrada para esse usuário nessa etapa."
}
```
---

### 💬 Descrição

Essa função retorna todas as vagas associadas a um determinado `user_id` que estejam em uma etapa específica (`p_step`), como por exemplo: `"draft"`, `"published"`, `"archived"`, etc.

Os resultados são ordenados da mais recente para a mais antiga com base na data de criação (`created_at`).

---

## 📘 Função: `get_user_jobs`

- **Rota:** `POST /rest/v1/rpc/get_user_jobs`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/get_user_jobs`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_user_id": "uuid-do-usuario",
  "p_company_id": "uuid-da-empresa",
  "p_contract": "CLT",
  "p_status": "Rascunho",
  "p_start_date": "2025-01-01T00:00:00",
  "p_end_date": "2025-12-31T23:59:59",
  "p_search": "Desenvolvedor",
  "p_page": 1
}
```
| Campo          | Tipo      | Obrigatório | Descrição                                                             |
|----------------|-----------|-------------|-----------------------------------------------------------------------|
| `p_user_id`    | uuid      | Sim         | ID do usuário proprietário das vagas                                  |
| `p_company_id` | uuid      | Não         | ID da empresa (opcional — se fornecido, filtra vagas dessa empresa)   |
| `p_contract`   | text      | Não         | Tipo de contrato (ex: "CLT", "PJ")                                     |
| `p_status`     | text      | Não         | Status da vaga (ex: "Rascunho", "Publicada", etc.)                    |
| `p_start_date` | timestamp | Não         | Data inicial para filtro por criação de vaga                           |
| `p_end_date`   | timestamp | Não         | Data final para filtro por criação de vaga                             |
| `p_search`     | text      | Não         | Termo de busca no título da vaga                                       |
| `p_page`       | integer   | Sim         | Número da página para paginação (mínimo 1)                             |

---

### 📤 Exemplo de resposta (response)

```json
{
  "data": [
    {
      "id": "uuid-da-vaga",
      "titulo_cargo": "Desenvolvedor Backend",
      "status": "Publicada",
      ...
    }
  ],
  "pageSize": 10,
  "currentPage": 1,
  "totalPages": 3,
  "isLastPage": false
}
```
---

### 💬 Descrição

Essa função retorna uma lista paginada de vagas do usuário, permitindo aplicar **filtros por empresa**, **tipo de contrato**, **status**, **intervalo de datas** e **busca textual** no título da vaga. O resultado é ordenado pela data de criação (`created_at`) da mais recente para a mais antiga.

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
| Campo         | Tipo   | Obrigatório | Descrição                                     |
|---------------|--------|-------------|-----------------------------------------------|
| `p_job_id`    | uuid   | Sim         | ID da vaga para a qual a descrição será salva |
| `p_descricao` | text   | Sim         | Conteúdo da descrição da vaga                 |

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

| Campo           | Tipo   | Obrigatório | Descrição                                        |
|-----------------|--------|-------------|--------------------------------------------------|
| `p_job_id`      | uuid   | Sim         | ID da vaga cuja descrição será atualizada       |
| `p_description` | text   | Sim         | Novo conteúdo da descrição da vaga              |

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

---

## 📘 Função: `update_job`

- **Rota:** `POST /rest/v1/rpc/update_job`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/update_job`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_job_id": "uuid-da-vaga",
  "p_idiomas": "Inglês, Espanhol",
  "p_salario": 8000,
  "p_arquivos": null,
  "p_horarios": "Horário comercial",
  "p_beneficios": "VR, VT",
  "p_localizacao": "São Paulo",
  "p_observacoes": "Preferência para início imediato",
  "p_escolaridade": "Superior completo",
  "p_titulo_cargo": "Dev Backend",
  "p_certificacoes": "Scrum, AWS",
  "p_regime_contratacao": "CLT",
  "p_habilidades_tecnicas": "Node.js, PostgreSQL",
  "p_experiencia_profissional": "3 anos de experiência",
  "p_habilidades_interpessoais": "Trabalho em equipe",
  "p_status": "Publicada",
  "p_step": "final",
  "p_company_id": "uuid-da-empresa"
}
```
| Campo                        | Tipo     | Obrigatório | Descrição                                         |
|-----------------------------|----------|-------------|---------------------------------------------------|
| `p_job_id`                  | uuid     | Sim         | ID da vaga a ser atualizada                       |
| `p_titulo_cargo`            | text     | Não         | Novo título do cargo                              |
| `p_salario`                 | numeric  | Não         | Novo salário                                      |
| `p_beneficios`              | text     | Não         | Benefícios atualizados                            |
| `p_regime_contratacao`      | text     | Não         | Tipo de contrato                                  |
| `p_localizacao`             | text     | Não         | Local da vaga                                     |
| `p_observacoes`             | text     | Não         | Observações adicionais                            |
| `p_arquivos`                | text     | Não         | Arquivos relacionados                             |
| `p_escolaridade`            | text     | Não         | Escolaridade mínima exigida                       |
| `p_certificacoes`           | text     | Não         | Certificações desejadas                           |
| `p_idiomas`                 | text     | Não         | Idiomas desejados                                 |
| `p_experiencia_profissional`| text     | Não         | Experiência necessária                            |
| `p_horarios`                | text     | Não         | Horário de trabalho                               |
| `p_habilidades_tecnicas`    | text     | Não         | Habilidades técnicas exigidas                     |
| `p_habilidades_interpessoais`| text    | Não         | Soft skills desejadas                             |
| `p_status`                  | text     | Não         | Novo status da vaga                               |
| `p_step`                    | text     | Não         | Etapa da vaga no funil                            |
| `p_company_id`              | uuid     | Não         | ID da empresa associada                           |

---

### 📤 Exemplo de resposta (response)

```json
{
  "status": "200 OK",
  "message": "Vaga atualizada com sucesso!",
  "job_id": "uuid-da-vaga"
}
```

#### ❌ Caso a vaga não seja encontrada:

```json
{
  "status": "400 Bad Request",
  "message": "Vaga não encontrada ou erro na atualização."
}

```

---

### 💬 Descrição

Essa função atualiza os campos de uma vaga existente na tabela `jobs`. Ela utiliza `COALESCE` para manter os valores antigos caso não sejam enviados novos valores.  
Além da atualização, a função também registra **dois logs na tabela `activity_logs`**:

- Um log de atualização geral da vaga (`Vaga Atualizada`).
- Um log específico se o campo `status` for alterado (`Status da Vaga Atualizado`).

---

## 📘 Função: `update_job_description`

- **Rota:** `POST /rest/v1/rpc/update_job_description`  
- **URL completa:** `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/rpc/update_job_description`  
- **Tipo de requisição:** `POST`  
- **Autenticação:** ✅ (Requer token JWT de usuário autenticado)

---

### 📝 Parâmetros esperados (request)

```json
{
  "p_job_id": "uuid-da-vaga",
  "p_descricao": "Atualização completa da descrição da vaga com novos requisitos."
}

| Campo         | Tipo   | Obrigatório | Descrição                                       |
|---------------|--------|-------------|-------------------------------------------------|
| `p_job_id`    | uuid   | Sim         | ID da vaga cuja descrição será atualizada      |
| `p_descricao` | text   | Sim         | Nova descrição da vaga                         |
```
---

### 📤 Exemplo de resposta (response)

#### ✅ Descrição atualizada com sucesso:

```json
{
  "status": "200 OK",
  "message": "Descrição da vaga atualizada com sucesso!",
  "job_id": "uuid-da-vaga"
}
```
#### ❌ Descrição não encontrada para o job_id informado:

```json
{
  "status": "404 Not Found",
  "message": "Nenhuma descrição encontrada para esta vaga."
}
```
---

### 💬 Descrição

Essa função atualiza a descrição de uma vaga existente na tabela `job_descriptions`.  
Se o `job_id` não possuir uma descrição cadastrada, a função retorna um erro 404.  
Além disso, um **log de atividade** é registrado na tabela `activity_logs`, detalhando a alteração feita.

---

🔙 [Voltar para o índice de endpoints](https://github.com/MorpphAI/Platform.Morph/blob/main/content/functions.md)
