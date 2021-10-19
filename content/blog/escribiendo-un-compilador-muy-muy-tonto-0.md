+++
title = "Escribiendo un compilador muy muy tonto 0: Introducción"
date = "2021-10-17T20:18:52-03:00"

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

tags = ["compilador","rust","vvdc"]
+++
*Esta es la primer parte introductoria de varios blog posts donde documento el proceso de desarrollo de un compilador muy muy tonto.*
## Introducción
Desde chico siempre me fascinó saber cómo funcionaban las cosas relacionadas con las computadoras, especialmente del software. Es por esto que aprendí a programar, para saber cómo funcionaba y poder crear mis propios juegos o aplicaciones.

Pero esta curiosidad no paró ahí. Podía hacer un sencillo juego en C, pero me seguía pareciendo magia. ¿Cómo se traducían esas líneas de código a gráficos que podía controlar en la pantalla? Desde que ejecutabas `gcc mijuego.c -o mijuego` hasta que podías ejecutarlo pasaba por una caja negra donde no tenía ni idea qué ocurría.

![[0_blackbox.png]]

En ese momento no llegué a profundizar mucho más, pero últimamente me picó la curiosidad de nuevo por el tema, y en búsqueda de algún proyecto nuevo, decidí ponerme a escribir un compilador. El compilador más tonto posible: así nació **vvdc (very very dumb compiler)**.

En realidad, el proceso de "caja negra" son varios procesos, lo que comúnmente a veces se denomina "compilar" o "interpretar" puede estar formado de varios procesos internos que quizá incluso no sean parte del mismo programa:

![[1_complex.png]]

El proyecto que tengo en mente va a abarcar **solo el compilador**, es decir, la primer flecha; ya que es, en mi opinión, el área más interesante y donde vamos a definir la gramática y funcionamiento de nuestro lenguaje de programación. Vamos a generar código ensamblador que luego pasaremos a `nasm`. Esto va a producir un archivo binario que nuestro sistema operativo (y finalmente el CPU) va a saber ejecutar.

## vvdl (very very dumb language)
La idea de un compilador es **traducir un lenguaje de programación a un lenguaje máquina**; por ende vamos a necesitar definir nuestro lenguaje.
Como mi idea es que el proyecto no me lleve 5 años, decidí pensar en el lenguaje más sencillo posible, y después ir expandiendo sobre eso:

```go
abs(x) {
	if x < 0 {
		return x * -1;
	} else {
		return x;
	}
}

main() {
	y = 0;
	while (y > -100) {
		y = y - 1;
	}
	y = abs(y);
	print("res: " y);
}
```
Cómo se puede ver, la syntaxis es muy C-like estándar, pero **decidí reducir el lenguaje a lo mínimo posible**: por ahora solo hay `if/else` , `while`, `return` y `print`; no hay tipado estático, y de hecho solo tenemos 2 tipos posibles: números enteros (`i64`) y `string`.

Este lenguaje está 100% sujeto a cambios a futuro, de hecho es muy probable que estos ocurran.

## El plan

El plan entonces es ir desarrollando el compilador en mis tiempos libres, a medida que voy documentando el proceso mediante estos blog posts.[^1]

Decidí escribir el compilador en **Rust** entre otras razones porque es un lenguaje que quiero aprender hace rato y vengo posponiendo, esto presenta el ligero drawback de que no se utilizar bien del todo el lenguaje, pero confío en que no va a ser un problema mayor.

Voy a estar haciendo uso extensivo de tests, la idea es utilizar algo similar a **TDD** donde escribo primero el test y luego implemento lo necesario para que este pase, aunque no voy a aplicar la metodología de manera estricta y voy a ser muy flexible con esto.

Sin más, durante los próximos posts voy a estar explicando, medio a modo de bitácora, el proceso de desarrollo de **vvdc**. Es muy importante destacar que **esto no es un tutorial. No se nada de compiladores.** mayormente escribo esto con el objetivo de documentar el proceso de desarrollo, motivarme a seguir trabajando en el proyecto, y brindar esta información a quien le sea de utilidad.

Prometo que el resto de los posts va a tener más contenido técnico y menos prosa.

