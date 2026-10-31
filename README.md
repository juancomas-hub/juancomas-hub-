# Tatacoa-Viva-Tours

Landing page de una agencia de turismo ficticia del Huila (Colombia), construida con **HTML, Tailwind CSS 4 y JavaScript puro**. Presenta tours al Desierto de la Tatacoa, San Agustín y el Estrecho del Magdalena, y permite enviar una solicitud de reserva mediante un formulario validado.

Proyecto del trabajo individual *Investigación y desarrollo de un sitio web con Tailwind CSS e inteligencia artificial* (Parte 2: Práctica), de Ingeniería de Software, Fundación Escuela Tecnológica de Neiva Jesús Oviedo Pérez.

| | |
|---|---|
| **Autor** | Juan Sebastian Comas Mateus |

---

## 1. Descripción del proyecto

**Tatacoa Viva Tours** es el sitio de una agencia de turismo local que quiere mostrar sus tours, generar confianza en los visitantes y recibir reservas en línea. El sitio es de una sola página (landing page) y se recorre de arriba hacia abajo con un menú de anclas.

- **Público objetivo:** viajeros nacionales y extranjeros de 20 a 50 años, y familias que visitan el Huila.
- **Propósito:** dar a conocer los tours, resolver dudas frecuentes y captar reservas.
- **Idioma:** español.

## 2. Tecnologías

| Tecnología | Uso |
|---|---|
| HTML5 | Estructura semántica (`header`, `nav`, `main`, `section`, `article`, `footer`) |
| Tailwind CSS 4 (Play CDN) | Estilos con clases utilitarias, tema propio con `@theme` y modo oscuro |
| JavaScript (sin librerías) | Menú móvil, modo oscuro, filtro, acordeón, validación y toast |
| Google Fonts | Playfair Display (títulos) e Inter (textos) |
| Wikimedia Commons | Fotografías de los lugares |

Tailwind se carga con `https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4`. El Play CDN es práctico para aprender y hacer prototipos, pero no se recomienda para producción porque compila los estilos en el navegador en cada visita.

## 3. Estructura del sitio

El sitio está en un único archivo `index.html`, dividido en secciones comentadas:

1. **Navbar:** fija arriba, con enlaces, botón "Reservar", botón de modo oscuro y menú hamburguesa en celular.
2. **Hero:** título principal, subtítulo, imagen de fondo con capa oscura y dos botones.
3. **Tours:** seis tarjetas en una cuadrícula, con filtro por categoría.
4. **Nosotros:** historia de la agencia, tres cifras destacadas y una imagen.
5. **Preguntas frecuentes:** acordeón con cuatro preguntas.
6. **Formulario de reserva:** campos validados y toast de confirmación.
7. **Pie de página:** dirección, horario, redes y derechos reservados.

```
/
├── index.html      # Página completa (HTML + estilos Tailwind + JavaScript)
├── README.md       # Este archivo
└── capturas/       # Capturas de Lighthouse y pruebas (agrégalas tú)
```

## 4. Funcionalidades

### Menú hamburguesa
En pantallas menores a `md` (768 px) los enlaces se ocultan y aparece un botón que abre y cierra el menú. El menú se cierra al hacer clic en un enlace, al presionar Escape y al agrandar la ventana. El botón actualiza `aria-expanded` y `aria-label` para lectores de pantalla.

### Modo oscuro
Un botón alterna entre modo claro y oscuro agregando o quitando la clase `dark` en `<html>`. La preferencia se guarda en `localStorage` y, si no existe, se usa la del sistema operativo. Un pequeño script en el `<head>` aplica el modo antes de pintar la página para evitar un parpadeo. Se activa en Tailwind con `@custom-variant dark`.

### Filtro de tours
Cuatro botones (Todos, Desierto, Cultura, Aventura) muestran u ocultan las tarjetas según su atributo `data-cat`. El botón activo usa `aria-pressed` y un texto oculto con `aria-live` anuncia cuántos tours se muestran.

### Acordeón de preguntas frecuentes
Cada pregunta es un botón con `aria-expanded` y `aria-controls`; al pulsarlo se muestra u oculta su respuesta y cambia el ícono `+` / `−`.

### Formulario con validación y toast
Los campos se validan con JavaScript (sin la validación nativa del navegador, por eso el `novalidate`):

| Campo | Regla |
|---|---|
| Nombre | Obligatorio, mínimo 3 caracteres |
| Correo | Obligatorio y con formato válido |
| Tour | Debe seleccionarse uno |
| Personas | Número entero entre 1 y 10 |
| Fecha | Obligatoria y no puede ser anterior a hoy |
| Comentarios | Opcional |

El error aparece en rojo debajo de cada campo, se valida al salir del campo (`blur`) y se corrige en vivo mientras se escribe. Si hay errores, el foco va al primer campo con problema. Cuando todo es correcto se muestra un **toast verde** de confirmación que desaparece a los 4 segundos y se limpia el formulario. El formulario no envía los datos a ningún servidor: es una demostración.

## 5. Diseño

### Regla 60-30-10 y colores semánticos

