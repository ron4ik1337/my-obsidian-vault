
## Практика 4. Индивидуальные задания на работу с одномерными массивами, указатели


1. Получить из массива новый массив из тех же элементов, идущих в обратном порядке.

Задание 15 выполнено

```C
#include <stdio.h>
int main() {
    int n;
    
    // Запрашиваем размер массива

    printf("Enter array size: ");
    scanf("%d", &n);
    
    // Проверка на корректность размера

    if (n <= 0) {
        printf("The array size must be positive.\n");
        return 1;
    }
    int arr[n];  // Исходный массив
    int reversed[n];  // Новый массив для хранения элементов в обратном порядке
    
    // Ввод элементов массива

    printf("Enter %d array elements:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    // Заполнение нового массива элементами в обратном порядке

    for (int i = 0; i < n; i++) {
       reversed[i] = arr[n - 1 - i];

    }

    // Вывод нового массива

    printf("New array in reverse order:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", reversed[i]);
    }
    printf("\n");
    return 0;
}

```


**Разбор кода.**


```
#include <stdio.h>
```

- Подключает стандартную библиотеку ввода-вывода, что позволяет использовать функции, такие как `printf` и `scanf`.



```
int main() {
```

- Начало основной функции `main`, с которой начинается выполнение программы.


```
    int n;
```

- Объявляет целочисленную переменную `n`, которая будет использоваться для хранения размера массива.


```
    // Запрашиваем размер массива
    printf("Enter array size: ");
```

- Выводит сообщение на экран с запросом размера массива.


```
    scanf("%d", &n);
```

- Считывает целое число, введенное пользователем, и сохраняет его в переменной `n`.


```
    // Проверка на корректность размера
    if (n <= 0) {
```

- Начинает условие `if`, которое проверяет, является ли `n` меньше или равным нулю.

```
        printf("The array size must be positive.\n");
```

- Если `n` некорректно (например, отрицательное число или ноль), выводит сообщение об ошибке.

```
        return 1;
```

- Завершает программу с кодом возврата 1, что указывает на ошибку.


```
    }
```

- Закрывает тело условия `if`.


```
    int arr[n];  // Исходный массив
```

- Объявляет массив `arr` размером `n`, который будет хранить элементы, введенные пользователем.


```
    int reversed[n];  // Новый массив для хранения элементов в обратном порядке
```

- Объявляет новый массив `reversed` размером `n`, который будет использоваться для хранения элементов исходного массива в обратном порядке.


```
    // Ввод элементов массива
    printf("Enter %d array elements:\n", n);
```

- Выводит сообщение с просьбой ввести элементы массива, указывая, сколько элементов нужно ввести.


```
    for (int i = 0; i < n; i++) {
```

- Начинает цикл `for`, который будет выполняться от 0 до `n - 1`, позволяя ввести все элементы массива.


```
        scanf("%d", &arr[i]);
```

- Считывает целое число, введенное пользователем, и сохраняет его в массив `arr` на позиции `i`.


```
    }
```

- Закрывает цикл `for` ввода элементов массива.


```
    // Заполнение нового массива элементами в обратном порядке
    for (int i = 0; i < n; i++) {
```

- Начинает цикл `for`, который будет выполняться от 0 до `n - 1`, чтобы заполнить массив `reversed` элементами из массива `arr` в обратном порядке.

```
        reversed[i] = arr[n - 1 - i];
```

- Присваивает элемент из исходного массива `arr` в обратном порядке в новый массив `reversed`. Например, первый элемент `reversed` будет равен последнему элементу `arr`.


```
    }
```

- Закрывает цикл `for`, который заполняет новый массив.


```
    // Вывод нового массива
    printf("New array in reverse order:\n");
```

- Выводит сообщение, информирующее о том, что будет показан новый массив в обратном порядке.



```
    for (int i = 0; i < n; i++) {
```

- Начинает цикл `for`, который будет выполняться от 0 до `n - 1`, чтобы вывести элементы нового массива.



```
        printf("%d ", reversed[i]);
```

- Печатает каждый элемент массива `reversed`, обеспечивая пробел между ними.



```
    }
```

- Закрывает цикл `for`, который выводит элементы.



```
    printf("\n");
```

- Выводит символ новой строки для отделения вывода от последующих возможных сообщений в терминале.



```
    return 0;
```

- Завершает функцию `main`, возвращая значение 0, что указывает на успешное завершение программы.


```
}
```

- Закрывает тело функции `main`.

