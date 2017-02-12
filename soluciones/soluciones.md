# EjerciciosC3

1.- Indica que tipos deben tener las variables var1, var2 y var3 para que el siguiente
fragmento sea correcto:
```
var1 = 5.5;
var2 = &varl;
var3 = var2;
var2 = var1 + **var3;
```

> A var1 se le asigna un valor real, por lo que su tipo ha de ser o bien float, o bien double. Asumiremos que es float.
var2 recibe la dirección donde está almacenada varl, por lo que var2 es un puntero. Como var1 es float, var2 tendrá por tipo float
La línea *var3 significa que al vaor apuntado por var3 se le asigna var2. Es decir, el valor apuntado por var3 es del mismo tipo que var2. Por tanto, var3 es un puntero a un puntero a
flotante: float
La última línea confirma nuestras tres suposiciones.

2.- ¿Existe algún problema con el siguiente código?

```
long dato = 0;
long *ptrDato;
ptrDato = dato;
```
> El código compila, pues no hay ningún error sintáctico ni semántico (a nivel de tipos). Sin embargo, en ejecución se pueden producir errores, debido a que intentamos
almacenar dato en la dirección de memoria apuntada por ptrDato. Pero ptrDato no ha sido inicializado, por lo que puede estar apuntando a cualquier sitio, seguramente a un lugar
donde no podemos (o debemos) escribir.

3.- ¿Qué problemas hay en el siguiente código?

```
void main(void)
int *ptrl, ptr2;
int datl = 5, dat2 = 4;

ptrl = 4;
free(ptrl);
ptr1 = malloc(l);

ptrl = 5;
(ptr2 + 1) = 3;
ptr1 = 5;

return 0;
```

> El estándar de C exige que la función main devuelva un entero. Si un compilador concreto soporta que la función main no devuelva nada es una licencia que se toma, para “facilitar” el trabajo al programador. Siendo puristas, deberíamos hacer que main
devolviera un entero. En cualquier caso, si lo dejáramos como void, la última línea (return 0) estaría mal, pues estariamos diciendo que es un procedimiento y luego devolveríamos un valor.

> El nombre de la variable ptr2 declarada en la primera línea parece indicar que queremos que sea de tipo puntero. Sin embargo, el * sólo afecta a la primera variable, no a la segunda.

> El estándar de C sólo permite inicializar la á/ííma MMlb/€ de una declaración. Por tanto, la inicialización de dat1 en su declaración es incorrecta según el estándar (aunque algunos compiladores lo permitan).

> La línea *ptr1 = 4 sufre el mismo problema que en el ejercicio anterior. Deberíamos pedir memoria para ptr1 antes de utilizarlo (usando malloc). Así, además,
conseguimos que la línea free (ptr1) no intente liberar una memoria no controlada por el gestor de memoria dinámica.

> La línea ptr1 = malloc(l) pide memoria pam un byte, no para el número de bytes que ocupe un entero. Por tanto, la línea siguiente escribirá en memoria que no
poseemos. La solución es pedir la memoria suficiente.

> La línea * (ptr2 + 1) = 3 sufre el mismo problema que *ptrl : 4. La diferencia es que ahora tenemos que pedir memoria para dos enteros en ptr2, porque con
el incremento del puntero estamos accediendo al entero siguiente al apuntado por ptr2.

> La asignación ptr1 = 5 no compila, pues se producen discrepancias de tipos.

> Por último, faltaría liberar toda la memoria que se ha pedido.

> Un posible modo de arreglar todos los problemas sería con el siguiente código:

```
int main(void)
  int *ptrl, *ptr2;
  int dat1, dat2 = 4;


  dat1 = 5;
  ptr1 = malloc(sizeof(int));
  if (ptrl == NULL)
     return 1;
  ptrl = 4;
  free(ptrl);
  ptr1 = malloc(sizeof(int));
  if (ptrl == NULL)
      return 1;
  ptrl = 5;
  ptr2 = malloc(2*sizeof(int));
  if (ptr2 == NULL)
     return 1;
  (ptr2 + 1) = 3;
  ptrl = 5;
  free(ptrl);
  free(ptr2);
  return 0;
```

