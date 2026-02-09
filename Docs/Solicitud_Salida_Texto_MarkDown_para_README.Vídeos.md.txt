20260209101413*

Solicitud_Salida_Texto_MarkDown_para_README.Vídeos.md.txt

Hola Gemini.
Tengo que entregar lo que tengo.
Creo que se ha producido un error en vscode.
Creo que debo notificar dicho error.
Para documentar he grabado la pantalla con: 
OBS Studio
32.0.2 (64 bit)
He eliminado el audio y he dividido el Vídeo en fragmentos de unos 100MB.
Para ello he usado:
https://www.google.com/search?q=como+dividir+un+video+de+3+GB+partes+de+100+MB+con+vlc+en+linea+de+comandos&newwindow=1&sca_esv=01e84e26bfa42c3c&rlz=1C1ONGR_esES1190ES1190&sxsrf=ANbL-n7D-gH044EGEiL9VUEEFZOx1NEK2A%3A1770479168618&ei=QF6HafCnJYWpkdUP_uaH2Qo&biw=1280&bih=499&ved=2ahUKEwjo-r2L3ceSAxXzKvsDHUZaN7YQ0NsOegQIAxAB&uact=5&sclient=gws-wiz-serp&udm=50&fbs=ADc_l-bpk8W4E-qsVlOvbGJcDwpnWL6Swv3cGYGr8GhrqffhqWQeKrzHXR8CrIbqBEGtaz2oeuogojn39yKgn18EXMkpIfKk4ahPgQj76TT6z2x7oS_spQa3RClEj-w68ZaOjsx0LdgBQE-RiADEFOMu1EwUBkFJLWol7ii1AUaal9Zf9pqEhT5kwCiUm3HXMJ5x5ZbZ8wJt&aep=10&ntc=1&mtid=316Had3xKd7X7M8P1aSn8Qo&mstk=AUtExfDKjjjLEkGPbPttkswTEFsc5mHVgjs9dhzIEPSeKiqxMw-1WQkMVX3ldspACfT53RJ77horBraQ0HJd8yAt6RwYSU8yHNklrFOJ8VSjYMuAffO_CUblaMrUtxX62tduOw0Q9aHIBsOwD9J0srzs5pn4D6UKYVPG3yQL4Xgj4t7-k61mjoaEUeLsCUISW2WccJhge4kH_6N3qL4vzpHqISkYw1FjjYVXvGbol-jQvXdlIPBb7JxsYN3jlm-B_HPueMK-tBNIb15OK0YV8lAawG6NZwa9VFCe3XjEngZS7jczFhXrSlxiErGifQSJZjMunSSX7FnFTOSziQ&csuir=1

Gracias a Google Search en modo IA.

powershell
winget install "FFmpeg (Essentials Build)"

https://github.com/GyanD/codexffmpeg/releases/download/8.0.1/ffmpeg-8.0.1-essentials_build.zip

Eliminación del audio:
ffmpeg -i "2026-02-04_21-46-08.mp4" -c:v copy -an "2026-02-04_21-46-08.A0.mp4"

DEterminación de la duración del vídeo.
ffprobe 2026-02-04_21-46-08.A0.mp4

Estimación de tamaño:
¡Ojo con este detalle! Tu video dura 21 horas y 56 minutos (21:56:32), pero solo pesa 735 MB. Esto significa que tiene un bitrate bajísimo (74 kb/s).
Si lo divides por tiempo usando fragmentos de 2 minutos como hablábamos antes, ¡te saldrán cientos de archivos de menos de 1 MB!
Para que cada trozo pese aproximadamente 100 MB, debemos dividir el tiempo total (79,000 segundos) entre 7 partes. Eso nos da unos 11,300 segundos por parte.


División en fragmentos de unos 100MB.
ffmpeg -i "2026-02-04_21-46-08.A0.mp4" -c copy -f segment -segment_time 11300 -reset_timestamps 1 "2026-02-04_21-46-08.A1_%03d.mp4"

20260207173201*

Un último consejo: Si alguna vez necesitas volver a unir estos fragmentos en un solo video sin perder calidad, puedes usar el Demuxer de concatenación de FFmpeg creando un archivo de texto con la lista de archivos.

20260207182829*
También he empleado VLC (ojo se ha actualizado después de la eliminación del audio), versión VLC actual:
Reproductor multimedia VLC
3.0.23 Vetinari
Versión VLC antigua:
videolan@runner-sgapdqg-project-435-concurrent-1 Jun 8 2024 21:22:44
de los dos primeros Videos (mp4).
La lista de los Vídeos .mp4 es:
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-43-07.A0.mp4	142.950	2026-02-06 12.49	-a--
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-44-22.A0.mp4	1.098.923	2026-02-06 12.52	-a--
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-46-08.A1_000.mp4	104.077.009	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-46-08.A1_001.mp4	103.766.634	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-46-08.A1_002.mp4	103.770.004	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-46-08.A1_003.mp4	103.860.807	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-46-08.A1_004.mp4	104.000.577	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-46-08.A1_005.mp4	106.956.027	2026-02-07 17.20	-a--
c:\Users\Coder\Proyectos\EDA\Docs\2026-02-04_21-46-08.A1_006.mp4	109.553.388	2026-02-07 17.20	-a--
Creo que debo subir esto para poder indicar la existencia de este error, debido al cual el retraso.
Creo que este tipo de error al intentar importar las librerías de Python para Jupyter Notebooks en vscode es lo suficientemente importante como para realizar esta serie de acciones y que deberían ser reportadas a Microsoft, Google y a quien corresponda.
Las siguientes opciones que realizar serían subir esto a un repositorio de github en el que se incluya todo este material.
¿Puedes darme la secuencia de acciones y comandos git para subir los archivos?.
Por favor incluye las instrucciones para crear el nuevo repositorio en git desde
https://github.com/new
He pensado que un nombre adecuado podría ser:
EDA_JJ_202602061342V
Con esto estoy creando un repositorio específico para la notificación de lo que creo que puede ser un error.
En caso de que sea necesario, permitiría poder eliminarlo (todo el repositorio) sin afectar a otras contribuciones.
Aquí estoy practicando también con vídeos para poder dar trazabilidad en imagen y tiempo al posible error.
No poseo los medios, pero creo que una IA debería poder procesar los vídeos que subo y obtener información relevante.

20260209101542*