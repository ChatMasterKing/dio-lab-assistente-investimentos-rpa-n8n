## 🚀 Solução Implementada

### Arquitetura e Decisões Técnicas
1. **Camada de RPA (`src/extrair_clientes.ipynb`):** Script em Python utilizando `requests` e `BeautifulSoup` para realizar o *web scraping* da tabela de clientes hospedada no GitHub Pages (`docs/index.html`) e envio estruturado via requisição HTTP `POST` (JSON).
2. **Orquestração no N8N (`n8n/workflow.json`):**
   - **Webhook (Entrada):** Recebe o payload JSON enviado pelo robô RPA no endpoint `/receber-clientes`.
   - **Padronização e Split:** Desempacota a lista de clientes e normaliza o campo `perfil`.
   - **Ingestão de Base de Investimentos:** Consome dinamicamente o arquivo `docs/data.csv` via `HTTP Request` e converte os registros utilizando `Extract from File`.
   - **Cruzamento de Dados (`Merge`):** Relaciona cada cliente com o produto financeiro correspondente ao seu perfil de *suitability* (`Conservador`, `Moderado` ou `Arrojado`).
   - **Geração de Mensagens:** Aplica regras de recomendação personalizadas considerando o nome, o saldo disponível e o perfil de risco de cada investidor.
