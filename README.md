# 📊 Telecom X - Predicción de Churn (Parte 2)

## 🎯 Contexto y Misión
Tras el análisis exploratorio inicial, este proyecto desarrolla un **Pipeline de Machine Learning** para predecir qué clientes tienen mayor probabilidad de cancelar sus servicios. El objetivo es permitir que la empresa tome decisiones proactivas para mejorar la retención.

## 🛠️ Pipeline de Preparación de Datos
1. **Limpieza:** Se eliminó el identificador `customerID` para evitar ruido en los modelos.
2. **Encoding:** Transformación de variables categóricas a numéricas mediante *One-Hot Encoding* para asegurar compatibilidad con los algoritmos.
3. **Balanceo (SMOTE):** Debido al desbalance de clases (~26% Churn), se aplicó la técnica **SMOTE** en el conjunto de entrenamiento para equilibrar la muestra y mejorar el aprendizaje de la clase minoritaria.
4. **Normalización:** Uso de `StandardScaler` para la Regresión Logística, garantizando que variables como `Charges.Monthly` no sesguen el modelo por su magnitud.

## 🤖 Comparativa de Modelos y Resultados
Se evaluaron dos modelos competitivos sobre un conjunto de prueba de 2,113 clientes:

| Métrica | Regresión Logística | Random Forest |
| :--- | :---: | :---: |
| **Exactitud (Accuracy)** | 76.52% | 76.53% |
| **Recall** | **68.09%** | 59.71% |
| **F1-Score** | 0.6054 | 0.5746 |

### Análisis de Desempeño
* **Ganador Operativo:** La **Regresión Logística** es el modelo recomendado para el negocio debido a su mayor **Recall**. Logró identificar correctamente a **382 clientes** en riesgo de fuga, minimizando los falsos negativos.
* **Random Forest:** Aunque fue más preciso (generando menos falsas alarmas con 270 falsos positivos), dejó escapar a más clientes que realmente cancelaron el servicio.



## 💡 Factores Críticos de Cancelación (Insights)
Basado en la importancia de variables del modelo, los factores que más detonan el Churn son:
1. **Tenure (Antigüedad):** Los clientes nuevos son los más propensos a irse.
2. **Charges.Monthly (Cargos Mensuales):** Existe una alta sensibilidad al precio; a mayor cargo, mayor riesgo de fuga.
3. **Tipo de Contrato:** Los contratos mensuales presentan la mayor volatilidad.

## 📈 Propuestas Estratégicas
* **Fidelización Temprana:** Programas de acompañamiento en los primeros 3 meses de contrato (basado en el factor `tenure`).
* **Migración de Contratos:** Incentivos para que clientes con modalidad mensual cambien a contratos anuales.
* **Alertas de Precio:** Ofertas de planes más económicos ante aumentos significativos en los cargos mensuales detectados por el modelo.

## 🚀 Cómo ejecutar
1. Clonar el repositorio.
2. Asegurarse de tener instalado `pandas`, `scikit-learn`, `seaborn` e `imblearn`.
3. Ejecutar el cuaderno `.ipynb` cargando el archivo `datos_tratados.csv`.
