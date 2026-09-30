# Sistema Operacional Pessoal (POS) com Inteligência Artificial

Sistema Operacional Pessoal (Personal Operating System - POS) desenvolvido como parte dos requisitos da disciplina de Produtividade e Gestão de Tempo da UniFECAF. O projeto integra automação em nuvem e processamento de linguagem natural para auxiliar na organização de demandas, priorização de atividades e gestão do tempo.

---

## 📋 Descrição do Sistema

O POS centraliza a gestão de tarefas e o planejamento temporal por meio de uma interface conversacional inteligente. Utilizando a **Matriz de Eisenhower** como método de produtividade (*Urgente*, *Importante*, *Delegável* e *Descartável*), a solução permite criar, listar e atualizar demandas no Notion sem a necessidade de preenchimento manual de formulários complexos, reduzindo a sobrecarga cognitiva e o risco de procrastinação.

---

## 🛠️ Ferramentas Utilizadas

- **Notion:** Banco de dados relacional em nuvem estruturado para persistência e gestão dos cartões de tarefas.
- **Make.com:** Plataforma de integração visual (*low-code*) para orquestração de webhooks e automação de fluxos.
- **Dify AI & Google Gemini 2.5 Pro:** Camada cognitiva responsável por interpretar as mensagens do usuário em linguagem natural e estruturá-las em objetos JSON normalizados.

---

## 🔄 Fluxo de Organização

1. **Entrada Conversacional:** O usuário envia uma mensagem em linguagem natural no chat do Dify (ex.: *"Crie uma tarefa..."* ou *"Altere o status para Concluído"*).
2. **Processamento Cognitivo:** O Google Gemini analisa o texto, extrai os parâmetros estruturados (ação, nome, prioridade, área, data e status) e retorna um JSON padronizado.
3. **Orquestração (Make Router):** O Make recebe o payload e direciona o fluxo por meio de caminhos condicionais (*Criar*, *Listar* ou *Alterar*).
4. **Persistência (Notion API):** O sistema executa a operação na base de dados (pesquisa flexível por aproximação com `Text: Contains`, atualização dinâmica via `Page ID` ou inserção de novo registro) e retorna a confirmação transacional.

---

## 🖼️ Prints e Evidências do Sistema

### 1. Painel de Tarefas no Notion
**Visualização do board de tarefas no Notion**
> **<img width="941" height="392" alt="image" src="https://github.com/user-attachments/assets/7efac459-5162-4de1-8850-e1bf3edf8ef2" />
*Detalhes da Tarefa*
> <img width="959" height="404" alt="image" src="https://github.com/user-attachments/assets/1060d1d2-72e3-4d45-a043-94a472e5fc90" />

### 2. Cenário Completo no Make.com
**Visualização da arquitetura do projeto no Make.com**
> **<img width="861" height="362" alt="image" src="https://github.com/user-attachments/assets/fa143f24-f220-48b8-beec-4e71ea52aaf5" />
*Módulo de conexão com a API do Make.com*
> **<img width="352" height="335" alt="image" src="https://github.com/user-attachments/assets/66b6a07a-cdfb-45a2-b356-2180ea763e5d" />

*Módulo de conexão com o Google Gemini API (Flash Lite 3.5)*
> **<img width="360" height="401" alt="image" src="https://github.com/user-attachments/assets/ab1b3ac5-6bf6-437e-ac44-0dfcb25bbf4e" />
### Prompt do Sistema (Google Gemini AI)

```text
Você é um assistente de produtividade rigoroso. A data e hora atual do sistema é {{now}}. Analise a mensagem do utilizador e extraia as informações estritamente com base nela. Retorne APENAS um objeto JSON válido, sem formatação markdown, sem blocos de código e sem texto adicional.

O JSON deve conter exatamente estas chaves:
- "acao": Identifique a intenção principal e classifique estritamente como "criar", "listar" ou "alterar".
- "filtro_status": Se a ação for "listar", "liste" ou instruções similares, extraia qual status ou coluna o usuário quer ver (ex: "Fazer Hoje", "Concluído", "Caixa de Entrada", "Em Andamento", "Backlog"). Se o usuário pediu para listar tudo sem especificar, retorne "todos" ou null.
- "nome_tarefa": Extraia o nome da tarefa exatamente como o utilizador se refere a ela, mantendo as palavras-chave principais intactas para que possam ser encontradas numa base de dados (evite inventar sinónimos ou parafrasear títulos se houver menção a uma tarefa específica).
- "prioridade": Classifique estritamente como "Urgente", "Importante", "Delegável" ou "Descartável".
- "area": Classifique estritamente como "Dev Front-end", "Faculdade" ou "Pessoal".
- "data": Calcule a data exata no formato ISO: YYYY-MM-DD HH:mm com base na data atual informada acima ({{now}}). Se o utilizador disser "amanhã", calcule o dia seguinte. Se não houver menção de data, retorne YYYY-MM-DD ou deixe null. Se não houver prazo final, deixe null.
- "status": Classifique estritamente com base no contexto entre estas opções exatas: "Backlog", "Caixa de Entrada", "Fazer Hoje", "Em Andamento" ou "Concluído". Com base no contexto fornecido.

Mensagem do utilizador: {{1.texto}}
```

*Módulo de conversão de dados coletados para JSON*
> **<img width="362" height="224" alt="image" src="https://github.com/user-attachments/assets/e0c88abd-ca3a-40e0-8a72-4da84dbe26e1" />

