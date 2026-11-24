# Changelog

## 1.0.0 â€” 01/11/2026
- Guia PT/EN/ES em guia/ (GitHub Pages), READMEs EN/ES, capa do catÃ¡logo.
- `publicar.sh` aceita REPO, CONECTOR e MARCA (conta prÃ³pria). Render acha o Chrome do Mac; setup sugere `npx playwright install chromium`.
- PERFIL.md com idioma dos textos.
- Render HTML â†’ PNG (capa, 5â€“10 slides, fecho, 3 stories) com Chromium sem janela; fontes Sora e Inter embutidas.
- Encolhe a letra atÃ© 30% quando o texto nÃ£o cabe e anota no `relatorio.json`.
- `checa.py`: tamanhos, texto estourado, letra < 24 px, imagem quebrada, palavra do comentÃ¡rio, hype, nÃºmero sem fonte, capa sem nÃºmero.
- `capa.py`: capa com tÃ­tulo desenhado pelo Codex image_gen (assinatura).
- `publicar.sh`: carrossel + stories no Metricool linnoff88-dev; rascunho por padrÃ£o. **Ainda nÃ£o testado.**
- `checa.py` mede o amarelado da capa ((R+G)/2âˆ’B): aviso acima de 18, erro acima de 25. Estilos da capa com luz neutra.
- Autoteste `setup.sh` â†’ `SELFTEST PASS`.
