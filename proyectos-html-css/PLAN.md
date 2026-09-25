# Plan: proyectos cortos de HTML + CSS

> Borrador para revisar. Cuando lo apruebes (o lo recortes o cambies), lo convertimos en la página HTML.

## La idea

**Todo es HTML + CSS, sin JavaScript.** Los efectos interactivos y las animaciones salen de pseudo-clases, `popover`, `:target`, `:has()` y `@keyframes`.

Cada proyecto es algo **concreto que te gustaría tener o enseñar** (un ticket, un reproductor, un chat...), se hace en 1 o 2 sesiones y está pensado para que **te atasques** en 2 o 3 problemas que no se resuelven con lo que ya sabes. Esos problemas vienen escritos como **preguntas para investigar**, no como respuestas.

Formato de cada proyecto:

- **Qué construyes**: el encargo, en una frase.
- **Referencia / assets**: la imagen o los archivos de partida (algunos se generan con `mmx`).
- **Reglas**: restricciones a propósito para que no tomes el camino fácil.
- **Te vas a topar con...**: los problemas que te tocará investigar.
- **Conceptos nuevos**: lo que deberías saber al terminar (HTML y CSS).
- **Reto extra**: opcional, para cuando termines.

### Lo que asumo que YA sabes (y no se repite)

**HTML:** estructura, texto, enlaces, imágenes, listas, tablas (colspan/rowspan), formularios (tipos de input, `required`, `pattern`), `<head>`/meta, rutas relativas, etiquetas semánticas, `<audio>`/`<video>`/`<track>`, accesibilidad básica (`alt`, `label`, `aria-label`), `<details>`/`<summary>`, texto semántico inline.

**CSS:** selectores de etiqueta/clase/id, colores, `font-size`/`font-family`, fondos (color e imagen), `width`/`height`, `margin`/`padding`/`border`, `border-radius`, `box-sizing`, **flexbox** (dirección, `justify`, `align`, `gap`, `flex: 1`), `position: relative/absolute`, `pointer-events`, `color-scheme`.

👉 Si algo de esta lista no lo tienes firme, o si ya sabes algo de lo que aparece como "nuevo", dímelo y ajusto.

---

## Bloque 1 · Cajas con personalidad

### P01 · Entrada de cine 🎟️
**Qué construyes:** la entrada de una película inventada, con la parte que se arranca separada por una línea punteada y los dos "mordiscos" semicirculares a los lados.
**Referencia / assets:** póster de la película (`mmx image`) + una imagen de referencia de cómo tiene que quedar la entrada.
**Reglas:** los semicírculos **no** pueden ser imágenes ni elementos HTML extra. Nada de `px` para los tamaños de letra.
**Te vas a topar con...**
- ¿Cómo hago un círculo "recortado" que parezca un agujero si no puedo añadir `<div>`s? → `::before` / `::after`
- ¿Por qué mi `::before` no aparece? (pista: le falta una propiedad obligatoria)
- ¿Qué diferencia hay entre `em` y `rem`, y por qué el tamaño se me descontrola al anidar?
- ¿Cómo uso una tipografía de Google Fonts o de un archivo `.woff2` propio?

**Conceptos nuevos:** pseudo-elementos, `content`, unidades `rem`/`em`/`%`, `@font-face` / Google Fonts, `letter-spacing`, `text-transform`, `border-style: dashed`, `<time>`.
**Reto extra:** un código de barras hecho **solo con CSS** (pista: `repeating-linear-gradient`).

### P02 · Carta de un restaurante 🍝
**Qué construyes:** la carta de un restaurante inventado, con los puntitos que van del nombre del plato hasta el precio (`Lasaña ........ S/ 32`).
**Referencia / assets:** textura de papel y logo del restaurante (`mmx image`).
**Reglas:** todos los colores y fuentes definidos **una sola vez** al principio del CSS. Si mañana cambia la marca, tienes que poder cambiar el tema tocando 3 líneas.
**Te vas a topar con...**
- ¿Cómo hago que los puntos rellenen *justo* el espacio que sobra entre el nombre y el precio?
- ¿Qué etiqueta HTML tiene sentido para "nombre + descripción + precio"? (`<dl>`, ¿otra?)
- ¿Cómo pongo una variable de color y la reutilizo? ¿Y si la cambio dentro de una sección concreta?
- El precio tachado de una oferta: ¿`<s>` o `<del>`? ¿Cuál es la diferencia?

