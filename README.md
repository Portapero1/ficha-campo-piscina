# Ficha de campo — Piscina recreacional, Sauna Spa Apolo

Aplicación de una sola página para el levantamiento hidráulico-sanitario en campo.
Guía el llenado paso a paso, calcula los parámetros de diseño en el sitio, los
contrasta contra la norma peruana y exporta todo a Excel.

Forma parte de la tesis *"Rediseño hidráulico-sanitario de piscina recreacional en
Cerro Colorado mediante el desarrollo de software para cumplir normativa peruana
de uso colectivo"* (UNSA, Escuela Profesional de Ingeniería Sanitaria).

## Qué hace

- **12 secciones guiadas** que siguen el recorrido físico del agua, de la piscina
  al retorno. Cada campo explica en lenguaje llano cómo tomar la medida, para que
  pueda llenarlo alguien sin formación en hidráulica.
- **Verificación normativa automática** contra el DS 007-2003-SA y la Directiva
  Sanitaria 033-MINSA/DIGESA V.02. Cada resultado indica valor obtenido, exigencia,
  artículo aplicable y veredicto: cumple, no cumple, revisar o falta dato.
- **Calculadoras auxiliares:** caudal por volumen y tiempo (balde y cronómetro),
  y diámetro del filtro a partir del perímetro.
- **Exportación a Excel** (.xlsx) con dos hojas: datos de campo y verificación
  normativa. También CSV y respaldo JSON.
- **Autoguardado** en el navegador y **funcionamiento sin señal.**

## Cómo publicarlo en GitHub Pages

```bash
git init
git add .
git commit -m "Ficha de campo para levantamiento hidráulico-sanitario"
git branch -M main
git remote add origin https://github.com/USUARIO/REPOSITORIO.git
git push -u origin main
```

Luego, en el repositorio: **Settings → Pages → Source: Deploy from a branch →
Branch: main / (root) → Save**. En un par de minutos queda en
`https://USUARIO.github.io/REPOSITORIO/`.

## Uso en campo

1. **Antes de salir, con internet:** abre la página en el teléfono. Se guarda sola
   para funcionar sin cobertura. En Android, *Menú → Agregar a pantalla de inicio*
   la deja como un ícono más.
2. **En la instalación:** recorre las secciones en orden. Los datos se guardan
   solos después de cada campo.
3. **Antes de irte:** entra a **Resultados** y revisa los veredictos. Si algo sale
   raro, todavía estás parado donde puedes volver a medir. Fíjate especialmente en
   las filas que digan *falta dato*: cada una es un segundo viaje.
4. **Exporta antes de salir:** pulsa *Exportar a Excel* y también *Guardar respaldo*.
   No confíes solo en la memoria del navegador.

## Notas técnicas

- Sin dependencias externas: ni CDN, ni fuentes remotas, ni librerías. Todo el
  código está en `index.html`, porque en campo no hay internet que valga.
- El generador de `.xlsx` está escrito a mano (ZIP sin compresión más
  SpreadsheetML con cadenas en línea). Verificado: integridad de CRC, lectura con
  `openpyxl`, y números exportados como números, no como texto.
- Los datos se guardan en `localStorage`, que es **propio de cada navegador y
  dispositivo**. No se sincronizan ni salen del teléfono.
- Servido por `file://` el autoguardado puede no funcionar en algunos navegadores.
  Úsalo desde GitHub Pages o desde un servidor local.

## Advertencia sobre las fuentes normativas

Los valores normativos programados provienen de los PDF del DS 007-2003-SA y de la
Directiva 033 digitalizados mediante OCR. **Antes de citar cualquier cifra
textualmente en la tesis, verifícala contra el PDF original.**

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La aplicación completa: formulario, cálculos y exportación |
| `sw.js` | Caché que permite usarla sin señal |
| `manifest.webmanifest` | Permite instalarla como app en el teléfono |
