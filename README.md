# EjerciciosC3

1.- Indica que tipos deben tener las variables var1, var2 y var3 para que el siguiente
fragmento sea correcto:
```
var1 = 5.5;
var2 = &varl;
var3 = var2;
var2 = var1 + **var3;
```

2.- ¿Existe algún problema con el siguiente código?

```
long dato = 0;
long *ptrDato;
ptrDato = dato;
```


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

4.- Construye un array dinámico para almacenar una sopa de letras de dimensiones
leídas por teclado.

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

7.- ¿Cual de las siguientes expresiones permite reservar memoria para un vector de 10 elementos de tipo float?

```
(float) malloc(10);
(float *) malloc(10);
(float *) malloc(10 * sizeof(float))
(float *) malloc(10 * sizeof(float*));
```

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

