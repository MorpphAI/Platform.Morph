# 📚 Documentação da API <img align="right" src="https://github.com/MorpphAI/platform.Morph/blob/main/content/images/morphTrans.png" alt="Imagem da linguagem" width="60">

## Índice
1. [Autenticação](#autenticação)
2. [Enviar Mensagens para o Agente](#enviar-mensagens-para-o-agente)
3. [Gerenciamento de Arquivos](#gerenciamento-de-arquivos)
4. [Listar e Excluir Arquivos](#listar-e-excluir-arquivos)

## 1. Autenticação

Todas as requisições à API devem ser autenticadas usando uma chave de API. A chave deve ser passada no cabeçalho `Authorization`.

**Cabeçalhos obrigatórios**:
```http
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```
<br/>
<br/>

## 2.  Enviar Mensagens para o Agente
### Este endpoint permite enviar mensagens para o modelo GPT e obter respostas.

#### Retorna um item

```http
  POST https://api.openai.com/v1/chat/completions
```
<br/>

| Parâmetro     | Tipo       | Obrigatório | Descrição                                      |
|---------------|------------|-------------|-----------------------------------------------|
| `model`       | string     | Sim         | Modelo a ser usado. Exemplo: `gpt-4` ou `gpt-3.5-turbo`. |
| `messages`    | array      | Sim         | Histórico de mensagens, incluindo a nova mensagem. |
| `temperature` | float      | Não         | Controla a criatividade da resposta (0.0 a 1.0). Padrão: `0.7`. |
| `max_tokens`  | integer    | Não         | Número máximo de tokens na resposta. Padrão: `256`. |

#### Exemplo de Requisição


```http
  POST https://api.openai.com/v1/chat/completions
  Content-Type: application/json
  Authorization: Bearer YOUR_API_KEY
  
  {
    "model": "gpt-4",
    "messages": [
      {"role": "system", "content": "Você é um assistente útil."},
      {"role": "user", "content": "Qual é a previsão do tempo para hoje?"}
    ],
    "temperature": 0.7,
    "max_tokens": 256
  }
```
#### Resposta Exemplo

```http
    {
      "id": "chatcmpl-123",
      "object": "chat.completion",
      "created": 1677652288,
      "choices": [
        {
          "index": 0,
          "message": {"role": "assistant", "content": "A previsão do tempo para hoje é de sol com temperaturas amenas."},
          "finish_reason": "stop"
        }
      ],
      "usage": {"prompt_tokens": 10, "completion_tokens": 15, "total_tokens": 25}
    }
```
<br/>
<br/>

## 3. Gerenciamento de Arquivos

Este endpoint permite enviar arquivos para a API. Ele é comumente usado para fine-tuning ou outras aplicações que dependem de dados externos.

#### Endpoint:
```http
  POST https://api.openai.com/v1/files
```

#### Parâmetros da Requisição

| Parâmetro | Tipo   | Obrigatório | Descrição                                  |
|-----------|--------|-------------|--------------------------------------------|
| `file`    | file   | Sim         | Arquivo a ser enviado (JSONL ou texto).     |
| `purpose` | string | Sim         | Propósito do arquivo (ex: fine-tune).       |

#### Exemplo de Requisição (cURL)
```http
  curl https://api.openai.com/v1/files \
    -X POST \
    -H "Authorization: Bearer YOUR_API_KEY" \
    -F "purpose=fine-tune" \
    -F "file=@seuarquivo.jsonl"
```
#### Resposta Exemplo

```http
   {
    "id": "file-abc123",
    "object": "file",
    "bytes": 12345,
    "created_at": 1677652288,
    "filename": "seuarquivo.jsonl",
    "purpose": "fine-tune",
    "status": "uploaded"
  }
```

<p align="right">
  <a href="https://github.com/Juniorbasck/astro4noobs/blob/main/content/intro/instalacao.md">Próximo -> Instalação</a>
</p>

<p align="left">
  <a href="https://github.com/MorpphAI/platform.Morph">Voltar para o menu principal</a>
</p>
