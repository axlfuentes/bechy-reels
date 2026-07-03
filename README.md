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

## Publicar (GitHub Pages)

1. Crie um repositório público (ex. `bechy-reels`).
2. Suba `index.html` na raiz.
3. Settings → Pages → Deploy from branch → `main` / root.
4. URL: `https://<user>.github.io/bechy-reels/`
