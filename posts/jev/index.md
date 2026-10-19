# Jevi: Jev bajó el 38% de gasto en Revi

La semana del 18 (de septiembre), probablemente mientras te comías una empanada, se lanzó Jev. Un modelo que abrió un submundo para todos los que estamos trabajando desarrollando agentes.

## ¿Quién es Jev?

Jev es un modelo de decisión de [TypeSafe AI](https://typesafe.ai/blog/introducing-system-one-models-and-jev). A diferencia de un LLM, en cambio de devolver texto, devuelve una decisión: le pasas una lista de alternativas y te devuelve la más probable. Le caben unos 32 mil tokens de texto por consulta, que es más o menos un libro corto como El Principito.

El público se volvió loco, Twitter estalló. Vieron en Jev un modelo generalista que toma decisiones muy rápido y no tardaron en encontrar casos de uso entretenidos (y realmente útiles). Además, como es inevitable, salieron varias copias que incluso pueden ser mejor que Jev. Como [Clef](https://blog.cloudflare.com/clef-decision-models/) de Cloudflare y otros open source como [Laya, Nimble y Kev](https://www.deeplearning.ai/the-batch/models-built-to-do-one-thing-well), y hace poco la [Decisions API de OpenAI](https://community.openai.com/t/decisions-api-is-now-available-in-public-beta/1403877).

Lo bacán de estos modelos es que nos permiten hacer estas elecciones a un nivel parecido al de los mejores LLMs de ahora mismo.

Si te interesa saber más sobre esto, pídele a tu ChatGPT o a Claudito que te expliquen sobre fast y slow thinking ([*Pensar rápido, pensar despacio*](https://es.wikipedia.org/wiki/Pensar_r%C3%A1pido,_pensar_despacio), de Kahneman) y los System 1 y System 2.

## Dónde lo usamos en Revi

En Revi, obviamente, no nos queríamos quedar atrás. Y el patrón es fácil de reconocer: cada vez que le pedimos a un LLM que elija entre opciones que ya conocemos, ahí puede ir Jev. Así que buscamos esos lugares y probamos meterlo.

### Reconocer documentos

Un expediente de permiso de edificación trae decenas de archivos. Para empezar, Revi necesita saber cuál es la solicitud (el formulario de la solicitud, un estándar del Minvu) y cuál es el acta de observaciones de la DOM (la muni). Antes se lo preguntábamos a Gemini. Ahora Jev elige entre los nombres de los archivos, más una opción «ninguno». Tarda unos 0,4 segundos, antes aprox 3 segundos, y cuesta US$ 0,00003 por expediente. Si falla, responde Gemini como antes.

### Filtrar la normativa

Cuando alguien pregunta por normativa, el agente busca en una base vectorial con la LGUC, la OGUC, los planes reguladores y las DDU (circulares). Como sabrás, esto es un RAG de toda la vida (3 años). Cada búsqueda trae varios fragmentos y todos entran al contexto, sirvan o no. La entrada del LLM es casi todo nuestro gasto: en nuestros evals, 4,3 millones de tokens de entrada contra 45 mil de salida.

Ahora, después de cada búsqueda, Jev revisa fragmento por fragmento si ayuda a responder la pregunta, y solo pasan los que sí:

```mermaid
flowchart TB
  subgraph antes [Antes]
    direction LR
    a1[LLM] --> a2[Llamada al tool de RAG] --> a3[Respuesta con todos los fragmentos]
  end
  subgraph ahora [Ahora]
    direction LR
    b1[LLM] --> b2[Llamada al tool de RAG] --> b3[Filtro con Jev] --> b4[Respuesta con los fragmentos relevantes]
  end
  antes ~~~ ahora
  classDef jev fill:#e3ebd9,stroke:#3d7a3a,color:#2f5f2d
  class b3 jev
```

En 20 preguntas de Puerto Varas, **los tokens de entrada bajaron 43 % y el costo 38 %**, con prácticamente la misma tasa de aprobación: 18,5 de 20 contra 19. Donde más se filtra es en los planes reguladores (a.k.a. PRC): de diez fragmentos por búsqueda, suelen servir dos.

## Lo que viene

Estamos probando atacar el uso de tokens en otros dos lados. Antes de llamar una herramienta (tenemos varias para especificar normas o lecturas), que Jev decida qué herramientas usar según la tarea y el estado del agente. Por otro lado, en conversaciones largas, que descarte los resultados de herramientas que ya no sirven para lo que el usuario pregunta ahora. Todavía no tenemos números, primero necesitamos evaluaciones con conversaciones de varias preguntas.

---

Si estás haciendo agentes, revisa cuántas de tus llamadas al LLM son en verdad una elección entre opciones que ya conoces. O haz copycat de lo que hicimos: si usas RAG, filtra los resultados con Jev o algo similar, y si necesitas clasificar cosas, Jev es una salida muy fácil y rápida.
