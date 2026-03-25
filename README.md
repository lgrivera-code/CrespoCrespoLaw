# Crespo & Crespo Law — crespocrespolaw.com

Sitio web bilingüe (español / inglés) para la firma de abogados Crespo & Crespo, con sede en Puerto Rico y Florida.

---

## Archivos del proyecto

```
/
├── index.html                        ← Página principal
├── quiebras.html                     ← Servicio: Quiebras (Cap. 7, 13, Sub V)
├── planificacion-sucesoral.html      ← Servicio: Planificación Sucesoral
├── sucesiones.html                   ← Servicio: Sucesiones / Probate
├── cobro-de-dinero.html              ← Servicio: Cobro de Dinero
├── naturalizacion-sentencia.html     ← Servicio: Naturalización de Sentencia
├── planificacion-contributiva.html   ← Servicio: Planificación Contributiva
└── README.md                         ← Este archivo
```

---

## Cómo hacer cambios

### Editar texto directamente en GitHub (forma más fácil)
1. Entra a este repositorio en github.com
2. Haz clic en el archivo que quieres editar (ej. `index.html`)
3. Haz clic en el ícono de lápiz ✏️ (arriba a la derecha del contenido)
4. Edita el texto
5. Haz clic en **"Commit changes"** — el sitio se actualiza automáticamente

### Editar localmente con GitHub Desktop (recomendado para cambios grandes)
1. Descarga [GitHub Desktop](https://desktop.github.com)
2. Clona este repositorio: **File → Clone repository**
3. Abre los archivos HTML en cualquier editor de texto (ej. VS Code, Notepad++)
4. Guarda los cambios
5. En GitHub Desktop: escribe un mensaje de commit y haz clic en **"Commit to main"**
6. Haz clic en **"Push origin"** para subir los cambios

---

## Bilingüe: cómo funciona

El sitio cambia entre español e inglés con un toggle en el menú. Técnicamente funciona así:

- El contenido en español usa: `<span data-lang="es">Texto en español</span>`
- El contenido en inglés usa: `<span data-lang="en">English text</span>`
- El JavaScript oculta/muestra el contenido correcto según el idioma seleccionado

**Para editar el texto en ambos idiomas**, busca las etiquetas `data-lang="es"` y `data-lang="en"` en el HTML y edita cada una por separado.

### Ejemplo:
```html
<!-- Antes -->
<span data-lang="es">Consulta Gratis</span>
<span data-lang="en">Free Consultation</span>

<!-- Después (cambiando el inglés) -->
<span data-lang="es">Consulta Gratis</span>
<span data-lang="en">Free Consult</span>
```

---

## Estructura de cada página de servicio

Todas las páginas de servicio (`quiebras.html`, etc.) tienen la misma estructura:

1. **Nav** — barra de navegación con logo y links
2. **Hero** — título del servicio, subtítulo y tags
3. **Contenido** — columna izquierda: título corto + botón CTA; columna derecha: contenido detallado
4. **Banner CTA** — llamada a la acción para contactar
5. **Footer**

---

## Cómo añadir un nuevo servicio

1. Copia cualquiera de los archivos de servicio existentes (ej. `quiebras.html`)
2. Renómbralo (ej. `nuevo-servicio.html`)
3. Edita el título, subtítulo y contenido dentro del archivo
4. En `index.html`, añade una nueva tarjeta en la sección `#servicios` apuntando al nuevo archivo:

```html
<a class="service-card" href="nuevo-servicio.html">
  <!-- contenido de la tarjeta -->
</a>
```

---

## Paleta de colores

| Variable | Color | Uso |
|---|---|---|
| `--navy` | `#0d1b2a` | Fondos oscuros, texto principal |
| `--gold` | `#c9a84c` | Acentos, labels, íconos |
| `--gold-light` | `#e2c77a` | Logo, hover states |
| `--gold-pale` | `#f5edd8` | Fondos de tarjetas en hover |
| `--cream` | `#faf8f4` | Fondo de página |

---

## Tipografía

- **Cormorant Garamond** — títulos y display (desde Google Fonts)
- **DM Sans** — cuerpo de texto, navegación, botones (desde Google Fonts)

---

## Deployment (para el desarrollador de AWS)

El sitio es HTML/CSS/JS estático — sin build process, sin dependencias, sin npm.

**Para conectar a AWS S3 + CloudFront:**
1. Crear un bucket S3 con static website hosting activado
2. Subir todos los archivos `.html` al root del bucket
3. Configurar GitHub Actions para auto-deploy en cada push a `main`

**Ejemplo de workflow de GitHub Actions (`.github/workflows/deploy.yml`):**
```yaml
name: Deploy to S3
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to S3
        run: aws s3 sync . s3://NOMBRE-DEL-BUCKET --exclude "*.md" --exclude ".git/*"
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: us-east-1
```

---

## Contacto del proyecto

Para preguntas sobre el código o el diseño del sitio, contactar al administrador del repositorio.
