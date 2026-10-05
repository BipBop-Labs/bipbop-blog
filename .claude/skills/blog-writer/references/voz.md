# Mantener la voz

Cómo pasar habla a texto sin que deje de sonar a la persona. Las fuentes están
al final.

## El nivel de edición

Los transcriptores distinguen niveles. Este blog usa el segundo:

| Nivel | Qué permite |
| --- | --- |
| Literal | Nada. Queda todo, con muletillas y tropiezos. |
| **Literal limpio** | Quitar relleno, tartamudeos y arranques en falso. Mantiene las palabras, la gramática y la estructura de las frases. |
| Literal inteligente | Además corrige gramática, recorta lo que se va por las ramas y parafrasea para que suene escrito. |
| Editado | Reordena y reestructura. |

Al literal limpio se le suma puntuación, tildes, párrafos y ralear las
muletillas. Parafrasear ya es el nivel siguiente, y ahí se pierde la voz.

## Qué se puede quitar

- Pausas llenas: "eh", "mmm", "este".
- Tartamudeos y repeticiones por tropiezo: "y y después", "yo, yo fui".
- Arranques en falso: "fuimos a, estábamos yendo a" queda "estábamos yendo a".
  Se deja el arranque solo si agrega algo.
- Autocorrecciones sin contenido: queda el valor final.
- Muletillas de relleno, según la prueba de más abajo.

## Qué se queda

- **Las palabras que eligió**, aunque se repitan. Si dice "bacán" tres veces,
  son tres "bacán".
- **Su gramática hablada**: chilenismos, "po", "cachái", frases que parten con
  "Y" o "Que", oraciones que un corrector marcaría.
- **Las repeticiones de énfasis**: "muy, muy lento" no es un tropiezo.
- **Los matices**: "creo que", "más o menos", "capaz que", "ni idea si". Sin
  ellos el autor termina afirmando más de lo que dijo.
- **La primera persona y el trato directo al lector**: "yo", "nosotros", "te
  cuento", "mira", "¿cachái?". Son lo primero que desaparece al pulir.
- **El razonamiento en voz alta**: "entonces", "porque", "por eso". No lo
  comprimas en una frase abstracta.
- **El ritmo**: frases largas que se encadenan y frases de tres palabras. No
  las empareje.
- **El humor, los paréntesis, las digresiones cortas, los garabatos y el
  spanglish** tal como salieron ("el tool de RAG", "aka").
- **Las autocorrecciones con contenido**: "pensábamos que era el modelo, pero
  no, era el prompt" cuenta algo.

## Muletillas: relleno o significado

La misma palabra puede ser las dos cosas. En el español de Chile, "onda", "como",
"o sea", "igual", "en el fondo", "al final" y "entonces" funcionan como
marcadores con significado, y solo a veces como tiempo para pensar.

**Primero: ¿está dentro de la frase o fuera?** Si es parte de lo que se dice
("buena onda", "es como un filtro", "me da igual"), es una palabra normal y no
se toca.

**Después, la prueba de sustitución.** Cambia el marcador por uno de estos. Si
alguno calza, tiene función y se queda:

| Si se puede cambiar por | Está haciendo esto | Ejemplo |
| --- | --- | --- |
| "es decir" | reformular o explicar | "es un modelo de decisión, o sea, elige entre opciones" |
| "por ejemplo" | dar un caso | "cosas chicas, onda, clasificar un archivo" |
| "digamos", "más o menos" | avisar que el término es aproximado | "es como un clasificador" |
| "de todas maneras", "aunque" | conceder o tomar distancia | "igual nos sirvió" |
| "en resumen" | cerrar | "al final, gastamos menos" |
| dos puntos y comillas | introducir lo que alguien dijo | "y él como: no funciona" |

Si ninguno calza y al borrarlo la frase dice lo mismo, es relleno.

**Cuánto relleno dejar.** No hay un número. El criterio de la historia oral es
dejar lo suficiente para que se reconozca la forma de hablar:

- todos los marcadores con función se quedan;
- del relleno, que no se repita el mismo en frases seguidas;
- se mantiene el orden de preferencia del autor: si su muletilla más usada es
  "como", sigue siendo la más usada en el texto.

Un texto sin ningún "como" ni "o sea" de alguien que los dice todo el tiempo
ya no es su voz.

## Errores del speech-to-text

- **Palabras en otro idioma.** El transcriptor las cambia por la palabra más
  parecida del idioma principal. La palabra existe, pero es otra. Pasa sobre
  todo con términos técnicos en inglés y nombres de productos.
- **Nombres propios**: personas, empresas, modelos, siglas.
- **Homófonos y puntuación**: "a ver" y "haber", "ahí" y "hay", preguntas sin
  signos.
