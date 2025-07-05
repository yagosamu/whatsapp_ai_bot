# 🤖 Whatsapp_ai_bot

Um chatbot inteligente para WhatsApp que utiliza **OpenAI**, **FastAPI**, **LangChain** e **EvolutionAPI**, com arquitetura pronta para produção via **Docker**!  
Ideal para criar assistentes automatizados, bots de atendimento, ou integração RAG (busca por documentos).

---

## ✨ Funcionalidades

- 🤖 Responde automaticamente mensagens do WhatsApp com IA (OpenAI)
- 📚 Suporte a RAG: busque respostas em seus próprios documentos
- 🔗 Integração pronta com EvolutionAPI (WhatsApp gateway)
- ⚡ Respostas rápidas e bufferizadas (debounce inteligente)
- 🧠 Personalização de prompts para adaptar o comportamento do bot
- 🐳 Deploy facilitado via Docker/Docker Compose

---

## 🚀 Como rodar o projeto

### 1. Clone o repositório

```bash
git clone https://github.com/yagosamu/whatsapp_ai_bot
cd whatsapp_ai_bot
```

### 2. Configure suas variáveis de ambiente

Copie o arquivo de exemplo e edite conforme necessário:

```bash
cp .env.example .env
```

Preencha as variáveis no `.env`:

- `OPENAI_API_KEY`: sua chave da OpenAI
- `AUTHENTICATION_API_KEY`: chave da EvolutionAPI
- `EVOLUTION_INSTANCE_NAME`: nome da instância no EvolutionAPI (deve ser igual ao painel)
- `AI_CONTEXTUALIZE_PROMPT`, `AI_SYSTEM_PROMPT`: personalize os prompts do seu bot
- Outras variáveis para Redis, etc.

### 3. (Opcional) Adicione documentos para RAG

Coloque arquivos (PDF, TXT, etc.) na pasta `rag_files/`.  
Eles serão lidos e indexados automaticamente para respostas baseadas em documentos.

### 4. Suba os containers

```bash
docker compose up --build
```

Acesse o painel EvolutionAPI em [http://localhost:8080/manager](http://localhost:8080/manager).

### 5. Configure o webhook no EvolutionAPI

- Conecte sua instância do WhatsApp no painel
- Adicione o webhook:  
  ```
  http://bot:8000/webhook
  ```
- Habilite o evento `MESSAGES_UPSERT`

---

## 🛠️ Estrutura do projeto

```
├── app.py                # Endpoint FastAPI do webhook
├── evolution_api.py      # Função para enviar mensagens via EvolutionAPI
├── chains.py             # Lógica do agent (OpenAI/LangChain)
├── message_buffer.py     # Bufferização e debounce das mensagens
├── prompts.py            # Prompts customizáveis
├── config.py             # Carrega variáveis do .env
├── requirements.txt
├── docker-compose.yml
├── Dockerfile
├── rag_files/            # Documentos para RAG
└── ...
```

---

## 💡 Personalização

- Modifique os prompts no `.env` para alterar o “tom” e o papel do bot
- Adicione documentos em `rag_files/` para que o bot utilize como base de conhecimento
- Adapte o código para novas integrações, fluxos e comportamentos

---

## 🏁 Dicas

- Use o Docker para evitar problemas de dependências!
- Para ambiente de produção, troque as URLs da EvolutionAPI e garanta a segurança do seu webhook.
- Consulte o [painel EvolutionAPI](https://doc.evolution-api.com/) para mais opções.

---

## 🤝 Contribuição

Achou útil? Tem dúvidas ou sugestões?  
Abra uma issue ou envie um pull request!  
Vamos construir juntos bots mais inteligentes! 🚀

---

