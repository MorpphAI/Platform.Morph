# 📡 Documentação de Endpoints (Functions) <img align="right" src="https://github.com/MorpphAI/platform.Morph/blob/main/images/morphTrans.png" alt="Logo Morph" width="60">

Este espaço reúne todas as **functions criadas no Supabase** que servem como interface de backend para os fluxos da Morph IA. Aqui você encontrará os endpoints documentados por área, com exemplos de uso e formato das requisições e respostas.

---

## 🧩 Por que documentar functions?

As `functions` são centrais para a lógica de negócio da plataforma. Elas encapsulam regras importantes e expõem pontos de integração via chamadas HTTP (REST). Documentar isso:

- Garante clareza entre os membros do time;
- Facilita o uso e reuso das funções;
- Ajuda na integração com frontend (Bubble via API Connector, por exemplo);
- Evita duplicação ou funções mal utilizadas.

---

## 📁 Estrutura da documentação

Cada área funcional do sistema terá sua própria página dedicada com as funções relacionadas:

- 🔐 [Users & Onboarding (Login, cadastro, redefinir senha)](./users-functions.md)
- 💼 [Jobs (Vagas, listagens, filtros)](./jobs-functions.md)
- 🏢 [Client Companies (Cadastro e gestão de empresas)](./client-companies-functions.md)

---

## 🧪 Como adicionar uma nova function na documentação

Para manter o padrão da documentação, **toda nova function precisa ser acompanhada de um PR com as seguintes informações**:

### 📌 Modelo de Documentação

```md
### Nome da Função: `nome_da_function`

- **Rota:** `POST /rpc/nome_da_function`
- **Tipo de requisição:** `POST`

#### 📝 Parâmetros esperados (request)
```json
{
    "user_id": "uuid",
    "status": "string"
}
```

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/README.md">⬅ Voltar para o menu principal</a>
</p>

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/content/Supabase/users/functions.md"> ver users endpoints </a>
</p>
