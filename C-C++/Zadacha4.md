
Задание 4
![[Pasted image 20241216014259.png]]

Выполнено

```C
#include <stdio.h>
#include <math.h>

double f(double a, int n) {
    double sum1 = 0.0;
    double sum2 = 0.0;
    for (int i = 1; i <= n; i++) {
        sum1 += pow(a, i) / i; // Сумма для 1
        sum2 += pow(a, i) / (pow(i, 2)); // Сумма для 2
    }
    return (fabs(sum1) <= 1) ? sum1 : sum2;
}
int main() {
    printf("========================================\n");
    printf("|   a   |   5   |   6   |   7   |   8   |\n");
    printf("========================================\n");
    for (double a = -1; a <= 2; a += 1.0) {
        printf("| %.1f  |", a);
        for (int n = 5; n <= 8; n++) {
            printf(" %5.3f |", f(a, n));
        }
        printf("\n");
    }
    printf("========================================\n");
    return 0;
}
```

### Объяснение:

- **Функция `f`** рассчитывает значения, используя две суммы и исходя из условия ∣sum1∣≤1∣sum1∣≤1.
- **Цикл в `main`**: перебирает значения aa и nn, выводя их в формате таблицы.
- Используется `printf` для форматированного вывода значений.