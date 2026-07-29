# Guia de Implementacion - Capsula del Tiempo Digital

## Como empezar (configuracion inicial)

### El propietario del repositorio debe:

1. Agregar a los 4 compañeros como colaboradores en GitHub:
   - Ir al repositorio → **Settings** → **Collaborators** → **Add people**
   - Buscar por username o email de GitHub de cada integrante
   - Enviar invitacion

2. Cada compañero debe:
   - Aceptar la invitacion que llega por email (o en notificaciones de GitHub)
   - Clonar el repositorio:
```bash
git clone https://github.com/wigsdev/capsula-tiempo-digital.git
```
   - Entrar a la carpeta del proyecto:
```bash
cd capsula-tiempo-digital
```

Una vez agregados como colaboradores, todos pueden hacer push directamente a la rama main. Sin este paso, podran clonar y ver el codigo pero **no podran subir cambios**.

---

## Flujo de trabajo con Git (evitar conflictos)

### Regla de oro

```
Pull → Editar → Commit → Pull → Push
```

Nunca hacer push sin haber hecho pull justo antes.

### Paso a paso

1. **Antes de empezar a trabajar:**
```bash
git pull origin main
```

2. **Editar SOLO tu seccion** (debajo de tu comentario en el HTML y CSS).

3. **Hacer commit con mensaje descriptivo:**
```bash
git add index.html css/styles.css
git commit -m "Seccion X: descripcion breve del cambio"
```

4. **Antes de hacer push, traer cambios nuevos:**
```bash
git pull origin main
```

5. **Subir tus cambios:**
```bash
git push origin main
```

### Si git pull muestra un conflicto

Git marcara las lineas en conflicto con `<<<<<<<` y `>>>>>>>`. Pasos:
1. Abrir el archivo en conflicto
2. Buscar las marcas de conflicto
3. Conservar ambos bloques de codigo (porque son secciones diferentes)
4. Eliminar las marcas `<<<<<<<`, `=======`, `>>>>>>>`
5. Guardar, hacer `git add` y `git commit`

---

## Donde escribir tu codigo

### En index.html

Cada seccion tiene un comentario que indica donde va tu codigo. **Escribi tu HTML inmediatamente debajo de tu comentario.**

Ejemplo para Javier (Seccion 4):
```html
        <!-- Seccion 4: Mis intereses (min. 6 tarjetas) - JAVIER | id="intereses" | ... -->
        <section class="seccion seccion--intereses" id="intereses">
            <!-- Tu codigo aqui -->
        </section>
```

### En css/styles.css

Mismo principio. Cada seccion tiene un comentario. **Escribi tus estilos inmediatamente debajo de tu comentario.**

Ejemplo para Javier (Seccion 4):
```css
/* === Seccion 4: Mis intereses - JAVIER | .seccion--intereses, .intereses__grid, .tarjeta-interes (Flexbox) === */
.seccion--intereses {
    /* tus estilos aqui */
}

.intereses__grid {
    /* tus estilos aqui */
}
```

### En las media queries (RESPONSIVE)

Dentro de cada `@media` hay comentarios por responsable. **Escribi tus ajustes responsive solo debajo de tu nombre.**

```css
@media (max-width: 768px) {
    /* Secciones 4-5: JAVIER */
    .intereses__grid {
        /* tus ajustes tablet aqui */
    }
}
```

---

## Reglas para evitar conflictos

1. **No tocar codigo de otro compañero.** Si necesitas que otro cambie algo, comunicalo.

2. **No editar las zonas comunes** (variables, reset, utilidades) sin avisar al equipo.

3. **Commits pequenios y frecuentes.** No acumular un dia entero de cambios en un solo commit.

4. **Comunicarse antes de hacer push.** Un mensaje rapido en el grupo: "voy a subir cambios" reduce el riesgo de push simultaneos.

5. **Si dos personas necesitan subir al mismo tiempo:** uno sube primero, el otro espera, hace pull, y luego sube.

---

## Archivos que cada responsable puede modificar

