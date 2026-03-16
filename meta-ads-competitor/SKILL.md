---
name: meta-ads-competitor
description: >-
  Analyzes competitor ads from Meta Ads Library (Facebook, Instagram, Threads).
  Extracts creative patterns, messaging strategies, emotional triggers, and funnel positioning.
  Works in two modes: automatic via MCP (fb_ad_library) or manual analysis when the user
  pastes ad examples. Use when the user asks to analyze, research, spy on, or review
  competitor ads on Facebook, Instagram, Meta Ads, or mentions "biblioteca de anúncios",
  "ad library", "concorrentes no Meta", or "anúncios do Facebook".
license: MIT
metadata:
  author: davi-graeff
  version: "1.0"
  language: pt-BR
---

# Meta Ads Competitor Analysis

Skill para análise de anúncios de concorrentes na Biblioteca de Anúncios do Meta.

## Modo de Operação

Detecte automaticamente qual modo usar antes de iniciar:

**Modo API (MCP disponível):** Se as tools `fb_ad_library:get_meta_platform_id`, `fb_ad_library:get_meta_ads`, `fb_ad_library:analyze_ad_image` e `fb_ad_library:analyze_ad_video` estiverem acessíveis, use-as para buscar e analisar automaticamente.

**Modo Manual (sem MCP):** Se o MCP não estiver configurado ou o usuário colar exemplos de anúncios diretamente no chat, analise o conteúdo fornecido com o mesmo rigor. Oriente o usuário a acessar `facebook.com/ads/library` para copiar os dados.

## Instruções

### Passo 1 — Coleta de Dados

**Com MCP:**
1. Use `fb_ad_library:get_meta_platform_id` para encontrar o ID da página da marca
2. Use `fb_ad_library:get_meta_ads` para baixar anúncios ativos — priorize os últimos 90 dias
3. Para cada criativo: use `fb_ad_library:analyze_ad_image` ou `fb_ad_library:analyze_ad_video` conforme o formato
4. Armazene os resultados para que a skill `ad-variations-creator` possa reutilizá-los

**Sem MCP:**
1. Peça ao usuário o nome da marca ou URL da página
2. Instrua a acessar `facebook.com/ads/library` e filtrar por "Todos" > país > nome da marca
3. Solicite que cole textos, prints ou links dos anúncios
4. Prossiga para análise com os dados disponíveis

Se o usuário não informar a marca/concorrente, pergunte antes de prosseguir.

### Passo 2 — Análise Individual de Criativos

Para cada anúncio coletado, extraia e classifique:

| Dimensão | O que extrair |
|---|---|
| Formato | Vídeo curto/longo, imagem estática, carrossel, stories/reels |
| Elementos visuais | Cores dominantes, estilo (lifestyle/produto/UGC), presença de pessoas |
| Headline | Texto principal, estrutura (pergunta/afirmação/número), tamanho |
| Body copy | Argumentos, tom de voz, extensão |
| CTA | Chamada para ação utilizada e botão |
| Oferta | Desconto, benefício, urgência, prova social, garantia |

Aplique o framework de avaliação detalhado em [references/analysis-framework.md](references/analysis-framework.md) para pontuar cada dimensão.

### Passo 3 — Identificação de Padrões

Após analisar todos os anúncios, sintetize:

- **Formatos dominantes**: distribuição percentual por tipo de criativo
- **Mensagens recorrentes**: hooks, CTAs e argumentos que se repetem
- **Gatilhos emocionais**: medo, desejo, urgência, prova social, curiosidade, novidade, autoridade
- **Posicionamento de preço**: premium, custo-benefício ou acessível
- **Público aparente**: linguagem, referências culturais, faixa etária inferida
- **Testes A/B visíveis**: variações de headline ou visual rodando simultaneamente
- **Estágio de funil**: topo (awareness), meio (consideração) ou fundo (conversão)

### Passo 4 — Relatório Final

Gere um relatório estruturado contendo obrigatoriamente:

1. **Resumo executivo** (3-5 linhas com os insights mais críticos)
2. **Posicionamento identificado** (como a marca se posiciona nos ads)
3. **Distribuição por formato** (tabela com quantidade e %)
4. **Top 5 anúncios** com maior destaque (headline, formato, CTA, insight)
5. **Padrões de mensagem** (hooks, CTAs, gatilhos, tom de voz)
6. **Estratégia de funil detectada** (% topo/meio/fundo)
7. **Gaps e oportunidades** (o que a concorrência NÃO está fazendo)
8. **Recomendações acionáveis** (mínimo 3, máximo 5)

Para ver um exemplo completo de relatório, consulte [examples/competitor-report-example.md](examples/competitor-report-example.md).

### Passo 5 — Encadeamento

Ao final do relatório, sempre pergunte:

> "Deseja que eu crie variações de anúncios baseadas nesses padrões?"

Se o usuário aceitar, ative a skill `ad-variations-creator` passando o contexto coletado.

## Comportamento Esperado

- Se o MCP retornar zero anúncios, informe o usuário e sugira busca manual na Biblioteca de Anúncios
- Nunca invente dados — se não houver informações suficientes para uma seção, indique "dados insuficientes"
- Mantenha o tom analítico e objetivo no relatório
- Se o usuário pedir análise de múltiplas marcas, gere um relatório separado para cada uma
