# Plantilla NoExpertise · Clínica estética

Web lujosa en blanco, oro y perla para clínicas estéticas, láser y dermatología, con tratamientos y cita.

- Sectores: clinica-estetica, medicina-estetica, laser, dermatologia, dental-estetica. Estilo: lujoso. Plan mínimo: presencia.
- Secciones: hero, tratamientos, sobre, tecnologia, equipo, ofertas, opiniones, preguntas, cita, contacto (más el diseño `texto` para apartados nuevos).
- Campos propios: `tratamientos[]` (nombre, texto, precio, duracion, categoria, imagen; filtro por `categoria`), `sobre.declaracion`, `ofertas[]` (titulo, texto, precio, validez), `cita.enlace_reservas`.
- A todo el ancho: bandas claras, perla, grafito y oro de borde a borde; portada y pedir cita con foto a sangre y velo claro; «La clínica» y contacto partidos 50/50 a sangre. Responsive de 375 a 1440 px sin scroll horizontal.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`MedicalClinic` por defecto) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`; diseño en `DISEÑO.md`; fotos de la demo en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.