**Conceptos nuevos:** variables CSS (`--color`, `var()`), `<dl>/<dt>/<dd>`, `<s>`/`<del>`/`<ins>`, `border-bottom: dotted` o `::after` con `flex: 1`, `text-align`, `font-variant-numeric`.
**Reto extra:** una versión "modo noche" de la carta cambiando **solo** las variables.

### P03 · Cartas coleccionables ✨
**Qué construyes:** 3 cartas estilo Pokémon/Magic de criaturas inventadas: imagen, nombre, tipo, stats y rareza. Al pasar el ratón se inclinan y brillan.
**Referencia / assets:** 3 ilustraciones de criaturas (`mmx image`) con **tamaños distintos a propósito**.
**Reglas:** todas las cartas deben medir lo mismo aunque las imágenes no. Las imágenes no se pueden deformar.
**Te vas a topar con...**
- La imagen se estira o se aplasta: ¿cómo la recorto sin deformarla? → `object-fit`
- ¿Cómo fijo la proporción de la carta (63×88 mm) sin calcular alturas a mano? → `aspect-ratio`
- ¿Cómo hago el borde holográfico con degradado?
- La animación del hover salta de golpe: ¿cómo la suavizo?
- ¿Cómo hago que la carta "legendaria" tenga otro estilo sin copiar todo el CSS?

**Conceptos nuevos:** `:hover`, `transition`, `transform` (`rotate`, `scale`, `translate`), `box-shadow`, `linear-gradient`/`radial-gradient`, `object-fit`, `aspect-ratio`, clases modificadoras (`.carta.legendaria`), `<meter>` para las stats.
**Reto extra:** que la carta se dé la vuelta al hacer clic y enseñe el reverso (pista: `backface-visibility` + un checkbox escondido).

---

## Bloque 2 · CSS Grid

### P04 · Tu horario, versión 2 📅
**Qué construyes:** tu horario de la universidad otra vez, pero **cada curso ocupa una altura proporcional a lo que dura**. En tu versión con tabla, "7:30–10:50" e "7:30–9:10" ocupan lo mismo; aquí no.
**Referencia / assets:** tu `calendario.html` (los mismos datos).
**Reglas:** prohibido `<table>`. Cada fila del grid = 10 minutos. Cada curso tiene su color, y el color se define en el HTML con `style="--c: ..."`.
**Te vas a topar con...**
- ¿Cómo digo "este bloque empieza en la fila 1 y ocupa 20 filas"? → `grid-row`
- Tener que contar filas es un dolor: ¿se pueden **ponerles nombre** a las líneas del grid?
- ¿Cómo hago que la cabecera con los días se quede fija al hacer scroll? → `position: sticky`
- Dos cursos que se solapan (sí, pasa): ¿qué hace el grid? ¿cómo lo muestro?
- ¿Es accesible? ¿Qué pierde un lector de pantalla respecto a la tabla?

**Conceptos nuevos:** `display: grid`, `grid-template-columns/rows`, `repeat()`, `fr`, `grid-row`/`grid-column`, `span`, líneas con nombre, `position: sticky`, variables en `style=""`.
**Reto extra:** en el móvil no caben 7 columnas: que se vea un día por pantalla y se pase al siguiente deslizando (pista: `overflow-x` + `scroll-snap`).

### P05 · Bento de "sobre mí" 🍱
**Qué construyes:** una página de presentación tipo "bento" (las cajas de distintos tamaños que usa Apple en sus presentaciones): foto, stack que manejas, cursos, música que escuchas, un mapa de tu ciudad...
**Referencia / assets:** imagen de referencia de un bento (`mmx image`) + los recursos que quieras.
**Reglas:** el layout se define con **`grid-template-areas`** (el "dibujo" en texto). En móvil las cajas se reorganizan en una sola columna **sin tocar el HTML**.
**Te vas a topar con...**
- ¿Cómo "dibujo" el layout con nombres? ¿Qué pasa si una área no es rectangular?
- ¿Cómo cambio el layout según el ancho de pantalla? → `@media`
- ¿Por qué mi página se ve diminuta en el móvil aunque tenga media queries? (pista: una etiqueta del `<head>`)
- ¿Cómo hago que el texto crezca con la pantalla, pero con un mínimo y un máximo? → `clamp()`

