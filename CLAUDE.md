# Plantilla «Clínica estética» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **lujoso**
(blanco cálido, oro champán, gris perla y grafito; bandas a todo el ancho). Todo en castellano de España, frases
cortas, sin jerga. El diseño completo está explicado en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = oro de botones, filetes y banda de promociones; acento = gris perla de las bandas perla; fondo = blanco cálido; texto = grafito, que también da el color de las bandas oscuras y del pie). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…, y calcula `--c-sobre-primario`, el color de texto legible encima del oro). Los derivados están en `src/styles/global.css` con `color-mix` (`--oro-texto`, `--oro-claro`, `--perla`, `--perla-honda`, `--grafito`, `--grafito-hondo`, `--linea`, `--linea-oro`).
- **Tipografías y aspecto general**: `src/styles/global.css` (serif fina tipo Garamond/Palatino para títulos, Gill Sans/Segoe para el texto; antetítulos en mayúsculas muy espaciadas con un filete de oro; botones rectangulares `.btn`, `.btn-sec`, `.btn--oscuro`; bandas `.banda--clara`, `.banda--perla`, `.banda--oscura`, `.banda--oro`; mitades a sangre `.mitad-texto`; marco fino `.marco`; cabecera `.cabecera--nacar` y pie `.pie--grafito`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las fotos de la demo se generan a partir de `fotos.json`; mientras una foto `/fotos/x.jpg` no exista, `Imagen.astro` usa su respaldo `/placeholders/x.svg`. Las fotos nuevas del cliente van en `public/fotos/`.
- **Personas**: `personas[].foto` usa la silueta `/placeholders/persona.svg` salvo que el cliente aporte su foto. No se generan caras. Nada de fotos de antes y después con caras.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = nombre en texto en la cabecera y en el pie.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie`.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. `hero` y `contacto` son obligatorias.
- `hero` → `src/components/secciones/hero.astro` (foto a sangre con velo claro, título enorme y franja de sellos)
- `tratamientos` → `tratamientos.astro` (rejilla a todo el ancho con filtro por categoría)
- `sobre` → `sobre.astro` (banda perla 50/50 con la foto a sangre)
- `tecnologia` → `tecnologia.astro` (banda grafito con franja panorámica)
- `equipo` → `equipo.astro` (retratos con marco fino)
- `ofertas` → `ofertas.astro` (banda de oro con las promociones)
- `opiniones` → `opiniones.astro` (cita grande y el resto en columnas)
- `preguntas` → `preguntas.astro` (acordeón `details/summary`; sin preguntas no se pinta)
- `cita` → `cita.astro` (foto a sangre con velo, pasos y botones)
- `contacto` → `contacto.astro` (datos y plano a la izquierda, formulario en panel perla a la derecha)
- Diseño extra para apartados nuevos: `texto` (genérico; con imagen sale partido 50/50 a sangre).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. **Precios siempre como cadena** (`precio: "85 €"`, `precio: "desde 120 €"`); precio vacío = no se muestra.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Para agrupar tratamientos usa el campo `categoria` de cada uno (no listas anidadas). Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Apartado nuevo**: añade `secciones.<id-nuevo>` en `site.yaml` con `tipo:` igual al diseño que quieras (`texto`, `tratamientos`, `ofertas`, `preguntas`, `tecnologia`…). Si ninguno sirve, crea `src/components/secciones/<id>.astro` copiando la estructura de uno existente (`seccion(Astro.props.id)`, bandas a todo el ancho, `Titular`). `src/pages/index.astro` lo recoge solo: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral (`.contenedor`), bandas y fotos a todo el ancho, sin scroll horizontal en móvil. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`, o el `nombre` de la ficha); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Nunca inventes precios, opiniones ni datos que el cliente no haya dado: deja el campo vacío o la lista vacía (los componentes lo ocultan).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `hero.imagen`: foto a sangre (16:9) bajo un velo claro. `hero.items`: sellos de la franja inferior (solo `titulo`). `hero.cta_secundario` opcional.
- `tratamientos.tratamientos[]`: `{ nombre, texto, precio, duracion, categoria, imagen }`. Con más de una `categoria` salen botones de filtro (en el orden en que aparece cada una). `tratamientos.nota` y `tratamientos.cta` opcionales. Sin tratamientos ni texto, la sección no se pinta.
- `sobre.declaracion`: frase grande en cursiva. `sobre.imagen`: foto vertical a sangre (3:4). `sobre.items[]`: `{ titulo, texto, icono }`. `sobre.cta`.
- `tecnologia.imagen`: franja panorámica (21:9). `tecnologia.items[]`: `{ titulo, texto, icono }` (iconos: rayo, sol, gota, ojo, escudo, estrella…).
- `ofertas.ofertas[]`: `{ titulo, texto, precio, validez }`. `ofertas.nota`, `ofertas.cta`. **Con `ofertas: []` la sección no se pinta.**
- `opiniones.testimonios[]` (`texto`, `autor`): la primera sale en grande. `opiniones.nota`. Sin testimonios, no se pinta.
- `cita.items`: pasos (numerales romanos). `cita.cta`: botón principal (si su `url` está vacía abre WhatsApp con `contacto.whatsapp`). `cita.enlace_reservas`: agenda externa opcional (con `enlace_reservas_texto`). `cita.imagen`: foto a sangre con velo (decorativa). `cita.nota`.
- `equipo.personas[]`: sin personas, la sección no se pinta.
- `contacto.imagen`: plano que enlaza a mapas. `contacto.boton`: texto del botón del formulario.
