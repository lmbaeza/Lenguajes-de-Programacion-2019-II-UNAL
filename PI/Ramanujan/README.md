# Decimales de PI con Formula de Ramanujan

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>

typedef long double double64;
typedef long long int64;


int64 factorial(int64 number) {
    int64 output = 1;
    for(int64 i = 2; i <= number; ++i) {
        output *= i;
    }
    return output;
}

double64 ramanujan(int64 n) {
    double64 numerador = (factorial(4*n) ) * (1103 + 26390 * n);
    
    double64 denominador = ( pow( factorial(n), 4) ) * ( pow(396, 4*n));

    return numerador / denominador;
}

double64 pi(int64 number) {

    double64 output = 0.0;


    for(int64 i = 0; i < number; ++i) {
        output += ramanujan(i);
    }

    return  2 * sqrt(2) * output;

}

int main() {

    clock_t t_ini, t_fin;
    double secs;

    t_ini = clock();

    // === Start ===
    int n = 66;

    double64 piRamanujan = pi(n);

    printf("%0.15Lf\n", 9801 / piRamanujan);
    // 3.141592653589793
    // 15 Decimales

    // === End ===

    t_fin = clock();

    secs = (double)(t_fin - t_ini) / CLOCKS_PER_SEC;
    printf("%.16g milisegundos\n", secs * 1000.0);


    return EXIT_SUCCESS;
}

// Tiempo de ejecución promedio de una muestra de 10 intentos con n=66

// 0.138 + 0.138 + 0.138 + 0.14 + 0.174 + 0.141 + 0.178 + 0.14 + 0.134 + 0.172 + 0.124
// = 1.617 Ms

// = 1.617 / 10 = 0.1617 Ms
```

### Makefile

```
app: clean PI.o

PI.o: main.o
	gcc main.o -lm  -o PI.o && ./PI.o

main.o:
	gcc -c main.c -lm  -o main.o

clean:
	rm -f *.o
```

![Formula de Ramanujan](https://images.theconversation.com/files/74718/original/image-20150312-13520-18pyzln.jpg?ixlib=rb-1.1.0&q=45&auto=format&w=1000&fit=clip)