**Conceptos nuevos:** `grid-template-areas`, `grid-area`, `@media`, `<meta name="viewport">`, mobile-first vs desktop-first, `clamp()`, `min()`/`max()`, `vw`/`vh`/`dvh`.
**Reto extra:** que una caja se reorganice según **su** ancho y no el de la pantalla (pista: container queries).

### P06 · Galería tipo Pinterest 🖼️
**Qué construyes:** una galería de fotos donde cada imagen tiene su altura natural y las columnas encajan como ladrillos. Clic en una foto → se ve en grande.
**Referencia / assets:** 12–15 imágenes con proporciones variadas (verticales, horizontales, cuadradas) generadas con `mmx image`, en dos tamaños (grande y miniatura).
**Reglas:** el número de columnas cambia solo según el ancho (1 → 2 → 4). El visor grande funciona **sin JavaScript**.
**Te vas a topar con...**
- Grid deja huecos si las imágenes tienen alturas diferentes. ¿Qué otra herramienta hace "columnas de periódico"? → `columns`
- Una imagen se parte entre dos columnas. ¿Cómo lo evito?
- ¿Cómo cargo la imagen pequeña en el móvil y la grande en pantalla grande? → `<picture>`, `srcset`, `sizes`
- ¿Cómo hago que las imágenes de abajo no se descarguen hasta que el usuario llegue? → `loading="lazy"`
- El visor: ¿`:target` o `<dialog>`? ¿Qué pasa con el botón "atrás" del navegador en cada caso?

**Conceptos nuevos:** `columns`, `break-inside`, `<figure>`/`<figcaption>`, `<picture>`/`srcset`/`sizes`, `loading="lazy"`, `:target`, atributo `popover` (se abre y se cierra sin JS), `z-index`, `inset`, `backdrop-filter`.
**Reto extra:** hover que oscurece la foto y muestra el título deslizándose desde abajo.

---

## Bloque 3 · Estados y formularios que se sienten vivos

### P07 · Registro con validación sin JS 📝
**Qué construyes:** el formulario de registro de una app inventada: los campos se ponen rojos/verdes según estén bien, la etiqueta "flota" hacia arriba al escribir, el checkbox de términos es un interruptor tipo iOS y el botón está gris hasta que todo es válido.
**Referencia / assets:** imagen de referencia del formulario (tú eliges una de Dribbble o te genero una).
**Reglas:** cero JavaScript. Tampoco puedes usar el checkbox/radio "de fábrica": el diseño es tuyo.
**Te vas a topar con...**
- `:invalid` pinta todo de rojo **antes** de que el usuario escriba nada. ¿Cómo espero a que el usuario haya tocado el campo? → `:user-invalid`, `:placeholder-shown`
- La etiqueta flotante: ¿cómo sabe el CSS si el input tiene texto?
- ¿Cómo borro el aspecto por defecto de un checkbox y dibujo el mío? → `appearance: none`
- ¿Cómo aplico un estilo al **formulario** según el estado de un **hijo**? → `:has()`
- Se ve bien con el ratón, pero con el teclado (Tab) no se sabe dónde estás: `:focus` vs `:focus-visible`.

**Conceptos nuevos:** `:valid`/`:invalid`/`:user-invalid`, `:placeholder-shown`, `:focus-visible`, `:checked`, `:disabled`, `:has()`, combinadores `+` y `~`, `appearance`, `accent-color`, `outline`, `autocomplete`, `inputmode`.
**Reto extra:** barra de "fuerza de contraseña" solo con CSS según `minlength`/`pattern`.

### P08 · Lista de tareas que cuenta sola ✅
**Qué construyes:** una lista de tareas del ciclo (de verdad, úsala) agrupada por curso. Al marcar una se tacha y se va al final; arriba pone "3 de 8 completadas".
**Referencia / assets:** ninguno, diseño libre.
**Reglas:** sin JavaScript. El contador tiene que ser real.
**Te vas a topar con...**
- ¿CSS puede **contar** cosas? → `counter-reset`, `counter-increment`, `counter()`
- ¿Y contar solo las marcadas?
- ¿Cómo muevo visualmente la tarea al final sin tocar el HTML? → `order`
- Tachar el texto con una animación que "dibuja" la línea.
- Cuando no quedan tareas: mostrar un mensaje "¡Todo listo! 🎉" (pista: `:has()` + `:not()`).

