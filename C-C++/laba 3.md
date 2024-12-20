**Вариант 5**

Задать случайно значения элементов вещественной матрицы размера _n__×__m__._

1) Упорядочить элементы в каждой строке по убыванию методом вставки.

2) Затем упорядочить элементы в столбцах матрицы, используя метод обмена.

Вывести на экран массив перед сортировкой и после каждого упорядочивания.

**ВЫПОЛНЕНО**

``` C
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Функция печати матрицы

void printMatrix(double matrix[][MAX_SIZE], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("%lf ", matrix[i][j]);
        }
        printf("\n");
    }
    printf("\n");
}

// Функция сортировки строки методом вставки (по убыванию)

void insertionSortRow(double row[], int size) {
    for (int i = 1; i < size; i++) {
        double key = row[i];
        int j = i - 1;
        while (j >= 0 && row[j] < key) {
            row[j + 1] = row[j];
            j = j - 1;
        }
        row[j + 1] = key;
    }
}

// Функция сортировки столбцов методом пузырьковой сортировки (по возрастанию)

void bubbleSortCol(double matrix[][MAX_SIZE], int rows, int cols) {
    for (int j = 0; j < cols; j++) {
        for (int i = 0; i < rows - 1; i++) {
            for (int k = 0; k < rows - i - 1; k++) {
                if (matrix[k][j] > matrix[k + 1][j]) {
                    double temp = matrix[k][j];
                    matrix[k][j] = matrix[k + 1][j];
                    matrix[k + 1][j] = temp;
                }
            }
        }
    }
}
 
int main() {
    int rows, cols;
    printf("Enter the number of rows: ");
    scanf("%d", &rows);
    printf("Enter the number of columns: ");
    scanf("%d", &cols);
    if (rows <= 0 || cols <= 0 || rows > MAX_SIZE || cols > MAX_SIZE) {
        printf("Invalid matrix dimensions.\n");
        return 1;
    }
    double matrix[MAX_SIZE][MAX_SIZE];

    // Задайте генератору случайных чисел начальное значение

    srand(time(NULL));
    
    // Генерация случайных значений матрицы

    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            matrix[i][j] = (double)rand() / RAND_MAX * 100; 
        }
    }
  
    printf("Original Matrix:\n");
    printMatrix(matrix, rows, cols);

    //  Сортировка строк методом вставки

    for (int i = 0; i < rows; i++) {
        insertionSortRow(matrix[i], cols);
    }
    printf("Matrix after row sorting:\n");
    printMatrix(matrix, rows, cols);

    // Сортировка столбцов методом пузырьковой сортировки

    bubbleSortCol(matrix, rows, cols);
    printf("Matrix after column sorting:\n");
    printMatrix(matrix, rows, cols);

    return 0;

}
```

Давайте разберем код на C по строкам, чтобы понять, что делает каждая из них.

```
#include <stdio.h>
```

- Подключает стандартную библиотеку ввода-вывода, позволяя использовать функции, такие как `printf` и `scanf`.


```
#include <stdlib.h>
```

- Подключает библиотеку для работы с функциями управления памятью, генерации случайных чисел и другими вспомогательными функциями.


```
#include <time.h>
```

- Подключает библиотеку для работы с временем, позволяя инициализировать генератор случайных чисел на основе текущего времени.


```
// Функция печати матрицы
void printMatrix(double matrix[][MAX_SIZE], int rows, int cols) {
```

- Определяет функцию `printMatrix`, которая принимает матрицу и ее размеры и выводит ее элементы на экран.



```
    for (int i = 0; i < rows; i++) {
```

- Начинает цикл по строкам матрицы.



```
        for (int j = 0; j < cols; j++) {
```

- Начинает цикл по столбцам текущей строки.


```
            printf("%lf ", matrix[i][j]);
```

- Выводит текущий элемент матрицы с плавающей точкой.



```
        }
        printf("\n");
```

- Закрывает цикл по столбцам и переходит на новую строку после вывода всех элементов текущей строки.



```
    }
    printf("\n");
}
```

- Закрывает цикл по строкам и печатает дополнительную пустую строку для отделения вывода.



```
// Функция сортировки строки методом вставки (по убыванию)
void insertionSortRow(double row[], int size) {
```

- Определяет функцию `insertionSortRow`, которая сортирует один массив (строку) по убыванию с использованием метода вставки.



```
    for (int i = 1; i < size; i++) {
```

- Начинает цикл с второго элемента (индекс 1) для сортировки.



```
        double key = row[i];
```

- Сохраняет текущий элемент в переменной `key`, чтобы вставить его в правильную позицию в отсортированной части массива.



