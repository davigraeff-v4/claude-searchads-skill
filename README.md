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
git clone https://github.com/davigraeff-v4/claude-searchads-skill ~/.claude/skills/ads
```

#### Opção B — Só para um projeto específico

Dentro da pasta do projeto que você quer usar:

```bash
cd /caminho/do/seu/projeto
git clone https://github.com/davigraeff-v4/claude-searchads-skill .claude/skills/ads
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

## Configurando os MCPs (opcional)

As skills funcionam **sem nenhum MCP** — basta colar os exemplos de anúncios no chat. Mas se você quiser que o Claude busque e analise os anúncios automaticamente via API, configure um ou ambos os MCPs abaixo.

### MCP do Meta Ads Library

Permite buscar anúncios de qualquer marca diretamente da Biblioteca de Anúncios do Meta.

**Repositório:** [facebook-ads-library-mcp](https://github.com/RamsesAguirre777/facebook-ads-library-mcp)

```bash
# 1. Clone o repositório
git clone https://github.com/RamsesAguirre777/facebook-ads-library-mcp.git
cd facebook-ads-library-mcp
pip install -r requirements.txt

# 2. Obtenha um token do Facebook
#    Acesse: https://developers.facebook.com/tools/explorer/
#    Gere um token com permissão "ads_read"
```

**3. Configure no Claude Desktop** — adicione ao `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "facebook_ads": {
      "command": "python",
      "args": [
        "/caminho/para/facebook-ads-library-mcp/facebook_ads_mcp_complete.py",
        "--facebook-token",
        "SEU_TOKEN_AQUI"
      ]
    }
  }
}
```

**4. Reinicie o Claude Desktop.**

> Onde fica o `claude_desktop_config.json`?
> - **Mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`
> - **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

---

### MCP do Google Ads Transparency Center

Permite buscar anúncios de qualquer marca diretamente do Google Ads Transparency Center.

**Repositório:** [google-ads-library-mcp](https://github.com/talknerdytome-labs/google-ads-library-mcp)

```bash
# 1. Clone o repositório
git clone https://github.com/talknerdytome-labs/google-ads-library-mcp.git
cd google-ads-library-mcp
npm install
```

Consulte o README do repositório para configuração completa e obtenção da API key.

---

### MCP do Nano Banana (geração de criativos)

Permite que o Claude gere criativos estáticos de teste automaticamente usando IA (Google Gemini). Usado pela skill `meta-ads-competitor` após a análise — se este MCP estiver configurado, o Claude cria os criativos direto; se não estiver, entrega sugestões de copy e briefing visual.

**1. Obtenha uma API key do Google Gemini** (gratuita):
- Acesse [Google AI Studio](https://aistudio.google.com/apikey)
- Crie uma nova API key e copie

**2. Configure no Claude Desktop** — adicione ao `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "nanobanana-mcp": {
      "command": "npx",
      "args": ["-y", "@ycse/nanobanana-mcp"],
      "env": {
        "GOOGLE_AI_API_KEY": "SUA_API_KEY_AQUI"
      }
    }
  }
}
```

**3. Reinicie o Claude Desktop.**

> Só precisa ter o Node.js instalado (se você já usa o Claude Code, já tem).

---

### Como verificar se os MCPs estão ativos

No Claude Code, digite:

```
Quais ferramentas MCP estão disponíveis?
```

- Se aparecer tools com prefixo `fb_ad_library:` → MCP do Meta está ativo
- Se aparecer tools com prefixo `google_ads:` → MCP do Google está ativo
- Se aparecer tools com prefixo `nanobanana-mcp:` → MCP do Nano Banana está ativo (geração de criativos)

As skills detectam automaticamente quais MCPs estão disponíveis e alternam entre modo automático e manual.

---

## Fluxo recomendado de uso

```
1. meta-ads-competitor   →  analisa concorrentes no Meta (+ gera criativos se Nano Banana estiver ativo)
2. google-ads-competitor →  analisa concorrentes no Google
3. ad-variations-creator →  gera variações de copy com base nos dados coletados
```

As skills são encadeáveis — o `ad-variations-creator` usa automaticamente os dados coletados pelas outras duas na mesma sessão.

Você pode usar cada skill individualmente também. O `ad-variations-creator` funciona standalone se você colar exemplos de anúncios diretamente.

**Para geração de criativos estáticos:** a skill `meta-ads-competitor` vai pedir tipografia, cores da marca, identidade visual e logo antes de gerar qualquer criativo via Nano Banana. Sem essas informações, ela entrega sugestões de copy e briefing visual.

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

## Feedback e Sugestões

Encontrou algo que pode melhorar? Abra uma issue diretamente no GitHub:

1. Acesse [Issues](https://github.com/davigraeff-v4/claude-searchads-skill/issues)
2. Clique em **New Issue**
3. Escolha o tipo: **Feedback/Sugestão** ou **Bug/Erro**
4. Preencha o formulário e envie

Não precisa saber programar — só descrever o que aconteceu e o que esperava.

---

## Contribuindo com código

1. Faça um fork do repositório
2. Edite o `SKILL.md` da skill que deseja melhorar
3. Teste localmente seguindo os passos acima
4. Abra um Pull Request descrevendo o que mudou

---

## Licença

MIT — use, modifique e distribua livremente.
