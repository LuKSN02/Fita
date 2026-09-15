# Fita

Um player de música com cara de Spotify que toca vídeos do YouTube dentro da própria página, sem redirecionar para o YouTube. Cole um link, a faixa entra na fila e toca ali mesmo.

## O que dá para fazer

- **Tocar qualquer link do YouTube** — vídeo normal, `youtu.be`, `/shorts`, `/embed` ou um link com `?list=`, que importa a playlist inteira de uma vez.
- **Fila reordenável** — arraste as faixas para mudar a ordem enquanto tocam.
- **Playlists de verdade** — crie, renomeie e apague coleções próprias; elas ficam salvas no navegador entre uma visita e outra.
- **Histórico** — as últimas faixas tocadas ficam guardadas e podem ser tocadas de novo com um clique.
- **Busca real no YouTube** — opcional, exige uma chave gratuita da YouTube Data API v3 (o app explica como gerar uma na hora).
- **Controles completos** — play/pause, anterior/próxima, aleatório, repetir (tudo ou uma faixa), barra de progresso arrastável e volume.
- **Integração com o sistema** — os botões de mídia do teclado e a tela de bloqueio do celular controlam a reprodução (Media Session API), com capa e título da faixa.

## Como publicar

O arquivo é uma página só (`index.html`), sem build e sem dependências para instalar. A única exigência é que ele seja servido por `http://` ou `https://` — a API do YouTube não funciona quando o arquivo é aberto direto do disco (`file://`).

**GitHub Pages (recomendado):**
1. Crie um repositório público no GitHub.
2. Suba o arquivo e renomeie para `index.html`.
3. Em *Settings → Pages*, ative o Pages na branch `main`, pasta `/ (root)`.
4. Acesse o link gerado (`https://seuusuario.github.io/nome-do-repo/`).

**Testar localmente:** rode um servidor simples na pasta do arquivo, por exemplo `python -m http.server`, e abra `http://localhost:8000`.

## Ativando a busca

A busca por nome de música precisa de uma chave própria da YouTube Data API v3, porque o YouTube não permite busca anônima:
1. Crie um projeto no [Google Cloud Console](https://console.cloud.google.com/).
2. Ative a **YouTube Data API v3**.
3. Gere uma chave de API em *Credenciais*.
4. Cole a chave na aba **Buscar** do site.

A chave fica salva só no seu navegador. Sem ela, tudo o resto do site continua funcionando normalmente — colar links, importar playlists e montar a biblioteca.

## Sobre os Termos de Serviço do YouTube

O player fica visível em um painel flutuante no canto da tela, em vez de escondido. Isso não é só estética: os Termos da API do YouTube exigem que o embed permaneça visível e que áudio e vídeo não sejam separados, e escondê-lo com `display: none` faz vários navegadores suspenderem a reprodução.

## Tecnologias

HTML, CSS e JavaScript puros, sem frameworks. A reprodução usa a [YouTube IFrame Player API](https://developers.google.com/youtube/iframe_api_reference); os títulos das faixas vêm do endpoint público `oEmbed` do YouTube.
