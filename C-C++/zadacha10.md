10. Задать значения элементам двумерного массива с помощью счетчика случайных чисел в диапазоне от -10 до 10. Транспонировать квадратную матрицу (поменять местами сроки со столбцами) на том же месте, т.е. без создания нового массива. Оформить транспонирование функцией.


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