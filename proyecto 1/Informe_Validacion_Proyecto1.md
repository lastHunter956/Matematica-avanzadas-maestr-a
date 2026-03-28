# Informe de Validación Numérica: Sistema Resorte-Masa

**Asignatura:** Matemáticas Avanzadas  
**Proyecto:** Simulación de Oscilador Armónico Simple (OAS)  
**Metodología:** Comparación de Solución Analítica vs. Método de Euler (Escalar y Matricial)

---

## 1. Introducción

Este informe documenta la validación del simulador dinámico desarrollado para el **Problema 2**. El objetivo es contrastar la precisión del método numérico de Euler frente a la solución exacta de la ecuación diferencial ordinaria (EDO) que rige el movimiento de un resorte sin amortiguamiento:

$$m \frac{d^2x}{dt^2} + kx = 0$$

---

## 2. Configuración del Experimento (Base de Control)

Para emular exactamente las pruebas realizadas en el notebook de validación (`Problema2_Validacion.ipynb`), se utilizaron los siguientes parámetros constantes:

- **Masa ($m$):** $1.00 \, \text{kg}$
- **Constante Elástica ($k$):** $4.00 \, \text{N/m}$
- **Equilibrio ($s$):** $0.00 \, \text{m}$
- **Frecuencia Angular ($\omega$):** $\sqrt{k/m} = 2.0000 \, \text{rad/s}$
- **Período ($T$):** $2\pi/\omega \approx 3.1416 \, \text{s}$

### Condiciones Iniciales:

- **Posición Inicial ($x_0$):** $0.50 \, \text{m}$ (estiramiento inicial)
- **Velocidad Inicial ($v_0$):** $0.00 \, \text{m/s}$

---

## 3. Experimento 1: Validación de Precisión ($h = 0.05 \, \text{s}$)

En esta fase, se configuró un paso de tiempo pequeño para observar la convergencia del método.

### Resultados Observados:

| $t_s$ | $x_{EX}$ (Exacta) | $x_{EU}$ (Euler) | $        | \Delta x | $ (Error) | $E_{EU}$ (Energía Euler) |
| :---- | :---------------- | :--------------- | :------- | :------- | --------- | ------------------------ |
| 0.00  | 0.5000            | 0.5000           | 0.000e+0 | 0.5000   |
| 0.05  | 0.4975            | 0.5000           | 2.498e-3 | 0.5050   |
| 0.10  | 0.4900            | 0.4950           | 4.967e-3 | 0.5101   |

### Análisis Técnico:

1.  **Coincidencia con Notebook:** Los valores de la tabla de validación del simulador coinciden al **100%** con los datos calculados en Python (Pandas/NumPy).
2.  **Crecimiento del Error:** Se observa un error absoluto creciente de orden lineal, típico de un método de primer orden como Euler.
3.  **Inyección de Energía:** La energía del sistema ($E_{EU}$) aumenta gradualmente (1% por paso aproximadamente), lo que confirma que el método de Euler explícito es **numéricamente inestable** para osciladores, "inyectando" energía artificial que causa que la amplitud aumente con el tiempo.

---

## 4. Experimento 2: Inestabilidad y Divergencia ($h = 0.5 \, \text{s}$)

Se incrementó el paso de tiempo a un valor crítico ($h = 0.5$) para poner a prueba los límites del algoritmo.

### Tabla de Datos de "Explosión Numérica":

| $t_s$     | $x_{EX}$   | $x_{EU}$      | $            | \Delta x   | $               | $E_{EX}$ (Real) | $E_{EU}$ (Simulada) |
| :-------- | :--------- | :------------ | :----------- | :--------- | :-------------- | --------------- | ------------------- |
| 0.00      | 0.5000     | 0.5000        | 0.000e+0     | 0.5000     | 0.5000          |
| 1.00      | -0.2081    | 0.0000        | 2.081e-1     | 0.5000     | 2.0000          |
| 5.00      | -0.4195    | 0.0000        | 4.195e-1     | 0.5000     | 512.0000        |
| **10.00** | **0.2040** | **-512.0000** | **5.122e+2** | **0.5000** | **524288.0000** |

### Fenómenos Observados:

1.  **Duplicación de Energía:** El factor de amplificación de Euler para este sistema es $(1 + h^2\omega^2)$. Al ser $h=0.5$ y $\omega=2$, el factor es exactamente **2**. La energía se duplica en cada paso de tiempo ($0.5 \to 1 \to 2 \to 4 \dots$).
2.  **Divergencia Exponencial:** En solo 10 segundos, el error pasó de 0 a **512 metros**. La posición calculada por Euler dejó de ser una oscilación para convertirse en una progresión geométrica hacia el infinito.
3.  **Comportamiento Visual (Efecto "Cubo Volador"):**
    - Debido a que el simulador no limita (clamp) la posición para permitir la fluidez de la animación, el cubo es desplazado a coordenadas masivas (ej. -512m).
    - Visualmente, el cubo **desaparece de la pantalla** casi instantáneamente. Esto ocurre porque el motor de renderizado intenta dibujarlo cientos de píxeles fuera del área visible del canvas (clipping).
    - La animación del resorte se estira de forma infinita y errática, reflejando la ruptura de la física simulada.

---

## 5. Conclusiones

- **Fiabilidad del Simulador:** El motor de cálculo del emulador HTML es **matemáticamente idéntico** al modelo teórico y al notebook de validación. Los errores observados no son fallos del código, sino propiedades intrínsecas del método de Euler.
- **Validación de Teoría:** Se demostró empíricamente que para mantener la estabilidad en este sistema, el paso $h$ debe ser significativamente menor a $1/\omega$.
- **Éxito del Proyecto:** La capacidad de la tabla de validación para registrar valores masivos (como $524,288 \, \text{J}$) mientras la solución exacta permanece estable en $0.5 \, \text{J}$ provee una evidencia visual y numérica contundente sobre la importancia de elegir métodos numéricos adecuados (como Runge-Kutta o Euler Implícito) para simulaciones de largo plazo en ingeniería.
