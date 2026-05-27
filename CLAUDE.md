# landing-cheatsheet

## Qué es este proyecto

Una landing-cheatsheet en español que sirve a Isabel como **referencia personal de consulta** mientras trabaja construyendo landings. Es un sitio web que ella misma visita para refrescar cómo se hace algo en HTML/CSS sin tener que buscar en la documentación oficial cada vez.

No es un producto público ni un curso para terceros — es su libreta de apuntes ejecutable.

## Stack

- **Astro 6** con TypeScript.
- **Sin frameworks de UI** (nada de React, Vue, Svelte salvo necesidad clara).
- **Sin librerías CSS** (nada de Tailwind, Bootstrap, UnoCSS, etc.).
- Prettier configurado con `semi: false`, `singleQuote: true`, `printWidth: 100`.
- Idioma del contenido: **español** (textos, ejemplos, comentarios).

## Filosofía: el propio sitio es ejemplo de lo que enseña

El CSS y HTML del sitio están escritos **a mano, sin librerías**, porque Isabel debe poder abrir DevTools, inspeccionar cualquier elemento, y aprender de cómo está construido. Esto significa:

- Todo el styling con CSS puro (variables CSS, nesting nativo si aplica, `@layer` si conviene).
- HTML semántico estricto (`header`, `main`, `section`, `article`, `nav`, `footer`, `aside`).
- Accesibilidad cuidada (atributos `aria-*`, contraste, navegación por teclado, `alt` en imágenes).
- Nada de utilidades atómicas estilo Tailwind.

## Formato de cada concepto explicado

Cada concepto del cheatsheet se presenta como **código + preview en vivo al lado** (o debajo en móvil). El usuario ve:

1. Una explicación corta en español del qué y el cuándo usarlo.
2. El snippet de código (HTML y/o CSS) en un bloque legible.
3. Un ejemplo real renderizado, en vivo, demostrando el efecto.

Para esto habrá un componente Astro reutilizable (TBD: `CodeExample.astro` o similar) que reciba el código a mostrar y renderice ambas cosas. Definirlo cuando haga falta, no antes.

## Alcance temático

El cheatsheet cubre:

1. **HTML** — estructura, semántica, formularios, meta tags, multimedia.
2. **CSS** — selectores, box model, unidades, flexbox, grid, position, responsive, variables, animaciones, pseudo-clases/elementos.
3. **Accesibilidad básica** — semántica accesible, aria-\*, foco, navegación por teclado, contraste.
4. **SEO básico para landings** — meta tags, Open Graph, estructura semántica para crawlers.
5. **Patrones típicos de landing** — hero, grid de features, testimonios, CTAs, footer.

Fuera de alcance (por ahora): JavaScript avanzado, frameworks JS, build pipelines, performance avanzada.

## Calidad del contenido de las páginas de sección

Cuando vayas a crear o editar contenido didáctico (explicaciones, ejemplos, snippets) dentro de cualquier página de sección (`/css`, `/html`, `/a11y`, `/seo`), **carga obligatoriamente la skill [`section-content`](.claude/skills/section-content/SKILL.md)** antes de escribir nada.

Resumen del estándar:

- Cobertura **completa y moderna** del tema (APIs actuales, no solo lo básico).
- Cada concepto con `CodeExample` que **demuestra visiblemente** el efecto.
- Si el concepto depende de interacción (hover, focus, scroll), añade nota guía ("Pasa el ratón…").
- Cuando aplique, doble ejemplo: **mecánica abstracta + contexto de landing real** (hero, card, nav, footer).
- Sección "Trampas y errores típicos" cuando el tema tenga gotchas conocidos.
- Código de ejemplo en inglés, explicaciones en español.

El detalle completo, checklist y antipatterns están en la skill.

## Convenciones de código

- **Sin punto y coma en JS/TS** (Prettier `semi: false`).
- **Nombres de variables completos** (ya está en CLAUDE.md global, no usar `e`, `i`, `c`...).
- **Comentarios en español** cuando aporten.
- **Nombres de archivos y carpetas en inglés** (estándar de la comunidad Astro).
- **Contenido del sitio en español**.

## Cómo trabajar en este proyecto

- `npm run dev` — servidor de desarrollo en http://localhost:4321.
- `npm run build` — build de producción.
- `npm run format` — formatea todo con Prettier.
- `npm run format:check` — comprueba formato sin modificar.

## Estructura prevista (irá cambiando)

```
src/
  pages/
    index.astro          ← landing principal con índice de secciones
    html/                ← una página por bloque temático
    css/
    a11y/
    seo/
  components/
    CodeExample.astro    ← bloque código + preview (por crear)
    SectionNav.astro     ← navegación lateral (por crear)
  layouts/
    BaseLayout.astro     ← layout común (por crear)
  styles/
    global.css           ← variables CSS, reset, tipografía base
```

## Decisiones pendientes

- Paleta de colores y tipografía (Isabel decidirá más adelante).
- Si habrá modo claro/oscuro o solo uno.
- Estructura exacta de la navegación (sidebar, tabs, scroll spy…).
- Si el contenido vive en `.astro` directamente o en Markdown/MDX con frontmatter.

Cuando una de estas decisiones se tome, actualizar esta sección.
