# Procesamiento de Neuroimágenes para la Identificación de Narcolepsia

## Resumen del Proyecto

Este repositorio contiene información y potencialmente código relacionado con el artículo de investigación "Procesamiento de neuroimágenes para la identificación de narcolepsia" por Brayan Agray Feo, Mitchell Bermin Suárez y Oscar Miranda Puentes de la Universidad Sergio Arboleda.

El proyecto se enfoca en aplicar técnicas avanzadas de procesamiento de imágenes a datos de neuroimagen (fMRI y PET) para identificar patrones sutiles y posibles biomarcadores asociados con la narcolepsia. El diagnóstico de la narcolepsia suele ser desafiante debido a la variabilidad de los síntomas y la falta de métodos diagnósticos definitivos, precisos y accesibles. Este trabajo explora el potencial de la mejora de neuroimágenes para revelar anomalías cerebrales relacionadas con el trastorno.

**Palabras Clave:** Neuroimágenes, Narcolepsia, fMRI, PET, Cataplejía, Tálamo, Hipotálamo, Corteza cerebral, Procesamiento de Imágenes

## Contexto del Problema

La narcolepsia es un trastorno neurológico del sueño caracterizado por somnolencia diurna excesiva, cataplejía, parálisis del sueño y sueño fragmentado. Diagnosticarla con precisión puede ser difícil. Aunque las técnicas de neuroimagen como fMRI y PET ofrecen formas de visualizar la estructura y función cerebral, correlacionar los hallazgos de imagen con los síntomas clínicos sigue siendo un desafío continuo. Este proyecto aborda la necesidad de mejores métodos para extraer información relevante de las neuroimágenes para el diagnóstico de la narcolepsia.

## Objetivo

El objetivo principal es desarrollar y aplicar un pipeline (secuencia de procesamiento) específico de procesamiento de imágenes para mejorar neuroimágenes (formato .nii) de individuos potencialmente afectados por narcolepsia. El fin es mejorar la visibilidad de regiones cerebrales clave e identificar anomalías estructurales o funcionales sutiles que puedan servir como posibles biomarcadores para la condición, centrándose particularmente en áreas involucradas en la regulación sueño-vigilia.

## Metodología

### Datos

*   Neuroimágenes obtenidas mediante Resonancia Magnética funcional (fMRI) y Tomografía por Emisión de Positrones (PET).
*   Formato de datos: NIfTI (.nii), capturando estructura y actividad cerebral 3D.
*   Fuente: Conjunto de datos público de actividad neuronal durante el sueño (detalles específicos no indicados en el resumen), centrado en pacientes de 20 a 30 años para minimizar factores de confusión como la degeneración relacionada con la edad.

### Regiones Cerebrales Clave de Interés

El análisis se centra en regiones conocidas por estar involucradas en la regulación del sueño y potencialmente afectadas en la narcolepsia:
1.  **Hipotálamo Lateral:** Sitio clave de las neuronas productoras de hipocretina (orexina), a menudo perdidas en la Narcolepsia Tipo 1.
2.  **Tálamo:** Papel central en la regulación del sueño y la vigilia. Se ha observado flujo sanguíneo reducido durante episodios de sueño REM en narcolépticos.
3.  **Corteza Prefrontal y Temporal:** Implicadas en la regulación cognitiva y emocional; se han reportado cambios estructurales (reducción de materia gris).
4.  **Tronco Encefálico y Sistema Límbico:** Involucrados en los ciclos sueño-vigilia y el procesamiento emocional (relevante para la cataplejía).
5.  **Tractos de Materia Blanca:** Alteraciones en la conectividad (estudiadas mediante DTI, mencionadas como contexto relevante).

### Pipeline de Procesamiento de Imágenes

Se aplicó una secuencia específica de filtros para mejorar las neuroimágenes y resaltar características relevantes (Ver Figura 3 en el artículo):

1.  **Corte Transversal:** Selección inicial de una vista lateral de la imagen NIfTI 3D.
2.  **Filtro Logarítmico:** Mejora el contraste, especialmente en regiones de baja intensidad (como hipotálamo/tálamo), comprimiendo valores de alta intensidad para hacer visibles detalles sutiles (Ver Figura 4).
3.  **Filtro de Afilado (Sharpening):** Mejora la definición de los bordes entre diferentes tejidos (ej. materia gris vs. blanca) y estructuras, clarificando detalles anatómicos (Ver Figura 5).
4.  **Ecualización Adaptativa del Histograma (CLAHE):** Mejora el contraste local de forma adaptativa en toda la imagen, revelando detalles finos en áreas como el tálamo y la corteza prefrontal. Puede incrementar el ruido (Ver Figura 6).
5.  **Filtro de Mediana:** Reduce el ruido impulsivo (potencialmente introducido por CLAHE) mientras preserva bordes importantes y detalles estructurales, llevando a una imagen más uniforme (Ver Figura 7).
6.  **Filtro de Gradiente Morfológico:** El paso final, basado en operaciones de dilatación y erosión. Resalta con precisión los bordes y las transiciones de intensidad, delineando eficazmente las estructuras anatómicas y eliminando áreas uniformes, dejando una representación clara de los límites estructurales (Ver Figura 8).

## Hallazgos Clave

*   El pipeline de procesamiento de imágenes propuesto mejoró con éxito las neuroimágenes, aumentando la claridad y el detalle de las estructuras cerebrales relevantes.
*   La aplicación del pipeline, particularmente el paso final del gradiente morfológico, reveló **sutiles irregularidades y relieves a lo largo de los bordes del hipotálamo y la corteza prefrontal** en las imágenes procesadas de pacientes con trastornos del sueño (Ver Figura 9).
*   Estas alteraciones sutiles se observaron consistentemente en la muestra de pacientes estudiada y difieren de las neuroimágenes de individuos sanos.
*   Aunque estos hallazgos son sutiles y pueden no ser suficientes para un diagnóstico independiente, representan **patrones o marcadores físicos potenciales interesantes** asociados con trastornos del sueño como la narcolepsia que justifican una mayor investigación.
*   El estudio demuestra el poder del procesamiento de imágenes dirigido para descubrir detalles no visibles en neuroimágenes crudas o mínimamente procesadas.

## Importancia / Relevancia

Este trabajo contribuye a la búsqueda de biomarcadores no invasivos para la narcolepsia. Al mejorar los datos de neuroimagen, los patrones sutiles identificados podrían potencialmente:
*   Mejorar la precisión y eficiencia del diagnóstico de narcolepsia.
*   Proporcionar evidencia fisiológica objetiva para complementar las evaluaciones clínicas.
*   Facilitar la investigación sobre la fisiopatología subyacente de la narcolepsia.
*   Conducir al desarrollo de enfoques de tratamiento más personalizados.

## Uso (Conceptual) del Repositorio

Este repositorio *idealmente contendría*:
*   Scripts de Python o cuadernos Jupyter implementando el pipeline de procesamiento descrito (usando bibliotecas como NiBabel para E/S NIfTI, Scikit-image, OpenCV o similares para el filtrado).
*   Datos NIfTI de muestra (anonimizados) para probar el pipeline.
*   Documentación detallando dependencias y cómo ejecutar los pasos de procesamiento.
