# Gastos diarios (PWA)

App de una sola página para apuntar cada gasto en segundos (monto, categoría, nota y fecha) y ver
en qué se va el dinero: por día, por mes, por categoría y contra un presupuesto mensual opcional.
Funciona sin conexión y se instala en el iPhone como una app más. Los datos viven en el teléfono
(`localStorage`); la copia de seguridad es el JSON que exporta la pestaña Historial.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | Toda la app: estilos, categorías y lógica. |
| `manifest.webmanifest` | Nombre, ícono y colores con los que se instala. |
| `sw.js` | Service worker: guarda la app en caché para abrirla sin internet. |
| `icon-*.png` | Íconos (180 para iOS, 192/512 para Android/Chrome, maskable). |

## Cómo funciona

- **Registrar**: monto en pesos (se formatea solo), una de 12 categorías, nota opcional y fecha
  (por defecto hoy). Debajo aparece la lista del día con su total; tocar un gasto lo carga para
  **editarlo o eliminarlo**.
- **Historial**: por mes, agrupado por día con totales, con filtro por categoría. Desde aquí se
  exportan las copias (`.json` completa, `.csv` para Excel) y se restauran.
- **Resumen**: semana / mes / mes pasado / año → total, promedio por día, comparación con el
  período anterior equivalente, reparto por categoría, gráfica por día (o por mes) y los gastos
  más grandes. En "Mes" se puede definir un **presupuesto** y ver cuánto queda y cuánto se puede
  gastar por día hasta fin de mes.

## Publicación

- Repositorio: <https://github.com/JeanPollC/gastos>
- App publicada (GitHub Pages, rama `main`, raíz): **<https://jeanpollc.github.io/gastos/>**

Para publicar cambios basta con hacer commit y `git push`; Pages redepliega en 1–2 minutos.
Cada vez que cambies `index.html`, **sube el número de `CACHE` en `sw.js`** (`gastos-v2`, `v3`, …)
para que los teléfonos descarguen la versión nueva. La actualización se aplica en el siguiente
arranque de la app.

## Instalar en el iPhone

1. Abre la URL en **Safari** (no en Chrome ni desde un enlace dentro de otra app).
2. Botón **Compartir** → **Añadir a pantalla de inicio**.
3. Abre la app desde el ícono. La primera apertura necesita internet; después funciona sin conexión.

## Probar en local

```bash
python -m http.server 8766
```

y abrir <http://localhost:8766/>. El service worker solo se registra sobre `http(s)`, no al abrir el archivo directamente.
