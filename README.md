# 🏖️ Dashboard de Inteligência Turística — Peruíbe

Dashboard interativo com dados consolidados de procura turística, sazonalidade, impacto econômico e comparativo regional entre Peruíbe e cidades da Baixada Santista.

**🔗 Dashboard ao vivo:** [GitHub Pages](https://jason-hash.github.io/dashboard-turismo-peruibe/)

## 📊 O que você encontra aqui

| Bloco | Conteúdo | Fontes |
|-------|---------|--------|
| **Perfil do Município** | Área, população, PIB, títulos (UNESCO/Ramsar) | IBGE Censo 2022 + PIB 2021 |
| **Evolução da Procura** | Hospedagens, Airbnb, Google Trends (5 anos), CADASTUR | Booking, Airbnb, Google Trends, CADASTUR |
| **Padrões Sazonais** | Taxa de ocupação, diária média, RevPar (Litoral Paulista) | ABIH-SP 71ª edição |
| **Retorno Econômico** | Empregos, empresas, estabelecimentos ativos | CAGED, JUCESP, Redesim/Receita |
| **Comparativo Regional** | PIB, população, Trends, CNPJ ativos | IBGE + Redesim + Google Trends |

## 🎯 Highlights do gráfico Google Trends

- **5 anos** de dados (jul/2021 a jul/2026) — 61 datapoints mensais
- **Termo de busca** `"peruibe"` (sem acento, lowercase) — mede interesse real pela cidade
- **Threshold visual** com linha laranja no nível 50
- Áreas sombreadas destacam períodos de **baixa procura** (abaixo de 50)
- Tooltip interativo ao passar o mouse (mês + valor + status)

> ℹ️ **Nota técnica — Escolha do termo de busca:**
>
> Testamos 3 abordagens para a série do Google Trends:
>
> 1. **Topic ID** `/g/11bxfy9vvd` (entidade "Peruíbe" via *entity reconciliation*): **descartada**. Entre 2016-11 e 2019-04 o topic ID retorna valores 0-3 (entidade mal reconhecida pelo Knowledge Graph do Google na época), gerando um vale implausível que não reflete o crescimento turístico real.
> 2. **Termo com acento** `"peruíbe"`/`"Peruíbe"`: **descartado**. Sofre viés de adoção tecnológica — a razão `peruibe/peruíbe` caiu de 11x (2016) para 1.5x (2026) porque teclados com autocorreção passaram a inserir acentos. Isso infla artificialmente a série com acento ao longo do tempo, confundindo adoção de teclados com crescimento de interesse turístico.
> 3. **Termo sem acento** `"peruibe"`: **ESCOLHIDA**. Sazonalidade mais limpa (100% dos picos anuais caem no verão jan/fev/dez), estável ao longo do tempo (não sofre viés de autocorreção), e captura todas as buscas independente de acentuação (Google normaliza).
>
> **Janela de 5 anos:**Delimitamos a série aos últimos 5 anos (jul/2021 a jul/2026) para dar foco ao período mais relevante para a leitura turística atual. A série foi renormalizada para 0-100 dentro desse período (pico 100 em jan/2024).

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
- Google Trends: jul/2021 a jul/2026 (5 anos, termo "peruibe" sem acento, renormalizado)
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
