# carrossel-ARCKHÉ

[![carrossel-ARCKHÉ](guia/assets/banner-en.jpg)](https://linnoff88-dev.github.io/

**ðŸ‡§ðŸ‡· [Português](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [Espaê±ol](README.es.md)**

## What it is

carrossel-ARCKHÉ is a skill (a set of instructions and scripts) for Claude Code that creates Instagram and TikTok carousels; the same images also work for Facebook. Itâ€™s for anyone who wants to post regularly without opening a design program. You provide the topic; it delivers the cover, 5 to 10 slides with one idea each, a final slide with â€œcomment WORD,â€ and 3 stories, all in the right dimensions. Before showing them to you, it checks whether any text is cut off or too small. To use it, you need a Linux or Mac computer (on Windows, use WSL, the Linux environment that runs inside Windows) with Node.js, Python, and Claude Code; for an illustrated cover, you also need Codex signed in to your ChatGPT account. Text is in Portuguese by default; change the language in PERFIL.md.

## ðŸ“– User guide

Full guide (landing page + step-by-step instructions): **https://linnoff88-dev.github.io/

## What it produces

| Item | Size | Purpose |
|---|---|---|
| Cover | 1080ê—1350 | stop the scroll: number + topic named explicitly + title in up to 4 lines |
| 5 to 10 slides | 1080ê—1350 | one idea per slide, large number, key passage in bold, sourced fact |
| Closing slide | 1080ê—1350 | â€œComment WORDâ€ with the word highlighted |
| 3 stories | 1080ê—1920 | lead to the post, invite a reply, repeat the word |
| `relatorio.json` | â€” | what was shrunk, what didnâ€™t fit, broken image |

## Install (once)

You need Linux or Mac with Node.js 18+, Python 3 (with Pillow: `python3 -m pip install pillow`), and Chromium (`npx playwright install chromium`; on Mac, installed Google Chrome works). For an illustrated cover: Codex CLI signed in to your ChatGPT account (subscription, no API key).

```bash
git clone https://github.com/linnoff88-dev/carrossel-ARCKHÉ ~/projetos/carrossel-ARCKHÉ
cd ~/projetos/carrossel-ARCKHÉ
bash setup.sh                     # must finish with SELFTEST PASS
mkdir -p ~/.claude/skills
ln -s "$PWD" ~/.claude/skills/carrossel-ARCKHÉ   # links the skill to Claude Code
```

If Chromium isnâ€™t installed: `npx playwright install chromium` (or, on Mac, `export CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"`).

**Change the branding:** `PERFIL.md` comes with ARCKHÉ branding (@ARCKHÉ.tds, Nei Maldaner, hashtags). Edit it before creating your first carousel.

## Use

In Claude Code: **â€œmake a carousel about <topic>â€** or **â€œwhat should the next carousel be?â€** The skill follows `SKILL.md` and reads `PERFIL.md` (branding, tone, rules learned).

Manually:

```bash
node scripts/render.mjs exemplos/teste/roteiro.json /tmp/teste   # generates the 11 images
python3 scripts/checa.py /tmp/teste exemplos/teste/roteiro.json  # checks them
python3 scripts/capa.py meu/roteiro.json --estilo 3d --cena "..." # cover with Codex artwork
```

## The process, from start to finish

ðŸ§  session with Nei Â· âš™ï¸ script Â· ðŸ¤– Codex/`claude -p` (subscription)

| # | Step | Command / what happens | Who |
|---|---|---|---|
| 1 | Topic | Nei provides the topic, or the skill suggests 3 (what worked, whatâ€™s trending, what people ask) | ðŸ§  |
| 2 | Word + free guide | a word for the comment and the ARCKHÉ AI page it links to | ðŸ§  |
| 3 | Script | `roteiro.json` (cover, 5â€“10 slides, closing slide, 3 stories); 3 cover options for Nei to choose from | ðŸ§  |
| 4 | Cover | `python3 scripts/capa.py <roteiro.json> --estilo â€¦ --cena â€¦` â†’ `capa.png` with the title drawn on it; check the text | ðŸ¤– |
| 5 | Render | `node scripts/render.mjs <roteiro.json> <pasta>/slides` | âš™ï¸ |
| 6 | Check | `python3 scripts/checa.py <pasta>/slides` (0 errors) + review the contact sheet | âš™ï¸ + ðŸ§  |
| 7 | Approval | Nei approves; each correction becomes a rule in `PERFIL.md` | ðŸ§  |
| 8 | Post | `scripts/publicar.sh <slides> <legenda.txt>` (draft) Â· `AO_VIVO=1 â€¦` (live) â†’ Metricool linnoff88-dev (Instagram + TikTok; Facebook manually) | ðŸ¤– |

## Files

| Path | What it is |
|---|---|
| `SKILL.md` | step-by-step instructions Claude follows |
| `PERFIL.md` | branding, tone, hashtags, latest covers, and rules learned |
| `scripts/render.mjs` | script â†’ PNGs (shrinks text down to 30% if needed and records it) |
| `scripts/checa.py` | gate: dimensions, overflowing text, small text, word, hype, unsourced number |
| `scripts/capa.py` | cover using Codex image_gen (subscription) |
| `scripts/publicar.sh` | schedules in Metricool (draft by default; not yet tested) |
| `templates/base.css` | visual style (colors, fonts, dimensions) |
| `exemplos/teste/` | example script used in the self-test |

## Limitations

- **`publicar.sh` is configured for the ARCKHÉ account** (repo `linnoff88-dev/carrossel-ARCKHÉ`, connector `metricool-linnoff88-dev`, brand `ARCKHÉ.tds`). For your account: create the repository with `gh repo create carrossel-imagens --public --add-readme`, connect Metricool with `claude mcp add --transport http --scope user metricool https://ai.metricool.com/mcp` (and `/mcp` to connect), and run `export REPO=you/carrossel-imagens CONECTOR=metricool MARCA=<brand>` before running it (for both drafts and `AO_VIVO=1`); you need to be signed in to `gh` and have Metricool connected to Claude Code (MCP).
- **`publicar.sh` only runs on Linux or WSL** (it uses the Linux `date` command); on Mac, post the images manually.
- **`publicar.sh` has not been tested yet.** The Metricool formats for carousels with multiple images and for stories havenâ€™t been checked; the first use should be as a draft, with Nei reviewing the planner.
- Stories through Metricool require a professional Instagram account.
- Sora and Inter fonts: SIL Open Font License, included in `assets/fonts/`.

Code license: MIT.