# *Jev*ification en Revi

## ¿Quién es Jev y por qué sale en mi feed?

Jev es un modelo que lanzó hace poco, la semana del 18, entre empanadas, [TypeSafe AI](https://typesafe.ai/blog/introducing-system-one-models-and-jev), una startup de Diogo Almeida, que antes trabajaba en OpenAI.

Tiene una gracia: a diferencia de los LLMs que ya tenemos, este es un modelo clasificador generalista, o System One Model, como lo llama TypeSafe. En el fondo, recibe inputs de texto y, en un tiempo ínfimo en comparación a lo que se demora un LLM en generar texto, toma una decisión que viene con un cierto grado de confianza que entrega el mismo modelo. TypeSafe habla de entre 70 y 500 milisegundos, contra 3 segundos o más de un LLM. Cuesta US$ 0,042 por millón de tokens de entrada y la salida es gratis.

El desafío que existía antes con los LLMs, y bueno, que en verdad sigue existiendo, es que a veces tú quieres outputs de texto libre, y eso está bien, pero a veces necesitas que el output sea una elección dentro de una lista que ya existe, o un output estructurado dentro de algo que ya está definido.

Entonces, lo que viene a resolver este modelo, y todos los que han salido después, como [Clef](https://blog.cloudflare.com/clef-decision-models/) de Cloudflare y otros open source como [Laya, Nimble y Kev](https://www.deeplearning.ai/the-batch/models-built-to-do-one-thing-well), es que nos permiten hacer estas elecciones de manera muy rápida y a un nivel parecido al de los mejores LLMs de ahora mismo.

## Dónde lo usamos en Revi

En Revi, el agente toma muchas decisiones chicas que no necesitan un LLM: qué documento es cuál, qué fragmento de normativa sirve, qué herramienta usar. Ahí pusimos a Jev.

## Reconocer documentos

Un expediente de permiso de edificación trae decenas de archivos. Para empezar, Revi necesita saber cuál es la solicitud (el FUN) y cuál es el acta de observaciones de la DOM. Antes se lo preguntábamos a Gemini. Ahora Jev elige entre los nombres de los archivos, más una opción «ninguno». Tarda unos 0,4 segundos, antes [TODO: X s con Gemini], y cuesta US$ 0,00003 por expediente. Si falla, responde Gemini como antes.

## Filtrar la normativa

Cuando alguien pregunta por normativa, el agente busca en una base vectorial con la LGUC, la OGUC, los planes reguladores y las DDU. Cada búsqueda trae varios fragmentos y todos entran al contexto, sirvan o no. La entrada es casi todo nuestro gasto: en las pruebas, 4,3 millones de tokens de entrada contra 45 mil de salida.

Ahora, después de cada búsqueda, Jev revisa fragmento por fragmento si ayuda a responder la pregunta, y solo pasan los que sí. En 20 preguntas de Puerto Varas, **los tokens de entrada bajaron 43 % y el costo 38 %**, con prácticamente la misma tasa de aprobación: 18,5 de 20 contra 19. Donde más se filtra es en los planes reguladores: de diez fragmentos por búsqueda, suelen servir dos. Llega a producción en los próximos días.

## Lo que viene

Queremos atacar los tokens desde dos frentes más. Antes de actuar, que Jev decida qué herramientas usar según la tarea y el estado del agente. Después, en conversaciones largas, que descarte los resultados de herramientas que ya no sirven para lo que el usuario pregunta ahora. Todavía no tenemos números: primero necesitamos evaluaciones con conversaciones de varias preguntas.

Jev no reemplaza al LLM, que sigue razonando y escribiendo las respuestas. Le quita el trabajo de elegir entre opciones conocidas. Tampoco es infalible: puede equivocarse con mucha seguridad, y [hay pruebas](https://x.com/nikhilmudholkar/status/2100604560335139083) donde pierde contra Gemini. Por eso siempre dejamos un camino de respaldo y medimos antes de cambiar.
