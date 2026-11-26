ï»¿# ê°Å¸Â¦Å¾ Gravity Claw

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


> Um agente de IA pessoal lean, seguro e totalmente compreendido ê¢â¬â construêÂ­do do zero em TypeScript.

**[ê¢â â Acesse o hub de recursos](https://inematds.github.io/gravityclaw/)** &nbsp;êÂ·&nbsp; **[ê¢â â Feature Store (live)](https://gravity-claw.vercel.app/)**

---

## O que êÂ©

Gravity Claw êÂ© um **bot Telegram com loop agêÂªntico**, inspirado no projeto OpenClaw mas construêÂ­do do zero ê¢â¬â para que cada linha seja entendida, auditada e sob controle do dono.

NêÂ£o êÂ© um fork. êâ° uma reimplementaêÂ§êÂ£o deliberada que resolve os problemas estruturais do original:

| Problema no OpenClaw | SoluêÂ§êÂ£o no Gravity Claw |
|---|---|
| 42.665 instêÂ¢ncias expostas publicamente | Telegram long-polling ê¢â¬â sem portas abertas |
| 341 community skills maliciosas encontradas | MCP apenas ê¢â¬â processos separados e auditêÂ¡veis |
| Custos de $500ê¢â¬â$5K/mêÂªs por token | Claude Max ($200 fixo) ou modelos locais |
| 100K+ linhas que ninguêÂ©m leu | ConstruêÂ­do brick-by-brick, cada linha revisada |

---

## PrincêÂ­pios NêÂ£o-NegociêÂ¡veis

- **Sem web server / sem portas abertas** ê¢â¬â Telegram long-polling apenas
- **Whitelist de Telegram ID** ê¢â¬â silenciosamente ignora qualquer outro usuêÂ¡rio
- **Secrets no `.env` apenas** ê¢â¬â nunca em cêÂ³digo, logs ou arquivos de memêÂ³ria
- **MCP para integraêÂ§êÂµes** ê¢â¬â nenhum skill file externo nêÂ£o-auditado
- **Limite de iteraêÂ§êÂµes** no agent loop + confirmaêÂ§êÂ£o para shell commands perigosos

---

## Tech Stack

| Pacote | FunêÂ§êÂ£o |
|---|---|
| `grammy` | Telegram bot framework |
| `@anthropic-ai/sdk` | LLM primêÂ¡rio (Claude Sonnet 4.6) |
| `better-sqlite3` + FTS5 | MemêÂ³ria de curto prazo / conversation buffer |
| `openai` SDK | Whisper transcription (STT) |
| ElevenLabs API | Text-to-speech |
| `tsx` | Dev runner com hot-reload |
| `node-cron` | Heartbeat / proactive check-ins |

---

## Build Levels

| Level | Foco | Features |
|---|---|---|
| **L1 ê¢â¬â Foundation** | Telegram + Claude + agent loop | Um tool: `get_current_time` |
| **L2 ê¢â¬â Memory** | SQLite + FTS5 + memory tools | `better-sqlite3`, `soul.md` |
| **L3 ê¢â¬â Voice** | Whisper in, ElevenLabs out | Notas de voz bidirecionais |
| **L4 ê¢â¬â Tools** | MCP bridge | Shell, files, Gmail, Notion, GitHub |
| **L5 ê¢â¬â Heartbeat** | `node-cron` | Briefings diêÂ¡rios, accountability |

---

## Recursos

### Feature Stores Interativas

| Arquivo | DescriêÂ§êÂ£o |
|---|---|
| [Feature Store ê¢â¬â AntiGravity Edition](doc/gravity-claw-antigravity.html) | Seleciona features ê¢â â gera prompt para o AntiGravity (CLAWS Framework) |
| [Feature Store ê¢â¬â Claude Code Edition](doc/gravity-claw-claudecode.html) | Seleciona features ê¢â â gera `CLAUDE.md` para o Claude Code CLI |
| [Feature Store ê¢â¬â Original](doc/gravity-claw.html) | VersêÂ£o original (7 categorias, tema roxo) |
| [Feature Store ê¢â¬â Vercel Clone](doc/gravity-claw-store.html) | Clone completo do site vercel (11 categorias, tema teal) |
| [Feature Store (live)](https://gravity-claw.vercel.app/) | VersêÂ£o publicada no Vercel |

### Documentos

| Arquivo | DescriêÂ§êÂ£o |
|---|---|
| [CLAUDE.md](CLAUDE.md) | InstruêÂ§êÂµes para o Claude Code ao trabalhar neste repo |
| [Prompt de InicializaêÂ§êÂ£o](doc/gravity-claw-initialisation-prompt.md) | Prompt para colar no AntiGravity e bootstrapar o projeto do zero |
| [Railway SOP](doc/update-gravity-claw-railway-sop.md) | Procedimento completo de deploy e gestêÂ£o no Railway |

### ReferêÂªncia Externa

| Link | DescriêÂ§êÂ£o |
|---|---|
| [Framework Comparison](https://inematds.github.io/intelecto/doc/framework-comparison-pt.html) | ComparaêÂ§êÂ£o dos 9 frameworks do ecossistema OpenClaw |

---

## Dev Workflow

```bash
# Antes de testar localmente ê¢â¬â evita conflito de instêÂ¢ncias
railway down

# Dev com hot-reload
npm run dev   # tsx watch src/index.ts

# Type-check antes de deployar
npx tsc --noEmit

# Deploy
railway up --detach
railway logs --lines 40
```

**Startup saudêÂ¡vel:**
```
ê¢Åâ¦ Soul loaded (soul.md)
ê¢Åâ¦ Connected as @your_bot_name
ê¢Åâ¦ Heartbeat scheduled
```

---

## MemêÂ³ria em 3 Camadas

```
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
ê¢ââ  Tier 1 ê¢â¬â Core Memory           ê¢ââ  soul.md ê¢â â injetado no system prompt
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ¤
ê¢ââ  Tier 2 ê¢â¬â Conversation Buffer   ê¢ââ  SQLite + FTS5 (reseta no Railway deploy)
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ¤
ê¢ââ  Tier 3 ê¢â¬â Semantic Long-Term    ê¢ââ  Supabase + pgvector (persiste sempre)
ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË
```

---

*Parte do ecossistema [OpenClaw](https://openclaw.ai) ê¢â¬â construêÂ­do com o [CLAWS Framework](https://gravity-claw.vercel.app/)*

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>