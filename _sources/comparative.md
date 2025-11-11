# **Comparativo general de modelos de clasificación de textos**

> Todos los modelos fueron entrenados con una división de datos 70 % entrenamiento, 15 % validación y 15 % prueba, y en los casos requeridos se aplicaron estrategias de balanceo de clases, debido al desbalance que existe entre los grupos.

---

## **1. Rendimiento en el conjunto de validación y prueba**

| Modelo                | Accuracy (Val) | F1-Macro (Val) | Accuracy (Test) | F1-Macro (Test) | Diferencia (Val–Test) | Observaciones                             |
| --------------------- | -------------- | -------------- | --------------- | --------------- | --------------------- | ----------------------------------------- |
| **BiLSTM + Word2Vec** | 0.7688         | 0.7652         | 0.7105          | 0.7055          | ↓ 0.058               | Pérdida leve, generalización moderada.  |
| **CNN1D + Word2Vec**  | 0.7070         | 0.7016         | 0.6622          | 0.6531          | ↓ 0.045               | Pérdida leve; buena generalización.       |
| **XGBoost + TF-IDF**  | 0.8199         | 0.8191         | 0.8123          | 0.8115          | ↓ 0.008               | Comportamiento estable, generaización sólida              |
| **FastText**          | 0.7823         | 0.7809         | 0.7078          | 0.7008          | ↓ 0.075               | Pérdida notoria, generalización moderada. |
| **DistilBERT**        | 0.8441         | —              | 0.8065          | 0.8067          | ↓ 0.038               | Pérdida leve, generalización sólida.   |


El modelo **XGBoost con TF-IDF** presenta la mayor estabilidad entre los conjuntos de validación y prueba, con apenas un descenso del 0.8 %. Esto indica un excelente equilibrio y mínima tendencia al sobreajuste. **DistilBERT** obtiene el mayor rendimiento absoluto en validación (Acc = 0.84) y test (Acc = 0.81), confirmando su capacidad para capturar representaciones semánticas más profundas.
Por otro lado, **FastText** evidencia una brecha mayor entre validación y prueba (≈ 7.5 %), lo que sugiere menor capacidad de generalización frente a datos nuevos.
Los modelos **BiLSTM** y **CNN1D**, basados en Word2Vec, muestran un rendimiento intermedio, con resultados consistentes pero inferiores a los modelos basados en TF-IDF y transformadores.

---

## **2. Balance por Clases**

| Clase                                  | Mejor F1-score    | Modelos Destacados  | Peor F1-score | Modelos con Bajo Rendimiento |
| -------------------------------------- | ----------------- | ------------------- | ------------- | ---------------------------- |
| **Negocios y Finanzas**                | 0.90 (DistilBERT) | XGBoost, DistilBERT | —             | —                            |
| **Tecnología y Ciencia**               | 0.90 (DistilBERT) | XGBoost, BiLSTM     | 0.68 (CNN1D)  | CNN1D                        |
| **Servicios Profesionales y Públicos** | 0.81 (XGBoost)    | XGBoost, FastText   | 0.67 (CNN1D)  | CNN1D                        |
| **Creatividad y Producción**           | 0.81 (XGBoost)    | XGBoost             | 0.59 (CNN1D)  | CNN1D                        |
| **Otros y Especializados**             | 0.76 (XGBoost)    | XGBoost             | 0.55 (CNN1D)  | CNN1D                        |


El **modelo XGBoost con TF-IDF** presenta el mejor balance de desempeño entre clases, con valores de F1-score altos y homogéneos en todas las categorías (rango ≈ 0.76–0.86). Esto sugiere que el modelo logra capturar patrones representativos incluso en clases con menor frecuencia. **DistilBERT** sobresale en las clases con mayor carga semántica (_Negocios y Finanzas_, _Tecnología y Ciencia_), superando el 0.90 en F1, pero muestra leves caídas en _Servicios Profesionales_ y _Otros_.
En contraste, el **modelo CNN1D** muestra una fuerte variación entre clases (de 0.55 a 0.78), evidenciando menor consistencia interclase.
**BiLSTM** y **FastText** mantienen un rendimiento medio, cercanos al 0.70 de F1-macro, aunque sin sobresalir en ninguna categoría específica.

---

## **3. Conclusiones Comparativas**


1. **Rendimiento global:**
   * El modelo más consistente y robusto, conmejor desempeño general es **XGBoost + TF-IDF** (Acc = 0.812), seguido muy de cerca por **DistilBERT** (Acc = 0.806).
   * Ambos modelos evidencian excelente capacidad de generalización y estabilidad entre validación y prueba, asi como una representación estable entre las distintas macro categorias de empleo. Aunque **DistilBERT** captura mejor ciertas clases, es el que mayor recursos computacionales compromete. 

2. **Modelos intermedios:**
    
   * **BiLSTM** logra resultados sólidos (Acc = 0.71, F1 = 0.70), destacando su estabilidad y coherencia entre validación y test.
   * **FastText** obtiene cifras similares, aunque con una ligera pérdida de rendimiento al pasar al conjunto de prueba. Al ser el más liviano de todos (con menor tiempo de entrenamiento) es una alternativa eficiente si se prioriza la velocidad sobre la precisión.

3. **Modelos menos consistentes:**

   * **CNN1D**, pese a entrenar eficientemente, muestra menor balance entre clases y una caída más pronunciada en el conjunto de prueba.

4. **Balance de clases:**

   * Las clases **“Negocios y Finanzas”** y **“Tecnología y Ciencia”** son consistentemente las mejor clasificadas por todos los modelos.
   * Las categorías **“Creatividad y Producción”** y **“Otros y Especializados”** presentan los desempeños más bajos, coincidiendo con su mayor diversidad léxica y posible menor representación en los datos.

## **4. Conclusión del problema**

De acuerdo con los resultados experimentales, los modelos presentan desempeños diferenciados tanto en precisión global como en equilibrio entre clases. En el contexto de clasificación de hojas de vida dentro de la empresa **Jarvis** para identificar el perfil profesional de cada candidato, los resultados permiten establecer que para la empresa, el **modelo XGBoost con TF-IDF** representa la mejor opción práctica:

* Ofrece alto rendimiento y estabilidad
* Requiere menor tiempo de entrenamiento