```
        int j = i - 1;
```

- Устанавливает индекс `j` на элемент перед `key`.



```
        while (j >= 0 && row[j] < key) {
```

- Начинает цикл, который продолжается, пока индекс `j` не выходит за пределы и элемент `row[j]` меньше `key`.



```
            row[j + 1] = row[j];
```

- Сдвигает элемент, чтобы освободить место для `key`.



```
            j = j - 1;
```

- Обновляет индекс `j` для следующей проверки.



```
        }
        row[j + 1] = key;
```

- Вставляет `key` в его правильное положение после завершения сдвига.


```
    }
}
```

- Закрывает цикл и тело функции `insertionSortRow`.


```
// Функция сортировки столбцов методом пузырьковой сортировки (по возрастанию)
void bubbleSortCol(double matrix[][MAX_SIZE], int rows, int cols) {
```

- Определяет функцию `bubbleSortCol`, которая сортирует каждый столбец матрицы по возрастанию с помощью пузырьковой сортировки.


```
    for (int j = 0; j < cols; j++) {
```

- Начинает цикл по столбцам матрицы.


```
        for (int i = 0; i < rows - 1; i++) {
```

- Начинает внешний цикл по строкам для сортировки.


```
            for (int k = 0; k < rows - i - 1; k++) {
```

- Начинает внутренний цикл, который проходит по оставшимся неотсортированным элементам в столбце.


```
                if (matrix[k][j] > matrix[k + 1][j]) {
```

- Проверяет, если текущий элемент больше следующего элемента в столбце.


```
                    double temp = matrix[k][j];
```

- Если условие истинно, временно сохраняет текущее значение в `temp`.


```
                    matrix[k][j] = matrix[k + 1][j];
                    matrix[k + 1][j] = temp;
```

- Обменивает текущий элемент с следующим.



```
                }
            }
        }
    }
}
```

- Закрывает внутренние циклы и начинает следующий столбец.



```
int main() {
```

- Начинает основную функцию программы.



```
    int rows, cols;
```

- Объявляет целочисленные переменные `rows` и `cols` для хранения размеров матрицы.


```
    printf("Enter the number of rows: ");
    scanf("%d", &rows);
```

- Запрашивает пользователя ввести количество строк матрицы и считывает его.



```
    printf("Enter the number of columns: ");
    scanf("%d", &cols);
```

- Запрашивает пользователя ввести количество столбцов матрицы и считывает его.



```
    if (rows <= 0 || cols <= 0 || rows > MAX_SIZE || cols > MAX_SIZE) {
```

- Проверяет, что введенные размеры допустимы.



```
        printf("Invalid matrix dimensions.\n");
        return 1;
    }
```

- Если размеры недопустимы, выводит сообщение об ошибке и завершает программу.



```
    double matrix[MAX_SIZE][MAX_SIZE];
```

- Объявляет двухмерный массив (матрицу) фиксированного размера.



```
    srand(time(NULL));
```

- Инициализирует генератор случайных чисел, используя текущее время.



```
    // Генерация случайных значений матрицы
    for (int i = 0; i < rows; i++) {
```

- Начинает цикл по строкам для генерации случайных значений.



```
        for (int j = 0; j < cols; j++) {
```

- Начинает цикл по столбцам текущей строки.



```
            matrix[i][j] = (double)rand() / RAND_MAX * 100; 
```

- Генерирует случайное число с плавающей частью в диапазоне от 0 до 100 и сохраняет его в текущий элемент матрицы.



```
        }
    }
```

- Закрывает циклы по строкам и столбцам.



```
    printf("Original Matrix:\n");
    printMatrix(matrix, rows, cols);
```

- Выводит оригинальную матрицу на экран.



```
    // Сортировка строк методом вставки
    for (int i = 0; i < rows; i++) {
```

- Начинает цикл по строкам для сортировки строк по убыванию.



```
        insertionSortRow(matrix[i], cols);
```

- Вызывает функцию для сортировки текущей строки методом вставки.



```
    }
    printf("Matrix after row sorting:\n");
    printMatrix(matrix, rows, cols);
```

- Выводит матрицу после сортировки строк.



```
    // Сортировка столбцов методом пузырьковой сортировки
    bubbleSortCol(matrix, rows, cols);
```

- Вызывает функцию для сортировки всех столбцов матрицы методом пузырьковой сортировки.



```
    printf("Matrix after column sorting:\n");
    printMatrix(matrix, rows, cols);
```

- Выводит матрицу после сортировки столбцов.



```
    return 0;
}
```

- Завершает функцию `main`, возвращая 0, что указывает на успешное выполнение программы.

