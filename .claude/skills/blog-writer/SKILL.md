---
name: blog-writer
description: Convierte un dictado (speech-to-text) en una sección de un post de este blog manteniendo la voz de quien habla, busca las citas que la persona pidió y verifica los datos que afirmó. Úsala cuando alguien dicte o pegue texto hablado para un post, pida "escribe el post", "agrega esta sección", "pasa esto al blog", "cita esto" o "revisa si lo que dije es cierto" sobre un post de `posts/`.
---

# Blog writer

El autor habla, tú escribes. El post tiene que leerse como si la persona lo
estuviera contando: se nota quién habla. Tu trabajo es de transcriptor y de
verificador, no de redactor. Las ideas, el orden y las palabras son del autor.

## Cuándo usarla

- Llega un dictado o un texto hablado para un post nuevo o para una sección más
  de un post que ya existe.
- El autor pide buscar una cita, o pregunta si lo que dijo es cierto.

No la uses para escribir un post desde cero sin dictado, ni para "mejorar" la
redacción de un post ya escrito. Si no hay texto del autor, pídeselo.

## Antes de escribir

1. Lee el `README.md` del repo: define el formato de `index.md` y
   `metadata.json`.
2. Identifica el post (`posts/<slug>/`) y al autor. Si el post es nuevo, propón
   el slug y crea `metadata.json` con `"draft": true`.
3. Lee `voces/<autor>.md` dentro de esta skill. Si no existe, créala con este
   dictado siguiendo [references/voz.md](references/voz.md).
4. Si el post ya tiene secciones, léelas completas. Son la referencia de cómo
   suena este post.

## Procedimiento

### 1. Separa lo que es texto de lo que es encargo

En un dictado hay cuatro cosas mezcladas. Márcalas antes de editar:

- **Texto del post.** Lo que el autor quiere que se lea.
- **Encargos para ti.** "Aquí cita tal cosa", "aquí menciona esto", "esto
  después lo arreglo", "pon un gráfico". No van al post: se ejecutan. Lo mismo
  con las preguntas que el autor se hace en voz alta: no las respondas dentro
  del texto.
- **Afirmaciones verificables.** Cifras, fechas, nombres, quién hizo qué, qué
  dijo alguien, cómo funciona algo.
- **Dudas de transcripción.** Nombres propios y términos en inglés que el
  speech-to-text pudo oír mal, y frases raras o genéricas que no calzan con el
  tema (el transcriptor a veces inventa frases en los silencios).

Si un encargo es ambiguo ("cita lo de Jeff") y el contexto no alcanza para
saber a qué se refiere, pregunta antes de buscar.

### 2. Edita el texto

Lee [references/voz.md](references/voz.md) la primera vez en cada sesión. El
resumen: **se borra y se puntúa, no se reescribe.**

Puedes:

- quitar muletillas de relleno, tartamudeos, arranques en falso y repeticiones
  por tropiezo;
- poner puntuación, tildes, mayúsculas y párrafos;
- quedarte con la versión final de una autocorrección ("el jueves, no, el
  viernes" queda "el viernes");
- corregir un nombre o término mal transcrito, solo si lo confirmas con el
  glosario de la hoja de voz, el repo o una fuente.

No puedes:

- cambiar una palabra del autor por un sinónimo, ni "mejorar" una frase;
- corregir su gramática coloquial ni sus chilenismos;
- agregar ideas, ejemplos, transiciones, conclusiones o títulos ingeniosos;
- reordenar el argumento, ni juntar o partir frases para que queden parejas;
- suavizar una opinión, un garabato o un chiste;
- adivinar una palabra dudosa: se deja `[TODO: ¿dijo X?]`.

Los títulos de sección (`##`) salen de palabras del autor. Si no dio ninguno,
propón uno corto y avísale.

### 3. Revisa la voz contra el dictado

Antes de escribir en el archivo, compara tu texto con el dictado:

- Cada palabra con contenido de tu texto está en el dictado. Las únicas
  excepciones son correcciones de transcripción y lo que marcaste con `[TODO]`.
- Cada afirmación del dictado sigue en el texto, con la misma fuerza: los "creo
  que", "más o menos", "igual" que matizan siguen ahí.
- Las frases largas siguen largas y las cortas, cortas.
- Lee seguidas la última sección ya escrita y la nueva. Si se nota el cambio de
  mano, la nueva quedó demasiado pulida.

Si algo falla, vuelve al dictado y borra menos. No lo arregles reescribiendo.

### 4. Citas y verificación

Sigue [references/verificacion.md](references/verificacion.md). Las búsquedas
de distintas afirmaciones son independientes: hazlas en paralelo.

- **Citas pedidas.** Encuentra la fuente original, ábrela, confirma que dice lo
  que el autor quiere citar, y ponla en el markdown.
- **Verificación.** Revisa cada afirmación verificable buscando primero lo que
  la contradice.

No cambies una afirmación del autor porque la verificación salió mal. El texto
queda como lo dijo, con un `[TODO: ...]` al lado, y la corrección se la
propones en el informe. El autor decide.

### 5. Escribe y reporta

Escribe la sección en `posts/<slug>/index.md`. Después dile al autor, en este
orden:

1. Lo que está mal o no se pudo verificar, con la fuente y una redacción
   sugerida.
2. Las citas que pusiste y de dónde salieron.
3. Las dudas de transcripción que quedaron como `[TODO]`.
4. Lo que borraste que no era relleno evidente (una digresión, una frase que
   no se entendía).

Lo confirmado no necesita detalle: basta con decir cuántas afirmaciones
revisaste y que calzan.

## Errores frecuentes

- **Texto más "escrito" que el dictado.** Palabras más largas, menos "yo",
  menos conectores, frases de largo parejo. Pasa aunque trates de evitarlo: por
  eso el paso 3 es una comparación y no una relectura.
- **Borrar una muletilla que significaba algo.** "Igual", "como", "onda", "o
  sea" a veces son relleno y a veces cambian lo que se dice. La prueba está en
  `references/voz.md`.
- **Corregir prolijo un término mal oído.** "Jev" transcrito como "Jeff" y
  dejado como "Jeff" con mayúscula bonita. Un error bien escrito es peor que
  uno desordenado.
- **Citar de memoria.** Toda cita sale de una página abierta en esta sesión.
- **Buscar para darle la razón al autor.** La primera búsqueda es en contra.
- **Arreglar el dato en silencio.** El autor tiene que enterarse de que se
  equivocó.

## Verificación

La sección está lista cuando:

- el paso 3 pasa completo;
- cada link del texto nuevo fue abierto y contiene lo que respalda;
- cada afirmación verificable tiene veredicto, y las que no quedaron
  confirmadas tienen su `[TODO: ...]` en el post;
- el autor recibió el informe del paso 5.
