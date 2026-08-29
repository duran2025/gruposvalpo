# Encuentra tu Grupo Scout — Valparaíso

Página estática de un solo archivo (`index.html`) con un mapa interactivo (Leaflet + OpenStreetMap/CARTO) que ubica los grupos scout de Valparaíso. No necesita backend ni base de datos.

## 1. Subir a GitHub

```bash
git init
git add index.html README.md banner.png flyers
git commit -m "Mapa de grupos scout de Valparaíso"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/TU-REPO.git
git push -u origin main
```

## 2. Desplegar en Render

1. Entra a [render.com](https://render.com) y crea un **New + → Static Site**.
2. Conecta tu cuenta de GitHub y selecciona este repositorio.
3. Configuración:
   - **Build Command:** (déjalo vacío, no hay build)
   - **Publish directory:** `.` (la raíz del repo)
4. Haz clic en **Create Static Site**. Render te dará una URL tipo `https://tu-sitio.onrender.com`.

Cada vez que hagas `git push` a `main`, Render vuelve a publicar la página automáticamente.

## Editar los grupos scout

Todos los datos (nombre, colegio/sede, coordenadas y link de Instagram/Facebook) están en un arreglo `grupos` al final de `index.html`, fácil de editar:

```js
const grupos = [
  { nombre: "...", lugar: "...", lat: ..., lng: ..., social: { tipo: "instagram", url: "..." } },
  ...
];
```

## Notas de esta versión

- **Popup = flyer + botón de red social:** al tocar un pin, el mapa ya no muestra una tarjeta con texto — muestra directamente el afiche (flyer) del grupo, con un botón "Ver en Instagram/Facebook" debajo. Las imágenes están en la carpeta `flyers/` (`car.jpg`, `blascuevas.jpg`, `antumanke.jpg`, `gaspar.jpg`, `aquitania.jpg`). Para actualizar un afiche, reemplaza el archivo correspondiente manteniendo el mismo nombre.

- **Encabezado con banner oficial:** el header ahora muestra `banner.png` (la imagen que enviaste, de la Agrupación Nacional de Boy Scouts de Chile — Localidad de Valparaíso) a todo el ancho. Si más adelante quieres cambiarla, solo reemplaza ese archivo por otro con el mismo nombre y las mismas proporciones (o ajusta `max-height` en el CSS si cambian mucho).

- **Mapa acotado a Valparaíso:** se definió `valpoBounds` (variable al final del `<script>`) que limita el arrastre y el zoom-out del mapa solo al área de Valparaíso. Si agregas un grupo fuera de ese rango, amplía esas coordenadas.
- **Tiles sin API key:** se usa el servidor de tiles estándar de OpenStreetMap (`tile.openstreetmap.org`), gratuito y sin necesidad de registrarte. (La versión anterior usaba CARTO, que ahora exige una API key y por eso aparecía la marca de agua "API KEY REQUIRED".)
- **Optimizado para móvil:** botones de zoom y de cerrar el popup más grandes para el dedo, tarjetas de información que se ajustan al ancho de pantallas chicas, y se respetan los márgenes de "notch"/barra de estado (`env(safe-area-inset-*)`).
