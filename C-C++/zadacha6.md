Задание 6 
![[Pasted image 20241216014519.png]]



```C
#include <stdio.h>
#include <math.h>

#define EPS 0.00001

// Функция для вычисления a^x с использованием ряда Тейлора

double ax(double a, double x) {
    if (a <= 0) {
        return (x == 0) ? 1 : 0; // Обработка случаев, когда a <= 0
    }
    double sum = 1.0; // Первый член ряда (k=0)
    double term = 1.0; // Текущий член ряда
    double factor = x * log(a); // Вычисляем x * ln(a)
    for (int k = 1; ; k++) {
        term *= factor / k; // Вычисляем k-ый член ряда
        sum += term; // Добавляем к сумме
        // Проверяем, достигли ли мы требуемой точности
        if (fabs(term) < EPS) {
            break;
        }
    }
    return sum; // Возвращаем результат
}
int main() {
    double a;
    
    // Считываем значение a

    printf("Enter value a: ");
    scanf("%lf", &a);
    printf("========================================\n");
    printf("|    x   |    ax()   |    pow()   |\n");
    printf("========================================\n");

    // Выводим значения a^x для x от 0 до 10

    for (int x = 0; x <= 10; x++) {
        printf("|   %2d   | %9.5f | %9.5f |\n", x, ax(a, x), pow(a, x));
    }
    printf("========================================\n");
    return 0;

}
```


