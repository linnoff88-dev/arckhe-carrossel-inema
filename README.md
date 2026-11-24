# carrossel-ARCKHÉ

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![carrossel-ARCKHÉ](guia/assets/banner.jpg)](https://linnoff88-dev.github.io/

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

O carrossel-ARCKHÉ Ã© uma skill (um conjunto de instruÃ§Ãµes e scripts) para o Claude Code que faz carrossÃ©is de Instagram e TikTok; as mesmas imagens servem para o Facebook. Serve para quem quer postar com frequÃªncia sem abrir programa de design. VocÃª dÃ¡ o tema; ele entrega a capa, de 5 a 10 slides com uma ideia cada, o slide final com "comenta PALAVRA" e 3 stories, todos no tamanho certo. Antes de mostrar, ele confere se algum texto ficou cortado ou pequeno demais. Para usar, precisa de um computador Linux ou Mac (no Windows, pelo WSL, o Linux que roda dentro do Windows) com Node.js, Python e o Claude Code; para a capa com arte, o Codex logado na sua conta do ChatGPT. Os textos saem em portuguÃªs por padrÃ£o; o idioma se troca no PERFIL.md.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/

## O que sai

| PeÃ§a | Tamanho | Para quÃª |
|---|---|---|
| Capa | 1080Ã—1350 | segurar o dedo: nÃºmero + assunto pelo nome + tÃ­tulo em atÃ© 4 linhas |
| 5 a 10 slides | 1080Ã—1350 | uma ideia por slide, nÃºmero grande, trecho-chave em negrito, dado com fonte |
| Fecho | 1080Ã—1350 | "Comenta PALAVRA" com a palavra em destaque |
| 3 stories | 1080Ã—1920 | levar ao post, puxar resposta, repetir a palavra |
| `relatorio.json` | â€” | o que encolheu, o que nÃ£o coube, imagem quebrada |

## Instalar (uma vez)

Precisa de Linux ou Mac com Node.js 18+, Python 3 (com Pillow: `python3 -m pip install pillow`) e um Chromium (`npx playwright install chromium`; no Mac, o Google Chrome instalado jÃ¡ serve). Para a capa com arte: Codex CLI logado na sua conta ChatGPT (assinatura, sem chave de API).

```bash
git clone https://github.com/linnoff88-dev/carrossel-ARCKHÉ ~/projetos/carrossel-ARCKHÉ
cd ~/projetos/carrossel-ARCKHÉ
bash setup.sh                     # tem que terminar em SELFTEST PASS
mkdir -p ~/.claude/skills
ln -s "$PWD" ~/.claude/skills/carrossel-ARCKHÉ   # liga a skill no Claude Code
```

Sem Chromium na mÃ¡quina: `npx playwright install chromium` (ou, no Mac, `export CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"`).

**Troque a marca:** o `PERFIL.md` vem com a marca do ARCKHÉ (@ARCKHÉ.tds, Nei Maldaner, hashtags). Edite antes do primeiro carrossel.

## Usar

No Claude Code: **"faz um carrossel sobre <tema>"** ou **"qual deve ser o prÃ³ximo carrossel?"**. A skill segue `SKILL.md` e lÃª `PERFIL.md` (marca, tom, regras aprendidas).

Ã€ mÃ£o:

```bash
node scripts/render.mjs exemplos/teste/roteiro.json /tmp/teste   # gera as 11 imagens
python3 scripts/checa.py /tmp/teste exemplos/teste/roteiro.json  # confere
python3 scripts/capa.py meu/roteiro.json --estilo 3d --cena "..." # capa com arte do Codex
```

## O processo, do inÃ­cio ao fim

ðŸ§  sessÃ£o com o Nei Â· âš™ï¸ script Â· ðŸ¤– Codex/`claude -p` (assinatura)

| # | Passo | Comando / o que acontece | Quem |
|---|---|---|---|
| 1 | Tema | Nei dÃ¡ o tema, ou a skill propÃµe 3 (o que funcionou, o que estÃ¡ em alta, o que perguntam) | ðŸ§  |
| 2 | Palavra + guia grÃ¡tis | uma palavra para o comentÃ¡rio e a pÃ¡gina do ARCKHÉ AI que ela entrega | ðŸ§  |
| 3 | Roteiro | `roteiro.json` (capa, 5â€“10 slides, fecho, 3 stories); 3 opÃ§Ãµes de capa para o Nei escolher | ðŸ§  |
| 4 | Capa | `python3 scripts/capa.py <roteiro.json> --estilo â€¦ --cena â€¦` â†’ `capa.png` com o tÃ­tulo desenhado; conferir o texto | ðŸ¤– |
| 5 | Render | `node scripts/render.mjs <roteiro.json> <pasta>/slides` | âš™ï¸ |
| 6 | Checagem | `python3 scripts/checa.py <pasta>/slides` (0 erro) + olhar a prancha | âš™ï¸ + ðŸ§  |
| 7 | AprovaÃ§Ã£o | Nei aprova; cada correÃ§Ã£o vira regra no `PERFIL.md` | ðŸ§  |
| 8 | Postar | `scripts/publicar.sh <slides> <legenda.txt>` (rascunho) Â· `AO_VIVO=1 â€¦` (ao vivo) â†’ Metricool linnoff88-dev (Instagram + TikTok; Facebook Ã  mÃ£o) | ðŸ¤– |

## Arquivos

| Caminho | O que Ã© |
|---|---|
| `SKILL.md` | passo a passo que o Claude segue |
| `PERFIL.md` | marca, tom, hashtags, Ãºltimas capas e regras aprendidas |
| `scripts/render.mjs` | roteiro â†’ PNGs (encolhe a letra atÃ© 30% se precisar e anota) |
| `scripts/checa.py` | portÃ£o: tamanhos, texto estourado, letra pequena, palavra, hype, nÃºmero sem fonte |
| `scripts/capa.py` | capa pelo Codex image_gen (assinatura) |
| `scripts/publicar.sh` | agenda no Metricool (rascunho por padrÃ£o; ainda nÃ£o testado) |
| `templates/base.css` | visual (cores, fontes, medidas) |
| `exemplos/teste/` | roteiro de exemplo usado no autoteste |

## Limites

- **`publicar.sh` vem configurado para a conta do ARCKHÉ** (repo `linnoff88-dev/carrossel-ARCKHÉ`, conector `metricool-linnoff88-dev`, marca `ARCKHÉ.tds`). Para a sua: crie o repositÃ³rio com `gh repo create carrossel-imagens --public --add-readme`, ligue o Metricool com `claude mcp add --transport http --scope user metricool https://ai.metricool.com/mcp` (e `/mcp` para entrar) e rode `export REPO=voce/carrossel-imagens CONECTOR=metricool MARCA=<marca>` antes de rodar (vale para o rascunho e para o `AO_VIVO=1`); precisa do `gh` logado e do Metricool ligado ao Claude Code (MCP).
- **`publicar.sh` sÃ³ roda no Linux ou no WSL** (usa o `date` do Linux); no Mac, poste as imagens Ã  mÃ£o.
- **`publicar.sh` ainda nÃ£o foi testado.** O formato de carrossel com vÃ¡rias imagens e de story no Metricool nÃ£o foi conferido; o primeiro uso deve ser como rascunho, com o Nei olhando o planner.
- Stories pelo Metricool dependem da conta Instagram ser profissional.
- Fontes Sora e Inter: licenÃ§a SIL Open Font License, incluÃ­das em `assets/fonts/`.

LicenÃ§a do cÃ³digo: MIT.

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>