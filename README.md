# Ecosystem_Safeguard_app

> Detección automática de ganado bovino en imágenes aéreas de dron, con geolocalización GPS y exportación de resultados.

Desarrollado por **EPICS IEEE** como herramienta de monitoreo ambiental y ganadero. Permite procesar lotes de imágenes capturadas desde drones, detectar presencia de ganado usando un modelo YOLO entrenado, visualizar los resultados anotados y ubicarlos en un mapa interactivo a partir de los metadatos GPS de cada imagen.

---

## Tabla de contenidos

- [Características](#características)
- [Capturas de pantalla](#capturas-de-pantalla)
- [Requisitos del sistema](#requisitos-del-sistema)
- [Instalación](#instalación)
- [Uso](#uso)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Desarrollo y compilación](#desarrollo-y-compilación)
- [Entorno Conda](#entorno-conda)

---

## Características

- **Detección con IA** — modelo YOLO entrenado específicamente para ganado bovino en imágenes aéreas
- **Procesamiento por lotes** — analiza carpetas completas de imágenes en un solo paso
- **Extracción de GPS** — lee coordenadas lat/lon/altitud directamente de los metadatos EXIF de cada imagen
- **Vista de inspección** — navega imagen por imagen con bounding boxes y mapa de ubicación individual
- **Resumen de sesión** — conteo total de imágenes procesadas, animales detectados y mapa global con clustering
- **Exportación** — genera imágenes anotadas, CSV con coordenadas y manifest JSON
- **Soporte GPU/CPU** — usa CUDA automáticamente si está disponible, con fallback a CPU

---

## Requisitos del sistema

| Requisito | Versión |
|-----------|---------|
| Windows | 10 / 11 (64-bit) |
| Python | 3.10 |
| CUDA (opcional) | 12.1 (para aceleración GPU) |

---

## Instalación

### Opción 1 — Instalador (recomendado)

1. Descargar `EcosystemSafeguard_Setup_0.1.0.exe` desde la carpeta `Installer/installer_out/`
2. Ejecutar el instalador como administrador
3. Abrir **Ecosystem Safeguard** desde el acceso directo en el escritorio

### Opción 2 — Desde el código fuente

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/ecosystem-safeguard.git
cd ecosystem-safeguard

# 2. Crear el entorno conda
conda env create -f epics-ieee.yaml
conda activate epics-ieee

# 3. Ejecutar la aplicación
python gui_app.py
```

---

## Uso

1. **Seleccionar carpeta** — usar el botón **Browse Folder** para elegir la carpeta con las imágenes del dron (`.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.webp`)
2. **Iniciar procesamiento** — clic en **Start Processing**; la barra de progreso muestra el avance imagen por imagen
3. **Inspeccionar resultados** — la vista de inspección muestra cada imagen con los bounding boxes del ganado detectado y su ubicación en el mapa
4. **Ver resumen** — clic en **View Summary Report** para ver el conteo total y el mapa global con todos los puntos detectados
5. **Exportar** — clic en **Export Data to Folder...** para guardar las imágenes anotadas, el CSV y los archivos de resultados en la carpeta destino que elijas

> Los resultados intermedios se guardan en `%LOCALAPPDATA%\EcosystemSafeguard\output\`

---

## Estructura del proyecto

```
Ecosystem-Safeguard/
├── gui_app.py                  # Interfaz gráfica (PyQt6)
├── detector_ganado.py          # Motor de detección (YOLO + GPS)
├── models/
│   └── best.pt                 # Modelo entrenado
├── assets/
│   ├── app.ico                 # Ícono de la aplicación
│   └── branding/               # Logos institucionales
├── Installer/
│   └── EcosystemSafeguard.iss  # Script de Inno Setup
├── EcosystemSafeguard.spec     # Configuración de PyInstaller
├── epics-ieee.yaml             # Entorno Conda reproducible
└── Manual_de_usuario.pdf       # Manual de usuario
```

---

## Desarrollo y compilación

### Compilar el ejecutable

```bash
conda activate epics-ieee
pyinstaller EcosystemSafeguard.spec
```

Esto genera la carpeta `dist/EcosystemSafeguard/` con todos los archivos necesarios.

### Generar el instalador

1. Abrir `Installer/EcosystemSafeguard.iss` en **Inno Setup Compiler**
2. Presionar `Ctrl+F9`
3. El instalador se genera en `Installer/installer_out/EcosystemSafeguard_Setup_0.1.0.exe`

---

## Entorno Conda

El archivo `epics-ieee.yaml` incluye todas las dependencias necesarias:

| Paquete | Versión | Uso |
|---------|---------|-----|
| `pytorch` | 2.5.1 + CUDA 12.1 | Backend de inferencia |
| `ultralytics` | 8.3.225 | Framework YOLO |
| `opencv-python` | 4.12.0 | Procesamiento de imágenes |
| `pillow` | 11.1.0 | Lectura de metadatos EXIF |
| `PyQt6` | — | Interfaz gráfica |
| `folium` | — | Mapas interactivos |

Para recrear el entorno en otra máquina:

```bash
conda env create -f epics-ieee.yaml
conda activate epics-ieee
```

---

## Logs de depuración

Si la aplicación falla, los logs se guardan automáticamente en:

```
%LOCALAPPDATA%\EcosystemSafeguard\
├── trace.log     # Trazabilidad paso a paso
├── stderr.log    # Errores de Python y crashes nativos
└── crash.log     # Traceback completo
```

---

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
