# Reels da Bechy 📸

Gerador de ideias, ganchos, captions e hashtags para Reels de fotografia de
paisagem/viagem/natureza. **Português por padrão** (alterna para Español).
Um único arquivo, zero dependências, funciona offline.

## Usar no celular

Abra a URL publicada (GitHub Pages) e adicione à tela inicial. Depois da
primeira carga funciona offline. Botões **Copiar** e **📲 Compartilhar**
mandam o texto direto para o Instagram (share sheet do celular).

## Usar no PC (com IA)

O botão **✨ Expandir com IA** só aparece quando um Ollama local responde:

    cd BechyReels
    python -m http.server 8925
    # abra http://localhost:8925/

Requisitos: [Ollama](https://ollama.com) rodando com um modelo (ex.
`ollama pull qwen2.5:7b-instruct-q4_K_M`). Se o navegador bloquear o fetch
por CORS, inicie o Ollama com `OLLAMA_ORIGINS=http://localhost:8925`.
Observação: a versão https (GitHub Pages) NUNCA mostra o botão de IA —
navegadores bloqueiam https→http://localhost (mixed content). É intencional:
celular = base offline; PC = base + IA.

## Testes

    node tests/run_tests.mjs

Valida a integridade bilíngue (todo item tem `pt` E `es`) e o contrato do
gerador (3-5 ganchos, 15-25 hashtags, placeholders preenchidos).

## Salvar ideias

Toque **💾 Salvar** numa ideia gerada — ela fica guardada no navegador
(`localStorage`, sobrevive a recarregar e funciona offline). O botão
**⭐ Salvos (N)** abre a lista: **Abrir** recarrega a ideia no cartão, **🗑**
remove. Nada sai do dispositivo.

## IA online (opcional) — servidor isolado

Para o botão **✨ Expandir com IA** funcionar na versão hospedada (https), o PC
publica um túnel Cloudflare que aponta para um proxy Ollama local. Tudo vive em
`server/` e é **totalmente separado do projeto FR24** — porta, túnel, tarefas e
repositório próprios (sem PAT compartilhado, sem imports cruzados):

| Peça | Bechy | (FR24, para referência — NÃO tocar) |
|------|-------|-------------------------------------|
| Proxy Ollama | `server/reels_ai_server.py` · `127.0.0.1:8926` | `:8889` |
| Túnel | `server/start_tunnel.ps1` (cloudflared próprio) | túnel próprio |
| Publica URL | `server/publish_endpoint.py` → repo **bechy-reels** (via `gh`) | repo fps-rte (via PAT) |
| Tarefas | `BechyReels-AIServer` / `-Tunnel` / `-Keepalive` | `FR24-PublicChat*` |

Único recurso compartilhado: o **Ollama** local (`:11434`) — um servidor de
modelo, não código de projeto. A app tenta primeiro `localhost:11434` (dev no
PC) e, se falhar, lê `agent_endpoint.json` (túnel publicado) e usa `<túnel>/reels`.

Registrar as tarefas de fundo (uma vez, PowerShell **como administrador**):

    powershell -ExecutionPolicy Bypass -File server\register_tasks.ps1

A IA online só fica ativa enquanto o **PC + Ollama + túnel** estiverem ligados;
caso contrário o botão some e o gerador base continua funcionando.

## Publicar (GitHub Pages)

1. Crie um repositório público (ex. `bechy-reels`).
2. Suba `index.html` na raiz.
3. Settings → Pages → Deploy from branch → `main` / root.
4. URL: `https://<user>.github.io/bechy-reels/`
