# bipbop-blog

Los posts de [bipbop.cl/blog](https://bipbop.cl/blog). El sitio lee este repo,
convierte el markdown y lo muestra: publicar un post es hacer push acá, sin
desplegar nada. Los cambios tardan hasta 5 minutos en verse.

## Un post

Una carpeta por post dentro de `posts/`. El nombre de la carpeta es la URL
(`posts/jev/` se ve en `bipbop.cl/blog/jev`), en minúsculas y con guiones.

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
- Cada `## Sección` aparece en el índice lateral y se puede enlazar.
- Las imágenes van con ruta relativa: `![Texto alternativo](grafico.png)`.
  Con un título entre comillas se muestra como pie de foto:
  `![Texto alternativo](grafico.png "Pie de foto")`. También sirven `.mp4`
  y `.webm`.
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

## Vista previa local

En el repo del sitio (`bipbop.cl`), apuntando a una copia local de este repo:

```
BLOG_DIR=../bipbop-blog pnpm dev
```

Así los cambios se ven al recargar, sin esperar la caché.

## Escribir con un agente

El repo trae una skill, `blog-writer`, en `.claude/skills/`. Si abres el repo
con Claude Code, dictas o pegas lo que quieres contar y el agente:

- lo pasa a una sección del post manteniendo tu forma de hablar;
- busca las citas que pediste ("aquí cita tal cosa") y las deja enlazadas;
- revisa los datos que diste y te avisa cuáles no calzan.

Guarda cada dictado sin editar en `dictados/<post>.md`, y lo que aprende de
cómo hablas en `.claude/skills/blog-writer/voces/`.
