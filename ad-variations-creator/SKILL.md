---
name: ad-variations-creator
description: >-
  Creates ad variations based on competitor analysis references or user-provided examples.
  Applies copywriting frameworks (AIDA, PAS, BAB, 4U) to generate distinct ad copies
  for Meta (Feed, Stories, Reels) and Google (Search, Display, YouTube).
  Works standalone or chained after meta-ads-competitor / google-ads-competitor.
  Use when the user asks to create, generate, write, or vary ads, ad copies, creatives,
  or mentions "variações de anúncio", "criar anúncios", "gerar copies", or "novas versões".
license: MIT
metadata:
  author: davi-graeff
  version: "1.0"
  language: pt-BR
---

# Ad Variations Creator

Skill para criação de variações de anúncios baseadas em referências competitivas.

## Modo de Operação

**Modo encadeado (recomendado):** Utiliza automaticamente os dados coletados pelas skills `meta-ads-competitor` ou `google-ads-competitor` na mesma sessão.

**Modo manual:** O usuário cola exemplos de anúncios diretamente no chat como referência base.

**Modo misto:** Combina dados coletados via MCP com exemplos manuais adicionais.

## Instruções

### Passo 1 — Coleta de Contexto

Antes de criar qualquer variação, colete as seguintes informações. Pergunte o que não foi fornecido:

| Informação | Por que é necessária |
|---|---|
| Marca/produto | O que será anunciado |
| Público-alvo | Para quem é o anúncio (idade, interesses, dores) |
| Objetivo | Conversão, tráfego, awareness, leads, app installs |
| Plataforma | Meta (Feed, Stories, Reels) ou Google (Search, Display, YouTube) |
| Diferencial | O que torna o produto/serviço único vs concorrência |
| Tom de voz | Formal, descontraído, técnico, emocional, provocativo |

Se o contexto veio da análise de concorrentes (modo encadeado), infira o máximo possível dos dados já coletados e confirme com o usuário antes de prosseguir.

### Passo 2 — Análise das Referências

Com base nos dados coletados ou exemplos fornecidos:

1. Identifique os **3 padrões mais fortes** dos concorrentes (estruturas de copy que se repetem)
2. Mapeie os **gatilhos emocionais** mais usados (medo, desejo, urgência, prova social, curiosidade)
3. Identifique **estruturas de headline** recorrentes (pergunta, número, afirmação, contra-intuitivo)
4. Note o **gap de posicionamento** — o que nenhum concorrente está fazendo

Consulte os frameworks de copywriting em [references/copywriting-frameworks.md](references/copywriting-frameworks.md) para fundamentar as variações.

### Passo 3 — Geração de Variações

Crie **mínimo 3 variações distintas** para cada formato solicitado, cada uma com abordagem diferente:

**Variação 1 — Padrão de Mercado (adaptado)**
Siga a estrutura que os concorrentes mais usam, mas com a proposta de valor da marca do usuário. Objetivo: capturar a mesma audiência com mensagem diferenciada.

**Variação 2 — Explorando o Gap**
Use o posicionamento que os concorrentes estão ignorando. Objetivo: ocupar um espaço vazio no mercado.

**Variação 3 — Contraste Emocional**
Se os concorrentes usam emoção, teste racional. Se usam racional, teste emoção. Objetivo: testar uma abordagem que quebre o padrão do mercado.

### Passo 4 — Formato de Entrega

Para cada variação, entregue neste formato exato:

```
── VARIAÇÃO [N] — [Nome da Abordagem] ──────────────────
Plataforma:  [Meta Feed / Google Search / YouTube / etc.]
Objetivo:    [Conversão / Lead / Awareness]
Framework:   [AIDA / PAS / BAB / 4U]

HEADLINE:    [texto]
BODY:        [texto]
CTA:         [texto]

Racional:    [Por que essa abordagem? O que ela explora?]
Referência:  [Qual padrão dos concorrentes inspirou ou contrastou?]
─────────────────────────────────────────────────────────
```

**Para Google Search Ads**, adapte o formato:
```
── VARIAÇÃO [N] — [Nome da Abordagem] ──────────────────
Formato: RSA (Responsive Search Ad)

HEADLINES (até 15, máx 30 caracteres cada):
  H1: [texto]
  H2: [texto]
  H3: [texto]
  ...

DESCRIPTIONS (até 4, máx 90 caracteres cada):
  D1: [texto]
  D2: [texto]

EXTENSIONS SUGERIDAS:
  Sitelinks: [lista]
  Callouts: [lista]

Racional:    [justificativa]
─────────────────────────────────────────────────────────
```

Para ver um exemplo completo de output, consulte [examples/variations-example.md](examples/variations-example.md).

### Passo 5 — Tabela de Priorização A/B

Ao final, entregue uma tabela de priorização:

| Variação | Ângulo | Hipótese | Métrica-chave | Prioridade |
|---|---|---|---|---|
| V1 | [nome] | [o que espera validar] | [CTR/CPL/ROAS] | Alta/Média/Baixa |
| V2 | ... | ... | ... | ... |
| V3 | ... | ... | ... | ... |

Indique:
- Qual variação testar primeiro e por quê
- Qual métrica principal observar (CTR, CPL, ROAS, CPA)
- Sugestão de público/segmento para cada variação

### Passo 6 — Próximos Passos

Ao final, pergunte:

> "Quer que eu adapte alguma variação, crie versões para outro formato, ou gere mais variações com um ângulo diferente?"

## Comportamento Esperado

- Nunca copie diretamente o anúncio do concorrente — sempre adapte, diferencie e melhore
- Se faltar contexto sobre o produto/marca, pergunte antes de gerar (não assuma)
- Sempre entregue no mínimo 3 variações, nunca menos
- Respeite os limites de caracteres de cada plataforma (Google Search: 30 chars headline, 90 chars description)
- Aplique pelo menos um framework de copywriting por variação (AIDA, PAS, BAB ou 4U)
