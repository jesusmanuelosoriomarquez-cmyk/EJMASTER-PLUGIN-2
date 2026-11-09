# EJ MASTER (VST3)

Plugin de mezcla y master automático para poner en el **Master** de FL Studio.
Interfaz verde. Cadena interna: filtro de subgraves → **corrección automática del beat (Auto-Fix)** → EQ del estilo → de-esser → compresor de cohesión → saturación suave → ancho estéreo (graves en mono) → volumen automático (LUFS) → limitador a -1 dB.

### Auto-Fix: arreglar el beat desde el Master

Mientras suena la canción, EJ MASTER mide la energía del beat en 8 bandas (60 Hz, 150 Hz, 350 Hz, 800 Hz, 1.8 kHz, 4 kHz, 8 kHz y 14 kHz), la compara con una curva objetivo según el estilo elegido y aplica una corrección lenta y suave (máximo -4 dB / +3 dB por banda). El panel central muestra en tiempo real cuánto está corrigiendo cada banda.

- Si el beat está oscuro, sube agudos; si está brillante o con mucho barro, los baja; si ya está equilibrado, casi no toca nada.
- La curva objetivo es una aproximación de un master moderno, no una verdad absoluta: si no te gusta cómo corrige, baja **AUTO-FIX** o cambia de estilo.

## Cómo obtener el .vst3 (GitHub lo compila por ti, gratis)

1. Crea una cuenta en https://github.com y un repositorio nuevo llamado `EJ-MASTER` (público o privado).
2. Sube **todo el contenido de esta carpeta** al repositorio (botón *Add file → Upload files*).
   - Importante: debe quedar el archivo `.github/workflows/build.yml`. Si GitHub no sube la carpeta `.github`, créalo a mano: *Add file → Create new file*, escribe el nombre `.github/workflows/build.yml` y pega el contenido del archivo.
3. Entra a la pestaña **Actions**. La compilación empieza sola (tarda unos 10–15 minutos la primera vez). Si no empieza: *Compilar EJ MASTER → Run workflow*.
4. Cuando salga la marca verde, abre esa ejecución y baja el archivo **EJ-MASTER-VST3-Windows** (sección *Artifacts*). Descomprímelo: dentro está `EJ MASTER.vst3`.

## Instalar en FL Studio (Windows)

1. Copia `EJ MASTER.vst3` a `C:\Program Files\Common Files\VST3\`
2. En FL Studio: *Options → Manage plugins → Find installed plugins* (con "Verify plugins" activado).
3. Abre el Mixer, selecciona **Master**, y en una ranura de efectos elige *EJ MASTER* (aparece en la lista de plugins instalados / "Verified").

## Cómo usarlo

- **Auto-Fix**: cuánto corrige el balance de graves/medios/agudos del beat (0 % = no corrige, 60 % por defecto).
- **Estilo**: Equilibrado, Trap / Hip-Hop, Pop / Voz o Suave (define la curva objetivo).
- **Intensidad**: cuánto trabaja el EQ, el compresor y la saturación.
- **Brillo**: más o menos aire en agudos (±3 dB).
- **Ancho**: abre o cierra el estéreo (los graves siempre quedan en mono).
- **De-esser**: reduce las "eses" agresivas de la voz.
- **Volumen**: volumen final objetivo en LUFS (-14 es el estándar de streaming; -9 suena más fuerte).

## Cosas que debes saber

- El plugin va en el Master, así que trabaja sobre la mezcla completa (beat + voz juntos). No puede separar la voz del beat ni arreglar una mezcla mala: si la voz está muy baja, un sonido está desafinado o el beat distorsiona antes de llegar al Master, eso debes corregirlo en cada pista. Auto-Fix corrige el balance general de frecuencias, no instrumentos individuales.
- El código se probó solo en cuanto a que compila contra JUCE y con espectros de prueba simulados; todavía no se ha escuchado con música real. Las curvas objetivo son estimaciones y probablemente haya que afinarlas con tus oídos.
- Para mejores resultados deja el Master con margen: que los picos lleguen a unos -6 dB antes del plugin.
- El volumen automático tarda unos segundos en ajustarse al empezar a sonar la canción.
- El techo es -1 dB de pico de muestra; no mide true-peak, así que al exportar revisa con un medidor si la plataforma es muy estricta.
- Los plugins sin firma digital pueden mostrar avisos de Windows SmartScreen; es normal en plugins hechos por uno mismo.
