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

*(Adicione abaixo as capturas de tela do seu projeto.)*

### 1. Cenário Completo no Make.com

> **[Inserir print do fluxo no Make mostrando os módulos de Webhook, Gemini, JSON, Router e Notion]**

### 2. Configuração do Filtro e Busca no Notion

> **[Inserir print do módulo de busca com o operador "Contains" e o mapeamento de ID]**

### 3. Painel de Tarefas no Notion

> **[Inserir print do seu Notion com o banco de dados organizado por colunas de status]**

---

## 🚀 Como Utilizar a Solução

Para interagir com o seu Sistema Operacional Pessoal via chat, utilize comandos diretos baseados nas palavras-chave do sistema:

- **Criar Tarefa:**

  > *"Crie uma tarefa chamada Estudar arquitetura de microsserviços com prioridade Importante, na área Dev Front-end e coloque o status como Fazer Hoje."*

- **Listar Tarefas:**

  > *"Liste todas as minhas tarefas que estão com o status Fazer Hoje."*

- **Alterar Status:**

  > *"Altere o status da tarefa Estudar arquitetura de microsserviços para Concluído."*

---

## 🔗 Links e Repositórios

- **Documentação Teórica e Acadêmica:** Disponível no repositório oficial.
- **Base de Dados de Apoio (Notion):** [Acessar Base de Dados](https://www.notion.so/Sistema-Operacional-Pessoal-b14c6cca712b44df87d3bf4bc88bea8f)
