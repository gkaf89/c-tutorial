# C structures

Structures in C are collection of variables in the computer memory, for instance:

```c
struct matrix
{
	double* x;
	int m;
	int n;
};

struct matrix A;
```

In computers memmory:

```
   +--------+--------+
   | m      | n      |
   +--------+--------+
   | x               |
   +-----------------+
```

## Assignment

```c
A.m = 2;
A.n = 3;
A.x = (double*) malloc(A.m*A.n*sizeof(double));
```

In computers memmory:

```
   +--------+--------+
   | m: 2   | n: 3   |
   +--------+--------+
   | x: 0x03da8cd6   |
   +-----------------+
```

## Assignment shortcut

Very often pointers to structures are used. In such cases the following notation shorthand is very handy:

```
   A->m == *A.m [ == (*A).m ]
```

For instance, we write,
```c
struct matrix* A = (struct matrix*) malloc(sizeof(struct matrix));

A->m = 2;
A->n = 2;
A->x = (double*) malloc(A->m*A->n*sizeof(double));
```
instead of:
```c
struct matrix* A = (struct matrix*) malloc(sizeof(struct matrix));

*A.m = 2;
*A.n = 2;
*A.x = (double*) malloc((*A.m)*(*A.n)*sizeof(double));
```


## Allignement

The order of definition matters!

```c
struct matrix
{
	int m;
	double* x;
	int n;
};

struct matrix A;
```

In computers memmory:

```
   +--------+--------+
   | m      |        |
   +--------+--------+
   | x               |
   +-----------------+
   | n      |        |
   +--------+--------+
```

- 3 bytes instead of 2 due to 64bit allignment for pointer tyes.
- If you have a large array of structures, it needs 50% more space!

For instace, when storing many 3x3 rotation matrices the size of the matrix structure is significant:

```c
struct matrix* A = (struct matrix*) malloc(500*sizeof(struct matrix))
```

## Structures/Classes in C++

Same as C in the computer memory, but they are also assigned conceptually a set of fuctions that can operate on instances of the structure.
