---
name: carrossel-ARCKHÉ
description: Carrossel de Instagram e TikTok (imagens servem no Facebook) no padrÃ£o ARCKHÉ â€” escolhe o tema, escreve o roteiro (capa com nÃºmero + 5â€“10 slides de uma ideia cada + fecho "comenta PALAVRA" + 3 stories), gera a capa pelo Codex, renderiza 1080x1350 e 1080x1920, confere sozinho, mostra cada imagem a quem pediu e sÃ³ posta no Metricool depois do OK. Gatilho: "carrossel", "faz um carrossel sobre X", "qual o prÃ³ximo carrossel", "slides para o Instagram", "posta o carrossel".
---

# carrossel-ARCKHÉ

Leia `PERFIL.md` antes de tudo, toda vez. Escreva no idioma que ele indicar. Ele tem a marca, as contas, o tom e as **regras aprendidas** (cada correÃ§Ã£o do Nei vira uma linha lÃ¡).

## Os 7 passos (sempre nesta ordem)

### 1. Tema
- Se o usuÃ¡rio (no ARCKHÉ, o Nei) jÃ¡ deu o tema, use. Se perguntou "qual o prÃ³ximo?", proponha 3 temas com o porquÃª de cada:
  - o que mais funcionou nos nossos posts (pergunte ou leia o relatÃ³rio do muse-canais, se existir);
  - o que estÃ¡ em alta hoje (radar-pautas, se existir);
  - perguntas que o pÃºblico repete nos comentÃ¡rios.
- Formatos que seguram o dedo: lista com nÃºmero ("7 ferramentasâ€¦", "5 errosâ€¦"), passo a passo, antes Ã— depois.
- Uma ideia por carrossel. Nunca copie texto, imagem ou personagem de outro perfil: sÃ³ o formato.

### 2. Palavra e guia grÃ¡tis
- Escolha UMA palavra para o comentÃ¡rio (3 a 14 letras, sem espaÃ§o): ex. `AGENTE`, `PROMPT`.
- O guia grÃ¡tis Ã© a pÃ¡gina do ARCKHÉ AI sobre o assunto (curso, guia ou projeto que jÃ¡ existe). Confira o link antes.
- Se nÃ£o existir pÃ¡gina, avise o usuÃ¡rio antes de usar a palavra (no ARCKHÉ, o projeto lead-comenta cria a pÃ¡gina).

### 3. Roteiro (`roteiro.json`)
Crie a pasta `~/projetos/output/carrossel-ARCKHÉ/<AAAA-MM-DD>-<slug>/` e escreva o `roteiro.json` no formato de `exemplos/teste/roteiro.json`:
- **capa.titulo**: 4 linhas curtas, lÃª como uma frase em voz alta, tem um **nÃºmero**, cita o **assunto/ferramenta pelo nome** (nunca "sua IA"). `capa.destaque` = a palavra que fica amarela.
- **slides** (5 a 10): `numero`, `titulo` (atÃ© ~60 caracteres), `texto` (2â€“3 frases, atÃ© ~240 caracteres, `**negrito**` no trecho-chave), opcional `dados` (atÃ© 2 caixas `{valor, rotulo}`), `print` (caminho de print real da ferramenta), `fonte` (obrigatÃ³ria quando hÃ¡ nÃºmero).
- **NÃºmeros sÃ³ checados hoje**, com fonte. Sem nÃºmero inventado. Sem hype (ver `regras/texto.md` do ARCKHÉ-design).
- **fecho**: tÃ­tulo com pergunta + texto curto; a palavra aparece grande.
- **stories** (3): 1Âº chama para o post (mostra a capa sozinho), 2Âº pergunta algo ao pÃºblico, 3Âº repete a palavra.

Mostre ao usuÃ¡rio 3 opÃ§Ãµes de tÃ­tulo da capa e o roteiro em texto ANTES de gerar imagem.

### 4. Capa
- PadrÃ£o: arte pelo Codex com o tÃ­tulo desenhado dentro (`python3 scripts/capa.py <roteiro.json> --estilo foto|3d|ilustracao --cena "..."`).
- Checklist da capa (todas):
  - [ ] lÃª como tÃ­tulo de vÃ­deo, faz sentido em voz alta;
  - [ ] tem nÃºmero;
  - [ ] cita o assunto/ferramenta pelo nome;
  - [ ] no mÃ¡ximo 4 linhas, letra enorme no celular;
  - [ ] tapando o texto, a imagem sozinha ainda diz o assunto;
  - [ ] logo real do produto, se houver, visÃ­vel e nÃ£o coberto;
  - [ ] diferente das Ãºltimas capas (cena e estilo) â€” ver `PERFIL.md â€º Ãºltimas capas`;
  - [ ] **texto desenhado conferido letra por letra** â†’ `capa.texto_conferido: true`.
- Sem arte (pressa ou Codex fora): tirar `capa.imagem`; o render faz a capa tipogrÃ¡fica.

### 5. Render e checagem
```bash
node scripts/render.mjs <pasta>/roteiro.json <pasta>/slides
python3 scripts/checa.py <pasta>/slides <pasta>/roteiro.json
```
- ERRO = corrigir e renderizar de novo. AVISO = olhar e decidir.
- Olhe TODAS as imagens vocÃª mesmo (monte uma prancha com ffmpeg `tile`) antes de mostrar: texto cortado, nÃºmero Ã— rÃ³tulo trocados, erro de digitaÃ§Ã£o, nada copiado.

### 6. AprovaÃ§Ã£o
Mostre a prancha + a legenda (`<pasta>/legenda.txt`: 1Âª linha = gancho, 2â€“4 linhas, "Comenta PALAVRA", atÃ© 5 hashtags). Espere "aprovado"/"posta".
Toda correÃ§Ã£o que o usuÃ¡rio fizer: aplique E escreva como regra em `PERFIL.md â€º Regras aprendidas` (uma linha, com data).

### 7. Postar (sÃ³ com OK)
```bash
scripts/publicar.sh <pasta>/slides <pasta>/legenda.txt ["AAAA-MM-DD HH:MM"]   # rascunho
AO_VIVO=1 scripts/publicar.sh <pasta>/slides <pasta>/legenda.txt              # ao vivo
```
PadrÃ£o: Instagram + TikTok `ARCKHÉ.tds` pelo Metricool da conta linnoff88-dev (conector `metricool-linnoff88-dev`, sem chave de API). Outra conta: `REPO`, `CONECTOR` e `MARCA` (ver README).
Depois: anote a capa em `PERFIL.md â€º Ãºltimas capas` e registre o post em `<pasta>/publicado.txt`.

## NÃ£o fazer
- Postar sem OK. Apagar post no Metricool (sÃ³ com OK, um por um).
- Usar API paga (ElevenLabs, OpenAI, Blotatoâ€¦). Arte = Codex pela assinatura; reserva = flux2-klein local.
- Mais de 10 slides; mais de uma ideia por slide; print falso (mock-up).
