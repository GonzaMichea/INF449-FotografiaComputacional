# Tarea 3 — Muestreo Comprimido: Análisis de Escasez


## Requisitos

- Python 3.9+
- Librerías:

```bash
pip install numpy scikit-image scipy PyWavelets matplotlib
```

## Cómo ejecutar

1. Abrir `tarea3.ipynb` en Jupyter Notebook, JupyterLab o VS Code.
2. Ejecutar todas las celdas en orden (`Run All`). No requiere archivos externos: la imagen `astronaut` se descarga automáticamente la primera vez mediante `imageio`.
3. El notebook genera, en orden:
   - Carga de la imagen y conversión a escala de grises (`x`).
   - Transformaciones Wavelet-2D (`db4`, 3 niveles) y DCT-2D.
   - Gráfico de los coeficientes ordenados por magnitud (dispersión).
   - Función `delete_coeff` para conservar solo el `P%` de mayores coeficientes.
   - Reconstrucciones para `P = 5%, 10%, 20%, 50%` en ambas bases.
   - Tabla y comparación visual de PSNR entre imagen original y reconstruida.

