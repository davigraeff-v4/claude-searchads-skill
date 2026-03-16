---
name: meta-ads-competitor
description: >-
  Performs strategic analysis of competitor ads from Meta Ads Library (Facebook, Instagram, Threads).
  Identifies winning creative compositions, extracts champion copy examples, analyzes emotional triggers
  and funnel positioning. Optionally generates static ad creatives via Nano Banana MCP.
  Works with MCP (fb_ad_library) for automatic collection or manual input.
  Use when the user asks to analyze, research, spy on, or review competitor ads on Facebook,
  Instagram, Meta Ads, or mentions "biblioteca de anúncios", "ad library", "concorrentes no Meta",
  "anúncios do Facebook", "criativos dos concorrentes", or "copies campeãs".
license: MIT
metadata:
  author: davi-graeff
  version: "2.0"
  language: pt-BR
---

# Meta Ads Competitor Analysis

Skill para análise estratégica de anúncios de concorrentes na Biblioteca de Anúncios do Meta, com foco em identificar criativos campeões, extrair copies vencedoras e, opcionalmente, gerar criativos estáticos de teste via Nano Banana.

## Modo de Operação

Detecte automaticamente quais recursos estão disponíveis antes de iniciar:

**MCP Meta Ads (coleta automática):** Se as tools `fb_ad_library:get_meta_platform_id`, `fb_ad_library:get_meta_ads`, `fb_ad_library:analyze_ad_image` e `fb_ad_library:analyze_ad_video` estiverem acessíveis, use-as para buscar e analisar automaticamente.

**MCP Nano Banana (geração de criativos):** Se as tools `nanobanana-mcp:*` estiverem acessíveis, o modo de geração de criativos estáticos fica disponível no Passo 6. Se não estiver disponível, entregue sugestões de copy e comunicação visual em vez de gerar imagens.

**Modo Manual (sem nenhum MCP):** Oriente o usuário a acessar `facebook.com/ads/library` para copiar os dados. Analise o conteúdo fornecido com o mesmo rigor.

## Instruções

### Passo 1 — Coleta de Dados

**Com MCP Meta Ads:**
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

### Passo 2 — Análise Estratégica de Criativos

Para cada anúncio coletado, vá além da extração básica. Analise estrategicamente:

| Dimensão | O que extrair | Análise estratégica |
|---|---|---|
| Formato | Vídeo, imagem, carrossel, stories/reels | Qual formato domina e por quê (custo, performance, público) |
| Composição visual | Layout, hierarquia, cores, tipografia, estilo | O que torna o criativo visualmente eficaz — o que para o scroll |
| Headline | Texto principal, estrutura | Por que essa headline funciona — qual gatilho ativa |
| Body copy | Argumentos, tom, extensão | Qual técnica de persuasão está sendo usada |
| CTA | Chamada para ação e botão | Alinhamento entre CTA e objetivo de campanha |
| Oferta | Desconto, benefício, urgência, prova social | Como a oferta reduz a barreira de compra |

Aplique o framework de avaliação detalhado em [references/analysis-framework.md](references/analysis-framework.md) para pontuar cada dimensão.

### Passo 3 — Identificação de Criativos Campeões

Identifique os **melhores criativos** com base nos seguintes critérios:

1. **Composição visual vencedora**: quais elementos visuais se repetem nos melhores anúncios? (layout, cores, tipografia, estilo fotográfico, presença de pessoas)
2. **Copies campeãs**: extraia as headlines e body copies que mais se destacam e explique por que funcionam
3. **Estruturas de hook**: quais aberturas estão sendo usadas nos criativos com mais destaque
4. **Padrão de CTA**: quais chamadas para ação convertem melhor no segmento

Para cada criativo campeão identificado, entregue:

```
CRIATIVO CAMPEÃO #[N]
─────────────────────────────────────
Formato:          [tipo]
Headline:         "[texto exato]"
Body copy:        "[texto exato]"
CTA:              "[texto exato]"
Composição:       [descrição dos elementos visuais: layout, cores, fonte, estilo]
Por que funciona: [análise estratégica — qual gatilho, qual técnica, qual diferencial]
─────────────────────────────────────
```

