# Reporte de Incidencia: Bloqueo en VS Code con Jupyter Notebooks

Este documento acompaña a la evidencia visual subida a este repositorio, demostrando un error crítico de rendimiento y ejecución al intentar trabajar con librerías de Python en Jupyter Notebooks dentro de Visual Studio Code.

## 📋 Descripción del Problema
Se ha detectado un retraso significativo y un comportamiento errático (bloqueo) al intentar importar librerías estándar de Data Science o iniciar el kernel, lo cual impide el desarrollo normal de la actividad.

## 🛠 Ficha Técnica de la Evidencia
Para documentar este error de forma transparente para su reporte a Microsoft/GitHub, se ha procedido de la siguiente manera:

* **Software de Grabación:** OBS Studio 32.0.2 (64 bit).
* **Procesamiento:** El vídeo original (aprox. 3 GB) ha sido procesado para eliminar el audio y dividirlo en partes manejables.
* **Herramienta de División:** Se utilizó **VLC** para el procesamiento de archivos mp4 pequeños.
* Para el archivo grande usé ffmpeg:
```Powershell
winget install "FFmpeg (Essentials Build)"
```

https://github.com/GyanD/codexffmpeg/releases/download/8.0.1/ffmpeg-8.0.1-essentials_build.zip

Comandos ffmpeg:

```sh
#Eliminación del audio:
ffmpeg -i "2026-02-04_21-46-08.mp4" -c:v copy -an "2026-02-04_21-46-08.A0.mp4"

#Determinación de la duración del vídeo.
ffprobe 2026-02-04_21-46-08.A0.mp4

#División en fragmentos de unos 100MB.
ffmpeg -i "2026-02-04_21-46-08.A0.mp4" -c copy -f segment -segment_time 11300 -reset_timestamps 1 "2026-02-04_21-46-08.A1_%03d.mp4"
```

Estimación de tamaño:
¡Ojo con este detalle! Tu video dura 21 horas y 56 minutos (21:56:32), pero solo pesa 735 MB. Esto significa que tiene un bitrate bajísimo (74 kb/s).
Si lo divides por tiempo usando fragmentos de 2 minutos como hablábamos antes, ¡te saldrán cientos de archivos de menos de 1 MB!
Para que cada trozo pese aproximadamente 100 MB, debemos dividir el tiempo total (79,000 segundos) entre 7 partes. Eso nos da unos 11,300 segundos por parte.


### 📂 Archivos de Vídeo Adjuntos
La secuencia completa de la reproducción del error se encuentra dividida en los siguientes fragmentos:

Listado de archivos:

```Text
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-43-07.A0.mp4	142.950	2026-02-06 12.49	-a--
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-44-22.A0.mp4	1.098.923	2026-02-06 12.52	-a--
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-46-08.A1_000.mp4	104.077.009	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-46-08.A1_001.mp4	103.766.634	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-46-08.A1_002.mp4	103.770.004	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-46-08.A1_003.mp4	103.860.807	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-46-08.A1_004.mp4	104.000.577	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-46-08.A1_005.mp4	106.956.027	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\2026-02-04_21-46-08.A1_006.mp4	109.553.388	2026-02-07 17.20	-a--
```

Un último consejo: Si alguna vez necesitas volver a unir estos fragmentos en un solo video sin perder calidad, puedes usar el Demuxer de concatenación de FFmpeg creando un archivo de texto con la lista de archivos.

Ver c:\Users\Coder\Proyectos\EDA_JJ_202602061342V\Docs\ProcesamientoVideo2026-02-04_21-46-08.mp4.txt	2.251	2026-02-07 18.28	-a--

Archivos Grandes:

| Archivo                          | Tamaño Aprox. | Descripción                                    |
| :------------------------------- | :------------ | :--------------------------------------------- |
| `2026-02-04_21-46-08.A1_001.mp4` | ~100 MB       | Inicio de la captura y reproducción del error. |
| `2026-02-04_21-46-08.A1_002.mp4` | ~100 MB       | Continuación de la incidencia.                 |
| `2026-02-04_21-46-08.A1_003.mp4` | ~100 MB       | Continuación de la incidencia.                 |
| `2026-02-04_21-46-08.A1_004.mp4` | ~104 MB       | Continuación de la incidencia.                 |
| `2026-02-04_21-46-08.A1_005.mp4` | ~106 MB       | Continuación de la incidencia.                 |
| `2026-02-04_21-46-08.A1_006.mp4` | ~109 MB       | Finalización de la captura.                    |

## 📢 Objetivo
El propósito de estos archivos es servir como reporte de *bug* para que la comunidad de desarrollo o los equipos técnicos de VS Code puedan analizar el comportamiento anómalo del entorno en ejecución local.

```bash
# 1. Iniciar el repositorio (si no lo has hecho ya)
git init

# 2. Instalar soporte para archivos grandes (LFS)
# Esto es OBLIGATORIO para tus archivos de 106MB y 109MB
git lfs install

# 3. Decirle a git que trate los mp4 como archivos grandes
# git lfs track "*.mp4"
git lfs track "./Docs/*.mp4"

# 4. Esto crea un archivo .gitattributes, hay que añadirlo
git add .gitattributes

# 5. Añadir el resto de archivos (tus videos y el README)
git add .
git status

# 6. Hacer el primer commit
# git commit -m "Subida de evidencia de error VS Code y README"
git commit -m "Intento de Trazablidad Error VS Code y jupyterNotebook.ipynb"

# 7. Renombrar la rama a main (estándar actual)
git branch -M main

# 8. Conectar con tu repositorio remoto
# SUSTITUYE "TU_USUARIO" por tu nombre real de GitHub
git remote add origin https://github.com/Bootcamp-IA-P6/EDA_JJ_202602061342V.git

# 9. Subir los archivos (esto tardará un poco por el tamaño de los videos)
git push -u origin main
```