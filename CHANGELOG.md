ï»¿# Changelog

## 1.0.0 ê¢â¬â 01/11/2026
- Guia PT/EN/ES em guia/ (GitHub Pages), READMEs EN/ES, capa do catêÂ¡logo.
- `publicar.sh` aceita REPO, CONECTOR e MARCA (conta prêÂ³pria). Render acha o Chrome do Mac; setup sugere `npx playwright install chromium`.
- PERFIL.md com idioma dos textos.
- Render HTML ê¢â â PNG (capa, 5ê¢â¬â10 slides, fecho, 3 stories) com Chromium sem janela; fontes Sora e Inter embutidas.
- Encolhe a letra atêÂ© 30% quando o texto nêÂ£o cabe e anota no `relatorio.json`.
- `checa.py`: tamanhos, texto estourado, letra < 24 px, imagem quebrada, palavra do comentêÂ¡rio, hype, nêÂºmero sem fonte, capa sem nêÂºmero.
- `capa.py`: capa com têÂ­tulo desenhado pelo Codex image_gen (assinatura).
- `publicar.sh`: carrossel + stories no Metricool linnoff88-dev; rascunho por padrêÂ£o. **Ainda nêÂ£o testado.**
- `checa.py` mede o amarelado da capa ((R+G)/2ê¢ËâB): aviso acima de 18, erro acima de 25. Estilos da capa com luz neutra.
- Autoteste `setup.sh` ê¢â â `SELFTEST PASS`.