### Passo 4 — Padrões e Oportunidades

Após analisar todos os anúncios, sintetize:

- **Formatos dominantes**: distribuição percentual por tipo de criativo
- **Copies que mais se repetem**: headlines e argumentos recorrentes
- **Gatilhos emocionais**: medo, desejo, urgência, prova social, curiosidade, novidade, autoridade
- **Composição visual padrão**: cores dominantes, tipografia, estilo de foto/vídeo
- **Posicionamento de preço**: premium, custo-benefício ou acessível
- **Público aparente**: linguagem, referências culturais, faixa etária inferida
- **Testes A/B visíveis**: variações rodando simultaneamente
- **Estágio de funil**: topo (awareness), meio (consideração) ou fundo (conversão)
- **Gaps e oportunidades**: o que a concorrência NÃO está fazendo

### Passo 5 — Relatório Estratégico

Gere um relatório estruturado contendo obrigatoriamente:

1. **Resumo executivo** (3-5 linhas com os insights mais críticos)
2. **Posicionamento identificado** (como a marca se posiciona nos ads)
3. **Distribuição por formato** (tabela com quantidade e %)
4. **Criativos campeões** (top 5 com análise completa — formato do Passo 3)
5. **Copies campeãs** (lista das melhores headlines e bodies com análise de por que funcionam)
6. **Padrões de composição visual** (cores, tipografia, layout, estilo que se repetem nos melhores)
7. **Estratégia de funil detectada** (% topo/meio/fundo)
8. **Gaps e oportunidades** (o que a concorrência NÃO está fazendo)
9. **Recomendações acionáveis** (mínimo 3, máximo 5)

Para ver um exemplo completo de relatório, consulte [examples/competitor-report-example.md](examples/competitor-report-example.md).

### Passo 6 — Geração de Criativos Estáticos (com Nano Banana)

**IMPORTANTE: Este passo só é executado se o MCP `nanobanana-mcp` estiver disponível.**

Antes de gerar qualquer criativo, colete obrigatoriamente do usuário:

| Informação | Obrigatório | Descrição |
|---|---|---|
| Tipografia | Sim | Fonte(s) usada(s) pela marca (ex: Montserrat Bold, Inter Regular) |
| Cores | Sim | Paleta de cores da marca (hex codes: primária, secundária, destaque) |
| Identidade visual | Se houver | Manual de marca, guidelines, ou descrição do estilo visual |
| Logo | Sim | Solicite que o usuário envie o arquivo da logo |

**Não gere nenhum criativo antes de ter todas as informações obrigatórias.** Pergunte o que estiver faltando.

Com todas as informações coletadas:
1. Crie prompts detalhados para criativos estáticos de teste baseados nos padrões campeões identificados
2. Inclua no prompt: tipografia, cores, estilo visual da marca, composição baseada nos criativos campeões
3. Use `nanobanana-mcp` para gerar os criativos estáticos
4. Gere no mínimo 3 variações de criativos com abordagens diferentes (seguindo o padrão das variações do `ad-variations-creator`)

**Se o MCP Nano Banana NÃO estiver disponível:**
Em vez de gerar imagens, entregue:
- Sugestões detalhadas de copy (headline + body + CTA) para cada variação
- Briefing visual descritivo para designer (composição, cores, elementos, estilo)
- Referências visuais baseadas nos criativos campeões analisados

### Passo 7 — Encadeamento

Ao final do relatório, sempre pergunte:

> "Deseja que eu crie variações de anúncios baseadas nesses padrões?"

Se o usuário aceitar, ative a skill `ad-variations-creator` passando o contexto coletado.

## Comportamento Esperado

- Se o MCP retornar zero anúncios, informe o usuário e sugira busca manual na Biblioteca de Anúncios
- Nunca invente dados — se não houver informações suficientes para uma seção, indique "dados insuficientes"
- Mantenha o tom analítico e estratégico no relatório — não apenas descreva, explique por que funciona
- Se o usuário pedir análise de múltiplas marcas, gere um relatório separado para cada uma
- Para geração de criativos: nunca pule a coleta de tipografia, cores e logo — são obrigatórios
