# Citas y verificación

Cómo encontrar la cita que el autor pidió y cómo revisar lo que afirmó. Las
fuentes están al final.

## Qué se verifica

Recorre el dictado frase por frase preguntando "¿de dónde sale esto?, ¿cómo
sabemos que es cierto?". Separa las frases compuestas en afirmaciones sueltas:
"salió en septiembre y le caben 32 mil tokens" son dos.

Siempre se revisa:

- nombres de personas, empresas y productos, y cómo se escriben;
- cargos y a qué organización pertenece alguien;
- fechas y orden de los hechos;
- cifras, unidades y orden de magnitud (¿miles o millones?);
- quién dijo qué;
- cómo funciona algo técnico;
- supuestos: lo que la frase da por hecho sin decirlo.

Con más cuidado: generalizaciones ("todos están usando", "los estudios
dicen"), lo que contradice lo conocido, lo que deja mal a una persona o empresa
con nombre, y comparaciones ("el más rápido", "el primero").

No se verifica, pero se anota como tal:

- **opinión**: "es una pésima idea";
- **predicción**: "en un año nadie va a usar esto";
- **experiencia propia y datos internos**: "nos bajó el costo 38 %". Si el dato
  está en el repo o en otro post, crúzalo. Si no, pregunta al autor de dónde
  sale: la carga de la prueba es de quien afirma.

Un dato dentro de una opinión se verifica igual: en "es absurdo que cueste 20
dólares", los 20 dólares se revisan.

## Cómo se verifica una afirmación

La gente busca con palabras que confirman lo que ya cree, y casi nadie se da
cuenta de que lo hace. Proponerse ser neutral no alcanza, así que el orden de
las búsquedas es fijo:

1. **Búsqueda neutra.** Solo los sustantivos del tema, sin la cifra ni el
   adjetivo del autor. Para "Jev responde en 0,4 segundos": `Jev latencia`,
   no `Jev 0,4 segundos`.
2. **Búsqueda en contra.** Lo que tendría que existir si el autor estuviera
   equivocado: el valor contrario, "crítica", "problema", "mito", "desmentido",
   "vs". Hazla siempre, aunque la primera ya haya confirmado.
3. **Búsqueda a favor**, al final y solo si falta.

Después:

4. **Lee hacia el lado.** Antes de confiar en una página que no conoces, busca
   qué dicen otros de ese sitio. Que tenga logo, referencias y buen diseño no
   prueba nada.
5. **Sube hasta el origen.** Sigue los links hasta el documento, el paper, el
   dato o la declaración original, y léelo ahí. La versión que te llegó puede
   estar mal resumida.
6. **Anota lo que apoya y lo que contradice.** Las dos cosas van al informe.

Juzga la afirmación con lo que se sabía en la fecha de la que habla el autor,
y revisa si desde entonces cambió.

## Qué fuente vale

De mejor a peor:

1. el documento o dato original: paper, ley, repositorio, anuncio oficial,
   grabación;
2. estadística oficial;
3. prensa o análisis serio que enlaza su fuente;
4. agregador, nota de prensa, copia sindicada;
5. foro, hilo, blog sin fuentes.

Cuántas: una basta si es el origen. Si no, dos independientes.

**Independientes se cuenta por origen, no por página.** Diez notas que repiten
un mismo tuit son una fuente. Señales de que varias páginas vienen de la
misma:

- la misma frase o la misma cifra rara y exacta en todas;
- ninguna enlaza un origen, o todas las cadenas de links terminan en la misma
  página;
- todas son posteriores a una misma publicación viral o a una edición de
  Wikipedia.

## Cifras

Confirma el valor, la unidad, el orden de magnitud, la fecha o período, sobre
quiénes se midió y qué mide exactamente: tasa o cantidad, mediana o promedio,
porcentaje o puntos porcentuales. Usa la versión más reciente del dato y di de
cuándo es.

## Citas textuales

- Entre comillas va solo texto copiado de una fuente que abriste. Si no
  encuentras las palabras exactas, se parafrasea con atribución.
- Busca la aparición más antigua de la frase. Las citas famosas suelen estar
  mal atribuidas: alguien que hablaba *sobre* una persona termina citado como
  esa persona, o una versión resumida pasa por la original.
- Lee el párrafo completo: confirma que en contexto dice lo que el autor
  quiere que diga.
- Si la atribución no se puede cerrar, escribe "atribuida a".
- Una cita traducida se marca como traducción y se enlaza al original.

## Reglas para el agente

Los modelos fallan aquí de formas conocidas: inventan referencias, dan links
reales que no contienen el dato, presentan una paráfrasis como cita y le dan
la razón a quien pregunta.

1. Nunca cites de memoria. Toda cita viene de una página abierta en esta
   sesión.
2. El resultado de un buscador no es una lectura. Abre la página.
3. Encuentra el pasaje exacto que respalda la afirmación y cópialo al informe.
4. Confirma que el pasaje respalda *esa* afirmación: el mismo número, la misma
   entidad, la misma fecha. Que hable del tema no basta.
5. Enlaza al que publicó primero, no a una copia.
6. Si no encuentras fuente, el veredicto es "no se pudo verificar". No pongas
   la fuente más parecida.
7. Decide el veredicto con la evidencia, no con la seguridad con que lo dijo el
   autor.

## Veredictos

| Veredicto | Cuándo | En el post |
| --- | --- | --- |
| Confirmado | La fuente dice lo mismo | Nada, o el link si aporta |
| Casi | Cierto con un matiz, o la cifra está un poco corrida | `[TODO: ...]` con el matiz |
| Incorrecto | La evidencia dice otra cosa | `[TODO: ...]` con lo que dice la fuente |
| Desactualizado | Fue cierto y cambió | `[TODO: ...]` con el dato vigente |
| Mal atribuido | La cita existe, pero es de otra persona | `[TODO: ...]` con el autor real |
| No se pudo verificar | Sin fuente a favor ni en contra | `[TODO: sin fuente para ...]` |
| No verificable | Opinión, predicción, experiencia propia | Nada |

## Cómo queda en el markdown

El formato sale del `README.md` del repo. No uses HTML ni notas al pie.

- **Dato con fuente**: link en línea sobre las palabras que respalda.

  ```markdown
  El modelo lo anunció [la empresa](https://ejemplo.com/anuncio) en septiembre.
  ```

- **Cita textual**: bloque de cita con quién, dónde y cuándo.

  ```markdown
  > El texto exacto, copiado de la fuente.
  >
  > Nombre Apellido, [título de la fuente](https://ejemplo.com/fuente), marzo de 2026
  ```

- **Cita pedida que no se encontró**:
  `[TODO: no encontré la fuente de X; lo más cercano es <link>, que dice Y]`.

- **Afirmación que no pasó**: la frase del autor queda intacta y el `[TODO]`
  va justo después.

  ```markdown
  Le caben unos 64 mil tokens por consulta. [TODO: el anuncio dice 32 mil: https://ejemplo.com/anuncio]
  ```

Los `[TODO: ...]` salen en rojo en el sitio, así que el post no se publica con
uno sin que el autor lo vea.

## El informe al autor

El verificador documenta y el autor decide. Una entrada por cada afirmación
que no quedó confirmada:

```markdown
**Lo que dijiste:** "le caben como 64 mil tokens"
**Veredicto:** Incorrecto
**Lo que dice la fuente:** "<pasaje copiado tal cual>" (quién publica, título, fecha, <link>)
**En contra / a favor:** no encontré ninguna fuente que diga 64 mil
**Sugerencia:** "le caben unos 32 mil tokens"
```

Las correcciones de nombres y fechas también se proponen así. Las confirmadas
se resumen en una línea con sus links, para que el autor pueda repetir la
revisión si quiere.

## Fuentes

- KSJ Science Editing Handbook, capítulo de fact-checking.
  https://ksjhandbook.org/fact-checking-science-journalism-how-to-make-sure-your-stories-are-true/the-fact-checking-process/
- IFCN, Code of Principles. https://www.ifcncodeofprinciples.poynter.org/the-commitments
- Full Fact, "How we fact check". https://fullfact.org/how-we-fact-check/
- PolitiFact, metodología del Truth-O-Meter.
  https://www.politifact.com/article/2018/feb/12/principles-truth-o-meter-politifacts-methodology-i/
- Mike Caulfield, "SIFT (The Four Moves)". https://hapgood.us/2019/06/19/sift-the-four-moves/
- Estudio sobre cómo las creencias previas sesgan los términos de búsqueda (21
  experimentos). https://knowledge.uchicago.edu/records/dnjcv-y9088
- Wikipedia, "Circular reporting". https://en.wikipedia.org/wiki/Circular_reporting
- Quote Investigator, "About". https://quoteinvestigator.com/about/
- Revisión de errores de cita en revistas médicas: 25,4 % de las referencias
  con error. https://pmc.ncbi.nlm.nih.gov/articles/PMC4627914
- Citas de LLM que la fuente no respalda (solo el resumen).
  https://arxiv.org/abs/2402.02008
- Columbia Journalism Review, comparación de ocho buscadores con IA.
  https://www.cjr.org/tow_center/we-compared-eight-ai-search-engines-theyre-all-bad-at-citing-news.php
- Complacencia de los modelos con las creencias del usuario (solo el resumen).
  https://arxiv.org/abs/2310.13548

El orden fijo de búsquedas, la escala de veredictos, el formato del informe y
las reglas para el agente son propias de esta skill, derivadas de esas fuentes.
