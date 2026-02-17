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
- Además, hay varias imágenes de esqueletos anotados en función del modelo de Human Pose Estimation (HPE) que se use y una imagen con números que usaba para numerar frames de vídeos.

En "Procesados" tenemos datos que hemos creado nosotr@s, en general, analizando y procesando los datos brutos. Hay cinco tipos de carpetas/archivos:
- En las carpetas "Letras_Sematos_lento", "Letras_Spread_Esqueletos", "Letras_Spread_lento", "Palabras_Spread_lento" y "Pruebas_A" hay vídeos de las carpetas de datos brutos a los que se les ha hecho alguna modificación: ralentizar y numerar los frames o añadir el esqueleto obtenido por algún modelo. Estos vídeos los usaba para obtener información de forma visual (en qué frame se hace el signo, si funciona bien el modelo...).
- En las carpetas "jsons", "results_2d" y "results_3d", y en los archivos "alphabet_landmarks_sematos.pkl" y "alphabet_landmarks_spread.pkl" tenemos los resultados de aplicar distintos modelos de HPE a vídeos. La información puede estar en formato JSON o en formato .pkl (Pickle en Python). El modelo que mejor parece funcionar es el ["skeleton_3d_uplift"](https://personalpages.surrey.ac.uk/r.bowden/publications/2023/IvashechkinSLTAT2023.pdf), sus resultados están en la carpeta "results_3d" ("skeleton_uplift.pkl) y, dentro de esta carpeta, en la carpeta "palabras".
- También están aquí distintos archivos de Blender en los que se define la armadura o hay animaciones creadas automáticamente.
- En el archivo "n_frames_signo_sematos.csv" están anotados (manualmente) los frames en los que se signa cada letra dentro de los vídeos de Sematos. El archivo "frame_letras_spread.txt" es análogo para los vídeos de Spreadthesign.
- En el archivo "explicacion_cuaderno_04.pdf" se trata de explicar el código del cuaderno de Jupyter 04 de la carpeta "Scripts".

### Publicaciones

Están el paper y el póster que hemos presentado.

### Scripts

En esta carpeta se encuentra todo el código escrito. Hay $15$ cuadernos de Jupyter numerados en función de cuando se crearon. Esto es, todo el proceso de desarrollo se puede seguir en los cuadernos. Los scripts de python recogen código de los cuadernos organizados para poder importarlos a otros cuadernos.
- Cuaderno $1$: Se define la función `tokenize_word`, que separa palabras escritas en castellano en sus letras, incluyendo "CH", "LL", "Ñ" y "RR". Esta función sirve para poder deletrear palabras en LSE.
- Cuaderno $2$: En este cuaderno se muestra como usar el modelo de 3D HPE [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/guide?hl=es-419) sobre vídeos. Se define una función (`try_setting`) para aplicar este modelo con diferentes configuraciones. Esta función se usó para crear los vídeos de la carpeta "Datos/Procesados/Pruebas_A". A continuación, se define la función `generate_skeleton` y `obtain_collection_dict_landmarks`, que en conjunto aplican el modelo MediaPipe y procesan los resultados para almacenarlos de una manera personalizada. Estas funciones se utilizaron para obtener los archivos "alphabet_landmarks_spread.pkl" y "alphabet_landmarks_sematos.pkl" en la carpeta "Datos/Procesados".
- Cuaderno $3$: En este cuaderno se crean los vídeos ralentizados y numerados de la carpeta "Datos/Procesados".
- Cuaderno $4$: Se definen funciones importantes como `pose2arm_position` y `arm_position2pose`. Estas funciones se explican en el PDF "explicacion_cuaderno_04.pdf", en la carpeta "Datos/Procesados". También se define la función `move_arms`, aunque finalmente no se usó.
- Cuadernos $5$: Se descarga el contenido de la carpeta "Datos/Brutos/Letras_Spread".
- Cuaderno $6$: Se usó para tratar de encontrar los frames de los vídeos de la carpeta "Datos/Brutos/Letras_Spread" en los que sucede la imagen asociada al vídeo.
- Cuaderno $7$: Se define la función `generate_armature`, que se usa para crear la armadura de Blender "avatar_armature.blend" de "Datos/Procesados". También se definen las funciones `move_arms_blender_v0` y `move_arms_blender_v1`, que se usaron para hacer pruebas de animaciones de la armadura.
- Cuaderno $8$: Similar al anterior, pero añadiendo manos a la armadura.
- Cuaderno $9$: En este cuaderno se comprobó que MediaPipe no daba buenos resultados en lo relativo a la profundidad, es decir, en la tercera dimensión del 3D HPE. Durante un breve periodo de tiempo se trató de mejorar los resultados sin éxito.
- Cuaderno $10$: La primera parte de este cuaderno es similar al cuaderno $8$, solo que reorganizando ideas. En la segunda parte se trabaja con los resultados obtenidos de aplicar el modelo "skeleton_3d_uplift" y se crean los archivos "abecedario_maksym.blend", "abecedario_maksym_filtered.blend", "LSEAvatar.blend" o "Pablo.blend" de la carpeta "Datos/Procesados". Para ello, se define la función "spell_word". A continuación, se crean también animaciones más complejas como "me_llamo_LSEAvatar.blend" o "video_Ceuta.blend".
- Cuaderno $11$: Información sobre modelos de HPE.
- Cuadernos $12$: Se probó a hacer las animaciones de Blender con otros modelos de 3D HPE.
- Cuaderno $13$: Se trató de entender el formato del modelo MotionBert.
- Cuaderno $14$: Como acercamiento a poder reconocer qué tipo de movimiento tiene un determinado signo (estático, oscilatorio...), se definieron varias funciones para trackear las muñecas a lo largo de un vídeo.
- `arm_movement_0.py` y `arm_movement.py`: Recopilación del código del cuaderno $4$.
- `blender.py`: Recopilación del código del cuaderno $10$.
- `config.py`: Proyecto de script con utilidades.