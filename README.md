# EnglishSpeaker

Aplicación Android (Kotlin + Jetpack Compose + Material 3) para practicar
vocabulario, pronunciación y tiempos verbales en inglés.

## Stack técnico

- Kotlin 1.9.24
- Android Gradle Plugin 8.5.2 / Gradle 8.7
- compileSdk 34 · minSdk 24 · targetSdk 34
- Jetpack Compose (BOM 2024.09.00) + Material 3
- Navigation Compose 2.7.7
- Room 2.6.1 (KAPT)
- Hilt 2.51.1
- Coroutines + Flow
- Android TextToSpeech, SpeechRecognizer, MediaRecorder/MediaPlayer

## Arquitectura

```
data/          -> entidades Room, DAOs, repositorios, importador/exportador SQL
domain/        -> modelos y utilidades de dominio (Levenshtein, comparador de respuestas)
presentation/  -> pantallas Compose + ViewModels (MVVM), por feature
di/            -> módulos Hilt
tts/           -> Text-to-Speech
speech/        -> SpeechRecognizer (versión básica)
audio/         -> grabación y reproducción de pronunciaciones
```

## Funcionalidades principales

- Gestión de vocabulario (crear/editar/eliminar/buscar) con tags N-N.
- Text-to-Speech configurable (en-US / en-GB, velocidad, tono).
- Quiz con 4 modos (Escuchar→Escribir, Español→Inglés, Inglés→Escribir,
  Mostrar respuesta→Escribir) y feedback específico basado en distancia de
  Levenshtein (letras faltantes, sobrantes o incorrectas).
- Historial de intentos y estadísticas (aciertos, errores, palabras más
  difíciles).
- Sección "Mi pronunciación": grabación y reproducción de intentos del
  usuario por palabra.
- Importación/exportación de vocabulario en el formato propio
  `.vocab.sql` (ver `FORMATO_SQL.md`), con resumen de importación.
- Preparado para reconocimiento de voz básico (SpeechRecognizer).

## Cómo compilar

```bash
cd EnglishSpeaker
./gradlew assembleDebug
```

El APK de debug queda en `app/build/outputs/apk/debug/app-debug.apk`.

Si `./gradlew` no existe todavía (el Gradle Wrapper no pudo generarse
automáticamente al crear el proyecto), instala Gradle o simplemente abre
el proyecto en Android Studio: el IDE genera y sincroniza el wrapper
automáticamente al abrir.

## Tests

- Unitarios (`app/src/test`): Levenshtein, comparador de respuestas, parser SQL.
- Instrumentados (`app/src/androidTest`): operaciones básicas del repositorio con Room en memoria.

```bash
./gradlew test
./gradlew connectedAndroidTest   # requiere un emulador/dispositivo conectado
```

## Datos de ejemplo

`sample_vocabulary.sql` contiene un pequeño set de palabras, tags y
relaciones en el formato documentado en `FORMATO_SQL.md`, listo para
importarse desde la pantalla de Vocabulario (menú ⋮ → "Importar SQL").
# English-Speaker
