# MINI PROYECTO 3



**Procesamiento del Lenguaje Natural:** Jarvis Calling Hiring Contest





1. Análisis Exploratorio de Datos (EDA)
   Incluya análisis de distribución de clases, longitud de los textos, palabras más frecuentes, n-gramas relevantes y visualizaciones como word clouds o histogramas.
   Limpieza de datos: eliminación de símbolos, stopwords y normalización de texto.



2\. Modelos a implementar:



Pos	Modelo

1	DistilBERT o RoBERTa-base fine-tuned

2	Word2Vec + BiLSTM

3	CNN-1D para texto (con embeddings preentrenados)

4	TF-IDF + XGBoost (GPU version)

5	FastText (entrenamiento local con GPU/CPU)



Preparación: 

* Tokenización y secuenciación según el modelo elegido (por ejemplo, para BiLSTM o CNN-1D).
* Aplicar embeddings preentrenados donde corresponda (Word2Vec, FastText).



Entrenamiento:

* Para modelos basados en transformers (DistilBERT, RoBERTa), utilice fine-tuning.
* Para BiLSTM, realice hiperparametrización usando el siguiente param\_grid:

lstm\_units: 32, 64, 128

num\_lstm\_layers: 1, 2

dropout\_rate: 0.3, 0.5

learning\_rate: 0.001, 0.005

batch\_size: 32, 64

sequence\_length: 50, 100

epochs: 20, 50

embedding\_dim: 100, 200



* Ajuste estos hiperparámetros para mejorar el desempeño del modelo.
* Divida los datos en train, validation y test.
* Entrene cada modelo con el set de entrenamiento y ajuste usando el de validación.
* Evalúe el rendimiento en el set de prueba.



Métricas de performance:

Para comparar los modelos, calcule las siguientes métricas:



* Exactitud (accuracy): proporción de predicciones correctas sobre el total.
* Precisión (precision): proporción de predicciones positivas correctas sobre el total de predicciones positivas.
* Exhaustividad o recall: proporción de verdaderos positivos detectados sobre el total de positivos reales.
* F1-Score: media armónica de precisión y recall.
* Matriz de confusión: para analizar errores por clase.
* ROC-AUC (si aplica): especialmente útil en problemas binarios o multi-clase usando one-vs-rest.



Nota: Para modelos basados en transformers, también se puede registrar el tiempo de entrenamiento y uso de memoria GPU como métricas complementarias.





Reporte final:



* Resumen del EDA con visualizaciones y conclusiones.
* Detalles de cada modelo: arquitectura, hiperparámetros seleccionados, embeddings usados, etc.
* Tabla comparativa de métricas para todos los modelos.
* Análisis crítico: cuál modelo funcionó mejor, posibles razones, limitaciones y recomendaciones de mejora.
