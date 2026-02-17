# LSE Avatar

El objetivo de este proyecto es diseñar un avatar tridimensional capaz de comunicar mensajes en Lengua de Signos Española (LSE).

El proyecto nació y se ha ido desarrollando por investigadoras e investigadores del Departamento de Matemáticas y Computación de la Universidad de La Rioja, y ha sido parcialmente financiado por ...

Este documento README.md lo escribe (febrero de 2026) Pablo Munarriz Senosiain, desarrollador principal del proyecto hasta septiembre de 2025, con la intención de facilitar a quien venga después la incorporación al proyecto.

## ¿Qué contiene cada carpeta?

### Datos

En la carpeta "Datos" tenemos dos subcarpetas: "Brutos" y "Procesados". En "Brutos" tenemos datos descargados directamente de internet:
- Letras_Sematos: vídeos de las letras del abecedario dactilológico del portal [Sématos](https://www.sematos.eu/lse.html).
- Letras_Spread: vídeos e imágenes de las letras del abecedario dactilológico del diccionario [Spreadthesign](https://spreadthesign.com/es.es/search/).
- Palabras_Spread: vídeos de algunas palabras del diccionario [Spreadthesign](https://spreadthesign.com/es.es/search/).
- Además, hay varias imágenes de esqueletos anotados en función del modelo de Human Pose Recognition que se use y una imagen con números que usaba para numerar frames de vídeos.

En "Procesados" tenemos datos que hemos creado nosotr@s, en general, analizando y procesando los datos brutos. Hay cinco tipos de carpetas/archivos:
- En las carpetas "Letras_Sematos_lento", "Letras_Spread_Esqueletos", "Letras_Spread_lento", "Palabras_Spread_lento" y "Pruebas_A" hay vídeos de las carpetas de datos brutos a los que se les ha hecho alguna modificación: ralentizar y numerar los frames o añadir el esqueleto obtenido por algún modelo. Estos vídeos los usaba para obtener información de forma visual (en qué frame se hace el signo, si funciona bien el modelo...).
- En las carpetas "jsons", "results_2d" y "results_3d", y en los archivos "alphabet_landmarks_sematos.pkl" y "alphabet_landmarks_spread.pkl" tenemos los resultados de aplicar distintos modelos de Human Pose Estimation a vídeos. La información puede estar en formato JSON o en formato .pkl (Pickle en Python). El modelo que mejor parece funcionar es el ["skeleton_3d_uplift"](https://personalpages.surrey.ac.uk/r.bowden/publications/2023/IvashechkinSLTAT2023.pdf), sus resultados son los archivos .pkl, que además de directamente en la carpeta "Procesados", están en la carpeta "results_3d" ("skeleton_uplift.pkl) y, dentro de esta carpeta, en la carpeta "palabras".
- También están aquí distintos archivos de Blender en los que se define la armadura o hay animaciones creadas automáticamente.
- En el archivo "n_frames_signo_sematos.csv" están anotados (manualmente) los frames en los que se signa cada letra dentro de los vídeos de Sematos.
- En el archivo "explicacion_cuaderno_04.pdf" se trata de explicar el código del cuaderno de Jupyter 04 de la carpeta "Scripts".

### Publicaciones

Están el paper y el póster que hemos presentado.

### Scripts

