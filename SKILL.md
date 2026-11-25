---
name: carrossel-ARCKHê
description: Carrossel de Instagram e TikTok (imagens servem no Facebook) no padrêÂ£o ARCKHê ê¢â¬â escolhe o tema, escreve o roteiro (capa com nêÂºmero + 5ê¢â¬â10 slides de uma ideia cada + fecho "comenta PALAVRA" + 3 stories), gera a capa pelo Codex, renderiza 1080x1350 e 1080x1920, confere sozinho, mostra cada imagem a quem pediu e sêÂ³ posta no Metricool depois do OK. Gatilho: "carrossel", "faz um carrossel sobre X", "qual o prêÂ³ximo carrossel", "slides para o Instagram", "posta o carrossel".
---

# carrossel-ARCKHê

Leia `PERFIL.md` antes de tudo, toda vez. Escreva no idioma que ele indicar. Ele tem a marca, as contas, o tom e as **regras aprendidas** (cada correêÂ§êÂ£o do Nei vira uma linha lêÂ¡).

## Os 7 passos (sempre nesta ordem)

### 1. Tema
- Se o usuêÂ¡rio (no ARCKHê, o Nei) jêÂ¡ deu o tema, use. Se perguntou "qual o prêÂ³ximo?", proponha 3 temas com o porquêÂª de cada:
  - o que mais funcionou nos nossos posts (pergunte ou leia o relatêÂ³rio do muse-canais, se existir);
  - o que estêÂ¡ em alta hoje (radar-pautas, se existir);
  - perguntas que o pêÂºblico repete nos comentêÂ¡rios.
- Formatos que seguram o dedo: lista com nêÂºmero ("7 ferramentasê¢â¬Â¦", "5 errosê¢â¬Â¦"), passo a passo, antes êâ depois.
- Uma ideia por carrossel. Nunca copie texto, imagem ou personagem de outro perfil: sêÂ³ o formato.

### 2. Palavra e guia grêÂ¡tis
- Escolha UMA palavra para o comentêÂ¡rio (3 a 14 letras, sem espaêÂ§o): ex. `AGENTE`, `PROMPT`.
- O guia grêÂ¡tis êÂ© a pêÂ¡gina do ARCKHê AI sobre o assunto (curso, guia ou projeto que jêÂ¡ existe). Confira o link antes.
- Se nêÂ£o existir pêÂ¡gina, avise o usuêÂ¡rio antes de usar a palavra (no ARCKHê, o projeto lead-comenta cria a pêÂ¡gina).

### 3. Roteiro (`roteiro.json`)
Crie a pasta `~/projetos/output/carrossel-ARCKHê/<AAAA-MM-DD>-<slug>/` e escreva o `roteiro.json` no formato de `exemplos/teste/roteiro.json`:
- **capa.titulo**: 4 linhas curtas, lêÂª como uma frase em voz alta, tem um **nêÂºmero**, cita o **assunto/ferramenta pelo nome** (nunca "sua IA"). `capa.destaque` = a palavra que fica amarela.
- **slides** (5 a 10): `numero`, `titulo` (atêÂ© ~60 caracteres), `texto` (2ê¢â¬â3 frases, atêÂ© ~240 caracteres, `**negrito**` no trecho-chave), opcional `dados` (atêÂ© 2 caixas `{valor, rotulo}`), `print` (caminho de print real da ferramenta), `fonte` (obrigatêÂ³ria quando hêÂ¡ nêÂºmero).
- **NêÂºmeros sêÂ³ checados hoje**, com fonte. Sem nêÂºmero inventado. Sem hype (ver `regras/texto.md` do ARCKHê-design).
- **fecho**: têÂ­tulo com pergunta + texto curto; a palavra aparece grande.
- **stories** (3): 1êÂº chama para o post (mostra a capa sozinho), 2êÂº pergunta algo ao pêÂºblico, 3êÂº repete a palavra.

Mostre ao usuêÂ¡rio 3 opêÂ§êÂµes de têÂ­tulo da capa e o roteiro em texto ANTES de gerar imagem.

### 4. Capa
- PadrêÂ£o: arte pelo Codex com o têÂ­tulo desenhado dentro (`python3 scripts/capa.py <roteiro.json> --estilo foto|3d|ilustracao --cena "..."`).
- Checklist da capa (todas):
  - [ ] lêÂª como têÂ­tulo de vêÂ­deo, faz sentido em voz alta;
  - [ ] tem nêÂºmero;
  - [ ] cita o assunto/ferramenta pelo nome;
  - [ ] no mêÂ¡ximo 4 linhas, letra enorme no celular;
  - [ ] tapando o texto, a imagem sozinha ainda diz o assunto;
  - [ ] logo real do produto, se houver, visêÂ­vel e nêÂ£o coberto;
  - [ ] diferente das êÂºltimas capas (cena e estilo) ê¢â¬â ver `PERFIL.md ê¢â¬Âº êÂºltimas capas`;
  - [ ] **texto desenhado conferido letra por letra** ê¢â â `capa.texto_conferido: true`.
- Sem arte (pressa ou Codex fora): tirar `capa.imagem`; o render faz a capa tipogrêÂ¡fica.

### 5. Render e checagem
```bash
node scripts/render.mjs <pasta>/roteiro.json <pasta>/slides
python3 scripts/checa.py <pasta>/slides <pasta>/roteiro.json
```
- ERRO = corrigir e renderizar de novo. AVISO = olhar e decidir.
- Olhe TODAS as imagens vocêÂª mesmo (monte uma prancha com ffmpeg `tile`) antes de mostrar: texto cortado, nêÂºmero êâ rêÂ³tulo trocados, erro de digitaêÂ§êÂ£o, nada copiado.

### 6. AprovaêÂ§êÂ£o
Mostre a prancha + a legenda (`<pasta>/legenda.txt`: 1êÂª linha = gancho, 2ê¢â¬â4 linhas, "Comenta PALAVRA", atêÂ© 5 hashtags). Espere "aprovado"/"posta".
Toda correêÂ§êÂ£o que o usuêÂ¡rio fizer: aplique E escreva como regra em `PERFIL.md ê¢â¬Âº Regras aprendidas` (uma linha, com data).

### 7. Postar (sêÂ³ com OK)
```bash
scripts/publicar.sh <pasta>/slides <pasta>/legenda.txt ["AAAA-MM-DD HH:MM"]   # rascunho
AO_VIVO=1 scripts/publicar.sh <pasta>/slides <pasta>/legenda.txt              # ao vivo
```
PadrêÂ£o: Instagram + TikTok `ARCKHê.tds` pelo Metricool da conta linnoff88-dev (conector `metricool-linnoff88-dev`, sem chave de API). Outra conta: `REPO`, `CONECTOR` e `MARCA` (ver README).
Depois: anote a capa em `PERFIL.md ê¢â¬Âº êÂºltimas capas` e registre o post em `<pasta>/publicado.txt`.

## NêÂ£o fazer
- Postar sem OK. Apagar post no Metricool (sêÂ³ com OK, um por um).
- Usar API paga (ElevenLabs, OpenAI, Blotatoê¢â¬Â¦). Arte = Codex pela assinatura; reserva = flux2-klein local.
- Mais de 10 slides; mais de uma ideia por slide; print falso (mock-up).
