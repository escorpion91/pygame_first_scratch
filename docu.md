Hay 3 elementos de tu juego que debes construir para que el juego funcione correctamente:

- la ventana donde verás el juego
- el while loop qie mantiene corriendo al jueg0
- el event handler

Despues de instalar pygame en tu entorno virtual, o localmente, como prefieras, debes obviamente importar la librería:

```python
import pygame
```

Luego, habra que crear la ventana. La ventana necesitara de dos argumentos para crearse, el ancho y la altura. Para eso, crearemo
dos variables, una para cada una, y luego crearemos otra variable, la cual sera nuestra pantalla, usando el metodo set_mode, el cual recibe el ancho y la altura.

```python
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
```

Hasta ahora le cogio se ve asi:

```python
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))

```

si corres ese codigo anterior, una pantalla se abremilesimas de segundos y se cierra. Eso es porque no has creando el loop que mantiene al juego abierto. aqui es cuando creamos al while loop. Pero, si solo creas el while loop, el programa jamas podra cerrarse, por lo que por las mismas, deberas crear el 3er elemento del juego, el event handler, el cual hara cerrar el juego apenas le des a cerrar.

El codigo en total estaría asi:

```python
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))

run = True

while run:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False

pygame.quit()
```

explicacion:
el for loop dentro del while esta barriendo por todos los eventos, y si encuentra un match, cuyo tipo sea QUIT, como estas indicando, run se hace falso, y de esa manera, se cierra el loop. Despues de eso solo cierra pygame con el metodo quit()

Lo siguiente que viene despues, es ir ya agregando mas features a tu programa, porque ya lo tienes fucionando. por ejemplo, por ahora, creeos un rectangulo que se pueda mover con las flechas del teclado.

Para eso necesitas escribir 3 lineas de codigo.

- la primera es para crear el rectangulo y asignandolo a una variable, esto lo haces antes del while loop:

```python
player = pygame.Rect((300,250,50,50))
```

React() recibe 4 argumentos. Los dos primeros son las coordenadas x y y donde sera peusto el rectandulo. Los otros dos son ancho y altura.

Luego, ya que ya tiees creado el rectangulo, debees dibujarlo en la pantalla:

```python
pygame.draw.rect(screen,(255,0,0),player)
```

rect() recibe 3 argumentos. El primero es en donde sera dibujado, el segundo son lso colores en formato rgb, y el ultimo argumeto es el rectangulo en si. Esta linea ya va escrita dentro del while loop. Al principio.

Ahora la 3ra linea, para que se actualize la pantalla, debes escribir:

```python
pygame.display.update()
```

Eso lo escirbes tb dentro del while loop. Al final o cuando quieras que se actualize la pantalla.

El codigo hasta ahora esta asi:

```python
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))

player = pygame.Rect((300,250,50,50))

run = True

while run:

    pygame.draw.rect(screen,(255,0,0),player)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False

    pygame.display.update()

pygame.quit()
```

Ahora queremos mover ese rectangulo. Para eso, se crea un objeto que tenga todos los key commandos de nuestro teclado, y la idea es que, con un condicional,
hagamos una accion dependiendo de que tecla este siendo presionada.

```python
    key = pygame.key.get_pressed()

    if key[pygame.K_a] == True:
        player.move_ip(-1,0)
    elif key[pygame.K_d] == True:
        player.move_ip(1,0)
    elif key[pygame.K_w] == True:
        player.move_ip(0,-1)
    elif key[pygame.K_s] == True:
        player.move_ip(0,1)
```

creamos un objeto key con el metodo get_pressed. Ahora si te das cuenta, en cada condicional, estamos indexando, para checar si hay o no una tecla presionada. Luego para mover al personaje, estamos usando el metodo move_ip() el cual recibe dos coordenadas para saber que tanto mueve.

De esta manera,m se mueve el rectangulo, pero hay un proeblema, el rectanguloe sta dejando un rastro de donde estuvo, y eso es porque la pantalla no se esta refresheando. Asi que justo apenas entras al while loop, debes escirbir:

```python
    screen.fill((0,0,0))
```

EL codigo hasta ahora seria asi, y con esto, ya tnes un rectangulo que se mueve:

```python
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))

player = pygame.Rect((300,250,50,50))

run = True

while run:

    screen.fill((0,0,0))

    pygame.draw.rect(screen,(255,0,0),player)

    key = pygame.key.get_pressed()
    if key[pygame.K_a] == True:
        player.move_ip(-1,0)
    elif key[pygame.K_d] == True:
        player.move_ip(1,0)
    elif key[pygame.K_w] == True:
        player.move_ip(0,-1)
    elif key[pygame.K_s] == True:
        player.move_ip(0,1)



    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False

    pygame.display.update()

pygame.quit()
```
