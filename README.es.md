# carrossel-ARCKHê

[![carrossel-ARCKHê](guia/assets/banner-es.jpg)](https://linnoff88-dev.github.io/

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## QuêÂ© es

carrossel-ARCKHê es una skill (un conjunto de instrucciones y scripts) para Claude Code que crea carruseles para Instagram y TikTok; las mismas imêÂ¡genes sirven para Facebook. Es para quienes quieren publicar con frecuencia sin abrir un programa de diseêÂ±o. TêÂº das el tema; entrega la portada, de 5 a 10 diapositivas con una idea cada una, la diapositiva final con êÂ«comenta PALABRAêÂ» y 3 stories, todo en el tamaêÂ±o correcto. Antes de mostrarlo, comprueba si algêÂºn texto quedêÂ³ cortado o demasiado pequeêÂ±o. Para usarlo, necesitas un ordenador Linux o Mac (en Windows, mediante WSL, el Linux que funciona dentro de Windows) con Node.js, Python y Claude Code; para la portada con ilustraciêÂ³n, Codex con la sesiêÂ³n iniciada en tu cuenta de ChatGPT. Los textos se generan en portuguêÂ©s de forma predeterminada; el idioma se cambia en PERFIL.md.

## ê°Å¸ââ GuêÂ­a de uso

GuêÂ­a completa (landing + paso a paso): **https://linnoff88-dev.github.io/

## QuêÂ© se genera

| Elemento | TamaêÂ±o | Para quêÂ© sirve |
|---|---|---|
| Portada | 1080êâ1350 | captar la atenciêÂ³n: nêÂºmero + tema identificado por su nombre + têÂ­tulo de hasta 4 lêÂ­neas |
| De 5 a 10 diapositivas | 1080êâ1350 | una idea por diapositiva, nêÂºmero grande, fragmento clave en negrita, dato con fuente |
| Cierre | 1080êâ1350 | êÂ«Comenta PALABRAêÂ» con la palabra destacada |
| 3 stories | 1080êâ1920 | dirigir a la publicaciêÂ³n, invitar a responder, repetir la palabra |
| `relatorio.json` | ê¢â¬â | quêÂ© se redujo, quêÂ© no cupo, imagen rota |

## Instalar (una vez)

Necesitas Linux o Mac con Node.js 18+, Python 3 (con Pillow: `python3 -m pip install pillow`) y Chromium (`npx playwright install chromium`; en Mac, basta con tener instalado Google Chrome). Para la portada con ilustraciêÂ³n: Codex CLI con la sesiêÂ³n iniciada en tu cuenta de ChatGPT (suscripciêÂ³n, sin clave de API).

```bash
git clone https://github.com/linnoff88-dev/carrossel-ARCKHê ~/projetos/carrossel-ARCKHê
cd ~/projetos/carrossel-ARCKHê
bash setup.sh                     # tem que terminar em SELFTEST PASS
mkdir -p ~/.claude/skills
ln -s "$PWD" ~/.claude/skills/carrossel-ARCKHê   # liga a skill no Claude Code
```

Si no tienes Chromium en el ordenador: `npx playwright install chromium` (o, en Mac, `export CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"`).

**Cambia la marca:** `PERFIL.md` viene con la marca de ARCKHê (@ARCKHê.tds, Nei Maldaner, hashtags). EdêÂ­talo antes del primer carrusel.

## Usar

En Claude Code: **êÂ«haz un carrusel sobre <tema>êÂ»** o **êÂ«êÂ¿cuêÂ¡l deberêÂ­a ser el prêÂ³ximo carrusel?êÂ»**. La skill sigue `SKILL.md` y lee `PERFIL.md` (marca, tono, reglas aprendidas).

A mano:

```bash
node scripts/render.mjs exemplos/teste/roteiro.json /tmp/teste   # gera as 11 imagens
python3 scripts/checa.py /tmp/teste exemplos/teste/roteiro.json  # confere
python3 scripts/capa.py meu/roteiro.json --estilo 3d --cena "..." # capa com arte do Codex
```

## El proceso, de principio a fin

ê°Å¸Â§Â  sesiêÂ³n con Nei êÂ· ê¢Å¡â¢ê¯Â¸Â script êÂ· ê°Å¸Â¤â Codex/`claude -p` (suscripciêÂ³n)

| # | Paso | Comando / quêÂ© sucede | QuiêÂ©n |
|---|---|---|---|
| 1 | Tema | Nei da el tema, o la skill propone 3 (lo que funcionêÂ³, lo que es tendencia, lo que la gente pregunta) | ê°Å¸Â§Â  |
| 2 | Palabra + guêÂ­a gratis | una palabra para el comentario y la pêÂ¡gina de ARCKHê AI a la que dirige | ê°Å¸Â§Â  |
| 3 | Guion | `roteiro.json` (portada, 5ê¢â¬â10 diapositivas, cierre, 3 stories); 3 opciones de portada para que Nei elija | ê°Å¸Â§Â  |
| 4 | Portada | `python3 scripts/capa.py <roteiro.json> --estilo ê¢â¬Â¦ --cena ê¢â¬Â¦` ê¢â â `capa.png` con el têÂ­tulo dibujado; revisar el texto | ê°Å¸Â¤â |
| 5 | Renderizado | `node scripts/render.mjs <roteiro.json> <pasta>/slides` | ê¢Å¡â¢ê¯Â¸Â |
| 6 | RevisiêÂ³n | `python3 scripts/checa.py <pasta>/slides` (0 errores) + revisar la lêÂ¡mina de vista general | ê¢Å¡â¢ê¯Â¸Â + ê°Å¸Â§Â  |
| 7 | AprobaciêÂ³n | Nei aprueba; cada correcciêÂ³n se convierte en una regla en `PERFIL.md` | ê°Å¸Â§Â  |
| 8 | Publicar | `scripts/publicar.sh <slides> <legenda.txt>` (borrador) êÂ· `AO_VIVO=1 ê¢â¬Â¦` (en vivo) ê¢â â Metricool linnoff88-dev (Instagram + TikTok; Facebook manualmente) | ê°Å¸Â¤â |

## Archivos

| Ruta | QuêÂ© es |
|---|---|
| `SKILL.md` | paso a paso que sigue Claude |
| `PERFIL.md` | marca, tono, hashtags, êÂºltimas portadas y reglas aprendidas |
| `scripts/render.mjs` | guion ê¢â â PNG (reduce la letra hasta el 30% si hace falta y lo anota) |
| `scripts/checa.py` | control: tamaêÂ±os, texto desbordado, letra pequeêÂ±a, palabra, exageraciones, nêÂºmero sin fuente |
| `scripts/capa.py` | portada mediante Codex image_gen (suscripciêÂ³n) |
| `scripts/publicar.sh` | programa en Metricool (borrador de forma predeterminada; aêÂºn no probado) |
| `templates/base.css` | aspecto visual (colores, fuentes, medidas) |
| `exemplos/teste/` | guion de ejemplo usado en la prueba automêÂ¡tica |

## LêÂ­mites

- **`publicar.sh` estêÂ¡ configurado para la cuenta de ARCKHê** (repo `linnoff88-dev/carrossel-ARCKHê`, conector `metricool-linnoff88-dev`, marca `ARCKHê.tds`). Para la tuya: crea el repositorio con `gh repo create carrossel-imagens --public --add-readme`, conecta Metricool con `claude mcp add --transport http --scope user metricool https://ai.metricool.com/mcp` (y `/mcp` para iniciar sesiêÂ³n) y ejecuta `export REPO=tu/carrossel-imagens CONECTOR=metricool MARCA=<marca>` antes de ejecutarlo (sirve tanto para el borrador como para `AO_VIVO=1`); necesitas haber iniciado sesiêÂ³n en `gh` y tener Metricool conectado a Claude Code (MCP).
- **`publicar.sh` solo funciona en Linux o WSL** (usa el `date` de Linux); en Mac, publica las imêÂ¡genes manualmente.
- **`publicar.sh` aêÂºn no se ha probado.** No se ha comprobado en Metricool el formato de carrusel con varias imêÂ¡genes ni el de story; el primer uso debe ser como borrador, con Nei revisando el planificador.
- Las stories mediante Metricool requieren que la cuenta de Instagram sea profesional.
- Fuentes Sora e Inter: licencia SIL Open Font License, incluidas en `assets/fonts/`.

Licencia del cêÂ³digo: MIT.