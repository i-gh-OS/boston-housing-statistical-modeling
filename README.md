# Proyecto Final – Inferencia y Modelos de Regresión para los Negocios

---

## 1. Selección de la variable objetivo

Debéis escoger:

* Una **variable numérica** como variable objetivo (**Y**).
* Hasta **10 variables explicativas** (**X**) que potencialmente influyan sobre Y.

---

## 2. Aprobación previa del profesor

Antes de comenzar el análisis, es obligatorio subir a Moodle:

* El **dataset** (archivo adjunto).
* Una **breve descripción del tema**.
* La **propuesta de variable objetivo** y las **variables explicativas** seleccionadas.

No se debe iniciar el análisis sin la confirmación del profesor.

---

## 3. Preprocesamiento del dataset

Deberéis realizar las transformaciones necesarias para que el modelo sea válido. Entre ellas:

* Eliminación de **valores atípicos**.
* Tratamiento de **datos ausentes**.
* Conversión de **tipos de datos incorrectos**.
* **Codificación one-hot** para variables categóricas.

---

## 4. Ajuste del modelo

Se debe ajustar un **modelo de regresión lineal múltiple** y justificar:

* Interpretación de los **coeficientes**.
* Inclusión de **términos cuadráticos**, **logarítmicos** e **interacciones** si procede.

---

## 5. Validación del modelo

Comprobación de los siguientes supuestos:

* **Normalidad** de los residuos.
* **Heterocedasticidad**.
* **Autocorrelación**.
* **Multicolinealidad** (VIF).

Además, debe proponerse un **modelo alternativo más simple**, con menor R² ajustado pero **más interpretable**.

---

## 6. Conclusiones e insights

El informe final debe incluir **al menos 5 conclusiones relevantes y aplicadas al contexto del dataset**.

---

## 7. Presentación y entrega

* **Presentación oral** de 5 minutos por grupo.
* **Diapositivas resumen** del trabajo.
* **Código empleado** (R).
* **Defensa oral** con preguntas.

---

## 8. Ejemplo de propuesta – Fondos de inversión

### Problema

Identificar qué factores explican la **rentabilidad anual** de los fondos de inversión.

### Datos

* Fuente: *Morningstar*, *Kaggle* u otros.
* Datos **transversales** (cada fila = un fondo).

### Variables

| Variable                   | Tipo                | Rango                | Justificación                                  |
| -------------------------- | ------------------- | -------------------- | ---------------------------------------------- |
| **Rentabilidad anual (%)** | Numérica (objetivo) | –30% a 60%           | Variable a explicar                            |
| **Expense ratio**          | Numérica            | 0.1% a 3%            | Costes altos ↓ rentabilidad neta               |
| **Volatilidad histórica**  | Numérica            | 5% a 40%             | Mayor riesgo → mayor rentabilidad esperada     |
| **Tamaño del fondo (USD)** | Numérica            | 10 a 100.000         | Tamaños extremos pueden afectar al rendimiento |
| **Estilo de inversión**    | Categórica          | Growth, Value, Blend | Se codifica con dummies                        |

### Modelo propuesto

```
Rentabilidad_fondo = β0 
                    + β1 · Expense_ratio 
                    + β2 · Volatilidad 
                    + β3 · Tamaño_fondo 
                    + β4 · Estilo
```

### Signos esperados

* **β₁ < 0**: mayores costes → menor rentabilidad.
* **β₂ > 0**: más riesgo → mayor rentabilidad esperada.
* **β₃**: signo incierto.
* **β₄**: estilo *Growth* positivo en años de expansión.

### Supuestos del modelo

* Errores con **media cero** si las variables relevantes están incluidas.
* **Heterocedasticidad probable** → test de White o Breusch–Pagan.
* **Exogeneidad** plausible.
* **Autocorrelación no aplicable** (datos de corte transversal).
* Comprobación de **multicolinealidad**.