**Conceptos nuevos:** contadores CSS, `:not()`, `:is()`/`:where()`, `order`, `text-decoration` animado, `::marker`, especificidad (¿por qué mi regla no se aplica?).
**Reto extra:** filtros "Todas / Pendientes / Hechas" arriba de la lista, hechos con radio buttons + `:has()`.

---

## Bloque 4 · Apps de verdad (layout completo)

### P09 · Chat estilo WhatsApp 💬
**Qué construyes:** una conversación de chat: cabecera fija con el contacto, burbujas a la izquierda y derecha con su "piquito", horas, doble check azul, una nota de voz que se puede reproducir y un campo para escribir fijo abajo.
**Referencia / assets:** avatares (`mmx image`) + nota de voz (`mmx speech`).
**Reglas:** la cabecera y la caja de escribir no se mueven; **solo** hace scroll la conversación. Tiene que verse bien en móvil.
**Te vas a topar con...**
- ¿Cómo hago que solo la parte del medio haga scroll y ocupe exactamente el alto que sobra? → `height: 100dvh` + grid/flex + `overflow`
- El piquito de la burbuja: un triángulo hecho con bordes o con `clip-path`.
- Los mensajes seguidos de la misma persona no llevan piquito, solo el primero. ¿Qué selector hace eso?
- ¿Cómo dibujo el reproductor de la nota de voz sin usar los controles feos del navegador?
- Modo oscuro automático según el sistema → `prefers-color-scheme`

**Conceptos nuevos:** `overflow`, `100dvh`, `clip-path`, `:first-child`/`:nth-child`/`:last-of-type`, selector `+`, `max-width` en %, `prefers-color-scheme`, `<audio>` sin `controls`.
**Reto extra:** que el chat empiece "abajo del todo" como las apps reales (pista: `flex-direction: column-reverse`).

### P10 · Reproductor de música 🎧
**Qué construyes:** una mini-app tipo Spotify: barra lateral con playlists, zona central con los discos, y barra del reproductor fija abajo con portada, barra de progreso y volumen.
**Referencia / assets:** 5–6 canciones instrumentales cortas (`mmx music`) + portadas de discos de bandas inventadas (`mmx image`).
**Reglas:** layout completo con grid. La barra de volumen es un `<input type="range">` **con tu diseño**. Los nombres largos de canción se cortan con "..." en vez de romper el layout.
**Te vas a topar con...**
- ¿Cómo estilizo un `range`? (spoiler: cada navegador tiene su propio pseudo-elemento, prepárate)
- Texto largo que desborda: `text-overflow: ellipsis` solo funciona si se cumplen 3 condiciones, ¿cuáles?
- En un flex, `ellipsis` no funciona aunque cumplas las 3. ¿Por qué? (el famoso `min-width: 0`)
- Menú de "⋯" en cada canción que se abre encima de todo → atributo `popover`
- Portada que gira mientras suena: `@keyframes` + `animation-play-state`

**Conceptos nuevos:** layout de app con grid, `::-webkit-slider-thumb` / `::-moz-range-thumb`, `text-overflow`, `white-space: nowrap`, `min-width: 0`, `popover`/`popovertarget`, `@keyframes`, `animation`.
**Reto extra:** ecualizador animado de barritas que "bailan" junto a la canción que suena (un solo `@keyframes` y `animation-delay` distinto en cada barra).

---

## Bloque 5 · Movimiento

### P11 · Sistema solar animado 🪐
**Qué construyes:** el sol en el centro y 4–5 planetas girando en sus órbitas a distintas velocidades, con una luna girando alrededor de la Tierra. Al pasar el ratón por un planeta aparece su ficha.
**Referencia / assets:** texturas de planetas (`mmx image`), fondo de estrellas.
**Reglas:** cada planeta tiene **una sola** animación y todas usan el **mismo** `@keyframes`; solo cambia una variable.
**Te vas a topar con...**
- ¿Cómo hago que algo gire alrededor de un punto que no es su centro? → `transform-origin`, o anidar
- La luna tiene que girar alrededor de la Tierra **mientras** la Tierra gira alrededor del Sol.
- ¿Por qué el orden en `transform: rotate() translate()` cambia totalmente el resultado?
- Hay personas a las que el movimiento les marea: `prefers-reduced-motion`.

