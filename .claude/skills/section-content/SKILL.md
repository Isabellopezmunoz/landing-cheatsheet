---
name: section-content
description: Receta obligatoria para crear o editar contenido didáctico de cualquier sección del cheatsheet (/css, /html, /a11y, /seo). Carga esta skill SIEMPRE que vayas a escribir, ampliar o reescribir contenido dentro de una página de sección — explicaciones, ejemplos en vivo, snippets, bullets, listas de conceptos. NO la cargues para tareas de layout, styling del propio sitio, configuración o debugging que no toquen el contenido de las páginas de sección.
---

# section-content

Esta skill define el estándar de calidad pedagógica para el contenido del cheatsheet. El sitio es la **referencia personal de Isabel** para construir landings — no es un curso público, pero debe ser **completo, claro, moderno y útil a primera vista** sin tener que volver a la MDN.

## Principios irrenunciables

1. **Completo**: si una sección habla de un tema, cubre **todo lo necesario para usarlo en producción**, no solo lo básico. Si se nos olvida algo importante, la sección no está terminada.
2. **Moderno**: prefiere las APIs y patrones actuales del navegador (CSS Nesting, `:has()`, container queries, logical properties, `clamp()`, etc.) frente a hacks antiguos. Menciona alternativas viejas solo cuando aporten (p. ej. floats: solo como nota histórica).
3. **Funcional**: cada `CodeExample` tiene que **demostrar visiblemente** el concepto. Si el preview se ve plano sin interactuar, está roto pedagógicamente.
4. **Interactivo cuando aplique**: hover, focus, animaciones, transitions, scroll, selección, etc. → el preview tiene que invitar a tocar. Añade una **nota guía** explicando qué hacer ("Pasa el ratón por encima", "Haz click en el input", "Haz scroll dentro del preview").
5. **En contexto de landing**: cada concepto debe tener **dos** `CodeExample` cuando aplique — uno **abstracto** (mecánica pura, cuadraditos OK) y otro **en contexto** (hero, feature card, navbar, footer, CTA). Si solo aporta uno, que sea el más didáctico para ese concepto.

## Estructura obligatoria de una subsección

```
<section id="kebab-id" class="subsection">
  <h2>Título de la subsección</h2>
  <p>Frase corta que dice qué es y cuándo se usa.</p>

  <h3>Subtema 1</h3>
  <p>Explicación corta (2-3 frases máx).</p>
  <ul class="bullet-list">
    <li><code>propiedad</code> — qué hace y cuándo usarla.</li>
    ...
  </ul>

  <CodeExample title="Mecánica: ..." html={...} css={...} />
  <CodeExample title="En una landing: ..." html={...} css={...} />

  <h3>Subtema 2</h3>
  ...

  <h3>Trampas y errores típicos</h3>
  <ul class="bullet-list">
    <li>Por qué falla X y cómo arreglarlo.</li>
    ...
  </ul>
</section>
```

**No es opcional** la sección "Trampas y errores típicos" cuando el tema tiene gotchas conocidos (flexbox, position, especificidad, z-index, márgenes colapsados...). Es lo más útil de un cheatsheet personal.

## Checklist antes de dar por buena una subsección

Antes de marcar una subsección como terminada, ve uno a uno:

- [ ] **Cobertura**: ¿están todos los conceptos modernos que un dev de landing necesita en 2026?
- [ ] **Ejemplos visibles**: ¿cada preview muestra el efecto **sin tener que leer el código**?
- [ ] **Ejemplos interactivos**: si el concepto depende de interacción (hover, focus, scroll, click), ¿hay una nota guía justo antes o después del `CodeExample`?
- [ ] **Coherencia código → preview**: ¿el CSS del ejemplo **realmente usa** todo lo que se está explicando? Antipattern habitual: declarar variables CSS y luego pintar con hex, o explicar `:has()` y no usarlo en el preview.
- [ ] **Contexto real**: ¿hay un ejemplo en formato landing (hero, card, nav, footer) además del abstracto?
- [ ] **Trampas**: si el tema tiene errores típicos, ¿están listados?
- [ ] **Idioma**: explicaciones en español, código en inglés.
- [ ] **Tokens del sitio**: los ejemplos usan los colores de la paleta del sitio (`#6dff8a`, `#ffb84a`, `#0d0f0d`, `#1c1f23`, `#e8e8e3`, `#2a2d31`) para mantener coherencia visual.

Si algún checkbox no aplica al concepto en cuestión, ignóralo. Pero **no inventes ejemplos solo por tachar la lista** — la calidad va primero.

## Antipatterns que NO se deben repetir

❌ **Ejemplo de Variables CSS** (caso real previo): declarar `--accent`, `--warm`, `--bg` en `:root` y luego pintar el `.btn` con `#hex` literal. El preview funciona pero no demuestra nada.

✅ **Bien**: declarar tokens → usar `var()` en todas las reglas → mostrar variante redefiniendo SOLO los tokens, no las reglas.

❌ **Ejemplo de `:hover` o `transition`** sin guía: el preview se ve estático y el usuario no sabe que tiene que hacer hover. Pareces estar mostrando un botón normal.

✅ **Bien**: una nota corta antes o después del `CodeExample` ("👉 Pasa el ratón por encima del botón para ver la transición") **o** un estado por defecto que insinúe el efecto (texto "hover →").

❌ **Cuadraditos abstractos** como único ejemplo en un tema que tiene uso obvio en landing (Grid, Flexbox, gradientes, sombras...).

✅ **Bien**: además del cuadradito mecánico, un mini-hero o feature card real.

❌ **`<style>` con clases de página dentro del .astro** cuando esas clases son patrones repetibles. Va a [src/styles/sections.css](src/styles/sections.css).

✅ **Bien**: solo va en `<style>` scoped lo que sea único de esa página.

❌ **Repetir explicaciones largas** de cosas que ya están en otra sección. Linka mentalmente y resume.

## Cómo plantear el contenido de un tema

Cuando vas a crear una subsección, antes de escribir nada plantéate:

1. **¿Para qué se usa esto en una landing real?** → eso decide los ejemplos en contexto.
2. **¿Qué confunde al usar esto?** → eso decide la sección "Trampas".
3. **¿Qué APIs modernas hay?** → asegúrate de incluirlas, no quedarse en lo "de toda la vida".
4. **¿Qué se ve en el preview si no toco nada?** → si la respuesta es "no mucho", añade nota guía o estado inicial.

## Recursos del proyecto

- Componente: [src/components/CodeExample.astro](../../../src/components/CodeExample.astro) — props: `html`, `css`, `title`, `height`, `showHtml`, `showCss`.
- Estilos compartidos de sección: [src/styles/sections.css](../../../src/styles/sections.css).
- Tokens disponibles: [src/styles/foundations.css](../../../src/styles/foundations.css).
- Convenciones generales del proyecto: [CLAUDE.md](../../../CLAUDE.md).
