# Orquestar agentes en la Platanus Hack

El fin de semana pasado fuimos con el equipo a participar de la [Platanus Hack](https://hack.platan.us/26-cl).

La hack tenía cinco tracks: Simulations, AI Security, Physical World, Multiplayer y Hardware. Nosotros nos fuimos por el de Simulations, porque creímos que era una oportunidad para usar el poder que nos dan los agentes para recolectar la mayor cantidad posible de datos y armar un motor, a través de evals, que nos permitiera hacer algo muy choro.

Después de elegir el track, cuando nos pusimos a pensar en un problema y en una solución, algo que sí acotamos rápido es que queríamos que la solución tuviera una propiedad bien interesante, que mejorara y se volviera más profunda a medida que más iteraciones de agentes operaran sobre ella.

Entonces, ¿qué implica esto? Que no podía ser una solución que solo creciera o mejorara añadiéndole más features o más pantallas ni nada. Teníamos solo tres minutos para presentar, y es mucho mejor enfocarse en algo que sea lo más profundo posible. Así, al mostrar cómo funciona y después explicar qué hay por debajo, la demo misma muestra todo lo que hicimos.

Una vez definido el problema que queríamos atacar, casi nos abstrajimos de él y nos enfocamos principalmente en la metodología que íbamos a usar para que el desarrollo fuera lo más rápido, eficiente y ambicioso posible. El desafío real pasó a ser cómo armar un mecanismo para orquestar la mayor cantidad de agentes posible, y que todo el código y las exploraciones que generaran nos acercaran a la solución.

## Cómo trabajamos

Apenas elegimos el track, tuvimos una reunión, que grabamos, para definir qué queríamos lograr durante la primera noche, que era la recolección de datos, la base del motor y las iteraciones en base a evals. También hablamos de qué valores queríamos que tuviera la simulación, qué nos parecía importante, qué queríamos que fuera posible y cómo queríamos que siguiera creciendo de manera autónoma cuando los agentes terminaran. Todo eso lo destilamos en un goal usando Fable 5.2 para ordenarlo.

En esa primera reunión también definimos que el approach iba a ser hacerle ingeniería inversa al pitch, e imaginarnos qué es lo que queríamos que ocurriera en los tres minutos que teníamos para presentar, como haciendo un moonshot de lo que era posible. Y después, cómo podíamos diseñar un sistema que les permitiera a los agentes implementar lo que queríamos mostrar en la demo.

Creo que este es un error que he cometido en otras hackatones, y quizás en otros ámbitos y proyectos, que es como que lo que en verdad es posible hacer con los agentes orquestando, con el conocimiento que tienen y la capacidad de iterar código, es demasiado más de lo que uno cree, o de lo que uno a veces ni siquiera se imagina que se puede hacer. Entonces, yo creo que es importante que, si uno se imagina algo en verdad como desquiciado, algo enorme que ni siquiera sabe cómo implementaría, vale la pena apuntar a eso igual y dejar que los agentes lo intenten.

## Cómo orquestamos los agentes

Las primeras horas cocinamos un [MCP de Discord](https://github.com/platanus-hack/platanus-hack-26-cl-team-14/tree/main/tools/discord-mcp) para que los agentes se pudieran orquestar ahí.

![Canal #agent-chat del Discord del equipo. Bruno pide revisar por qué hay calles vacías en la simulación; los agentes, cada uno con su nombre, su modelo y el computador donde corre, abren un thread, reportan el estado de las PRs y suben capturas del estadio trasladado a Tobalaba.](discord-agent-chat.png "El canal #agent-chat, de madrugada.")

Partimos con la idea más loca de tener muchos agentes, los máximos posibles dentro de los recursos, enchufados al Discord y listos para operar en base a lo que les dijéramos, pero eso salió más o menos mal y eran desorganizados. Después nos dimos cuenta de que no estábamos aprovechando bien los recursos e hicimos un canal donde los computadores pudieran mostrar cuánta CPU y RAM tenían libre y qué tan cerca del límite de tokens estaban.

> The team works as a swarm: one orchestrator session per laptop, coordinated in Discord.
>
> Keep 4 subagent slots ready, as section 5 of the playbook says. Take tasks that appear in Discord threads. Start or wake an agent only when a slot has a task.
>
> Skill `enjambre` del equipo, [`.agents/skills/enjambre/SKILL.md`](https://github.com/platanus-hack/platanus-hack-26-cl-team-14/blob/main/.agents/skills/enjambre/SKILL.md), 21 de noviembre de 2026

## Cosas que descubrimos

La primera noche les dejamos el goal corriendo, y en las seis horas que dormimos ya lograron como juntar 282 fuentes en el catálogo y recuperar millones de datos.

También surgieron cosas como que los agentes mismos decidieron usar Python para los scrapers y la recolección de datos, y optaron por una versión web del visualizador de Santiago que no imaginábamos, que después terminamos pivoteando a Rust para que pudiera correr lo fluido que necesitábamos.

Otra cosa interesante es que después los agentes también decidieron armar un CI/CD para verificar que el código en Rust compilara. Yo me imagino que fue porque de repente mergeaban PRs que rompían la compilación y tenían que volver a corregirlas.

Otra cosa que descubrimos es que en un momento los mismos agentes se comenzaron a enredar mucho, delegándose tareas entre sí y esperando a que los otros las terminaran, armando una maraña de dependencias entre las tareas que ni ellos mismos pudieron resolver. Así fue como decidimos hacer el primer cooldown, donde implementamos un rol nuevo para un agente, el "cerrador", que se encargaba de ir dando vueltas agente por agente preguntando qué necesitaba y cómo lo podía terminar. Ahí frenamos el prompteo de ideas nuevas y nos encargamos de cerrar una primera versión de todo antes de hacer una nueva reunión, donde nos pusimos a hablar sobre la siguiente iteración.

![Animación de la hack, del viernes en la noche al domingo a las 9:00. Arriba crecen juntas cinco curvas: PRs mergeadas (destacada en verde), commits, mensajes en Discord, comentarios en PRs e issues, e issues, cada una hasta su total final. Abajo, cada agente es una línea en la fila del computador donde corrió, y su nombre aparece cuando habla por primera vez en Discord: primero nombres de animales como gentle-fox o witty-llama, después nombres chilenos como Eliseo-21 o Raquel-35. De fondo se marcan las fases: setup del enjambre, primer enjambre, cooldown, las 5 verticales y pulido del pitch.](la-hack-hora-por-hora.mp4 "Cada curva va de cero a su propio total. Fuente: GitHub y el export de Discord del repo del equipo; el export de Discord termina el domingo a las 3:23.")
