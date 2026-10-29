# Clínica estética: brief de diseño

Plantilla `clinica-estetica` creada el 29/10/2026 a partir de `belleza-estetica` con `php artisan plantillas:nueva`
y rediseñada entera. Este fichero se queda en el repo: es lo que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: clínicas de medicina estética, centros de láser y depilación, dermatología estética y estética
  dental (`sectores`: clinica-estetica, medicina-estetica, laser, dermatologia, dental-estetica). Su paciente busca
  confianza antes que precio: quién le va a tratar (médicos colegiados), qué tratamientos hay, cuánto duran y
  cuánto cuestan más o menos, con qué equipos y cómo se pide la primera valoración.
- **Qué tiene que conseguir la web**: que pidan la primera valoración (botón de cabecera, portada, tratamientos,
  promociones, banda «Pedir cita» por WhatsApp o teléfono, y el formulario de contacto).
- **Tono y estilo** (`estilo: lujoso`): sereno, exclusivo y médico. Referencia que sí: losmartesnohayluna.com por
  las bandas a sangre y los titulares enormes, pero en clave clara y silenciosa (revista de lujo, clínica de
  autor). Que no: la caja centrada estrecha con tarjetas blancas de las plantillas antiguas; el rosa empolvado,
  los arcos y las píldoras de `belleza-estetica`; el negro y oro de hotel o joyería (aquí manda el blanco).
- **Paleta de ejemplo**: primario `#b8955c` (oro champán), acento `#a7a29c` (gris perla), fondo `#fcfbf9`
  (blanco cálido), texto `#2a282d` (grafito). Derivados en `global.css` con `color-mix`: `--oro-texto` (oro
  oscurecido con el texto, para antetítulos y precios sobre claro), `--oro-claro` (oro aclarado, sobre grafito),
  `--perla` y `--perla-honda` (acento sobre fondo: bandas perla y huecos de foto), `--grafito` y
  `--grafito-hondo` (texto con una gota de oro: banda de tecnología y pie), `--linea` y `--linea-oro` (filetes).
  El oro como texto pequeño nunca va tal cual sobre blanco (no llega a AA): va `--oro-texto`. Sobre la banda de
  oro, el texto es `--c-sobre-primario` (grafito u otro legible, lo calcula `Base.astro`).
- **Tipografía**: del sistema. Títulos en serif fina (pila «Cormorant Garamond», «EB Garamond», Garamond, Iowan,
  Palatino Linotype, Georgia), peso 300-400, interletrado ligeramente negativo; portada a 7,25 rem en escritorio
  y 2,75 rem en móvil. Frases destacadas (`sobre.declaracion`, la primera opinión) en cursiva. Texto en Gill Sans
  / Segoe UI. Antetítulos, etiquetas, menú y botones en mayúsculas pequeñas muy espaciadas (0,2-0,32 em); los
  antetítulos con un filete de oro delante (y detrás si van centrados). Botones rectangulares sin radio, 52 px.
- **Forma de las fotos**: rectángulos a sangre o en rejilla, con un **marco interior fino** blanco a 0,85 rem
  del borde (`.marco`); nada de arcos ni círculos. Velo claro (degradado del color de fondo) sobre las fotos de
  portada y de cita para que el texto se lea encima.
- **Ritmo de bandas** (todas de borde a borde; contenido a 90 rem como mucho, 16 px de margen en móvil):
  1. `hero` — foto a sangre de cabina luminosa con velo claro de izquierda a derecha (en móvil, de abajo arriba),
     92 svh; antetítulo, título enorme, párrafo y dos botones; abajo, franja translúcida con los sellos
     (`items`) separados por filetes de oro. Sin foto: banda perla con un aro de oro.
  2. `tratamientos` — clara; titular partido (título a la izquierda, texto a la derecha tras un filete de oro);
     botones de filtro por `categoria` (JavaScript mínimo en línea); rejilla 1 → 2 → 3 → 4 columnas sin
     tarjetas: foto 3:4 con marco, categoría en oro, nombre en serif, texto y, sobre filete de oro, duración y
     precio. En móvil, ficha horizontal (foto estrecha a la izquierda) para no alargar la página.
  3. `sobre` — perla, partida 50/50 a sangre: foto vertical tocando el borde izquierdo; a la derecha (alineado
     con el contenedor) título, `declaracion` en cursiva grande con filete, párrafos y `items` en dos columnas.
  4. `tecnologia` — grafito; franja panorámica 21:9 a sangre que se funde con la banda; titular partido e
     `items` en 4 columnas con filetes verticales, número de orden e icono en oro.
  5. `equipo` — clara; retratos 3:4 con marco en 2 (móvil y tableta) o 4 columnas.
  6. `ofertas` — oro pleno; promociones en columnas separadas por filetes con el precio enorme; botón grafito.
  7. `opiniones` — perla; la primera opinión como cita gigante en cursiva centrada; el resto en columnas.
  8. `preguntas` — clara, partida 5/7: titular fijo a la izquierda y acordeón con filetes y «+» en oro.
  9. `cita` — foto a sangre con velo claro casi opaco; titular centrado, pasos con numerales romanos en oro y
     botones (WhatsApp, agenda externa opcional, teléfono). Sin foto: perla.
  10. `contacto` — partida 50/50: datos en filas con etiqueta e icono de oro y plano con marco a la izquierda;
      formulario en panel perla a sangre hasta el borde derecho.
  - Cabecera fija, blanca translúcida con filete de oro: nombre en versalitas espaciadas, menú en el centro
    (desde 1280 px; por debajo, menú plegable), teléfono (desde 1440 px) y «Pedir cita».
  - Pie grafito con filete de oro arriba y 4 columnas (marca y redes, menú, contacto, horario).
- **Fotos** (`fotos.json`, 12): cabina luminosa (portada), bodegones de cosmética médica sin etiquetas para cada
  tratamiento, recepción de mármol (la clínica), sala de aparatología panorámica, rincón de espera (cita). Sin
  texto legible, sin logotipos, sin caras; nada de antes y después.
- **Qué no hacer**: tarjetas blancas con sombra, esquinas redondeadas, píldoras, rosa; columnas estrechas
  centradas para secciones enteras; fotos de caras o de antes y después; dorados chillones.

## Hecho

- [x] `site.yaml` de ejemplo: Nácar Clínica Estética, Marbella (ficticia), todo activo y relleno.
- [x] Secciones nuevas: `tratamientos`, `sobre`, `tecnologia`, `cita`; rediseñadas `hero`, `equipo`, `ofertas`,
      `opiniones`, `preguntas`, `contacto`, `texto`, `404` y aviso legal. Quitadas `tarifas`, `galeria`, `reservas`.
- [x] `template.yaml` con sectores con nombre y guion del asistente de 11 pasos; `fotos.json` con 12 fotos.
- [x] `README.md`, `CLAUDE.md`, placeholders y `favicon.svg` propios.
- [ ] Fotos generadas y previews definitivas (paso de fotos), repo y etiqueta `v1.0.0`, alta en la plataforma.