- **Frases inventadas.** En las pausas largas el transcriptor a veces escribe
  una frase que nadie dijo. Sospecha de lo genérico o fuera de tema junto a un
  corte.

Qué hacer:

- Corrige solo lo que puedas confirmar: con el glosario de la hoja de voz, con
  otros posts del repo, o con una fuente.
- Lo que no puedas confirmar queda `[TODO: ¿dijo X?]`. No elijas tú.
- Cada término corregido se agrega al glosario.

## La hoja de voz

Una por autor, en `voces/<autor>.md` dentro de esta skill. Se arma con
el dictado crudo de la conversación, nunca con texto ya editado: si no, cada pasada se aleja un
poco más de la persona.

```markdown
# Voz de <autor>

## Frases de muestra
10 a 20 frases textuales de sus dictados que suenen muy a esta persona.

## Cómo habla
- Muletillas, de más a menos usada, y cuáles suelen ser relleno.
- Conectores con que arma el argumento.
- Intensificadores y expresiones propias.
- Largo de frase típico y cómo lo varía.
- Tipo de humor. Cómo le habla al lector.

## Lo que no dice
Palabras y giros que nunca usaría.

## Decisiones tomadas
Lo que el autor ya resolvió: cuánta muletilla quiere, garabatos sí o no,
términos en inglés con o sin cursiva.

## Glosario
Términos y nombres con su grafía correcta, y cómo los suele oír el
transcriptor: `Jev (lo transcribe como "Jeff")`.
```

En la primera sesión con un autor, escribe un párrafo de prueba y pregúntale
si suena a él antes de seguir. Lo que responda va a "Decisiones tomadas".
Después, actualiza la hoja cuando el autor corrija algo de tu texto.

## Ejemplo

Dictado:

> ya entonces como que lo primero que que hicimos fue eh probar el modelo con
> los archivos del expediente no y la verdad es que igual funcionó súper bien
> onda se demoraba como medio segundo y antes eran como tres o sea una
> diferencia brutal y ahí yo dije ya filo metámoslo en todos lados que
> obviamente fue una pésima idea

Bien:

> Lo primero que hicimos fue probar el modelo con los archivos del expediente.
> Y la verdad es que igual funcionó súper bien: se demoraba como medio segundo
> y antes eran como tres. O sea, una diferencia brutal. Y ahí yo dije "ya,
> filo, metámoslo en todos lados". Que obviamente fue una pésima idea.

Se fueron "ya entonces como que", "que que", "eh", "no" y "onda" (relleno). Se
quedaron "igual" (concede), los dos "como" (aproximan la cifra), "o sea"
(reformula), el "yo dije" y la frase final que parte con "Que".

Mal:

> Inicialmente evaluamos el modelo con los archivos del expediente y los
> resultados fueron excelentes: el tiempo de respuesta se redujo de tres
> segundos a medio segundo. Entusiasmados, decidimos implementarlo en todo el
> sistema, lo que resultó ser un error.

Dice lo mismo y no lo dijo nadie. Las cifras aproximadas ahora son exactas, y
"entusiasmados" no estaba.

## Fuentes

- San Martín, Rojas y Guerrero (2016), "La función discursiva de *onda* y *por
  ser* en el habla santiaguina", *Boletín de Filología* LI(2).
  https://boletinfilologia.uchile.cl/index.php/BDF/article/download/44878/46948
- Samuel Proctor Oral History Program, *Style Guide* (2016).
  https://oral.history.ufl.edu/wp-content/uploads/sites/214/SPOHP-Style-Guide-2016.pdf
- GoTranscript, "Editing oral history transcripts: what to fix and what to
  leave".
  https://gotranscript.com/en/blog/editing-oral-history-transcripts-what-to-fix-and-what-to-leave-examples
- Brass Transcripts, "Verbatim vs clean vs intelligent verbatim".
  https://brasstranscripts.com/blog/verbatim-vs-clean-vs-intelligent-verbatim-transcription
- AssemblyAI, "Dictation cleanup". https://assemblyai.com/blog/dictation-cleanup
- Gladia, "What is code-switching in speech recognition".
  https://gladia.io/blog/what-is-code-switching-in-speech-recognition
- Estudio sobre lo que cambia cuando un LLM reescribe un texto (solo el
  resumen): menos palabras funcionales y primera persona, más vocabulario y
  abstracción, también con instrucciones de mantener la voz.
  https://arxiv.org/abs/2604.22142
- River Editor, "How ghostwriters capture client voice".
  https://rivereditor.com/blogs/how-ghostwriters-capture-client-voice-first-interview

La prueba de sustitución, el criterio de cuánto relleno dejar y el formato de
la hoja de voz son reglas propias de esta skill, derivadas de esas fuentes.