4.- Construye un array dinámico para almacenar una sopa de letras de dimensiones
leídas por teclado.

> Podríamos pedir memoria con un malloc simple. El problema es que el acceso se tendría que realizar únicamente con una ¿”dirección, y tendríamos que preocuparnos
nosotros del acceso. En lugar de eso, queremos poder poner algo como:

`sopa[3][4] = 'A';`

> Para eso, necesitaremos un doble puntero, de modo que el primer índice
desreferencie el primer puntero, llegando a un array de punteros (uno por cada fila), y
desreferenciar el nuevo puntero nos lleve al array de caracteres (uno por cada columna):

```
char **sopa;

unsigned int alto;
unsigned int ancho;
unsigned int contador;

// [..] Leemos por teclado alto y ancho

sopa malloc(alto * sizeof(char*));
for (contador = 0; contador < alto; contador++)
sopa[contador] malloc(ancho * sizeof(char));
```
> Por simplicidad, no se ha tenido en cuenta la posibilidad de que algún malloc devuelva NULL.

5.- Dado el siguiente fragmento de programa:

```
float a = 0.001;
float *b;
float *c;

a;
b;
c + *b;
```
Cual de las siguientes afirmaciones es cierta?

* Las variables b y c se almacenan en la misma dirección de memoria.
* La sentencia *c = 4; modiñcaría el contenido de la variable a.
* a tomará un valor indeterminado.
* c almacena la dirección de la variable b.

> Tanto b como c son punteros que conseguimos que apunten a a. Ambos apuntan a la misma dirección de memoria, pero cada una se almacena en una diferente. Al final de la ejecución, a contendrá el valor 0.002. Por tanto, la única opción correcta es la segunda.

6.- Dadas las siguientes definiciones de variables:
```
int x;
int *p1;
int **p2;
```
Cual de las siguientes sentencias permite que x tome el valor 4 correctamente?

```
pl = &p2; *p2 = &x; *p1 = 4;

p2 = &x; *p2 = 4;

p2 = pl; pl = &x; *p2 = 4;

p2 = &p1; pl = &x; **p2 = 4;
```

> Por discrepancia de tipos, ninguna de las tres primeras alternativas compilan. La última sí lo hace. Su ejecución termina haciendo que p2 apunte 3 pl, y éste a x. Bs por
tanto la opción correcta, pues la ejecución, por lo tanto, de **p2 = 4 hace que se modif1que el valor de x.

7.- ¿Cual de las siguientes expresiones permite reservar memoria para un vector de 10 elementos de tipo float?


* `(float) malloc(10);`
* `(float *) malloc(10);`
* `(float *) malloc(10 * sizeof(float));`
* `(float *) malloc(10 * sizeof(float*));`


>El “molde”, conversion () ms! de tipos de la primera línea hace que no compile. La segunda línea pide memoria para 10 bytes, no para 10 variables de tipo float. La tercera si lo pide, por lo que es correcta. La última pide espacio suficiente para albergar 10 elementos de tipo float*, que no necesariamente serán del mismo tamaño que 10 variables float, por lo que es incorrecta.

8.- Después de ejecutar el siguiente fragmento de código:

```
float nl = 10;
float n2 = 5;
float *p, *q;

n1;
n2;

q=*p+*p;
```
Cual de las siguientes afirmaciones es correcta?

* `n1 = 10 y n2 = 5`

* `n1 = 10 y n2 = 10`

* `la sentencia *p==*p es ilegal`

* `n1 = 10 y n2 = 20`

> El programa compila correctamente. Las dos primeras asignaciones hacen que p apunte a nl, y q a n2. La parte derecha de la última asignación suma el contenido de *p consigo mismo; como p apunta a nl, el resultado de la suma será 20. Ese valor es asignado al valor apuntado por q, que resulta ser 112. Por tanto, tras la ejecución nl no se modifica, pero n2 si (a través de q), y pasa a valer 20. La opción válida es, por lo tanto, la última.
