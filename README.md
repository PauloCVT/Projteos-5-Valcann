# Dashboard Valcann — Projetos 5

Dashboard interativo para visualização de Epics do Jira, desenvolvido com **Streamlit** e integrado à **API REST v3 do Jira**.

---

## Pré-requisitos

- [Docker](https://www.docker.com/) (recomendado) **ou** Python 3.12+
- Conta no Jira com um **API Token** gerado em [id.atlassian.com/manage-profile/security/api-tokens](https://id.atlassian.com/manage-profile/security/api-tokens)

---

## Configuração

1. Clone o repositório:
   ```bash
   git clone <url-do-repositorio>
   cd <pasta-do-projeto>
   ```

2. Copie o arquivo de variáveis de ambiente e preencha com suas credenciais:
   ```bash
   cp .env.example .env
   ```

   | Variável    | Descrição                        |
   |-------------|----------------------------------|
   | `EMAIL`     | E-mail da sua conta Atlassian    |
   | `API_TOKEN` | Token gerado no portal Atlassian |

---

## Como rodar

### Com Docker (recomendado)

```bash
docker compose up --build
```

Acesse em: [http://localhost:8501](http://localhost:8501)

### Sem Docker (local)

```bash
pip install -r requirements.txt
streamlit run main.py
```

---

## Estrutura do projeto

```
.
├── main.py              # Aplicação principal (dashboard Streamlit)
├── requirements.txt     # Dependências Python
├── Dockerfile           # Imagem Docker da aplicação
├── docker-compose.yml   # Orquestração do container
├── .env.example         # Template de variáveis de ambiente
├── .gitignore           # Arquivos ignorados pelo Git
└── README.md            # Este arquivo
```

---

## Como funciona

O dashboard consome a **API REST v3 do Jira** via `POST /rest/api/3/search/jql`, buscando todos os Epics com status diferente de "Done". Os resultados são exibidos em uma tabela interativa com as seguintes colunas:

- **Chave** — identificador do Epic no Jira
- **Resumo** — título do Epic
- **Status** — estado atual
- **Responsável** — membro atribuído
- **Prioridade** — nível de prioridade

Os dados ficam em cache por **5 minutos** para evitar chamadas desnecessárias à API.

---

## Contribuindo

1. Crie uma branch a partir da `main`: `git checkout -b feature/sua-feature`
2. Faça suas alterações e commite: `git commit -m "feat: descrição"`
3. Abra um Pull Request
