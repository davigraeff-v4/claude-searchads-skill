# Claude Ads Skills — Análise de Concorrentes e Criação de Variações

Skills para o Claude Code que analisam anúncios de concorrentes no **Meta Ads** e **Google Ads** e geram variações de anúncios com base nas referências coletadas.

Funcionam em dois modos:
- **Com MCP configurado** → busca e analisa automaticamente via API
- **Sem MCP** → você cola os exemplos no chat e o Claude analisa com o mesmo rigor

---

## O que está incluído

| Skill | O que faz |
|---|---|
| `meta-ads-competitor` | Analisa anúncios de concorrentes na Biblioteca de Anúncios do Meta (Facebook, Instagram) |
| `google-ads-competitor` | Analisa anúncios de concorrentes no Google Ads Transparency Center (Search, Display, YouTube) |
| `ad-variations-creator` | Gera variações de anúncios com base nas referências coletadas, aplicando frameworks de copywriting |

---

## Pré-requisitos

Antes de instalar, verifique se você tem:

- [ ] **Claude Desktop** instalado → [claude.ai/download](https://claude.ai/download)
- [ ] **Claude Code** instalado → abra o terminal e rode:
  ```bash
  npm install -g @anthropic-ai/claude-code
  ```
- [ ] **Git** instalado → [git-scm.com/downloads](https://git-scm.com/downloads)

> Não sabe se já tem o Git? Abra o terminal e digite `git --version`. Se aparecer um número de versão, já está instalado.

---

## Instalação — Passo a Passo

### Passo 1 — Abra o Terminal

**No Mac:** pressione `Cmd + Espaço`, digite `Terminal` e aperte Enter.
**No Windows:** pressione `Win + R`, digite `cmd` e aperte Enter.
**No Linux:** pressione `Ctrl + Alt + T`.

### Passo 2 — Escolha onde instalar

#### Opção A — Para todos os seus projetos (recomendado)

As skills ficam disponíveis em qualquer projeto que você abrir no Claude Code.

```bash
git clone https://github.com/seu-usuario/claude-ads-skills ~/.claude/skills/ads
```

#### Opção B — Só para um projeto específico

Dentro da pasta do projeto que você quer usar:

```bash
cd /caminho/do/seu/projeto
git clone https://github.com/seu-usuario/claude-ads-skills .claude/skills/ads
```

> Não sabe o caminho do projeto? Arraste a pasta para dentro do terminal — o caminho aparece automaticamente.

### Passo 3 — Confirme que os arquivos estão no lugar certo

```bash
# Se instalou na Opção A:
ls ~/.claude/skills/ads

# Se instalou na Opção B:
ls .claude/skills/ads
```

Você deve ver exatamente isso:

```
README.md
meta-ads-competitor/
google-ads-competitor/
ad-variations-creator/
```

Se aparecer isso, a instalação foi bem-sucedida.

### Passo 4 — Abra o Claude Code

```bash
claude
```

---

## Como testar se as skills estão funcionando

### Teste 1 — Ver se o Claude reconhece as skills

Digite no Claude Code:

```
Quais skills estão disponíveis?
```

O Claude deve listar as 3 skills. Se não aparecer, volte ao Passo 3 e confirme os caminhos.

### Teste 2 — Ativar manualmente pelo nome

```
/meta-ads-competitor
```

```
/google-ads-competitor
```

```
/ad-variations-creator
```

Se cada uma carregar sem erro, estão funcionando.

### Teste 3 — Ativar por linguagem natural

```
Analise os anúncios da Nike no Meta
```

```
Quero ver o que o Nubank está anunciando no Google
```

```
Crie variações de anúncio baseadas nesses exemplos
```

O Claude deve identificar qual skill usar automaticamente e iniciar o processo.

### Teste 4 — Confirmar que NÃO ativa no contexto errado

```
Me ajude a escrever um email
```

As skills de ads **não devem** ativar. Se ativarem, a `description` do `SKILL.md` está genérica demais.

---

## Usando com MCP do Meta Ads (opcional)

Se você tem o **Facebook Ads Library MCP** instalado e configurado no `claude_desktop_config.json`, as skills detectam automaticamente e se conectam via API para análise automática.

Se **não tem o MCP**, não tem problema — as skills funcionam no modo manual: basta colar os exemplos de anúncios diretamente no chat.

### Como verificar se o MCP está ativo

No Claude Code, digite:

```
Quais ferramentas MCP estão disponíveis?
```

Se aparecer tools com prefixo `fb_ad_library:` na lista, o MCP está ativo e a skill usará a API automaticamente.

---

## Fluxo recomendado de uso

```
1. meta-ads-competitor   →  analisa concorrentes no Meta
2. google-ads-competitor →  analisa concorrentes no Google
3. ad-variations-creator →  gera variações com base nos dados coletados
```

As skills são encadeáveis — o `ad-variations-creator` usa automaticamente os dados coletados pelas outras duas na mesma sessão.

Você pode usar cada skill individualmente também. O `ad-variations-creator` funciona standalone se você colar exemplos de anúncios diretamente.

---

## Estrutura do repositório

```
claude-ads-skills/
├── README.md
├── meta-ads-competitor/
│   ├── SKILL.md
│   ├── references/
│   │   └── analysis-framework.md
│   └── examples/
│       └── competitor-report-example.md
├── google-ads-competitor/
│   ├── SKILL.md
│   ├── references/
│   │   └── search-ad-patterns.md
│   └── examples/
│       └── google-report-example.md
└── ad-variations-creator/
    ├── SKILL.md
    ├── references/
    │   └── copywriting-frameworks.md
    └── examples/
        └── variations-example.md
```

---

## Problemas comuns

**"Skills não aparecem quando pergunto"**
→ Confirme que o arquivo se chama exatamente `SKILL.md` (maiúsculas). O nome é case-sensitive.

**"O Claude não ativa a skill automaticamente"**
→ Tente invocar pelo nome direto: `/meta-ads-competitor`
→ Se funcionar assim mas não automaticamente, a `description` precisa ter as palavras que você usa naturalmente.

**"Erro ao clonar o repositório"**
→ Confirme que o Git está instalado: `git --version`
→ Confirme que tem conexão com a internet.

**"Pasta `.claude` não existe"**
→ Crie antes de clonar:
```bash
mkdir -p ~/.claude/skills
```

**"MCP não conecta"**
→ Verifique se o `claude_desktop_config.json` está configurado corretamente.
→ Reinicie o Claude Code após alterar a configuração MCP.

---

## Como atualizar as skills

Para pegar a versão mais recente:

```bash
# Opção A (global):
cd ~/.claude/skills/ads && git pull

# Opção B (projeto):
cd .claude/skills/ads && git pull
```

---

## Contribuindo

1. Faça um fork do repositório
2. Edite o `SKILL.md` da skill que deseja melhorar
3. Teste localmente seguindo os passos acima
4. Abra um Pull Request descrevendo o que mudou

---

## Licença

MIT — use, modifique e distribua livremente.
