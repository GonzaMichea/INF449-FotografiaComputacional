# Tarea 1 — Arreglo de Filtros de Bayer e Interpolación (Demosaicking)

## Descripción

Implementación de un sistema de fotografía computacional de color: se simula la etapa de muestreo mediante un arreglo de filtros de Bayer (patrón RGGB) y se reconstruye la imagen a color (*demosaicking*) mediante tres algoritmos de interpolación 2D:

- **Bilineal** — núcleos de convolución clásicos (3×3).
- **Bicúbico** — convolución cúbica normalizada (compensa la mayor densidad de muestras del canal G).
- **Malvar-He-Cutler (2004)** *(bonus)* — filtro lineal de 5×5 que corrige la interpolación bilineal usando el gradiente del canal conocido en cada píxel ([Malvar, He & Cutler, ICASSP 2004](https://ieeexplore.ieee.org/document/1326587)).

El sistema se evaluó sobre las 24 imágenes del [Kodak Lossless True Color Image Suite](https://github.com/MohamedBakrAli/Kodak-Lossless-True-Color-Image-Suite), usando las métricas PSNR, SSIM y SAM.

## Estructura de la carpeta

```
Tarea1/
├── informe/
│   ├── informe.tex          # Informe en LaTeX
│   ├── Referencias.bib      # Bibliografía
│   ├── Fig/                 # Figuras usadas en el informe
│   └── informe.pdf          # Informe compilado
├── notebook/
│   ├── tarea1.ipynb         # Notebook con la implementación completa
│   ├── dataset/              # Imágenes Kodak (descargadas por el notebook, no versionadas)
│   ├── resultados/           # Métricas y figuras: bilineal + bicúbico
│   └── resultados_bonus/     # Métricas y figuras: bilineal + bicúbico + Malvar-He-Cutler
└── README.md
```

## Ejecución

1. Instalar dependencias:
   ```bash
   pip install numpy opencv-python scikit-image pandas matplotlib
   ```
2. Abrir `notebook/tarea1.ipynb` y ejecutar las celdas en orden. La primera celda de descarga genera automáticamente la carpeta `dataset/` con las 24 imágenes Kodak.
3. Al finalizar, se generan en `resultados/` y `resultados_bonus/`:
   - `metricas_por_imagen.csv` — PSNR, SSIM y SAM por imagen y método.
   - `metricas_resumen.csv` — media ± desviación estándar por método.
   - `comparativo_XX.png` — figuras comparativas (recorte central) por imagen.
4. El informe en `informe/informe.tex` se compila con `pdflatex` + `bibtex` (dos pasadas de `pdflatex` después de `bibtex`), aunque incluye pdf.

## Resultados

Media ± desviación estándar sobre las 24 imágenes del dataset Kodak:

| Método | PSNR (dB) | SSIM | SAM (°) |
|---|---|---|---|
| Bilineal | 29.21 ± 2.75 | 0.891 ± 0.040 | 2.509 ± 1.031 |
| Bicúbico (conv. normalizada) | 29.19 ± 2.95 | 0.881 ± 0.046 | 2.312 ± 0.988 |
| **Malvar-He-Cutler (bonus)** | **35.36 ± 2.95** | **0.969 ± 0.008** | **1.697 ± 0.690** |

El filtro de Malvar-He-Cutler supera en más de 6 dB de PSNR a los métodos bilineal y bicúbico, y reduce notablemente el efecto *zipper* y el falso color característicos de la interpolación simple en bordes de alta frecuencia. El detalle completo del análisis está en `informe/informe.pdf`.

## Notas

- La carpeta `dataset/` no se versiona en el repositorio (son ~40 MB de imágenes públicas fácilmente reproducibles al correr el notebook); ver `.gitignore`.
- Cualquier intento de copia o fraude anula el trabajo, según las bases de la tarea.