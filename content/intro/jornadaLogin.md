
# **Documentação do Endpoint de Login e Cadastro**

## **1. Informações Básicas**

### **Base URL**
- **Autenticação e Criação de Usuários:**  
  `https://xwbdvaqggcdfgsqnxico.supabase.co/auth/v1`

- **Conexão com a Tabela `users`:**  
  `https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/users`

### **Autenticação**
- **Método:** `Bearer Token` (obtido no login).
- **Headers Necessários:**
  ```json
  {
    "apikey": "sua-API-key-pública",
    "Authorization": "Bearer {access_token}",
    "Content-Type": "application/json"
  }
  ```

---

## **2. Fluxo de Cadastro de Usuário**

### **2.1. Criar Usuário no Auth**
#### **Método:** `POST`  
#### **Endpoint:**
```text
https://xwbdvaqggcdfgsqnxico.supabase.co/auth/v1/signup
```

#### **Headers:**
```json
{
  "apikey": "sua-API-key-pública",
  "Content-Type": "application/json"
}
```

#### **Body:**
```json
{
  "email": "exemplo@email.com",
  "password": "senhaSegura123"
}
```

#### **Resposta Sucesso:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1...",
  "user": {
    "id": "f9faf665-441f-4b8a-bacd-644cc64770fa",
    "email": "exemplo@email.com"
  }
}
```

---

### **2.2. Adicionar Dados na Tabela `users`**
#### **Método:** `POST`  
#### **Endpoint:**
```text
https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/users
```

#### **Headers:**
```json
{
  "apikey": "sua-API-key-pública",
  "Authorization": "Bearer {access_token}",
  "Content-Type": "application/json"
}
```

#### **Body:**
```json
{
  "id": "f9faf665-441f-4b8a-bacd-644cc64770fa",
  "nome": "Nome Completo",
  "nome_empresa": "Nome da Empresa",
  "first_date": "2025-01-06",
  "cargo": "diretor-de-rh"
}
```

#### **Resposta Sucesso:**
```json
{
  "id": "f9faf665-441f-4b8a-bacd-644cc64770fa",
  "nome": "Nome Completo",
  "nome_empresa": "Nome da Empresa",
  "first_date": "2025-01-06",
  "cargo": "diretor-de-rh",
  "created_at": "2025-01-06T20:30:00.123Z"
}
```

---

## **3. Fluxo de Login de Usuário**

### **Método:** `POST`  
### **Endpoint:**
```text
https://xwbdvaqggcdfgsqnxico.supabase.co/auth/v1/token?grant_type=password
```

### **Headers:**
```json
{
  "apikey": "sua-API-key-pública",
  "Content-Type": "application/json"
}
```

### **Body:**
```json
{
  "email": "exemplo@email.com",
  "password": "senhaSegura123"
}
```

### **Resposta Sucesso:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1...",
  "user": {
    "id": "f9faf665-441f-4b8a-bacd-644cc64770fa",
    "email": "exemplo@email.com"
  }
}
```

### **Erro Credenciais Inválidas:**
```json
{
  "code": 400,
  "msg": "Invalid login credentials"
}
```

---

## **4. Buscar Dados do Usuário na Tabela `users`**

Após o login, você pode buscar dados complementares do usuário.

#### **Método:** `GET`  
#### **Endpoint:**
```text
https://xwbdvaqggcdfgsqnxico.supabase.co/rest/v1/users?id=eq.{id}
```

#### **Headers:**
```json
{
  "apikey": "sua-API-key-pública",
  "Authorization": "Bearer {access_token}"
}
```

#### **Exemplo de Resposta:**
```json
{
  "id": "f9faf665-441f-4b8a-bacd-644cc64770fa",
  "nome": "Nome Completo",
  "nome_empresa": "Nome da Empresa",
  "first_date": "2025-01-06",
  "cargo": "diretor-de-rh",
  "created_at": "2025-01-06T20:30:00.123Z"
}
```

---

### **Observações Finais**
- **Confirmação de Email:** O usuário precisa confirmar o email antes de fazer login, a menos que a funcionalidade seja desativada.
- **Tokens JWT:** Utilize o `access_token` retornado no login para autenticar requisições futuras.
- **Segurança:** Garanta que os tokens e chaves públicas estejam seguros.
