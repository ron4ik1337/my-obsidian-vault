10. Задать значения элементам двумерного массива с помощью счетчика случайных чисел в диапазоне от -10 до 10. Транспонировать квадратную матрицу (поменять местами сроки со столбцами) на том же месте, т.е. без создания нового массива. Оформить транспонирование функцией.

Выполнено.


```C
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 3 // Определение размера матрицы

// Функция для транпонирования матрицы

void transpose(int matrix[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = i + 1; j < SIZE; j++) {
        
            // Меняем местами элементы

            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
}

// Функция для отображения матрицы
void printMatrix(int matrix[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%3d ", matrix[i][j]);
        }
        printf("\n");
    }
}
int main() {
    int matrix[SIZE][SIZE];
    
    // Инициализация генератора случайных чисел

    srand(time(NULL));
    
    // Заполнение матрицы случайными числами от -10 до 10

    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            matrix[i][j] = rand() % 21 - 10; // Генерация числа в диапазоне от -10 до 10

        }
    }
    
    // Вывод исходной матрицы

    printf("Original matrix:\n");
    printMatrix(matrix);

    // Транспонирование матрицы
    
    transpose(matrix);

    // Вывод транспонированной матрицы

    printf("\nTransposed matrix:\n");
    printMatrix(matrix);
    return 0;
}
```

### Объяснение программы:

1. **Объявления и макросы**:
    
    - Мы объявляем максимальный размер массива `MAX_SIZE`, чтобы ограничить размер пользовательского ввода.
2. **Функция `find_max_element`**:
    
    - Эта функция находит максимальный элемент массива и его индекс. Она обновляет переменные, переданные по указателям.
3. **Функция `swap`**:
    
    - Обменяет два элемента местами, принимая указатели на эти элементы.
4. **Основная функция `main`**:
    
    - Запрашивает у пользователя размер массива и сами элементы.
    - Вызывает функцию `find_max_element` для нахождения максимального элемента и выводит его на экран.
    - Запрашивает индекс элемента, с которым пользователь хочет поменять максимальный элемент местами.
    - Проверяет допустимость ввода индекса, и если он валиден, выполняет обмен местами, затем выводит обновленный массив.


Разбор кода.
### Определение константы для размера матрицы



```
#define SIZE 3 // Определение размера матрицы
```

- Определяет константу `SIZE`, которая указывает размер матрицы (в данном случае 3 на 3).

### Функция для транспонирования матрицы


```
void transpose(int matrix[SIZE][SIZE]) {
```

- Объявляет функцию `transpose`, которая принимает двухмерный массив (матрицу) размером `SIZE x SIZE`.

#### Циклы для транспонирования


```
    for (int i = 0; i < SIZE; i++) {
        for (int j = i + 1; j < SIZE; j++) {
```

- Внешний цикл проходит по всем строкам, а внутренний цикл проходит по столбцам, начиная с `i + 1`, чтобы не менять элементы, которые уже были обработаны.

##### Обмен значениями



```
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
```

- Здесь происходит обмен значениями элементов матрицы, делая её транспонированной. Элемент с индексами `[i][j]` заменяется элементом `[j][i]`, а значение `[j][i]` сохраняется во временной переменной `temp`.

### Функция для отображения матрицы



```
void printMatrix(int matrix[SIZE][SIZE]) {
```

- Эта строка объявляет функцию `printMatrix`, которая принимает матрицу для отображения её элементов.

#### Циклы для вывода элементов



```
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%3d ", matrix[i][j]);
        }
        printf("\n");
    }
}
```

- Внешний цикл проходит по строкам, а внутренний цикл — по столбцам, печатая каждый элемент матрицы с выравниванием в 3 символа.
- После завершения внутреннего цикла печатается перевод строки, чтобы перейти к следующей строке матрицы.

### Главная функция


```
int main() {
```

- Начало главной функции программы.

#### Объявление и инициализация матрицы

```
    int matrix[SIZE][SIZE];
```

- Объявляет двумерный массив `matrix` размером 3 на 3.

#### Инициализация генератора случайных чисел



```
    srand(time(NULL));
```

- Инициализирует генератор случайных чисел с помощью текущего времени, чтобы каждый запуск программы давал разные случайные числа.

#### Заполнение матрицы случайными числами


```
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            matrix[i][j] = rand() % 21 - 10; // Генерация числа в диапазоне от -10 до 10
        }
    }
```

- Два вложенных цикла заполняют матрицу случайными числами в диапазоне от -10 до 10. Выражение `rand() % 21 - 10` генерирует случайное число от 0 до 20 и затем уменьшает его на 10.

#### Вывод исходной матрицы


```
    printf("Original matrix:\n");
    printMatrix(matrix);
```

- Выводит сообщение "Original matrix:" и вызывает функцию `printMatrix` для отображения исходной матрицы.

#### Транспонирование матрицы


```
    transpose(matrix);
```

- Вызывает функцию `transpose`, которая изменяет матрицу, меняя местами элементы.

#### Вывод транспонированной матрицы


```
    printf("\nTransposed matrix:\n");
    printMatrix(matrix);
```

- Выводит сообщение "Transposed matrix:" и снова вызывает `printMatrix`, чтобы отобразить изменённую (транспонированную) матрицу.

### Завершение программы


```
    return 0;
}
```

- Возврат 0 указывает на успешное завершение программы.