| Responsable | Archivos |
|-------------|----------|
| Mirian | `index.html`, `css/styles.css`, imagenes en `img/` |
| Javier | `index.html`, `css/styles.css`, imagenes en `img/` |
| Rous Medina | `index.html`, `css/styles.css`, imagenes en `img/` |
| Wilmer Gulcochia | `index.html`, `css/styles.css`, archivos en `audio/` y `video/`, imagenes en `img/` |
| Daniel | `index.html`, `css/styles.css` |

---

## Orden sugerido de implementacion

Para reducir aun mas los conflictos, se sugiere que no todos trabajen al mismo tiempo en el mismo archivo. Orden sugerido:

### Fase 1 - Estructura HTML (todos pueden trabajar en paralelo)
Cada uno agrega su estructura HTML debajo de su comentario. Como las secciones estan separadas, el riesgo de conflicto es minimo.

### Fase 2 - Estilos CSS (todos pueden trabajar en paralelo)
Cada uno agrega sus estilos CSS debajo de su comentario. Misma logica.

### Fase 3 - Responsive (coordinar)
Todos escriben dentro de las mismas media queries. Aqui hay que hacer pull con mas frecuencia y subir cambios rapido.

### Fase 4 - Revision final (en equipo)
Revisar juntos que todo se vea bien y hacer ajustes finales.

---

## Nomenclatura BEM para nombres de clases

En este proyecto usamos la convencion **BEM** (Bloque, Elemento, Modificador) para nombrar las clases CSS. Esto mantiene el codigo organizado y evita conflictos de estilos entre secciones.

### Estructura

```
.bloque                → Componente independiente
.bloque__elemento      → Parte interna del bloque
.bloque--modificador   → Variante visual del bloque
```

### Ejemplo con la seccion multimedia

```css
.seccion                → Bloque base (general, se reutiliza en todas las secciones)
.seccion--multimedia    → Modificador (estilos unicos de esta seccion)
.multimedia__audio      → Elemento (el bloque de audio dentro de multimedia)
.multimedia__video      → Elemento (el bloque de video dentro de multimedia)
```

### En el HTML se ve asi

```html
<section class="seccion seccion--multimedia" id="multimedia">
    <article class="multimedia__audio">
        <h3>Mi audio</h3>
        <audio controls>...</audio>
    </article>
    <article class="multimedia__video">
        <h3>Mi video</h3>
        <video controls>...</video>
    </article>
</section>
```

### Reglas basicas

| Separador | Significado | Ejemplo |
|-----------|-------------|---------|
| `__` (doble guion bajo) | Elemento hijo del bloque | `.navegacion__lista` |
| `--` (doble guion) | Variante/modificador del bloque | `.seccion--galeria` |
| `-` (guion simple) | Separador de palabras | `.tarjeta-interes` |

### Por que dos clases en un section?

```html
<section class="seccion seccion--intereses">
```

- `.seccion` → Da los estilos BASE compartidos (padding, max-width, centrado)
- `.seccion--intereses` → Agrega los estilos UNICOS de esa seccion (fondo, sombra, etc.)

Asi no se repite codigo. Todas las secciones heredan la base y solo agregan lo particular.

### Ejemplos por seccion

| Seccion | Bloque | Elementos | Modificador |
|---------|--------|-----------|-------------|
| Navegacion | `.navegacion` | `__lista`, `__enlace` | — |
| Intereses | `.tarjeta-interes` | `__imagen`, `__titulo`, `__descripcion` | — |
| Metas | `.metas` | `__tabla-contenedor`, `__tabla` | `.seccion--metas` |
| Habilidades | `.tarjeta-habilidad` | `__icono`, `__titulo`, `__nivel` | — |
| Galeria | `.galeria` | `__grid`, `__item` | `.seccion--galeria` |
| Multimedia | `.multimedia` | `__audio`, `__video`, `__descripcion` | `.seccion--multimedia` |
| Recursos | `.recurso` | `__titulo`, `__descripcion` | `.seccion--recursos` |
| Carta | `.carta` | `__papel`, `__fecha`, `__saludo` | `.seccion--carta` |
| Footer | `.footer` | `__contenido`, `__lista`, `__copyright` | — |

