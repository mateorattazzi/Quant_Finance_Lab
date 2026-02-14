# 📈 Notas de Finanzas Cuantitativas
## Módulo: [Nombre del Módulo]
**Fecha:** 2026-02-14
**Estado:** 🟢 En Progreso | 🟡 Revisión | 🔵 Completado

---

## 🧠 Conceptos Teóricos Clave
> Aquí describes la lógica financiera antes de tocar el código.

### 1. Definición Matemática
* **Concepto:** [Ej. Sharpe Ratio]
* **Lógica:** Mide el exceso de rendimiento por unidad de desviación típica (riesgo).
* **Fórmula (LaTeX):**
  $$SR = \frac{R_p - R_f}{\sigma_p}$$
  *Donde $R_p$ es el retorno de la cartera, $R_f$ la tasa libre de riesgo y $\sigma_p$ la volatilidad.*

---

## 💻 Implementación en Python
> Notas sobre librerías o funciones específicas descubiertas en el vídeo.

```python
import pandas as pd
import numpy as np

# Tip: Para calcular retornos logarítmicos (más precisos para Quants)
log_ret = np.log(data / data.shift(1))