Los colores se definen una sola vez con `@theme` y se usan como clases (`bg-dominant`, `text-secondary`, `bg-accent`, etc.).

| Rol | Color | Valor | Dónde se usa |
|---|---|---|---|
| **60 % dominante** | Crema arena | `#FBF5EA` (tarjetas `#F3E7D3`) | Fondos de la página y las tarjetas |
| **30 % secundario** | Terracota oscuro | `#7C2D12` | Títulos, bloque "Nosotros", pie de página |
| **10 % acento** | Amarillo sol | `#F5B301` | Botones principales y detalles |
| Éxito | Verde | `#15803D` | Toast de confirmación |
| Error | Rojo | `#B91C1C` | Mensajes del formulario |
| Advertencia | Ámbar | `#B45309` | Definido en el tema, reservado para avisos |
| Modo oscuro | Marrón noche | `#1C120C`, `#2A1A11`, `#120A06` | Fondos en modo oscuro |

> Los contrastes se diseñaron para cumplir 4.5:1 o más (texto `#2B1408` sobre crema, crema sobre terracota, texto oscuro sobre el amarillo y blanco sobre el verde). **Verifica los valores finales en [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) y anota aquí el resultado:** _(pendiente)_.

### Tipografía

Se usan **dos fuentes**: Playfair Display para títulos (`font-display`) e Inter para el resto (`font-sans`).

| Nivel | Clases de Tailwind |
|---|---|
| H1 (hero) | `font-display text-4xl font-extrabold sm:text-5xl lg:text-6xl` |
| H2 (secciones) | `font-display text-3xl font-bold sm:text-4xl` |
| H3 (tarjetas) | `font-display text-xl font-bold` |
| Párrafo | tamaño base, `text-muted` |
| Texto pequeño | `text-sm` |

### Diseño responsive (mobile-first)

Los estilos base son para celular y se amplían con prefijos:

- `sm:` (640 px): botones del hero en fila, tarjetas en 2 columnas.
- `md:` (768 px): aparece el menú de escritorio y desaparece la hamburguesa; "Nosotros" pasa a dos columnas.
- `lg:` (1024 px): tarjetas en 3 columnas y más espacio vertical.

## 6. Accesibilidad

- Enlace "Saltar al contenido" visible al navegar con teclado.
- Todas las imágenes tienen texto alternativo descriptivo.
- Todos los campos del formulario tienen `<label>` asociado; los errores se vinculan con `aria-describedby` y `aria-invalid`.
- Foco visible en todos los elementos interactivos (`:focus-visible`), con color distinto en modo claro, oscuro y sobre el hero.
- Componentes interactivos con atributos ARIA (`aria-expanded`, `aria-controls`, `aria-pressed`, `role="status"` en el toast).
- Jerarquía de títulos ordenada (un H1, H2 por sección, H3 por tarjeta).
- Respeto a `prefers-reduced-motion` (se desactivan transiciones y desplazamiento suave).

## 7. Clases de Tailwind destacadas

| Clase | Qué hace | Dónde se usa |
|---|---|---|
| `grid sm:grid-cols-2 lg:grid-cols-3` | Cuadrícula que cambia de columnas según la pantalla | Tarjetas de tours |
| `hidden md:flex` | Oculta el elemento en celular y lo muestra como flex desde `md` | Enlaces del navbar |
| `sticky top-0 z-40` | Deja la barra fija al hacer scroll, por encima del contenido | Navbar |
| `dark:bg-night` | Cambia el fondo cuando está activo el modo oscuro | Todo el sitio |
| `hover:-translate-y-1 hover:shadow-xl transition` | Levanta la tarjeta con animación suave | Tarjetas |
| `bg-gradient-to-b from-secondary/80 to-night/90` | Degradado oscuro encima de la foto | Hero |
| `sr-only` / `focus:not-sr-only` | Oculta visualmente pero lo deja disponible a lectores de pantalla | Enlace para saltar |
| `object-cover` | Recorta la imagen sin deformarla | Todas las fotos |

## 8. Cómo ejecutarlo

1. Descarga o clona el repositorio.
2. Abre `index.html` en el navegador (necesita internet para Tailwind, las fuentes y las imágenes).

No requiere instalación ni servidor.

### Cómo personalizarlo

- **Colores y fuentes:** bloque `@theme` dentro de `<style type="text/tailwindcss">`.
- **Tours:** cada `<article class="tour-card">` en la sección de tours; cambia `data-cat` para asignar la categoría.
- **Imágenes:** cambia el `src` y el `alt` de cada `<img>`. Si una imagen no carga se muestra un recuadro de marcador.
- **Reglas del formulario:** objeto `reglas` al final del script.

## 9. Publicación

1. Crea un repositorio público en GitHub y sube `index.html` y este `README.md`.
2. En **Settings → Pages**, elige la rama `main` y la carpeta `/ (root)`.
3. Abre el enlace generado desde tu celular para comprobarlo.

(Alternativa: arrastrar la carpeta a Netlify Drop.)

---

## 10. Bitácora de prompts

