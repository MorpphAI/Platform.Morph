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
