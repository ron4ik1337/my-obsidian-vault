Задание 11
![[Pasted image 20241216024333.png]]

Выполнено

```C
#include <stdio.h>

#define SIZE 3 // Определим размер матриц

// Функция для вычисления элементов матрицы A

void calculate_matrix_A(double A[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            A[i][j] = (double)(i - j) / (i + j + 1); // Формула для A[i][j]
        }
    }
}

// Функция для вычисления элементов матрицы B

void calculate_matrix_B(double B[SIZE][SIZE]) {
    for (int k = 0; k < SIZE; k++) {
        for (int l = 0; l < SIZE; l++) {
            B[k][l] = (double)(k * l) / (2 * k + l + 1); // Формула для B[k][l]
        }
    }
}

// Функция для вывода матрицы на экран

void print_matrix(const char* title, double matrix[SIZE][SIZE]) {
    printf("%s\n", title);
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%6.2f ", matrix[i][j]);
        }
        printf("\n");
    }
    printf("\n");
}
int main() {
    double A[SIZE][SIZE];
    double B[SIZE][SIZE];

    // Вычисляем элементы матриц A и B

    calculate_matrix_A(A);
    calculate_matrix_B(B);

    // Выводим матрицы на экран

    print_matrix("Matrix A:", A);
    print_matrix("Matrix B:", B);
    return 0;
}
```