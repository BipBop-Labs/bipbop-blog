# Orquestar agentes en la Platanus Hack

El fin de semana pasado fuimos con el equipo a participar de la [Platanus Hack](https://hack.platan.us/26-cl).

Dentro de la Platanus Hack había cinco tracks: Simulations, AI Security, Physical World, Multiplayer y Hardware. Nosotros nos fuimos por el de simulación, porque creímos que era también una oportunidad para utilizar el poder que nos dan los agentes para recolectar como la mayor cantidad posible de datos y armar un motor a través de evals que nos permita hacer algo muy choro.

Después de elegir el track, cuando nos pusimos a pensar en un problema y en una solución, algo que sí acotamos rápidamente es que queríamos que la solución tuviera una propiedad bien interesante, que es como: necesitamos que la solución mejore y se vuelva más profunda a medida que más iteraciones de agentes operan sobre ella.

Entonces, ¿qué implica esto? Como que no puede ser una solución que solo creciera o mejorara añadiéndole más features o más pantallas ni nada, porque, pensando en que tenís que presentar tres minutos solamente, y es mucho mejor enfocarte en algo que sea lo más profundo posible. Así, cuando comienzas a mostrar cómo funciona y después explicas qué es lo que estamos haciendo por debajo, se ejemplifica lo que estamos haciendo.

Y además estas soluciones que son más profundas también nos dan la posibilidad de que, mientras más tiempo y más recursos de agentes orquestando y haciendo cosas tengamos, más detallada se vuelve la simulación.

Y algo interesante que hicimos, o un enfoque que quisimos tomar, es como al final casi que abstraernos un poco de cómo funcionaba o del problema específico que estábamos resolviendo, después de que ya definimos cuál era el problema que queríamos atacar, y enfocarnos principalmente en la metodología que íbamos a usar para poder hacer que el desarrollo fuera lo más rápido, eficiente y ambicioso posible.

Entonces, una visión que teníamos era que, más allá de ser un problema de código lo que queríamos resolver, es un problema de cómo definimos un mecanismo para orquestar la mayor cantidad de agentes y generar la mayor cantidad de códigos, exploraciones y todo para moverse hacia nuestro problema.

## Cómo trabajamos

Básicamente nuestro approach desde el principio fue como, ya, uno: apenas elegimos el track, grabamos y tuvimos una reunión donde hablamos qué es lo que queríamos lograr como goal durante la primera noche, que fue como toda esta recolección de datos, más la base del motor, más como las iteraciones en base a evals, etc. Y cómo queríamos que hiciera esto, qué valores queríamos que tuviese, qué puntos nos parecían importantes para simulación, qué queríamos que fuera posible y, en el fondo, también cómo queríamos que creciera de manera autónoma, si es que terminaban ese goal los agentes. Y eso lo destilamos en un goal usando Fable 5.2 para ordenarlo y orquestarlo.

Algo que al principio, en la primera reunión, definimos de antemano fue, bueno, además de que íbamos a encontrar una solución que tuviese la propiedad de que pudiera ser expandida y mejorada infinitamente por los agentes, es que al final íbamos a hacer como la ingeniería inversa de los pitches, e imaginarnos qué es lo que queríamos que ocurriese en estos tres minutos que teníamos para presentar, como haciendo un moonshot de lo que era posible. Y después, cómo podíamos diseñar un sistema que permite a los agentes posiblemente implementar algo que nos permita hacer lo que queremos hacer en la demo.

Entonces, creo que también este es un error que he cometido en otras hackatones, y en otros, quizás, ámbitos y proyectos, que es como en verdad lo que es posible hacer con los agentes y orquestando y con el conocimiento que tienen y la capacidad de iterar código, etc., es demasiado más de lo que uno cree, o uno ni siquiera a veces se imagina que se puede hacer. Entonces, como que yo creo que también es importante que de repente, si te imaginas algo que es en verdad como desquiciado, y como que fuera completamente algo que ni siquiera te imaginas la implementación de lo que vas a hacer, como podía ser cosas que son como enormes y en verdad como fuera lo que uno se imagina que puede caer [TODO: la frase queda sin cerrar; ¿qué querías decir con "lo que uno se imagina que puede caer"?].

Bueno, en esa reunión, además de ese goal en específico, también destilamos cómo queríamos que se ordenaran nuestros agentes en Discord. Entonces, como que ahí nuestro approach fue, dijimos: vamos a crear un Discord, vamos a hacer que cada uno de nuestros computadores permanezca prendido y tengan la mayor cantidad de agentes que quepan dentro de los recursos, atentos al Discord, para comenzar a solucionar cosas.

Algo que cocinamos la primera noche es como ni siquiera enfocarnos en el problema aún. Como que lo que estábamos haciendo fue desarrollar también el [MCP de Discord](https://github.com/platanus-hack/platanus-hack-26-cl-team-14/tree/main/tools/discord-mcp) para que los agentes se pudieran orquestar y ordenar a través de este servidor.

![Canal #agent-chat del Discord del equipo. Bruno pide revisar por qué hay calles vacías en la simulación; los agentes, cada uno con su nombre, su modelo y el computador donde corre, abren un thread, reportan el estado de las PRs y suben capturas del estadio trasladado a Tobalaba.](discord-agent-chat.png "El canal #agent-chat, de madrugada.")

Y ahí también es importante dentro del blog, yo creo que vamos a ir mostrando cómo en el fondo partimos con la idea más loca de como tener muchos agentes, nomás los máximos posibles dentro de los recursos, enchufados al Discord y listos para operar en base a lo que les dijéramos, pero como que eso estaría más o menos mal y eran desorganizados. Entonces después nos dimos cuenta que no estábamos aprovechando bien los recursos e hicimos un canal donde pudieran mostrar los computadores cuántos recursos tenían, cuántas CPU, cuántas RAM, qué tan cerca de los tokens estaban, etc.

> The team works as a swarm: one orchestrator session per laptop, coordinated in Discord.
>
> Keep 4 subagent slots ready, as section 5 of the playbook says. Take tasks that appear in Discord threads. Start or wake an agent only when a slot has a task.
>
> Skill `enjambre` del equipo, [`.agents/skills/enjambre/SKILL.md`](https://github.com/platanus-hack/platanus-hack-26-cl-team-14/blob/main/.agents/skills/enjambre/SKILL.md), 21 de noviembre de 2026

## Cosas que descubrimos

Y bueno, lo otro interesante: cosas que descubrimos a medida que fueron iterando los agentes. La primera noche lo que hicimos fue dejarles el goal de llegar con la iteración del motor como lo más profunda posible y recolectar la mayor cantidad de datos que puedan. Y ahí, bueno, pasó que en la primera noche nomás, que en verdad fueron seis horas de sueño que tuvimos, ya lograron como scrapear más de 70 cosas distintas [TODO: en el repo, a las 9:00 del sábado había 28 scripts en tools/scrape y 282 fuentes en el catálogo de context/research/sources; ¿de dónde sale 70?] y recuperar miles de datos o millones de datos [TODO: no pude verificar el volumen; data/raw no está en git].

Y también surgieron cosas como que los agentes mismos decidieron cómo usar Python para hacer todo esto de scrapers y cosas y recolectar datos [TODO: la regla "Use only the Python standard library" está en context/research/sources/README.md, commiteada desde la sesión de Emerson; confirmar que la eligió un agente y no una persona], y además optaron por una versión web del visualizador de Santiago que no imaginábamos, que después terminamos pivoteando a Rust para que pudiera correr los fluidos [TODO: ¿dijo "fluido"?] que necesitábamos.

![Animación de la hack, del viernes en la noche al domingo a las 9:00. Arriba crecen juntas cinco curvas: PRs mergeadas (destacada en verde), commits, mensajes en Discord, comentarios en PRs e issues, e issues, cada una hasta su total final. Abajo, cada agente es una línea en la fila del computador donde corrió, y su nombre aparece cuando habla por primera vez en Discord: primero nombres de animales como gentle-fox o witty-llama, después nombres chilenos como Eliseo-21 o Raquel-35. De fondo se marcan las fases: setup del enjambre, primer enjambre, cooldown, las 5 verticales y pulido del pitch.](la-hack-hora-por-hora.mp4 "Cada curva va de cero a su propio total. Fuente: GitHub y el export de Discord del repo del equipo; el export de Discord termina el domingo a las 3:23.")
