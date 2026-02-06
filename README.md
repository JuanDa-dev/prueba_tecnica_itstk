
---

## 🧠 Clasificación de Texto con SVM (Procesamiento NLP)

Este proyecto utiliza un pipeline de procesamiento de lenguaje natural (NLP) para clasificar mensajes en categorías como **Petición**, **Queja** y **Reclamo**, usando un modelo supervisado SVM entrenado con datos textuales.

---

### 📁 Estructura del Dataset

El dataset de entrada tiene tres columnas principales:

- `Tipo`: Categoría del mensaje (Petición, Queja, Reclamo).
- `Descripción`: Texto que contiene la solicitud o comentario del usuario.
- `Respuesta`: Texto que se usaría como respuesta automática (no se usa para entrenamiento).

> **Nota**: Algunos datos vienen en una sola columna con comillas, por lo que es necesario repararlos antes del análisis.

---

### 🧼 1. Limpieza y Preparación del Dataset

1. **Carga del CSV**  
   Se usa `pandas.read_csv()` con parámetros especiales (`quotechar='"'`, `engine="python"`) para manejar correctamente los delimitadores.

2. **Reparación de columnas**  
   Si los datos vienen en una sola columna, se dividen usando expresiones regulares para reconstruir `Tipo`, `Descripción` y `Respuesta`.

3. **Limpieza del texto**  
   - Se convierte todo a minúsculas.
   - Se eliminan puntuaciones.
   - Se tokeniza el texto.
   - Se eliminan stopwords en español.
   - Se vuelve a unir el texto limpio.

   Esto se aplica en una nueva columna: `Descripción_Limpiada`.

---

### 🏷️ 2. Etiquetado y División de Datos

- Se define `X` como el texto limpio (`Descripción_Limpiada`).
- Se define `y` como la clase (`Tipo`).
- Se divide el dataset en conjunto de **entrenamiento (80%)** y **prueba (20%)**.

---

### 🛠️ 3. Pipeline de Clasificación

Se construye un `Pipeline` de `scikit-learn` con:

- `TfidfVectorizer`: Convertir texto en vectores numéricos, considerando unigramas y bigramas.
- `SVC`: Clasificador SVM con kernel lineal y ajuste fino de parámetros (`C=10`, `gamma='scale'`).

---

### 🧪 4. Entrenamiento y Evaluación

- Se entrena el modelo con `pipeline.fit()`.
- Se evalúa con `accuracy_score` y `classification_report`.
- Se imprime el rendimiento del modelo.

---

### 💾 5. Guardado del Modelo y Datos

- El modelo SVM entrenado se guarda con `joblib` como `modelo_svm.pkl`.
- El dataset con columna limpia se guarda como `datatxt_procesado.csv`.

---


### 📦 Requisitos

- Python 3.7+
- Pandas
- NLTK
- scikit-learn
- joblib

Instala con:

```bash
pip install pandas nltk scikit-learn joblib
```

---

A continuación **guía de ejecución paso a paso** para correr tu proyecto completo de procesamiento de texto con NLP y SVM. Está pensada para que cualquier persona pueda entender qué hace tu código y cómo utilizarlo.

---

## 🧪 Guía de Ejecución - Clasificación de Texto con NLP + SVM

Este proyecto realiza clasificación de texto usando técnicas de NLP y un modelo supervisado SVM, entrenado con un dataset de quejas, peticiones y reclamos.

---

### ✅ Requisitos

Antes de ejecutar el código, asegúrate de tener instalado:

```bash
pip install pandas nltk scikit-learn joblib
```

---

### 🗂 Archivos esperados

- `datatxt.csv`: Dataset original con columnas **Tipo**, **Descripción** y **Respuesta**.
- `Procesar_Texto_NLP.py`: Archivo con el script que realiza todo el procesamiento y entrenamiento.
- (Salida esperada) `modelo_svm.pkl`: Archivo del modelo entrenado.
- (Salida esperada) `datatxt_procesado.csv`: Dataset con la columna `Descripción_Limpiada`.

---

### ⚙️ Pasos de ejecución

#### 1. 📥 Cargar el dataset
El script abre `datatxt.csv` y corrige automáticamente si las columnas están mal formateadas (por ejemplo, si vienen todas en una sola columna con comillas).

#### 2. 🧼 Limpieza de texto
La columna **Descripción** es procesada:
- Minúsculas
- Eliminación de puntuación
- Tokenización
- Eliminación de stopwords (palabras vacías)
- Resultado: nueva columna `Descripción_Limpiada`

#### 3. 🧠 Preparación del modelo
- Se definen `X` (entrada) como `Descripción_Limpiada` y `y` (etiquetas) como `Tipo`.
- Se divide en entrenamiento y prueba (80% / 20%).

#### 4. 🔎 Entrenamiento con Pipeline
Se entrena un modelo SVM dentro de un pipeline que incluye:
- `TfidfVectorizer`: para vectorizar texto (con ngramas y escalado logarítmico).
- `SVC`: clasificador con kernel lineal.

#### 5. 📊 Evaluación
- Se evalúa el modelo con `accuracy_score` y `classification_report`.

#### 6. 💾 Guardado de resultados
- Se guarda el modelo entrenado como `modelo_svm.pkl`.
- Se guarda el dataset limpio como `datatxt_procesado.csv`.

---

---

