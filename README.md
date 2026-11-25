# carrossel-ARCKHê

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![carrossel-ARCKHê](guia/assets/banner.jpg)](https://linnoff88-dev.github.io/

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## O que êÂ©

O carrossel-ARCKHê êÂ© uma skill (um conjunto de instruêÂ§êÂµes e scripts) para o Claude Code que faz carrossêÂ©is de Instagram e TikTok; as mesmas imagens servem para o Facebook. Serve para quem quer postar com frequêÂªncia sem abrir programa de design. VocêÂª dêÂ¡ o tema; ele entrega a capa, de 5 a 10 slides com uma ideia cada, o slide final com "comenta PALAVRA" e 3 stories, todos no tamanho certo. Antes de mostrar, ele confere se algum texto ficou cortado ou pequeno demais. Para usar, precisa de um computador Linux ou Mac (no Windows, pelo WSL, o Linux que roda dentro do Windows) com Node.js, Python e o Claude Code; para a capa com arte, o Codex logado na sua conta do ChatGPT. Os textos saem em portuguêÂªs por padrêÂ£o; o idioma se troca no PERFIL.md.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/

## O que sai

| PeêÂ§a | Tamanho | Para quêÂª |
|---|---|---|
| Capa | 1080êâ1350 | segurar o dedo: nêÂºmero + assunto pelo nome + têÂ­tulo em atêÂ© 4 linhas |
| 5 a 10 slides | 1080êâ1350 | uma ideia por slide, nêÂºmero grande, trecho-chave em negrito, dado com fonte |
| Fecho | 1080êâ1350 | "Comenta PALAVRA" com a palavra em destaque |
| 3 stories | 1080êâ1920 | levar ao post, puxar resposta, repetir a palavra |
| `relatorio.json` | ê¢â¬â | o que encolheu, o que nêÂ£o coube, imagem quebrada |

## Instalar (uma vez)

Precisa de Linux ou Mac com Node.js 18+, Python 3 (com Pillow: `python3 -m pip install pillow`) e um Chromium (`npx playwright install chromium`; no Mac, o Google Chrome instalado jêÂ¡ serve). Para a capa com arte: Codex CLI logado na sua conta ChatGPT (assinatura, sem chave de API).

```bash
git clone https://github.com/linnoff88-dev/carrossel-ARCKHê ~/projetos/carrossel-ARCKHê
cd ~/projetos/carrossel-ARCKHê
bash setup.sh                     # tem que terminar em SELFTEST PASS
mkdir -p ~/.claude/skills
ln -s "$PWD" ~/.claude/skills/carrossel-ARCKHê   # liga a skill no Claude Code
```

Sem Chromium na mêÂ¡quina: `npx playwright install chromium` (ou, no Mac, `export CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"`).

**Troque a marca:** o `PERFIL.md` vem com a marca do ARCKHê (@ARCKHê.tds, Nei Maldaner, hashtags). Edite antes do primeiro carrossel.

## Usar

No Claude Code: **"faz um carrossel sobre <tema>"** ou **"qual deve ser o prêÂ³ximo carrossel?"**. A skill segue `SKILL.md` e lêÂª `PERFIL.md` (marca, tom, regras aprendidas).

êâ¬ mêÂ£o:

```bash
node scripts/render.mjs exemplos/teste/roteiro.json /tmp/teste   # gera as 11 imagens
python3 scripts/checa.py /tmp/teste exemplos/teste/roteiro.json  # confere
python3 scripts/capa.py meu/roteiro.json --estilo 3d --cena "..." # capa com arte do Codex
```

## O processo, do inêÂ­cio ao fim

ê°Å¸Â§Â  sessêÂ£o com o Nei êÂ· ê¢Å¡â¢ê¯Â¸Â script êÂ· ê°Å¸Â¤â Codex/`claude -p` (assinatura)

| # | Passo | Comando / o que acontece | Quem |
|---|---|---|---|
| 1 | Tema | Nei dêÂ¡ o tema, ou a skill propêÂµe 3 (o que funcionou, o que estêÂ¡ em alta, o que perguntam) | ê°Å¸Â§Â  |
| 2 | Palavra + guia grêÂ¡tis | uma palavra para o comentêÂ¡rio e a pêÂ¡gina do ARCKHê AI que ela entrega | ê°Å¸Â§Â  |
| 3 | Roteiro | `roteiro.json` (capa, 5ê¢â¬â10 slides, fecho, 3 stories); 3 opêÂ§êÂµes de capa para o Nei escolher | ê°Å¸Â§Â  |
| 4 | Capa | `python3 scripts/capa.py <roteiro.json> --estilo ê¢â¬Â¦ --cena ê¢â¬Â¦` ê¢â â `capa.png` com o têÂ­tulo desenhado; conferir o texto | ê°Å¸Â¤â |
| 5 | Render | `node scripts/render.mjs <roteiro.json> <pasta>/slides` | ê¢Å¡â¢ê¯Â¸Â |
| 6 | Checagem | `python3 scripts/checa.py <pasta>/slides` (0 erro) + olhar a prancha | ê¢Å¡â¢ê¯Â¸Â + ê°Å¸Â§Â  |
| 7 | AprovaêÂ§êÂ£o | Nei aprova; cada correêÂ§êÂ£o vira regra no `PERFIL.md` | ê°Å¸Â§Â  |
| 8 | Postar | `scripts/publicar.sh <slides> <legenda.txt>` (rascunho) êÂ· `AO_VIVO=1 ê¢â¬Â¦` (ao vivo) ê¢â â Metricool linnoff88-dev (Instagram + TikTok; Facebook êÂ  mêÂ£o) | ê°Å¸Â¤â |

## Arquivos

| Caminho | O que êÂ© |
|---|---|
| `SKILL.md` | passo a passo que o Claude segue |
| `PERFIL.md` | marca, tom, hashtags, êÂºltimas capas e regras aprendidas |
| `scripts/render.mjs` | roteiro ê¢â â PNGs (encolhe a letra atêÂ© 30% se precisar e anota) |
| `scripts/checa.py` | portêÂ£o: tamanhos, texto estourado, letra pequena, palavra, hype, nêÂºmero sem fonte |
| `scripts/capa.py` | capa pelo Codex image_gen (assinatura) |
| `scripts/publicar.sh` | agenda no Metricool (rascunho por padrêÂ£o; ainda nêÂ£o testado) |
| `templates/base.css` | visual (cores, fontes, medidas) |
| `exemplos/teste/` | roteiro de exemplo usado no autoteste |

## Limites

- **`publicar.sh` vem configurado para a conta do ARCKHê** (repo `linnoff88-dev/carrossel-ARCKHê`, conector `metricool-linnoff88-dev`, marca `ARCKHê.tds`). Para a sua: crie o repositêÂ³rio com `gh repo create carrossel-imagens --public --add-readme`, ligue o Metricool com `claude mcp add --transport http --scope user metricool https://ai.metricool.com/mcp` (e `/mcp` para entrar) e rode `export REPO=voce/carrossel-imagens CONECTOR=metricool MARCA=<marca>` antes de rodar (vale para o rascunho e para o `AO_VIVO=1`); precisa do `gh` logado e do Metricool ligado ao Claude Code (MCP).
- **`publicar.sh` sêÂ³ roda no Linux ou no WSL** (usa o `date` do Linux); no Mac, poste as imagens êÂ  mêÂ£o.
- **`publicar.sh` ainda nêÂ£o foi testado.** O formato de carrossel com vêÂ¡rias imagens e de story no Metricool nêÂ£o foi conferido; o primeiro uso deve ser como rascunho, com o Nei olhando o planner.
- Stories pelo Metricool dependem da conta Instagram ser profissional.
- Fontes Sora e Inter: licenêÂ§a SIL Open Font License, incluêÂ­das em `assets/fonts/`.

LicenêÂ§a do cêÂ³digo: MIT.

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>