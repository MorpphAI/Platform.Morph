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


<p align="left"> <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/content/functions.md">⬅ Voltar para o índice de endpoints</a> </p> 

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/README.md"> Ver login endpoints</a>
</p>