*Rota Superior: Módulo de criação de tarefa no Board*
 > **<img width="288" height="106" alt="image" src="https://github.com/user-attachments/assets/146a9119-7e09-43d1-b957-b3262b9d1af1" />
 > **<img width="266" height="398" alt="image" src="https://github.com/user-attachments/assets/3c652b67-6219-4aa4-b483-99efbcf46dfc" />
 > **<img width="271" height="400" alt="image" src="https://github.com/user-attachments/assets/69492224-128c-45b5-bb75-8897c4ea4bba" />
 > **<img width="263" height="200" alt="image" src="https://github.com/user-attachments/assets/79798318-d85d-4620-b548-cfb41969ec6d" />


 *Rota do Meio: Módulo de listagem de tarefas do Board*
> **<img width="490" height="95" alt="image" src="https://github.com/user-attachments/assets/3c92ed0b-2d7c-45b0-a14f-ec641a7c2518" />
> **<img width="265" height="401" alt="image" src="https://github.com/user-attachments/assets/a677e2f8-e4f0-46cc-8502-dc98f7f528be" />
> **<img width="263" height="399" alt="image" src="https://github.com/user-attachments/assets/8133a5e0-b5cb-4d4e-b169-958d626f5b65" />
> **<img width="263" height="243" alt="image" src="https://github.com/user-attachments/assets/a4596821-0d82-490b-833f-018b466270b7" />

*Rota Inferior: Módulo de alteração de tarefa do Board*
> **<img width="399" height="122" alt="image" src="https://github.com/user-attachments/assets/31572c3c-87c4-40cb-8431-33a92f58500d" />
> **<img width="269" height="398" alt="image" src="https://github.com/user-attachments/assets/7c86d8d0-31da-4002-8c7d-9ad328ca43db" />
> **<img width="261" height="229" alt="image" src="https://github.com/user-attachments/assets/bd0e2032-2a9d-4d2c-b5a5-257ac2e05808" />
> **<img width="263" height="198" alt="image" src="https://github.com/user-attachments/assets/d9eabe2a-b3ac-4771-8239-0ddc9c1ca822" />

### 3. Fluxo no Dify AI (Chatbot)

> **<img width="703" height="191" alt="image" src="https://github.com/user-attachments/assets/6445b4c4-47d6-4b5d-87c1-a1b7628c41f1" />
**
*Módulo de Inicio/Entrada*
>**<img width="286" height="359" alt="image" src="https://github.com/user-attachments/assets/e4713812-4ef9-4ac6-a92d-7da6aeac7d67" />
**

*Módulo de Requisição HTTP (GET)*
>**<img width="284" height="367" alt="image" src="https://github.com/user-attachments/assets/ab6ce5da-1d64-4352-b8b1-1325c0a27949" />
**

*Módulo de Resposta (Answer) e exibição do Chatbot*
>**<img width="731" height="371" alt="image" src="https://github.com/user-attachments/assets/63c2812f-2638-453b-af58-8c4b8608408e" />
**

---

## 🚀 Como Utilizar a Solução

Inicialmente, o fluxo de webhooks do Make.com deverá estar em modo *listening*, aguardando dados/informações que chegam do Chatbot do Dify AI.
Para interagir com o seu Sistema Operacional Pessoal via chat, utilize comandos diretos baseados nas palavras-chave do sistema:

- **Criar Tarefa:**

  > *"Crie uma tarefa chamada Estudar arquitetura de microsserviços com prioridade Importante, na área Dev Front-end e coloque o status como Fazer Hoje."*

- **Listar Tarefas:**

  > *"Liste todas as minhas tarefas que estão com o status Fazer Hoje."*

- **Alterar Status:**

  > *"Altere o status da tarefa Estudar arquitetura de microsserviços para Concluído."*

---

## 🔗 Links e Repositórios

- **Documentação Teórica e Acadêmica:** Entregue através do portal UniFECAF.
- **Base de Dados (Notion):**[https://app.notion.com/p/b14c6cca712b44df87d3bf4bc88bea8f?v=bb364ad1ee7e43da8e479c64fa64843c&source=copy_link](https://app.notion.com/p/b14c6cca712b44df87d3bf4bc88bea8f?v=bb364ad1ee7e43da8e479c64fa64843c&source=copy_link)
- **Fluxo de conexões API e Webhooks (Make.com):**[https://app.notion.com/p/b14c6cca712b44df87d3bf4bc88bea8f?v=bb364ad1ee7e43da8e479c64fa64843c&source=copy_link](https://us2.make.com/public/shared-scenario/LGAs1sK4Ra8/integration-webhooks)
- **Fluxo do Chatbot (Dify AI):**[https://app.notion.com/p/b14c6cca712b44df87d3bf4bc88bea8f?v=bb364ad1ee7e43da8e479c64fa64843c&source=copy_link](https://udify.app/chat/0gJ1412mPbvlftFr)
- **Chatbot (Dify AI):**https://udify.app/chat/0gJ1412mPbvlftFr
- **Vídeo Pitch (YouTube):**[https://app.notion.com/p/b14c6cca712b44df87d3bf4bc88bea8f?v=bb364ad1ee7e43da8e479c64fa64843c&source=copy_link](https://youtu.be/c5ERKeBDKv8)
