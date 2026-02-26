# Sure Tomorrow (Sprint 14) — Machine Learning + Ofuscación de datos

Proyecto de *machine learning* para una aseguradora ficticia (**Sure Tomorrow**) con 4 objetivos: búsqueda de clientes similares, clasificación de probabilidad de recibir prestaciones, regresión del número de prestaciones y una técnica de **ofuscación** para proteger datos personales sin perder capacidad de modelado.

---

## Objetivo 

Evaluar si modelos de *machine learning* pueden apoyar al equipo de negocio en:

1. **Encontrar clientes similares** (para marketing y atención comercial) 
2. **Predecir si un cliente recibirá prestaciones** (clasificación) 
3. **Predecir el número de prestaciones** que podría recibir (regresión) 
4. **Proteger datos personales** mediante transformación matemática reversible 

---

## Datos 

Dataset: `insurance_us.csv`

Columnas usadas:

- `gender`
- `age`
- `income`
- `family_members`
- `insurance_benefits` (objetivo de regresión)
- `insurance_benefits_received` (objetivo de clasificación: si recibió prestaciones o no)

> Nota: el dataset no se incluye en este repositorio si viene de un entorno del curso. Colócalo en `data/` y ajusta la ruta en el notebook.

---

## Enfoque por tarea 

### 1) Clientes similares (kNN / Nearest Neighbors) 
- Se implementa una función para obtener los **k vecinos más cercanos** usando `NearestNeighbors`.
- Se comparan distancias con diferentes métricas (p. ej. Euclidiana / Manhattan).
- Se observa el impacto del **escalado**: sin escalado, variables con valores grandes (como `income`) dominan la distancia.

### 2) Clasificación: ¿recibirá prestaciones? 
- Modelo: `KNeighborsClassifier`.
- Baseline: `DummyClassifier` (para validar si el modelo realmente aprende señal).
- Se detecta **desbalance de clases** y se aplica **sobremuestreo (upsampling)** para mejorar el aprendizaje.
- Métricas: **Accuracy, AUC-ROC, F1**.

**Resultados (en el split de prueba del notebook):**
- kNN: Accuracy **0.97**, AUC **1.00**, F1 **0.8825**
- Dummy: Accuracy **0.1127**, AUC **0.50**, F1 **0.2025**
- Mejora de Accuracy: **+0.8573** (≈ **+85.73 puntos porcentuales**) 

### 3) Regresión: número de prestaciones (Linear Regression) 
- Se implementa una **Regresión Lineal desde cero** (álgebra lineal) y se compara contra un enfoque estándar.
- Métricas: **RMSE** y **R²**.

**Resultados:**
- RMSE **0.333**
- R² **0.413**

### 4) Ofuscación de datos (protección sin perder modelado) 
- Se genera una matriz aleatoria **invertible** `P` y se transforma `X` con:
  - `X' = X · P`
- Se comprueba que la reversión es posible con:
  - `X = X' · P⁻¹`
- En el notebook se valida la recuperación exacta con `np.allclose(...)=True`.

---

## Tecnologías 

- Python
- NumPy, pandas
- scikit-learn (NearestNeighbors, KNN, métricas, train/test split, DummyClassifier)
- (Opcional) seaborn / matplotlib para visualización 

---

