# Mapa UE — Guía rápida

**Sitio:** https://azullecaros.github.io/mapa-ue/

**Repo:** mapa-ue

**Datos:** `regiones_chile_centros.geojson`


## Esquema de datos por región
```json
{
  "type": "Feature",
  "properties": {
    "región": "Nombre",
    "manuales": 0,
    "maleta": 0,
    "mobilelab": 0
  },
  "geometry": { "type": "Point", "coordinates": [-70.0, -33.0] }
}
```
> **Ojo:** `región` lleva tilde. Las coordenadas son **[longitud, latitud]** (no al revés).

## Cómo actualizar cifras
1. Abrir `regiones_chile_centros.geojson` en el repo y pulsar **✏️ Edit this file**.
2. Cambiar los números de `manuales`, `maleta`, `mobilelab` (sin comillas).
3. **Commit** (p. ej. “update cifras 2025-08”).
4. Abrir https://azullecaros.github.io/mapa-ue/ y hacer **hard refresh** (⌘⇧R / Ctrl+F5).

### Forzar siempre la última versión (anti‑caché)
El `index.html` ya carga el GeoJSON con `?v=Date.now()` para evitar caché.

## Estilo / UI
- Fondo `#F1F1F1`; tierra `#C3C3C3` (base *light‑v11*).
- Círculos `#E2D2F6` sin borde. Número centrado `#201245`. Radio ∝ total.
- Popup con tres tarjetas (`#E2D2F6`, `#89ACDB`, `#A3D7DE`).
- Zoom **arriba‑derecha**. Atribución **compacta** abajo‑derecha.
- Toolbar **arriba‑izquierda**: “Solo con actividad” (default) / “Mostrar todo” (0 en gris sin número).
- Leyenda **abajo‑izquierda**: “Puntos grises: 0 casos” (solo en *Mostrar todo*).

## Estructura del repo
```
/ (root)
├── index.html
└── regiones_chile_centros.geojson
```

## Troubleshooting — GitHub Pages
### “pages build and deployment: All jobs were cancelled”
No es un error de código. Se canceló ese *run* porque:
- hiciste otro commit y el nuevo *run* canceló el anterior, o
- cambiaste la config de Pages/branch durante el build, o
- deshabilitaste y re‑habilitaste Pages.

**Qué hacer:**
1) Ir a **Actions → pages build and deployment** y abrir el *run* más reciente.  
   Si dice “_cancelled because a newer run started_”, ignóralo: el último *run* es el válido.  
2) En **Settings → Pages**, confirmar `Branch: main` y `/(root)` y guardar si cambiaste algo.  
3) Si no hay *run* “deployed”, haz un commit mínimo (p. ej. edita este README) para re‑disparar el build.  
4) Espera 30–60s y recarga el sitio. Si hace falta, pulsa **Re‑run jobs** en Actions.

### Página en blanco / 404
- Asegúrate de que `index.html` existe en la **raíz** del repo.
- Si la página abre pero el mapa no, abre **Console** (F12) y revisa errores de URL/CORS.

## Notas
- El token es público (`pk.`). No colocar tokens secretos de servidor en el front‑end.
- Mantener nombres de regiones consistentes (tildes, mayúsculas).
