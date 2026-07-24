# 🏖️ Dashboard de Inteligência Turística — Peruíbe

Dashboard interativo com dados consolidados de procura turística, sazonalidade, impacto econômico e comparativo regional entre Peruíbe e cidades da Baixada Santista.

**🔗 Dashboard ao vivo:** [GitHub Pages](https://jason-hash.github.io/dashboard-turismo-peruibe/)

## 📊 O que você encontra aqui

| Bloco | Conteúdo | Fontes |
|-------|---------|--------|
| **Perfil do Município** | Área, população, PIB, títulos (UNESCO/Ramsar) | IBGE Censo 2022 + PIB 2021 |
| **Evolução da Procura** | Hospedagens, Airbnb, Google Trends (10 anos), CADASTUR | Booking, Airbnb, pytrends, CADASTUR |
| **Padrões Sazonais** | Taxa de ocupação, diária média, RevPar (Litoral Paulista) | ABIH-SP 71ª edição |
| **Retorno Econômico** | Empregos, empresas, estabelecimentos ativos | CAGED, JUCESP, Redesim/Receita |
| **Comparativo Regional** | PIB, população, Trends, CNPJ ativos | IBGE + Redesim + pytrends |

## 🎯 Highlights do gráfico Google Trends

- **10 anos** de dados (jan/2016 a jul/2026) — 127 datapoints mensais
- **Threshold visual** com linha laranja no nível 50
- Áreas sombreadas destacam períodos de **baixa procura** (abaixo de 50)
- Tooltip interativo ao passar o mouse (mês + valor + status)

## 🔄 Fontes automatizáveis

Todas as fontes do comparativo regional (Bloco 4) são **100% automatizáveis**:

| Fonte | Método | Endpoint |
|-------|--------|----------|
| IBGE (PIB, População) | API REST | `servicodados.ibge.gov.br/api/v3/agregados` |
| Google Trends | pytrends | `trends.google.com/trends/api` |
| Redesim (CNPJ) | Web scraping | `estatistica.redesim.gov.br/situacao-cnpj` |

## 🚀 Como executar localmente

```bash
# Clonar o repositório
git clone https://github.com/jason-hash/dashboard-turismo-peruibe.git
cd dashboard-turismo-peruibe

# Servir localmente (qualquer servidor HTTP estático)
python -m http.server 3000

# Abrir no navegador
open http://localhost:3000
```

O dashboard é um **arquivo HTML único e self-contained** — não precisa de backend. O `index.html` carrega os dados via JSON inline ou via fetch ao `data/dashboard.json`.

## 📁 Estrutura do projeto

```
├── index.html                          # Dashboard principal (single-file, 52 KB)
├── data/
│   ├── dashboard.json                  # Dados consolidados (19 KB)
│   └── processed/
│       ├── google_trends_peruibe_10y.csv      # Série 10 anos Peruíbe
│       ├── google_trends_comp_baixada_10y.csv  # Comparativo Baixada (Peruíbe/Itanhaém/Mongaguá)
│       └── google_trends_comp_santos_10y.csv   # Comparativo Santos/São Vicente
├── .gitignore
├── LICENSE
└── README.md
```

## 📋 Metodologia

### Dados agregados (não nominais)
Este dashboardsegue o princípio de **transparência sem exposição** — todos os dados são **agregados por categoria/atividade**, nunca individuais ou nominais.

### Período coberto
- Google Trends: jan/2016 a jul/2026 (10 anos)
- IBGE Censo: 2022
- IBGE PIB: 2021 (último disponível)
- ABIH-SP: Maio/2026
- CADASTUR: Julho/2026
- CAGED: acumulado jan-mai/2026
- Redesim: base CNPJ 30/06/2026

### Limitações
- **Bloco 2 (Sazonalidade):** dados do Litoral Paulista (região), não de Peruíbe isoladamente — a ABIH-SP não divulga por município
- **PIB:** último ano disponível no IBGE é 2021
- **ISS Turístico:** pendente de coleta (restrição eleições 2026 no Portal da Transparência)

## 📜 Licença

MIT License — Copyright (c) 2026 [inovatudo.com](https://inovatudo.com)

## 🤝 Contribuindo

Este é um projeto de código aberto para a comunidade de Peruíbe. Contribuições são bem-vindas via Issues e Pull Requests.

---

**Desenvolvido por:** [inovatudo.com](https://inovatudo.com)
