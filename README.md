# InvestAI — Sistema Inteligente de Predicción Bursátil y Soporte de Decisiones

### 🎓 Facultad de Ingeniería de Sistemas e Informática — UNMSM
**Curso:** Introducción al Desarrollo de Software  
**Docente:** Mg. Ernesto Cancho-Rodríguez  
**Entorno de Despliegue:** Ingesta e Inteligencia en Google Colab/Jupyter Notebooks, Persistencia distribuida en MongoDB Atlas, API asíncrona mediante FastAPI expuesta vía ngrok, e Interfaz de Usuario Web interactiva.

---
## 📂 Estructura de Componentes del Proyecto

### 1. Modelado e Inteligencia Artificial (Notebooks)

* **`Notebook1_Ingesta_Datos_Mineras_MongoDB.ipynb`**
    * **Función:** Descarga datos reales diarios de 5 activos mineros estratégicos (`FSM`, `VOLCABC1.LM`, `ABX.TO`, `BVN`, `BHP`).
* **`Notebook2_SVC_MongoDB.ipynb`**
    * **Función:** Clasificación direccional binaria (BUY/SELL) basada en Support Vector Machines.
* **`Notebook3_RNN_LSTM_MongoDB.ipynb`**
    * **Función:** Clasificador de Deep Learning mediante redes recurrentes de memoria a largo y corto plazo (LSTM).
* **`Notebook4_RNN_BiLSTM_MongoDB.ipynb`**
    * **Función:** Clasificador LSTM Bidireccional (BiLSTM).
* **`Notebook5_RNN_GRU_MongoDB.ipynb`**
    * **Función:** Clasificador basado en Gated Recurrent Units (GRU).
* **`Notebook6_RNN_SimpleRNN_Baseline_MongoDB.ipynb`**
    * **Función:** Modelo base de control estadístico (*Baseline*).
* **`Notebook7_LSTM_Regresor_Precios_MongoDB.ipynb`**
    * **Función:** Pronóstico numérico continuo del valor real del activo (Regresión en USD).

### 2. Capa de Exposición: Backend (`Notebook8_API_FastAPI.ipynb`)
Implementa un servidor web asíncrono robusto con el framework **FastAPI**. Diseñado bajo principios de baja latencia, interactúa con MongoDB en modo estricto de **Solo Lectura** para servir datos pre-calculados, garantizando respuestas en el orden de los milisegundos.

### 3. Capa de Interfaz de Usuario UI (`index.html`)
Aplicación Frontend SPA (*Single Page Application*) construida en HTML5 adaptativo, CSS3 con arquitectura de variables y JavaScript nativo asíncrono.
* **Motores Gráficos integrados:** **Plotly.js** para renderizado avanzado de velas japonesas (*candlesticks*), heatmaps matriciales para la visualización de matrices de confusión y trazos continuos de curvas de confianza; y **Chart.js** para la gestión estática de diagramas de distribución de portafolios y curvas acumuladas de rendimiento bursátil (*equity curves*).
* **Módulos del Sistema:** Control de acceso (Login), Terminal de Mercado, Paneles Analíticos específicos para clasificadores SVC y RNN, Regresor LSTM de Precios Futuros, Gestor de Análisis NLP, Asignación de Activos según perfil de riesgo, Integración TWS simulada con Interactive Brokers (*Paper Trading*) y Consola de Control de Ensamblado General de Modelos.

---

## ⚙️ Requisitos del Sistema y Variables de Entorno

Para desplegar el pipeline completo, se requiere configurar las siguientes claves de acceso seguro dentro del panel de **Secrets** (`🔑`) en el entorno de ejecución de Google Colab:

1.  `MONGO_URI`: Cadena de conexión cifrada provista por MongoDB Atlas Cluster (ej. `mongodb+srv://<user>:<password>@cluster.mongodb.net/spbi`).
2.  `NGROK_AUTHTOKEN`: Token de autenticación de seguridad de la infraestructura de túneles ngrok para la exposición segura del puerto del backend local hacia la red externa.

---

## 🚀 Guía de Despliegue de la Plataforma

### Paso 1: Población de la Base de Datos Distribuida
1. Abra y ejecute en secuencia total el `Notebook1_Ingesta_Datos_Mineras_MongoDB.ipynb` para descargar los datos de Yahoo Finance y estructurar la colección intermedia de mercado `precios_ohlcv`.
2. Ejecute el `Notebook2_SVC_MongoDB.ipynb` para procesar la inteligencia clásica del clasificador correlacionando los modelos matemáticos óptimos en la colección `metricas_modelos` y `predicciones`.
3. Ejecute de forma independiente los notebooks de redes neuronales recurrentes (`Notebook3`, `Notebook4`, `Notebook5`, `Notebook6` y `Notebook7`) para completar el espectro comparativo avanzado y el regresor continuo en el clúster.

### Paso 2: Inicialización y Exposición del Backend REST
1. Abra el archivo `Notebook8_API_FastAPI.ipynb`.
2. Asegúrese de que los Secrets `MONGO_URI` y `NGROK_AUTHTOKEN` se encuentren validados en el entorno de Colab actual.
3. Ejecute todas las celdas del documento. La lógica del script levantará el servidor asíncrono Uvicorn en un hilo independiente (`threading.Thread`) y desplegará una **URL PÚBLICA** generada por ngrok (ejemplo: `https://xxxx-xxxx.ngrok-free.dev`).
4. Copie la dirección URL pública generada. Puede validar su correcto funcionamiento accediendo al endpoint interactivo de documentación auto-generada: `https://xxxx-xxxx.ngrok-free.dev/docs`.

### Paso 3: Configuración y Lanzamiento de la Interfaz Web
1. Localice el archivo frontend `index.html`.
2. Abra el archivo en un editor de código y diríjase a la línea inicial del bloque `<script>`, específicamente donde se inicializa la constante global de red:
   ```javascript
   const API_URL = "[https://actualiza-con-tu-url-ngrok.ngrok-free.dev](https://actualiza-con-tu-url-ngrok.ngrok-free.dev)";
3. Reemplace el valor de la constante con la URL PÚBLICA exacta copiada del terminal de ngrok del Paso 2. Guarde los cambios en el archivo.
4. Ejecute el archivo index.html en cualquier navegador web moderno.
5. Para acceder al área protegida de la suite ejecutiva de inversión, ingrese las siguientes credenciales del entorno demostrativo del sistema:
    Correo Electrónico: demo@investai.com
    Contraseña: demo123
