# Ecosystem_Safeguard_app

> Detección automática de ganado bovino en imágenes aéreas de dron, con geolocalización GPS y exportación de resultados.

Desarrollado por **EPICS IEEE** como herramienta de monitoreo ambiental y ganadero. Permite procesar lotes de imágenes capturadas desde drones, detectar presencia de ganado usando un modelo de visión por computador entrenado, visualizar los resultados anotados y ubicarlos en un mapa interactivo a partir de los metadatos GPS de cada imagen.

---

## Tabla de contenidos

- [Características](#características)
- [Requisitos del sistema](#requisitos-del-sistema)
- [Instalación](#instalación)
- [Uso](#uso)
- [Resultados generados](#resultados-generados)
- [Documentación](#documentación)

---

## Características

- **Detección con IA** — modelo entrenado específicamente para ganado bovino en imágenes aéreas
- **Procesamiento por lotes** — analiza carpetas completas de imágenes en un solo paso
- **Extracción de GPS** — lee coordenadas lat/lon/altitud directamente de los metadatos EXIF de cada imagen
- **Vista de inspección** — navega imagen por imagen con bounding boxes y mapa de ubicación individual
- **Resumen de sesión** — conteo total de imágenes procesadas, animales detectados y mapa global con clustering
- **Exportación** — genera imágenes anotadas, CSV con coordenadas y manifest JSON

---

## Requisitos del sistema

| Requisito | Detalle |
|-----------|---------|
| Sistema operativo | Windows 10 / 11 (64-bit) |
| GPU  | NVIDIA con soporte CUDA 12.1 |

---

## Instalación

1. Ejecutar `EcosystemSafeguard_Setup_0.1.0.exe` como administrador
2. Seguir los pasos del instalador
3. Abrir **Ecosystem Safeguard** desde el acceso directo en el escritorio

---

## Uso

1. **Seleccionar carpeta** — usar **Browse Folder** para elegir la carpeta con las imágenes del dron (`.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.webp`)
2. **Iniciar procesamiento** — clic en **Start Processing**; la barra de progreso muestra el avance imagen por imagen
3. **Inspeccionar resultados** — navega por cada imagen con los bounding boxes del ganado detectado y su ubicación en el mapa
4. **Ver resumen** — clic en **View Summary Report** para el conteo total y el mapa global con todos los puntos detectados
5. **Exportar** — clic en **Export Data to Folder...** para guardar los resultados en la carpeta que elijas

Para instrucciones detalladas con capturas de pantalla, consultar el [Manual de Usuario](Manual_de_usuario_Ecosystem_Safeguard_App.pdf).

---

## Resultados generados

Los resultados se guardan en `%LOCALAPPDATA%\EcosystemSafeguard\output\` y al exportar contienen:

| Archivo / Carpeta | Descripción |
|-------------------|-------------|
| `boxes/` | Imágenes anotadas con bounding boxes |
| `originales/` | Copia de las imágenes originales con detecciones |
| `cattle_points.csv` | Coordenadas GPS y conteo de detecciones por imagen |
| `cattle_detection_manifest.json` | Resumen completo de la sesión en formato JSON |

---

## Documentación

- [Manual de Usuario](Manual_de_usuario_Ecosystem_Safeguard_App.pdf) — guía completa de uso de la aplicación

---

*Desarrollado por EPICS IEEE*

## Agradecimientos
Desarrollado con apoyo de:
- Universidad de La Sabana
- EPICS in IEEE
- Alcaldía de Sopó

## Autores
- Luis Alejandro Gonzales Guevara
- Juan Sebastian Ulloa Mejia
- Maria Juliana Amezquita Herrera
- Jorge Castellanos Rivilla
- David Felipe Celeita Rodriguez
- Universidad de La Sabana
- EPICS IEEE
- Alcaldía de Sopó
