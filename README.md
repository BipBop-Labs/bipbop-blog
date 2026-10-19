# bipbop-blog

Los posts de [bipbop.cl/blog](https://bipbop.cl/blog). El sitio lee este repo,
convierte el markdown y lo muestra: publicar un post es hacer push acá, sin
desplegar nada. Los cambios tardan hasta 5 minutos en verse.

## Un post

Una carpeta por post dentro de `posts/`, en minúsculas y con guiones. La URL
sale del título (`# La mejor UX` se ve en `bipbop.cl/blog/la-mejor-ux`); la
del nombre de la carpeta también sirve y redirige a esa. Lo normal es que la
carpeta se llame igual que la URL: al editar en la página se renombra sola.
Ojo: cambiar el título de un post publicado cambia su URL.

```
posts/jev/
├── index.md         el texto
├── metadata.json    quién lo escribió y si es borrador
└── grafico.png      imágenes, al lado del texto
```

### index.md

Markdown normal (tablas, bloques de código, listas, citas).

- El primer `# Título` es el título del post. Lo que vaya en *cursiva* dentro
  del título sale en verde.
- `==así==` sale en el verde de BipBop, sin cursiva, en el título o el texto.
- Cada `## Sección` aparece en el índice lateral y se puede enlazar.
- Las imágenes van con ruta relativa: `![Texto alternativo](grafico.png)`.
  Con un título entre comillas se muestra como pie de foto:
  `![Texto alternativo](grafico.png "Pie de foto")`. También sirven `.mp4`
  y `.webm`.
- Los diagramas van en un bloque ` ```mermaid ` ([sintaxis](https://mermaid.js.org/intro/syntax-reference.html))
  y se dibujan con los colores del sitio. Para destacar un nodo en verde:
  `classDef jev fill:#e3ebd9,stroke:#3d7a3a,color:#2f5f2d` y `class nodo jev`.
  Si el diagrama tiene un error de sintaxis, se muestra como texto.
- Lo que falta confirmar antes de publicar se escribe `[TODO: qué falta]` y
  sale marcado en rojo.
- El HTML suelto no se interpreta: se muestra como texto.

### metadata.json

```json
{
  "authors": [{ "name": "Nombre Apellido", "url": "https://su-sitio.cl" }],
  "description": "Una línea que resume el post.",
  "draft": true
}
```

- `authors`: quién lo escribió. `url` es opcional.
- `description`: la bajada bajo el título, y lo que se ve al compartir el
  enlace. Si falta, se usa el primer párrafo.
- `draft`: con `true` el post se ve solo con el enlace directo, con un marco
  rojo, y no aparece en `/blog` ni en buscadores. Para publicar, se borra.
- `date`: opcional (`"2026-09-22"`). Sin esto, la fecha es la del primer
  commit de `index.md`.

## Escribir en la página

Con este repo al lado del sitio (`bipbop/bipbop-blog` y `bipbop/bipbop.cl`),
en el repo del sitio:

```
pnpm dev
```

Si la copia está en otro lado: `BLOG_DIR=/ruta/al/blog pnpm dev`.

Abre `localhost:3000/blog/<slug>` y escribe directo sobre el post: el título,
la bajada y el texto se editan ahí mismo, tal como se van a ver. Se guarda
solo en `index.md` y `metadata.json` (abajo a la derecha dice si guardó;
`Ctrl+S` guarda al tiro). Después, commit y push como siempre.

- `Ctrl+B` y `Ctrl+I` dan negrita y cursiva. Clic derecho, en el título o el
  texto, abre un menú de formato (con Shift, el del navegador).
- También se puede escribir markdown en un párrafo (`## Sección`, `- lista`,
  `[enlace](https://...)`, ` ``` `): al salir del párrafo se convierte.
- Solo cambian en el archivo los bloques que tocaste; el resto queda igual.
- El índice lateral se actualiza al recargar.

## Escribir con un agente

El repo trae una skill, `blog-writer`, en `.claude/skills/`. Si abres el repo
con Claude Code, dictas o pegas lo que quieres contar y el agente:

- lo pasa a una sección del post manteniendo tu forma de hablar;
- busca las citas que pediste ("aquí cita tal cosa") y las deja enlazadas;
- revisa los datos que diste y te avisa cuáles no calzan.

Lo que aprende de cómo hablas lo guarda en
`.claude/skills/blog-writer/voces/`.
