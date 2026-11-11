# Updepth: profundidad, upscale, subtítulos y promos en tu ordenador

Una ventana con cuatro herramientas: **mapas de profundidad** (Depth Anything V2), **upscale** de imágenes y vídeos, **subtítulos** con transcripción de voz (.srt, .txt y vídeo con subtítulos estilo TikTok) y **promo** (vídeos para anuncios con portada, fondo, audio y texto). Todo se ejecuta en tu propio ordenador, sin subir nada a internet.

## Descarga

| Tu ordenador | Descarga |
|---|---|
| **Mac** con Apple Silicon (M1 o más nuevo) | [`Updepth-Mac.zip`](https://github.com/martamakes/updepth/releases/latest/download/Updepth-Mac.zip) |
| **Windows** 10 u 11 (64 bits) | [`Updepth-Windows.zip`](https://github.com/martamakes/updepth/releases/latest/download/Updepth-Windows.zip) |

Necesitas internet durante la instalación (unos 3 GB de descargas; unos 5,5 GB si tienes tarjeta NVIDIA). Incluye el modelo de voz para subtítulos (~480 MB).

## Instalar

### Mac
1. Descomprime el zip.
2. Haz doble clic en `Install Depth Anything.command`.
   Si macOS dice que no se puede abrir (por ser de un desarrollador no identificado): abre **Ajustes del Sistema → Privacidad y seguridad**, baja hasta la sección **Seguridad**, pulsa **Abrir igualmente** junto al aviso del instalador y escribe tu contraseña. Después vuelve a abrir el instalador.
3. Espera a ver `All done!` (unos minutos la primera vez).

### Windows
1. Descomprime el zip (haz clic derecho → *Extraer todo*; no ejecutes desde dentro del zip).
2. Haz clic derecho en `Install Depth Anything.bat` → **Ejecutar como administrador** (así evitas problemas de permisos).
   Si sale *"Windows protegió su PC"*: **Más información → Ejecutar de todas formas**.
3. Si pide permiso para instalar *Microsoft Visual C++*, acepta.
4. Espera a ver `All done!` (unos minutos la primera vez).

## Usar

Abre **Updepth** (icono naranja con flecha) desde el Escritorio: se abre una ventana con cuatro pestañas. Arrastra archivos a la lista (o usa *Añadir archivos / carpeta*) y pulsa el botón. El resultado se guarda junto al original, y al terminar el botón **Abrir carpeta** (abajo a la derecha) te enseña dónde ha quedado.

**Mapa de profundidad** (imágenes y vídeos):

| Entrada | Salida |
|---|---|
| `foto.jpg` | `foto_depth.png` |
| `clip.mov` | `clip_depth.mp4` |

**Upscale:**

| Modo | Sirve para | Salida |
|---|---|---|
| x2 / x4 / 720p / 1080p / 1440p (ffmpeg) | imágenes y vídeos (conserva el audio) | `clip_ffmpeg_1080p.mp4` |

**Subtítulos** (vídeos y audios): transcribe la voz en tu ordenador (Whisper, vía faster-whisper) y genera subtítulos.

| Entrada | Salida |
|---|---|
| `clip.mp4` | `clip.srt`, `clip.txt` y `clip_subs.mp4` (subtítulos quemados estilo TikTok) |
| `nota.mp3` | `nota.srt` y `nota.txt` |

Opciones:

- **Palabras por bloque:** por defecto salen **de una en una** (1-5), porque fija más la atención.
- **Estilo:** mayúsculas, fuente Anton, contorno negro, color de resaltado a elegir y posición abajo o centro. El texto queda por encima de los botones de TikTok.
- **Modelo:** base (~145 MB), small (~480 MB, por defecto, se descarga al instalar) o turbo (~1,6 GB, se descarga al primer uso).
- **Idioma:** automático o a elegir.
- **Es una canción:** usa el modelo turbo, desactiva el filtro de voz y evita repeticiones en los estribillos. Con música Whisper falla más: la letra puede salir incompleta y los tiempos por palabra pueden desfasarse.

**Promo** (vídeos para anuncios, por ejemplo Meta Ads): pon la portada centrada sobre una imagen o vídeo de fondo, con el audio que elijas.

| Entrada | Salida |
|---|---|
| `portada.png` + audio (mp3/wav…) + fondo | `portada_promo_9x16.mp4` (también 4:5 y 1:1) |

- **Fondo:** una imagen o un vídeo (si es vídeo, se repite hasta cubrir el audio). Rellena todo el cuadro.
- **Duración:** la del audio.
- **Hook (opcional):** texto de varias filas, con emojis, arriba y centrado, para que no se solape con los subtítulos de abajo. Las banderas y emojis combinados pueden no salir.
- La app recuerda el último audio, fondo, formato y hook.

Funciona en CPU (sin GPU).

## Notas

- Usa el modelo **Depth Anything V2 Small** (licencia Apache-2.0, válido para uso comercial).
- El vídeo se procesa fotograma a fotograma, así que puede haber parpadeo de brillo entre fotogramas.
- La transcripción usa **Whisper** (licencia MIT) mediante faster-whisper, y la fuente **Anton** tiene licencia OFL (`fonts/OFL.txt`).
- Todo se instala en la carpeta `DepthAnything` de tu usuario. Para desinstalar, borra esa carpeta y el acceso directo del Escritorio.
- **Windows sin tarjeta NVIDIA:** funciona en CPU, pero es lento (sobre todo con vídeo). Con NVIDIA usa la GPU automáticamente; si avisa de que no puede, actualiza el driver de NVIDIA y vuelve a ejecutar el instalador.

## Problemas frecuentes

- **Falla la descarga o la instalación:** suele ser la red (proxy o firewall del centro) bloqueando `astral.sh`, `github.com`, `download.pytorch.org` o `huggingface.co`. Prueba desde otra red.
- **Windows: "PyTorch no arranca":** instala [Visual C++ Redistributable](https://aka.ms/vs/17/release/vc_redist.x64.exe), reinicia y vuelve a ejecutar el instalador.
- **No hay acceso directo en el Escritorio:** ejecuta directamente `DepthAnything\venv\Scripts\pythonw.exe DepthAnything\app.py` (Windows) o `~/DepthAnything/venv/bin/python ~/DepthAnything/app.py` (Mac).
