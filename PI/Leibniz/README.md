# Decimales de PI con Formula de Leibniz

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>

typedef long double double64;


double64 piLeibniz(double64 n) {
  double64 out = 0.0;
  double signo = 1;
  double64 x = 0.0;

  for(double i = 1.0; i < n; i+=2.0) {
    x = 4.0/i;
    x = x * signo;
    signo *= -1;
    out += x;
  }
  return out;
}


int main() {

    clock_t t_ini, t_fin;
    double secs;

    t_ini = clock();

    // === Start ===
    double64 n = 1e09;
    double64 ans = piLeibniz(n);

    printf("%.15Lf\n", ans);
    // 3.141592651589794
    
    // === End ===

    t_fin = clock();

    secs = (double)(t_fin - t_ini) / CLOCKS_PER_SEC;
    printf("%.16g milisegundos\n", secs * 1000.0);

    return EXIT_SUCCESS;
}

// Tiempo de ejecución promedio de una muestra de 10 intentos con n=1e09

// 4702.808 + 4607.422 + 4629.008 + 4682.840 + 4598.438 + 4588.191 + 4621.618 + 4646.010 + 4739.406 + 4619.677
// = 46435.418 Ms

// = 46435.418 / 10 = 4643.542 Ms
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


![Formula de Leibniz para calcular Pi](https://imgur.com/9dcPQfP.png)