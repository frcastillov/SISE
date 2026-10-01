# Registro de Pruebas y Correcciones

| Dispositivo / Condición | Resultado                          | Evidencia / Ruta                    |
| :---------------------- | :--------------------------------- | :---------------------------------- |
| Mobile (320px)          | Sin desbordamiento horizontal.     | `docs/capturas/320px.png`           |
| Tablet (768px)          | Menú adaptado, grid de 2 columnas. | `docs/capturas/768px.png`           |
| Desktop (1440px)        | Contenido centrado y ajustado.     | `docs/capturas/1440px.png`          |
| Foco visible            | Navegación por TAB funciona.       | `docs/evidencias/foco.png`          |
| Formulario Inválido     | Bordes rojos, impide envío.        | `docs/evidencias/form-novalido.png` |
| Formulario Válido       | Bordes verdes, simulación exitosa. | `docs/evidencias/form-valido.png`   |

## Correcciones aplicadas durante el desarrollo

1. **Problema:** La tabla de "Estados" causaba desbordamiento horizontal (scroll en toda la página) en 320px.
   - **Corrección:** Se encapsuló la tabla en un `<div class="table-responsive">` con `overflow-x: auto;`.
2. **Problema:** La etiqueta `skip-link` interfería con el diseño al usar el tabulador inicialmente.
   - **Corrección:** Se ajustó el CSS para asegurar que tenga un `z-index` alto y fondo contrastante solo al recibir `:focus`.
