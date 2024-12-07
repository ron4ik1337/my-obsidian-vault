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