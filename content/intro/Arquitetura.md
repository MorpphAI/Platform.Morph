

# Arquitetura da Plataforma 🏗️ <img align="right" src="https://github.com/MorpphAI/platform.Morph/blob/main/images/morphTrans.png" alt="Imagem da linguagem" width="60">

A plataforma **Morph IA** foi projetada para ser **modular, escalável e acessível**, combinando tecnologias no-code/low-code com infraestrutura moderna para entregar agentes de IA inteligentes de forma rápida e funcional.

---

## 🔧 Componentes Principais

### 🧩 Bubble (Frontend)

Utilizamos o **[Bubble.io](https://bubble.io)** como nossa camada de frontend. Ele permite construir toda a interface gráfica da plataforma sem necessidade de código, utilizando **lógica visual e plugins**.

- Plugin utilizado: `API Connector` – responsável pela comunicação com serviços externos (OpenAI, Supabase, etc).
- Com ele, conseguimos integrar e consumir qualquer REST API, incluindo autenticação, chamadas de IA e dados do usuário.

---

### 🗃️ Supabase (Backend e Core de Dados)

O **[Supabase](https://supabase.com)** é o núcleo da nossa aplicação – responsável pelo banco de dados, autenticação e lógica de negócio via SQL Functions.

- **Banco de Dados**: PostgresSQL
- **Autenticação**: gerenciamento de usuários via e-mail (login, reset de senha, confirmação, etc).
- **Functions**: usamos funções SQL/PLPGSQL para executar lógicas personalizadas da plataforma.

🔗 **Veja todas as functions que utilizamos**: [Funções cadastradas no Supabase](https://github.com/MorpphAI/Platform.Morph/blob/main/content/infra/functions.md)

---

### 📬 Hospedagem de E-mail (SMTP)

Utilizamos um serviço SMTP customizado para envio de e-mails transacionais, como:

- Confirmação de e-mail
- Recuperação de senha
- Alertas e notificações automatizadas

Esse serviço está integrado diretamente com o módulo de autenticação do Supabase.

---

### 📊 Looker Studio (Visualização de Dados)

Os dados capturados e processados pela plataforma são organizados em painéis criados no **[Looker Studio](https://lookerstudio.google.com/)**.

- Permite acompanhar métricas de uso, performance dos agentes e estatísticas em tempo real.
- Integração direta com o banco de dados via conector PostgreSQL.

---

### 🔗 Integrações Externas

- **OpenAI API** – utilizada para alimentar os agentes com capacidade de raciocínio e linguagem natural.
- **APIs REST** – criadas e consumidas entre Supabase, Bubble e terceiros via API Connector.

---

## 💡 Visão Geral da Arquitetura

```mermaid
graph TD;
    UI[Frontend - Bubble] --> Connector[API Connector]
    Connector --> OpenAI[OpenAI API]
    Connector --> Supabase
    Supabase --> DB[(Postgres DB)]
    Supabase --> Auth[Auth + SMTP]
    Supabase --> Functions[Functions 🔗]
    Supabase --> Looker[Looker Studio]

---

<p align="right">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/content/intro/DocsJornadas.md">Próximo -> Documentação jornada</a>
</p>

<p align="left">
  <a href="https://github.com/MorpphAI/Platform.Morph/blob/main/README.md">Voltar para o menu principal</a>
</p>
