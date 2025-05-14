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
