---
name: google-ads-competitor
description: >-
  Analyzes competitor ads from Google Ads Transparency Center across Search, Display, and YouTube formats.
  Extracts copy patterns, keyword strategies, bidding signals, and funnel positioning.
  Works in two modes: automatic via MCP (Google Ads API) or manual analysis when the user
  pastes ad examples. Use when the user asks to analyze, research, spy on, or review
  competitor ads on Google, Google Ads, YouTube, or mentions "transparency center",
  "concorrentes no Google", "anúncios de busca", or "Google Ads".
license: MIT
metadata:
  author: davi-graeff
  version: "1.0"
  language: pt-BR
---

# Google Ads Competitor Analysis

Skill para análise de anúncios de concorrentes no Google Ads Transparency Center.

## Modo de Operação

Detecte automaticamente qual modo usar antes de iniciar:

**Modo API (MCP disponível):** Se houver MCP do Google Ads configurado (tools com prefixo `google_ads:`), use-o para buscar automaticamente.

**Modo Manual (sem MCP):** Oriente o usuário a acessar `adstransparency.google.com`, buscar pelo nome da marca ou domínio, e colar os resultados. Analise o conteúdo fornecido com o mesmo rigor.

## Instruções

### Passo 1 — Coleta de Dados

**Com MCP:**
1. Busque o domínio/marca do concorrente via API
2. Colete anúncios ativos por formato: Search (RSA), Display, Vídeo (YouTube)
3. Priorize os últimos 90 dias
4. Armazene os resultados para que a skill `ad-variations-creator` possa reutilizá-los

**Sem MCP:**
1. Peça ao usuário o nome da marca ou domínio
2. Instrua a acessar `adstransparency.google.com`
3. Guie: buscar pelo nome da marca → filtrar por país/período → copiar textos dos anúncios
4. Solicite que cole os textos, prints ou descrições dos anúncios encontrados
5. Analise os exemplos fornecidos

Se o usuário não informar a marca/domínio, pergunte antes de prosseguir.

### Passo 2 — Análise por Formato

#### Anúncios de Busca (Search / RSA)

| Elemento | O que extrair |
|---|---|
| Headlines (até 15) | Estrutura, keywords usadas, proposta de valor, tamanho |
| Descriptions (até 4) | Argumentos, CTAs, diferenciais, tom |
| Extensions | Sitelinks, callouts, structured snippets, call extensions |

#### Anúncios Display

| Elemento | O que extrair |
|---|---|
| Tamanhos | Formatos utilizados (300x250, 728x90, etc.) |
| Visuais | Estilo, marca, cores, elementos gráficos |
| Mensagem | Copy principal, CTA, oferta |

#### Anúncios em Vídeo (YouTube)

| Elemento | O que extrair |
|---|---|
| Formato | Bumper (6s), skippable, non-skippable, in-feed |
| Hook | Primeiros 5 segundos — o que prende a atenção |
| Narrativa | Estrutura da história, argumentos, prova |
| CTA | Chamada final e overlay |

Consulte os padrões de copy e sinais estratégicos em [references/search-ad-patterns.md](references/search-ad-patterns.md).

### Passo 3 — Identificação de Padrões

Após analisar todos os formatos, sintetize:

- **Keywords implícitas**: termos de busca inferidos a partir do copy (ver tabela de inferência em search-ad-patterns.md)
- **Posicionamento competitivo**: atacam concorrentes? defendem branded terms? usam conquista?
- **Sazonalidade**: promoções, datas especiais, countdown timers
- **Tom de voz**: formal, descontraído, técnico, emocional
- **Oferta principal**: desconto, trial, garantia, frete, urgência
- **Estratégia de bidding**: sinais inferidos pelo comportamento de anúncios
- **Estágio de funil**: transacional (fundo), informacional (topo), navegacional (brand)

### Passo 4 — Relatório Final

Gere um relatório estruturado contendo obrigatoriamente:

1. **Resumo executivo** (3-5 linhas)
2. **Distribuição por formato** (Search, Display, YouTube — tabela)
3. **Headlines e descriptions mais recorrentes** (Search)
4. **Análise de copy por formato** (padrões consolidados)
5. **Keywords e temas recorrentes**
6. **Estratégia de posicionamento detectada** (bidding, sazonalidade, funil)
7. **Gaps e oportunidades**
8. **Recomendações para campanhas próprias** (mínimo 3, máximo 5)

Para ver um exemplo completo, consulte [examples/google-report-example.md](examples/google-report-example.md).

### Passo 5 — Encadeamento

Ao final do relatório, sempre pergunte:

> "Deseja que eu crie variações de anúncios baseadas nesses padrões?"

Se o usuário aceitar, ative a skill `ad-variations-creator` passando o contexto coletado.

## Comportamento Esperado

- Se não tiver acesso via MCP, guie o usuário passo a passo para coletar no Transparency Center
- Nunca invente dados — se não houver informações suficientes, indique "dados insuficientes"
- Mantenha o tom analítico e objetivo
- Se o usuário pedir análise de múltiplas marcas, gere um relatório separado para cada uma