---

## Unidades de medida CSS

En este proyecto usamos principalmente `rem` y `px`. Aqui la diferencia entre las unidades mas frecuentes:

### Unidades absolutas

| Unidad | Que es | Uso comun |
|--------|--------|-----------|
| `px` | Pixel fijo, no cambia | Bordes, sombras, valores pequenios y precisos |

### Unidades relativas

| Unidad | Relativa a... | Uso comun |
|--------|---------------|-----------|
| `rem` | Tamano de fuente del `<html>` (16px por defecto) | Padding, margin, font-size, espaciado general |
| `em` | Tamano de fuente del elemento padre | Espaciado interno que escale con el texto del padre |
| `%` | Tamano del elemento padre | Anchos, alturas, layouts fluidos |
| `vw` | 1% del ancho de la ventana | Elementos que ocupen un porcentaje del viewport |
| `vh` | 1% del alto de la ventana | Secciones de pantalla completa (hero, modales) |

### Conversion rapida (base 16px)

```
1rem    = 16px
0.5rem  = 8px
0.75rem = 12px
1.5rem  = 24px
2rem    = 32px
3rem    = 48px
4rem    = 64px
```

### Por que usamos rem en este proyecto?

```css
/* Con rem: si el usuario cambia el tamano de fuente en su navegador,
   todo el diseno se adapta proporcionalmente */
padding: 2rem;        /* 32px que se adapta */
font-size: 1.5rem;   /* 24px que se adapta */

/* Con px: valor fijo, no se adapta a preferencias del usuario */
border: 1px solid;   /* bordes finos siempre igual */
box-shadow: 0 2px 8px rgba(0,0,0,0.1);  /* sombras precisas */
```

### Cuando usar cada una

| Situacion | Usar | Ejemplo |
|-----------|------|---------|
| Padding, margin, espaciado | `rem` | `padding: 2rem;` |
| Font-size | `rem` | `font-size: 1.2rem;` |
| Bordes | `px` | `border: 1px solid;` |
| Sombras | `px` | `box-shadow: 0 4px 16px...` |
| Border-radius | `px` | `border-radius: 8px;` |
| Anchos fluidos | `%` | `width: 100%;` |
| Max-width de contenedores | `px` | `max-width: 1200px;` |
| Altura completa de pantalla | `vh` | `min-height: 100vh;` |

### Regla simple

- **rem** → para todo lo que deba escalar con las preferencias del usuario (texto, espaciado)
- **px** → para valores pequenios y precisos que no necesitan escalar (bordes, sombras, border-radius)
- **%** → para que un elemento ocupe un porcentaje de su padre

---

## Uso de variables CSS

Todos deben usar las variables definidas en `:root`. No usar colores directos.

```css
/* CORRECTO */
background-color: var(--color-primario);
color: var(--color-claro);
box-shadow: var(--sombra-suave);
font-family: var(--fuente-titulo);

/* INCORRECTO */
background-color: #2C3E50;
color: #ECF0F1;
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
font-family: 'Playfair Display', serif;
```

Esto garantiza que si se cambia un color en las variables, se actualiza en todo el proyecto automaticamente.

---

## Nombres de archivos multimedia

| Carpeta | Convencion de nombres | Responsable |
|---------|----------------------|-------------|
| `img/` | `hero.jpg`, `interes-1.jpg` a `interes-6.jpg` | Mirian, Javier |
| `img/` | `galeria-1.jpg` a `galeria-8.jpg` | Rous Medina |
| `img/` | `video-poster.jpg` | Wilmer Gulcochia |
| `audio/` | `mi-audio.mp3` | Wilmer Gulcochia |
| `video/` | `mi-video.mp4` | Wilmer Gulcochia |

---

## Resumen rapido

- Pull antes de editar
- Editar solo tu seccion
- Commit con mensaje claro
- Pull antes de push
- Push
- Comunicarse con el equipo
