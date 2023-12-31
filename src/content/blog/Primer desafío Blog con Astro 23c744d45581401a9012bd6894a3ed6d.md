---
title: "Primer desafío: Blog con Astro"
description: "Nada es trivial en lo que refiere al desarrollo de software. Ni siquiera un Blog."
pubDate: "August 13 2023"
heroImage: "https://www.notion.so/images/page-cover/met_goya_1789.jpg"
tags: "Astro"
---

Cuando pensé en construir un blog, lo primero que me vino a la mente fue 🚀[Astro](https://astro.build/). Era algo que no había probado pero que resonaba en el ambiente hace ya tiempo como una perfecta opción cuando de sitios estáticos se trata.

Como siempre, acudí a mis fuentes preferidas cuando de tecnologías web se trata y tras un tiempo me vino una idea: _“Y si paso mis notas de física a una web”_.

Este año comencé una nueva carrera y tras finalizar un largo primer cuatrimestre, me quede con una serie de apuntes escritos en [Notion](https://www.notion.so/) que serian perfectos para un primer experimento.

El proceso seria sencillo, exportar cada una de las notas a un formato soportado por Astro, adaptar los detalles necesarios para que el blog lusca profesional y académico. Publicar el sitio en GitHub Pages para que cualquiera pueda consultar el material de estudio y realizar aportes si lo creen necesario a través de un simple `pull request`.

El diseño esta inspirado en [Astro Pappers](https://astro.build/themes/details/astro-paper/), un tema que encontré en la galería oficial de Astro.

![Untitled](/joacko-blog/Primer%20desafi%CC%81o%20Blog%20con%20Astro%2023c744d45581401a9012bd6894a3ed6d/Untitled.png)

![Untitled](/joacko-blog/Primer%20desafi%CC%81o%20Blog%20con%20Astro%2023c744d45581401a9012bd6894a3ed6d/Untitled%201.png)

Pequeña advertencia para  él que quiera aplicar estilos desde [TailwindCSS](https://tailwindcss.com/). No es sencillo aplicar los estilos a las paginas que se renderizan desde un archivo `.md`. En mi caso, aplique estilos desde una hoja `css` a sabiendas de los elementos que Astro genera y englobando los artículos en una etiqueta `article` con una clase particular. Por ejemplo:

```html
<article class="article-md">
    <!-- Contendido del archivo md -->
    <slot />
</article>
```

```css
article.article-md h1 {
  font-size: 1.875rem; /* 30px */
  line-height: 2.25rem; /* 36px */
}
```

Todo venia a pedir de boca hasta que me tope con una sorpresa. Astro no renderiza formulas matemáticas basadas en [Latex](https://www.latex-project.org/).

Luego de varias búsquedas en la web y muchas pruebas, pude dar con la solución en un pequeño [articulo](https://www.ileumas.com/writing/2022/03/astro-math-katex/) que proponía utilizar dos plugins: [remark-math](https://www.npmjs.com/package/remark-math) y [rehype-katex](https://www.npmjs.com/package/rehype-katex). Ambas herramientas se adaptaron perfectamente a mi proyecto por lo que no fueron necesarios grandes ajustes.

```js
import remarkMath from "remark-math";
import rehypeKatex from "rehype-katex";

// https://astro.build/config
export default defineConfig({
  integrations: [mdx(), sitemap(), tailwind()],
  markdown: {
    remarkPlugins: [remarkMath],
    rehypePlugins: [rehypeKatex],
  },
});
```

Tras algunos reparos que no vale la pena mencionar, finalmente pude publicar los [apuntes](https://joackob.github.io/fisica1q/) y su recepción fue excelente.
