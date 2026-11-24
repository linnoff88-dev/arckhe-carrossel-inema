# carrossel-ARCKHÉ

[![carrossel-ARCKHÉ](guia/assets/banner-es.jpg)](https://linnoff88-dev.github.io/

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## QuÃ© es

carrossel-ARCKHÉ es una skill (un conjunto de instrucciones y scripts) para Claude Code que crea carruseles para Instagram y TikTok; las mismas imÃ¡genes sirven para Facebook. Es para quienes quieren publicar con frecuencia sin abrir un programa de diseÃ±o. TÃº das el tema; entrega la portada, de 5 a 10 diapositivas con una idea cada una, la diapositiva final con Â«comenta PALABRAÂ» y 3 stories, todo en el tamaÃ±o correcto. Antes de mostrarlo, comprueba si algÃºn texto quedÃ³ cortado o demasiado pequeÃ±o. Para usarlo, necesitas un ordenador Linux o Mac (en Windows, mediante WSL, el Linux que funciona dentro de Windows) con Node.js, Python y Claude Code; para la portada con ilustraciÃ³n, Codex con la sesiÃ³n iniciada en tu cuenta de ChatGPT. Los textos se generan en portuguÃ©s de forma predeterminada; el idioma se cambia en PERFIL.md.

## ðŸ“– GuÃ­a de uso

GuÃ­a completa (landing + paso a paso): **https://linnoff88-dev.github.io/

## QuÃ© se genera

| Elemento | TamaÃ±o | Para quÃ© sirve |
|---|---|---|
| Portada | 1080Ã—1350 | captar la atenciÃ³n: nÃºmero + tema identificado por su nombre + tÃ­tulo de hasta 4 lÃ­neas |
| De 5 a 10 diapositivas | 1080Ã—1350 | una idea por diapositiva, nÃºmero grande, fragmento clave en negrita, dato con fuente |
| Cierre | 1080Ã—1350 | Â«Comenta PALABRAÂ» con la palabra destacada |
| 3 stories | 1080Ã—1920 | dirigir a la publicaciÃ³n, invitar a responder, repetir la palabra |
| `relatorio.json` | â€” | quÃ© se redujo, quÃ© no cupo, imagen rota |

## Instalar (una vez)

Necesitas Linux o Mac con Node.js 18+, Python 3 (con Pillow: `python3 -m pip install pillow`) y Chromium (`npx playwright install chromium`; en Mac, basta con tener instalado Google Chrome). Para la portada con ilustraciÃ³n: Codex CLI con la sesiÃ³n iniciada en tu cuenta de ChatGPT (suscripciÃ³n, sin clave de API).

```bash
git clone https://github.com/linnoff88-dev/carrossel-ARCKHÉ ~/projetos/carrossel-ARCKHÉ
cd ~/projetos/carrossel-ARCKHÉ
bash setup.sh                     # tem que terminar em SELFTEST PASS
mkdir -p ~/.claude/skills
ln -s "$PWD" ~/.claude/skills/carrossel-ARCKHÉ   # liga a skill no Claude Code
```

Si no tienes Chromium en el ordenador: `npx playwright install chromium` (o, en Mac, `export CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"`).

**Cambia la marca:** `PERFIL.md` viene con la marca de ARCKHÉ (@ARCKHÉ.tds, Nei Maldaner, hashtags). EdÃ­talo antes del primer carrusel.

## Usar

En Claude Code: **Â«haz un carrusel sobre <tema>Â»** o **Â«Â¿cuÃ¡l deberÃ­a ser el prÃ³ximo carrusel?Â»**. La skill sigue `SKILL.md` y lee `PERFIL.md` (marca, tono, reglas aprendidas).

A mano:

```bash
node scripts/render.mjs exemplos/teste/roteiro.json /tmp/teste   # gera as 11 imagens
python3 scripts/checa.py /tmp/teste exemplos/teste/roteiro.json  # confere
python3 scripts/capa.py meu/roteiro.json --estilo 3d --cena "..." # capa com arte do Codex
```

## El proceso, de principio a fin

ðŸ§  sesiÃ³n con Nei Â· âš™ï¸ script Â· ðŸ¤– Codex/`claude -p` (suscripciÃ³n)

| # | Paso | Comando / quÃ© sucede | QuiÃ©n |
|---|---|---|---|
| 1 | Tema | Nei da el tema, o la skill propone 3 (lo que funcionÃ³, lo que es tendencia, lo que la gente pregunta) | ðŸ§  |
| 2 | Palabra + guÃ­a gratis | una palabra para el comentario y la pÃ¡gina de ARCKHÉ AI a la que dirige | ðŸ§  |
| 3 | Guion | `roteiro.json` (portada, 5â€“10 diapositivas, cierre, 3 stories); 3 opciones de portada para que Nei elija | ðŸ§  |
| 4 | Portada | `python3 scripts/capa.py <roteiro.json> --estilo â€¦ --cena â€¦` â†’ `capa.png` con el tÃ­tulo dibujado; revisar el texto | ðŸ¤– |
| 5 | Renderizado | `node scripts/render.mjs <roteiro.json> <pasta>/slides` | âš™ï¸ |
| 6 | RevisiÃ³n | `python3 scripts/checa.py <pasta>/slides` (0 errores) + revisar la lÃ¡mina de vista general | âš™ï¸ + ðŸ§  |
| 7 | AprobaciÃ³n | Nei aprueba; cada correcciÃ³n se convierte en una regla en `PERFIL.md` | ðŸ§  |
| 8 | Publicar | `scripts/publicar.sh <slides> <legenda.txt>` (borrador) Â· `AO_VIVO=1 â€¦` (en vivo) â†’ Metricool linnoff88-dev (Instagram + TikTok; Facebook manualmente) | ðŸ¤– |

## Archivos

| Ruta | QuÃ© es |
|---|---|
| `SKILL.md` | paso a paso que sigue Claude |
| `PERFIL.md` | marca, tono, hashtags, Ãºltimas portadas y reglas aprendidas |
| `scripts/render.mjs` | guion â†’ PNG (reduce la letra hasta el 30% si hace falta y lo anota) |
| `scripts/checa.py` | control: tamaÃ±os, texto desbordado, letra pequeÃ±a, palabra, exageraciones, nÃºmero sin fuente |
| `scripts/capa.py` | portada mediante Codex image_gen (suscripciÃ³n) |
| `scripts/publicar.sh` | programa en Metricool (borrador de forma predeterminada; aÃºn no probado) |
| `templates/base.css` | aspecto visual (colores, fuentes, medidas) |
| `exemplos/teste/` | guion de ejemplo usado en la prueba automÃ¡tica |

## LÃ­mites

- **`publicar.sh` estÃ¡ configurado para la cuenta de ARCKHÉ** (repo `linnoff88-dev/carrossel-ARCKHÉ`, conector `metricool-linnoff88-dev`, marca `ARCKHÉ.tds`). Para la tuya: crea el repositorio con `gh repo create carrossel-imagens --public --add-readme`, conecta Metricool con `claude mcp add --transport http --scope user metricool https://ai.metricool.com/mcp` (y `/mcp` para iniciar sesiÃ³n) y ejecuta `export REPO=tu/carrossel-imagens CONECTOR=metricool MARCA=<marca>` antes de ejecutarlo (sirve tanto para el borrador como para `AO_VIVO=1`); necesitas haber iniciado sesiÃ³n en `gh` y tener Metricool conectado a Claude Code (MCP).
- **`publicar.sh` solo funciona en Linux o WSL** (usa el `date` de Linux); en Mac, publica las imÃ¡genes manualmente.
- **`publicar.sh` aÃºn no se ha probado.** No se ha comprobado en Metricool el formato de carrusel con varias imÃ¡genes ni el de story; el primer uso debe ser como borrador, con Nei revisando el planificador.
- Las stories mediante Metricool requieren que la cuenta de Instagram sea profesional.
- Fuentes Sora e Inter: licencia SIL Open Font License, incluidas en `assets/fonts/`.

Licencia del cÃ³digo: MIT.