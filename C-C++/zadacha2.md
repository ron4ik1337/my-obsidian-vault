
![[Pasted image 20241216012308.png]]



выполнено 

```C
#include <stdio.h>
#include <math.h>

double f(double x) {
    if (x < 0) {
        return pow(x, 2) + 7 * x;
    } else if (x == 0) {
        return 0;
    } else {
        return pow(x, 2) + 9 * x;
    }
}  
int main() {
    double x;
    
    // a) Ввод значения x и вычисление функции f(x)

    printf("Enter x value: ");
    scanf("%lf", &x);
    printf("f(%.2lf) = %.2lf\n", x, f(x));
    
    // b) Вычисление и вывод таблицы значений функции

    printf("\nTable of values of function f(x) for x from -5 to 5:\n");
    printf(" x       | f(x)\n");
    printf("--------------------\n");
    for (x = -5; x <= 5; x += 1) {
        printf("%-8.2f | %.2f\n", x, f(x));
    }
    return 0;
}
```

### Объяснение кода:

1. **Подключение библиотек:** `#include <stdio.h>` и `#include <math.h>` — подключаем необходимые библиотеки для ввода/вывода и математических функций.
2. **Функция `f`:** определяет значение функции в зависимости от значения xx по заданным условиям.
3. **Ввод значения:** программа запрашивает у пользователя ввод значения xx и вычисляет его значение с помощью функции `f`.
4. **Таблица значений:** программа выводит таблицу значений функции f(x)f(x) для xx от −5−5 до 55 с шагом 11.