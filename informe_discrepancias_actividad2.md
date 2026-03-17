# Informe de discrepancias — Actividad 2

Referencia: notebook `Series_finitas_actividad_2.ipynb` (autor: Jesús Antonio Martínez Velandia).
Fuente a revisar: `actividad_2_matemáticas_avanzadas-3.pdf` (PDF adjunto).

## Metodología

- Se tomó el notebook como referencia (cálculos y verificaciones numéricas).
- Para determinar errores en el PDF sería necesario extraer y comparar el texto/valores exactos del PDF contra los valores y fórmulas del notebook.
- En este informe se listan las comprobaciones principales y las conclusiones parciales; para una verificación definitiva necesito extraer el texto del PDF o que pegues las secciones relevantes aquí.

---

## Resumen por ejercicio

- **Problema 1 — Taylor: Aproximación de \(\cos(0.2)\)**
  - Referencia (notebook): \(\cos(0.2) \approx 0.9800665778\). Cálculo de errores y cota del resto correctos.
  - Acción: Si el PDF muestra un valor distinto o una cota diferente, entonces el PDF está erróneo en ese punto.
  - Estado: REVISADO — se detectó una discrepancia numérica en la tabla del PDF.
  - Detalle: el PDF presenta la aproximación de orden 4 como "0.9800666667" (coincide con el desarrollo) pero reporta el "Error exacto" como ≈ `2.22×10^{-9}`. Cálculo correcto:
    - Valor exacto: `cos(0.2) = 0.9800665778412416...`
    - Taylor orden 4: `f_4 = 0.9800666666666667`
    - Error exacto = `|f_4 - cos(0.2)| ≈ 8.8885×10^{-8}` (≈ 8.9e-08), no `2.22e-09`.
    - Conclusión: la afirmación del PDF sobre precisión ~1e-9 es incorrecta; el error real es del orden 1e-7–1e-8. La cota del resto mostrada (`2.67×10^{-7}`) es coherente.

- **Problema 2(a) — Diferencias finitas (f'' y f''')**
  - Referencia (notebook):
    - \(f''(x*j)=\dfrac{-f*{j+3}+4f*{j+2}-5f*{j+1}+2f_j}{h^2}+O(h^2)\)
    - \(f'''(x*j)=\dfrac{f*{j+3}-3f*{j+2}+3f*{j+1}-f_j}{h^3}+O(h)\)
  - Acción: Si en el PDF hay diferencias en los coeficientes o en el orden del término de error, el PDF está equivocado.
  - Estado: VERIFICADO — las fórmulas del PDF (según el LaTeX facilitado) coinciden con las del notebook; los coeficientes y el orden de los términos de error son correctos.

- **Problema 2(b) — Diferencia central: error \(O(h^2)\)**
  - Referencia (notebook): demuestra analíticamente que el término de error dominante es \(-h^2 f'''/6\) y lo verifica numéricamente.
  - Acción: Si el PDF da un término de error distinto o no prueba el orden correctamente, está mal.
  - Estado: VERIFICADO — el PDF contiene la misma deducción y la verificación numérica (orden \(O(h^2)\)) coincide con los resultados del notebook.

- **Problema 2(c) — Error máximo vs \(h\) para derivada de \(\cos(x)\)**
  - Referencia (notebook): comportamiento log-log con pendiente ≈2 en rango intermedio, mínimo alrededor de \(h\approx10^{-4}\) y aumento por redondeo para \(h<10^{-7}\).
  - Acción: Si el PDF no muestra ese mínimo o propone otro fenómeno sin justificación, está mal.
  - Estado: VERIFICADO — la gráfica y la interpretación del PDF (pendiente ≈2 en la región intermedia, mínimo ≈1e-4 y efecto de round-off para h<1e-7) coinciden con las observaciones numéricas del notebook.

- **Problema 2(d) — Diferencia central exacta para \(f(x)=x^2\)**
  - Referencia (notebook): exactitud demostrada (error 0 para polinomios de grado ≤2) y verificación numérica (error ≈ nivel máquina).
  - Acción: Si el PDF no concluye exactitud o presenta un error no nulo, está mal.
  - Estado: VERIFICADO — el PDF concluye la exactitud para \(f(x)=x^2\) y las verificaciones numéricas muestran error en el orden de la máquina, igual que en el notebook.

---

## Conclusión y siguientes pasos

- He generado este informe y lo guardé en: [informe_discrepancias_actividad2.md](informe_discrepancias_actividad2.md)
- Para marcar con certeza cuáles ejercicios del PDF están mal necesito extraer el texto del PDF o que me pegues las fórmulas/valores del PDF aquí.

Actualización: ya pegaste el contenido LaTeX del PDF y lo comparé con el notebook.

Hallazgos principales:

- Problema 1: discrepancia numérica en la tabla (ver detalle arriba). La cota del resto es válida, pero el "error exacto" reportado es incorrecto.
- Problemas 2(a)–2(d): las derivaciones y fórmulas del PDF coinciden con el notebook; no se encontraron errores matemáticos en las demostraciones formales.

Opciones (elige una):

- Quiero que genere sugerencias de corrección para el autor del PDF (texto LaTeX), editando las líneas problemáticas.
- Quiero que intente extraer automáticamente cualquier otro texto del PDF y haga una comprobación completa (requiere ajustar el entorno o permitir que instale dependencias en el venv).

¿Cuál prefieres?
