# Campo Analítico — Análise de Futebol com Dados em R

#### Por: Campo Analítico
#### Suporte: [campoanalitico.com.br](https://campoanalitico.com.br/) · [@analiticocampo](https://x.com/analiticocampo) · [@campoanalitico360](https://www.instagram.com/campoanalitico360/)
#### Atualizado em: Abril de 2025

---

Este repositório reúne materiais, scripts e projetos desenvolvidos pela **1ª Escola Brasileira de Estatística para Analistas de Desempenho no Futebol**. O objetivo é ensinar análise de dados aplicada ao futebol utilizando R, com foco em fontes profissionais como StatsBomb, Opta, FBref, WhoScored e Catapult.

---

## Instalação

Para utilizar os pacotes e scripts deste repositório, certifique-se de ter o **R 4.0 ou superior** instalado.

```r
# Instale os pacotes necessários
install.packages(c("devtools", "tidyverse", "ggplot2", "shiny"))

# StatsBombR — dados abertos e via API
devtools::install_github("statsbomb/StatsBombR")

# worldfootballR — scraping de FBref, WhoScored e outros
devtools::install_github("JaseZiv/worldfootballR")
```

---

## Repositórios

| Repositório | Descrição | Linguagem |
|---|---|---|
| [xg_brasileirao](https://github.com/campoanaliticoestudos/xg_brasileirao) | Cálculo e visualização de xG no Campeonato Brasileiro | R |
| [Banco-de-dados-futebol](https://github.com/campoanaliticoestudos/Banco-de-dados-futebol) | Banco de dados estruturado para estudos de futebol | R |
| [campoanalytics](https://github.com/campoanaliticoestudos/campoanalytics) | Funções e utilitários para análise de futebol | R |

---

## Uso

### Lendo dados abertos da StatsBomb

```r
library(StatsBombR)

# Listar competições disponíveis gratuitamente
Comp <- FreeCompetitions()

# Listar partidas de uma competição
Matches <- FreeMatches(Comp)

# Carregar eventos de uma partida
StatsBombData <- get.matchFree(Matches[1, ])

# Limpeza e normalização dos dados
StatsBombData <- allclean(StatsBombData)
```

### Coletando dados do FBref via worldfootballR

```r
library(worldfootballR)

# Estatísticas de jogadores do Brasileirão
brasileirao_stats <- fb_league_stats(
  country = "BRA",
  gender = "M",
  season_end_year = 2024,
  stat_type = "standard"
)
```

### Exemplo: Mapa de chutes com xG

```r
library(ggplot2)
library(StatsBombR)

# Filtrar eventos de chute
shots <- StatsBombData %>%
  filter(type.name == "Shot")

# Plotar campo com localização dos chutes
ggplot(shots, aes(x = location.x, y = location.y, size = shot.statsbomb_xg,
                  color = shot.outcome.name)) +
  geom_point(alpha = 0.7) +
  scale_color_manual(values = c("Goal" = "#1D9E75", "Saved" = "#0F6E56",
                                "Off T" = "#5DCAA5", "Blocked" = "#aaaaaa")) +
  labs(title = "Mapa de Chutes", x = NULL, y = NULL) +
  theme_minimal()
```

---

## Métricas Cobertas

- **xG (Expected Goals)** — probabilidade de gol por chute
- **xA (Expected Assists)** — probabilidade de assistência por passe
- **PPDA (Passes Permitidos por Ação Defensiva)** — intensidade de pressão
- **Progressive Passes / Carries** — progressão com e sem bola
- **Defensive Actions** — pressão, recuperações, duelos
- **Redes de Passes** — estrutura de jogo e conexões entre jogadores
- **Mapas de Calor** — zonas de atuação e padrões táticos

---

## Fontes de Dados Compatíveis

| Fonte | Acesso | Tipo de Dado |
|---|---|---|
| [StatsBomb Open Data](https://github.com/statsbomb/open-data) | Gratuito | Eventos, chutes, passes, pressão |
| [FBref](https://fbref.com) | Gratuito (scraping) | Estatísticas agregadas |
| [WhoScored](https://whoscored.com) | Gratuito (scraping) | Avaliações e dados táticos |
| [StatsBomb API](https://statsbomb.com) | Pago | Dados de alta frequência |
| [Opta](https://optasports.com) | Pago | Dados de alta frequência |
| [Catapult](https://catapultsports.com) | Institucional | GPS e carga física |

---

## Pré-requisitos

- R ≥ 4.0
- RStudio (recomendado)
- Conhecimento básico de R (o curso ensina do zero)
- Nenhum conhecimento prévio em estatística é necessário

---

## Estrutura dos Projetos

```
campoanaliticoestudos/
├── xg_brasileirao/
│   ├── data/          # Dados brutos e processados
│   ├── R/             # Scripts de análise
│   └── output/        # Visualizações geradas
├── Banco-de-dados-futebol/
│   ├── data/
│   └── README.md
└── campoanalytics/
    ├── R/             # Funções reutilizáveis
    └── DESCRIPTION
```

---

## Notas Finais

- Scripts são atualizados regularmente com novos exemplos e correções.
- Verifique as dependências de pacotes em caso de erros na instalação.
- Cada projeto possui seu próprio `README.md` com instruções específicas.
- Para dúvidas técnicas, abra uma [Issue](https://github.com/campoanaliticoestudos) no repositório correspondente.
- Acompanhe novos projetos e análises em [campoanalitico.com.br](https://campoanalitico.com.br/).

---

## Sobre

Campo Analítico é a primeira escola brasileira de estatística aplicada ao futebol voltada para analistas de desempenho. Ensinamos linguagem R, métricas avançadas e visualização de dados com foco em aplicação prática e desenvolvimento de portfólio profissional.

[![Acesse o Curso](https://img.shields.io/badge/Acesse%20o%20Curso-campoanalitico.com.br-1D9E75?style=for-the-badge)](https://campoanalitico.com.br/)
[![GitHub followers](https://img.shields.io/github/followers/campoanaliticoestudos?style=for-the-badge&color=0F6E56&label=Seguidores)](https://github.com/campoanaliticoestudos)