**Conceptos nuevos:** `@keyframes`, `animation-duration/timing-function/iteration-count/delay`, `transform-origin`, transformaciones compuestas y su orden, `prefers-reduced-motion`, `filter` (brillo del sol con `drop-shadow`/`blur`).
**Reto extra:** un reloj analógico cuyas agujas se mueven con `steps(60)`.

### P12 · Portada de un videojuego inventado 🎮
**Qué construyes:** la landing de un videojuego: vídeo de fondo en bucle con una capa oscura encima, logo que aparece con animación al entrar, botón "JUGAR" que late, capturas en carrusel que se desliza con el dedo/scroll y una sección de personajes.
**Referencia / assets:** clip de vídeo de fondo (`mmx video`), logo, capturas y personajes (`mmx image`), música de ambiente (`mmx music`).
**Reglas:** el carrusel funciona **sin JS** y se "engancha" a cada captura. La página pasa [PageSpeed/Lighthouse](https://pagespeed.web.dev/) con 90+ en accesibilidad.
**Te vas a topar con...**
- Vídeo de fondo que cubra siempre toda la pantalla sin deformarse (sí, `object-fit` otra vez, pero en `<video>`).
- ¿Por qué el navegador no reproduce mi vídeo solo? (`autoplay` necesita otros dos atributos)
- Carrusel que se engancha: → `scroll-snap-type`, `scroll-snap-align`
- Animaciones que se disparan al hacer scroll hasta un elemento, sin JS → `animation-timeline: view()` (moderno, revisa soporte en caniuse)
- Texto encima del vídeo que no se lee: overlay, `text-shadow`, contraste.

**Conceptos nuevos:** `<video>` de fondo (`autoplay muted loop playsinline`), `scroll-snap`, `scroll-behavior`, `animation-timeline`, `mix-blend-mode`, `text-shadow`, Open Graph (`og:image`) y favicon, cómo usar **caniuse.com**.
**Reto extra:** que al compartir el enlace por WhatsApp salga la imagen y descripción del juego.

---

## Bloque 6 · Retos de precisión

### P13 · CSS Battle x3 🎯
**Qué construyes:** tres imágenes objetivo que tienes que calcar **al píxel**, con el mínimo número de elementos HTML.
**Referencia / assets:** los objetivos de [cssbattle.dev](https://cssbattle.dev) (tiene comparador de píxeles y ranking) o 3 objetivos que te preparo.
**Reglas:** máximo 2 elementos HTML por objetivo. Medir con el comparador de la web.
**Te vas a topar con...**
- Formas raras con un solo `div`: `border-radius` con 8 valores, `clip-path: polygon()`.
- Varias formas con un único elemento: múltiples `box-shadow` o múltiples `background`.
- `inset`, `place-items`, y centrar de 5 maneras distintas.

**Conceptos nuevos:** `clip-path`, `border-radius` elíptico (`50% / 30%`), múltiples fondos y sombras, `conic-gradient`, `place-items`, `inset`.

### P14 · Integrador: la Net antes del Blackwall 🌆 (Cyberpunk)
**Qué construyes:** un pequeño sitio de la Net de Night City, con el estilo "arcaico" de esas páginas viejas que vigila NetWatch: fondo negro, texto de terminal, neón, líneas de escaneo de monitor CRT y glitches. Tiene 3 páginas enlazadas:
1. **Landing "Secure Your Soul"**: el anuncio corporativo del programa de Arasaka/Relic, que está "hackeado". Cada cierto tiempo el texto se rompe con un glitch y aparece un mensaje oculto.
2. **Catálogo de mercs**: la base de datos de un fixer con las fichas de mercs inventados (reutiliza tus cartas de P03): foto, alias, especialidad (netrunner, solo, techie...), implantes y "street cred" con `<meter>`. Se filtra por especialidad **sin JS**.
3. **Tablón de contratos**: tabla de encargos (distrito, pago en €$, riesgo, estado) que **no se rompe en el móvil**, y un botón que abre un aviso de "⚠ ICE DETECTADO" encima de todo.

**Referencia / assets:** retratos de mercs originales y fondos de la ciudad (`mmx image`), un tema synthwave oscuro (`mmx music`) y la voz corporativa del anuncio "Secure your soul" (`mmx speech`). Referencias visuales: capturas del juego o de las pantallas de la Net que te gusten.
**Reglas:** **un solo** archivo CSS para las 3 páginas, organizado (variables → base → componentes → páginas) y sin estilos repetidos. Cero imágenes para los efectos: las scanlines, el glitch y el neón son solo CSS. Tipografía monoespaciada y todo medido en `ch`/`rem`.
**Te vas a topar con...**
- Las líneas de escaneo del CRT encima de toda la página, sin que bloqueen los clics → `repeating-linear-gradient` + `pointer-events` (esto ya lo usaste)
- Texto con glitch: dos copias del mismo texto desplazadas en rojo/cian y cortadas a tiras → `::before`/`::after` con `content: attr(data-text)` + `clip-path` animado
- Efecto de máquina de escribir de terminal: el texto aparece letra a letra con un cursor que parpadea → `steps()` + unidad `ch`
- Filtrar el catálogo por especialidad con radio buttons → `:has()` + selectores de atributo `[data-rol="netrunner"]`
- Tablas en el móvil: ¿scroll horizontal o convertir cada fila en una tarjeta?
- Que en el menú se resalte la página en la que estás → `aria-current="page"` + selector de atributo
- Un CSS de 400 líneas se vuelve un caos: ¿cómo lo organizo? (lee sobre BEM, `@layer` y el anidamiento nativo de CSS)
- Tanto parpadeo puede ser un problema para algunas personas → `prefers-reduced-motion` desactiva los glitches

**Conceptos nuevos:** `attr()`, atributos `data-*`, selectores de atributo, `clip-path` animado, `steps()`, unidad `ch`, `text-shadow` múltiple (neón), `mix-blend-mode`, arquitectura CSS (BEM / `@layer`), CSS nesting, `aria-current`, `popover` para el aviso de ICE.
**Reto extra:** una hoja de impresión (`@media print`) que convierta la ficha de un merc en un "dossier" en blanco y negro listo para imprimir, sin menú, sin fondos y con el texto `CONFIDENCIAL` en marca de agua.

## Assets a generar con `mmx`

| Proyecto | Tipo | Cantidad aprox. |
|---|---|---|
| P01 | imagen (póster) | 1–2 |
| P02 | imagen (textura, logo) | 2 |
| P03 | imagen (criaturas) | 3 |
| P05 | imagen (referencia bento) | 1 |
| P06 | imagen (fotos variadas) | 12–15 |
| P09 | imagen (avatares) + voz | 2 + 1 |
| P10 | música + imagen (portadas) | 5 + 5 |
| P11 | imagen (planetas, estrellas) | 5–6 |
| P12 | vídeo + imágenes + música | 1 + 6 + 1 |
| P14 | imágenes (retratos, ciudad) + música + voz | ~8 + 1 + 1 |

⚠️ Aviso: los modelos de imagen no son buenos haciendo **capturas de interfaces** con texto exacto. Para las "imágenes de referencia" de diseño (entrada de cine, formulario, bento) propongo generar solo el estilo visual y describir el resto con texto, o que tú elijas una captura real de Dribbble/Behance como hiciste con el login.

## Cómo sería la página HTML (propuesta)

- Mismo estilo que tu `ejercicios.html` (barra lateral, progreso guardado, bloques con colores).
- Por proyecto: encargo, reglas, **"Te vas a topar con..."** y **pistas escalonadas** (pista 1 = qué buscar en Google/MDN → pista 2 = la propiedad → pista 3 = un fragmento de código). **Sin solución completa**, porque el objetivo es investigar.
- Enlaces directos a MDN / caniuse para cada concepto nuevo.
- Una **checklist de "¿lo he conseguido?"** por proyecto para comprobarlo tú mismo.

## Preguntas para ti

1. ¿14 proyectos está bien o prefieres menos y más largos?
2. ¿Hay alguno que te aburra o algún tema que te gustaría (algo de tu carrera, un juego, un anime...) para cambiarle la temática?
3. Pistas: ¿escalonadas y sin solución, o quieres la solución escondida al final como en la hoja anterior?
