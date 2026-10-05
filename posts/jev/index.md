# *Jev*ification en Revi

La semana del 18 (de septiembre), probablemente mientras te comías una empanada, se lanzó Jev. Un modelo abrió un submundo para todos los que estamos trabajando desarrollando agentes.

## ¿Quién es Jev?

Jev es un modelo de decisión de [TypeSafe AI](https://typesafe.ai/blog/introducing-system-one-models-and-jev). A diferencia de un LLM, en cambio de devolver texto, devuelve una decisión: le pasas una lista de alternativas y te devuelve la más probable. Le caben unos 32 mil tokens de texto por consulta, que es más o menos un libro corto como El Principito.

[TODO: en el mismo estilo, acá hacemos la comparativa de las tareas donde es útil vs. los LLM]

El público se volvió loco, Twitter (ni cagando le digo X) estalló. Vieron en Jev un modelo generalista que toma decisiones muy rápido y no tardaron en encontrar casos de uso entretenidos (y realmente útiles). Además, como es inevitable, salieron varias copias que incluso pueden ser mejor que Jev. Como [Clef](https://blog.cloudflare.com/clef-decision-models/) de Cloudflare y otros open source como [Laya, Nimble y Kev](https://www.deeplearning.ai/the-batch/models-built-to-do-one-thing-well).

Lo bacán de estos modelos es que nos permiten hacer estas elecciones a un nivel parecido al de los mejores LLMs de ahora mismo.

Si te interesa saber más sobre esto, pídele a tu ChatGPT o a Claudito que te expliquen sobre slow y fast thinking y los System One.

## Dónde lo usamos en Revi

En Revi, obviamente no queremos quedarnos atrás y es rápido hacer el reconocimiento de patrones para saber dónde podemos y probamos en meterlo.

### Reconocer documentos

Un expediente de permiso de edificación trae decenas de archivos. Para empezar, Revi necesita saber cuál es la solicitud (el formulario de la solicitud, un estándar del Minvu) y cuál es el acta de observaciones de la DOM (la muni). Antes se lo preguntábamos a Gemini. Ahora Jev elige entre los nombres de los archivos, más una opción «ninguno». Tarda unos 0,4 segundos, antes aprox 3 segundos, y cuesta US$ 0,00003 por expediente. Si falla, responde Gemini como antes.

### Filtrar la normativa

Cuando alguien pregunta por normativa, el agente busca en una base vectorial con la LGUC, la OGUC, los planes reguladores y las DDU (circulares). Cada búsqueda trae varios fragmentos y todos entran al contexto, sirvan o no. La entrada del LLM es casi todo nuestro gasto: en las pruebas, 4,3 millones de tokens de entrada contra 45 mil de salida.

Ahora, después de cada búsqueda, Jev revisa fragmento por fragmento si ayuda a responder la pregunta, y solo pasan los que sí:

```
Antes: llm -> llamada al tool de RAG -> respuesta con todos los fragmentos
Ahora: llm -> llamada al tool de RAG -> filtro con Jev -> respuesta con los fragmentos que Jev filtró
```

En 20 preguntas de Puerto Varas, **los tokens de entrada bajaron 43 % y el costo 38 %**, con prácticamente la misma tasa de aprobación: 18,5 de 20 contra 19. Donde más se filtra es en los planes reguladores (aka PRC): de diez fragmentos por búsqueda, suelen servir dos.

## Lo que viene

Queremos atacar los tokens desde dos frentes más. Antes de llamar una herramienta (tenemos varias para especificar normas o lecturas), que Jev decida qué herramientas usar según la tarea y el estado del agente. Después, en conversaciones largas, que descarte los resultados de herramientas que ya no sirven para lo que el usuario pregunta ahora. Todavía no tenemos números: primero necesitamos evaluaciones con conversaciones de varias preguntas.

---

Jev no reemplaza al LLM, que sigue razonando y escribiendo las respuestas. Le quita el trabajo de elegir entre opciones conocidas. Tampoco es infalible: puede equivocarse con mucha seguridad, y [hay pruebas](https://x.com/nikhilmudholkar/status/2100604560335139083) donde pierde contra Gemini. Por eso siempre dejamos un camino de respaldo y medimos antes de cambiar.
