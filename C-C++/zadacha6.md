Задание 6 
![[Pasted image 20241216014519.png]]


Выполнено.


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
### Объяснение кода:

1. **Функция `ax`**:
    
    - Вычисляет значение aX по формуле разложения:
    - ![[Pasted image 20241216015706.png]]
    - Использует переменную `term` для хранения текущего члена ряда.
    - Цикл продолжается до тех пор, пока текущий член ряда не станет меньше заданной точности `EPS`.
2. **Функция `main`**:
    
    - Считывает значение aa от пользователя.
    - Выводит заголовок таблицы.
    - Вычисляет и выводит значения aX от 0 до 10, используя как собственную функцию `ax()`, так и `pow()` из стандартной библиотеки.


Разбор кода.

### Определение константы точности


```
#define EPS 0.00001
```

- Эта строка определяет макрос `EPS`, который задает допустимую погрешность для вычислений. Он используется позже для проверки, достигнута ли достаточная точность вычислений.

### Определение функции


```
double ax(double a, double x) {
```

- Объявляет функцию `ax`, которая принимает два параметра: `a` (основание) и `x` (экспонента). Функция возвращает значение типа `double`.

### Обработка специальных случаев

```
    if (a <= 0) {
        return (x == 0) ? 1 : 0; // Обработка случаев, когда a <= 0
    }
```

- Если `a` меньше или равно нулю, функция проверяет, равно ли `x` нулю. Если да, возвращается 1 (по определению, любое число в степени 0 равно 1). В противном случае возвращается 0, что может отражать недопустимость операции.

### Инициализация переменных



```
    double sum = 1.0; // Первый член ряда (k=0)
    double term = 1.0; // Текущий член ряда
    double factor = x * log(a); // Вычисляем x * ln(a)
```

- `sum` инициируется значением 1.0, что соответствует первому члену ряда Тейлора.
- `term` также инициализируется как 1.0, что удобно для последующих вычислений.
- `factor` вычисляет значение `x * логарифм(a)`, что необходимо для расчёта членов ряда.

### Основной цикл для вычисления ряда


```
    for (int k = 1; ; k++) {
```

- Это безусловный цикл, который будет выполняться до достижения определенного условия прерывания.

#### Вычисление k-го члена ряда


```
        term *= factor / k; // Вычисляем k-ый член ряда
        sum += term; // Добавляем к сумме
```

- Каждая итерация цикла рассчитывает текущий член ряда, умножая предыдущий член (`term`) на `factor / k`.
- Текущий член добавляется к `sum`, в результате чего формируется сумма ряда.

#### Проверка точности


```
        if (fabs(term) < EPS) {
            break;
        }
```

- Используется функция `fabs` для получения абсолютного значения текущего члена. Если это значение меньше `EPS`, цикл прерывается, что указывает на достижение необходимой точности в вычислениях.

### Возвращение результата


```
    return sum; // Возвращаем результат
}
```

- Функция возвращает итоговое значение `sum`, которое представляет axax вычисленное с использованием ряда Тейлора.

### Главная функция


```
int main() {
```

- Начало основной функции программы, где происходит выполнение.

#### Считывание значения `a`



```
    double a;
    printf("Enter value a: ");
    scanf("%lf", &a);
```

- Переменная `a` объявляется для хранения значения, которое вводит пользователь. Сообщение выводится на экран, и `scanf` считывает значение с плавающей запятой.

#### Заголовок для таблицы



```
    printf("========================================\n");
    printf("|    x   |    ax()   |    pow()   |\n");
    printf("========================================\n");
```

- Эти строки выводят заголовок таблицы, где первое поле будет значением `x`, второе - значением, вычисленным с помощью функции `ax`, а третье - значением, рассчитанным с использованием встроенной функции `pow`.

### Цикл для вывода значений



```
    for (int x = 0; x <= 10; x++) {
        printf("|   %2d   | %9.5f | %9.5f |\n", x, ax(a, x), pow(a, x));
    }
```

- Этот цикл перебирает значения `x` от 0 до 10. Для каждого значения вызывается функция `ax(a, x)` и встроенная функция `pow(a, x)`, после чего результаты выводятся в таблице в отформатированном виде.

### Завершение вывода таблицы


```
    printf("========================================\n");
```

- Эта строка завершает таблицу, выводя её нижнюю границу.

### Завершение программы


```
    return 0;
}
```

- Возврат 0 указывает на успешное завершение программы.

### Общая концепция

Программа вычисляет значение axax с использованием ряда Тейлора для значений xx от 0 до 10 и сравнивает эти результаты со встроенной функцией `pow`. Она демонстрирует, как использовать ряд для приближенного вычисления экспоненциальной функции, учитывая допустимую погрешность.