**Herramienta de IA usada:** Claude

### Prompt maestro (versión 1)

Rol: Actúa como desarrollador frontend senior especializado en Tailwind CSS 4, diseño responsive y accesibilidad web.

Contexto: Voy a crear la landing page de "Tatacoa Viva Tours", una agencia de turismo de Neiva (Huila) dirigida a viajeros de 20 a 50 años. El sitio debe mostrar los tours, generar confianza y recibir reservas por un formulario.

Tareas: Construye una página con estas secciones en orden: (1) navbar fija con enlaces y botón "Reservar", con menú hamburguesa en celular que se abre y cierra con JavaScript; (2) hero con título, subtítulo, imagen de fondo con capa oscura y dos botones; (3) tours en tarjetas con grid de 1, 2 y 3 columnas según pantalla, con filtro por categoría; (4) sección "Nosotros" con texto e imagen; (5) preguntas frecuentes en acordeón; (6) formulario de reserva con validación en JavaScript, errores junto a cada campo y toast verde que desaparece a los 4 segundos; (7) pie de página. Agrega botón de modo claro y oscuro.

Restricciones: Solo HTML, Tailwind CSS 4 por Play CDN y JavaScript puro. Paleta con @theme en una etiqueta style type="text/tailwindcss": crema 
#FBF5EA (60 %), terracota 
#7C2D12 (30 %), amarillo 
#F5B301 (10 %), más verde 
#15803D para éxito, rojo 
#B91C1C para error y ámbar 
#B45309 para advertencia. Máximo dos fuentes de Google Fonts: Playfair Display e Inter. Diseño mobile-first. Accesibilidad: textos alternativos, etiquetas en los campos, contraste mínimo 4.5:1 y foco visible.

Formato de salida: Un único archivo index.html con el JavaScript al final del body, código indentado y comentarios en español separando cada sección. Al final, lista corta de cómo abrirlo y qué personalizar.

**Resultado de la versión 1:** Funciono la mayoria del sitio web, lo unico que fallo fue las imagenes

### Iteraciones

| # | Prompt de ajuste enviado | Problema que buscaba resolver | Resultado obtenido | ¿Funcionó? |
|---|---|---|---|---|
| 1 |"en las imagenes pon cualquier cossa peo trata de que no este vacio" |Las imágenes apuntaban a archivos locales (img/...) que no existían, así que el hero y las tarjetas se veían vacíos. |La IA cambió las 8 rutas por imágenes de ejemplo en línea (picsum.photos) y actualizó el README y el marcador de error. |Parcialmente: ya no había espacios vacíos, pero las fotos eran aleatorias y no tenían relación con el contenido. |
| 2 |	"pon imagenes relacionado al contenido" |Las fotos aleatorias no correspondían a los tours ni al Huila. |La IA buscó fotos reales en Wikimedia Commons (Tatacoa, observatorio, San Agustín, Lavapatas, Estrecho del Magdalena, Salto de Bordones y Neiva), actualizó los textos alternativos y cambió dos tours (café por Lavapatas y La Chaquira; cabalgata por Salto de Bordones) porque no halló fotos libres de esos temas. |Sí, pero la IA no pudo comprobar que las imágenes carguen: hay que verificarlo en el navegador y revisar la licencia de cada foto. |
| 3 |"hazme un readme donde describas el proyecto" |El README era solo una plantilla y no describía el proyecto. |La IA escribió un README completo: descripción, tecnologías, estructura, funcionalidades, diseño, accesibilidad, clases de Tailwind y publicación. |Sí. Faltan datos propios por completar (enlaces, pruebas, créditos). |
| 4 |----- |----- |----- |----- |
| 5 |-----|----- |----- |----- |


## 11. Pruebas y resultados

| Prueba | Herramienta | Resultado |
|---|---|---|
| Responsive en celular, tablet y computador | Modo responsive del navegador (F12) | _(pendiente)_ |
| Validación de HTML | validator.w3.org | _(pendiente)_ |
| Accesibilidad | Lighthouse (meta: 90 o más) | _(puntaje; captura en `capturas/`)_ |
| Contraste de colores | WebAIM Contrast Checker | _(pendiente)_ |
| Navegación solo con teclado | Tab, Enter y Escape | _(pendiente)_ |

## 12. Créditos

- **Imágenes:** Wikimedia Commons (Desierto de la Tatacoa, Observatorio de la Tatacoa, Parque Arqueológico de San Agustín, Lavapatas, Estrecho del Magdalena, Salto de Bordones y Neiva). Cada archivo tiene su propio autor y licencia: _(completa aquí autor y licencia de cada foto, consultándolos en la página del archivo en commons.wikimedia.org)_.
- **Fuentes tipográficas:** Playfair Display e Inter, de Google Fonts.
- **Framework:** [Tailwind CSS](https://tailwindcss.com/docs).
- **Asistencia de IA:** _(indica qué herramienta usaste y para qué)_.

Tatacoa Viva Tours es una marca ficticia creada con fines académicos. Los precios, cifras y datos de contacto son de ejemplo.
