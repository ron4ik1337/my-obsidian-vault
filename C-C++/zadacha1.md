1.  Вычислить значение трехчлена         ![](file:///C:/Users/ron4i/AppData/Local/Temp/msohtmlclip1/01/clip_image002.gif)

Выполнено

```C
#include <stdio.h>

int main() {
    // Объявление переменных
    double a, b, c, x, y;

    // Ввод коэффициентов и значения x
    printf("Enter odds a, b and c: ");
    scanf("%lf %lf %lf", &a, &b, &c);
    printf("Enter x value: ");
    scanf("%lf", &x);

    // Вычисление значения трёхчлена
    y = a * x * x + b * x + c;

    // Вывод результата
    printf("Trinomial meaning y = %.2lf\n", y);
    return 0;
}
```
### Объяснение кода:

1. **Подключение библиотеки:** `#include <stdio.h>` — подключает стандартную библиотеку для ввода и вывода.
2. **Объявление переменных:** переменные `a`, `b`, `c`, `x`, `y` используются для хранения коэффициентов и значений.
3. **Ввод значений:** программа запрашивает у пользователя ввод коэффициентов и значения xx.
4. **Вычисление:** используется формула для вычисления значения трёхчлена.
5. **Вывод результата:** программа выводит рассчитанное значение yy.

Вы можете скопировать и вставить этот код в среду разработки C и скомпилировать его.