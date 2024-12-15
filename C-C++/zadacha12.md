12. Отсортировать одномерный массив каждым из методов:

а) простого выбора,

б) простого обмена,

в) простых вставок.

Для каждого метода подсчитать трудоемкость (по числу присваиваний).

Методы сортировки оформить в виде функций.

Для вывода двумерного массива на экран использовать функцию из задачи 11.

Выполнено.

```C
#include <stdio.h>

#define SIZE 3 // Размер массива

// Функция для вычисления элементов матрицы A

void calculate_matrix_A(double A[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            A[i][j] = (double)(i - j) / (i + j + 1); // Формула для A[i][j]
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

// Функция сортировки методом простого выбора

int selection_sort(int arr[], int n) {
    int i, j, min_idx, temp;
    int assign_count = 0; // Счетчик присваиваний
    for (i = 0; i < n - 1; i++) {
        min_idx = i;
        for (j = i + 1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        if (min_idx != i) {
            temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
            assign_count += 3; // Учтем 3 присваивания
        }
    }
    return assign_count;
}

// Функция сортировки методом простого обмена

int bubble_sort(int arr[], int n) {
    int i, j, temp;
    int assign_count = 0; // Счетчик присваиваний
    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                assign_count += 3; // Учтем 3 присваивания
            }
        }
    }
    return assign_count;
}

// Функция сортировки методом простых вставок

int insertion_sort(int arr[], int n) {
    int i, key, j;
    int assign_count = 0; // Счетчик присваиваний
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
            assign_count++; // Учтем 1 присваивание
        }
        arr[j + 1] = key;
        assign_count++; // Учтем 1 присваивание
    }
    return assign_count;
}
int main() {
    double A[SIZE][SIZE];
    int arr[SIZE] = {3, 1, 2}; // Пример массива для сортировки

    // Вычисляем элементы матриц A

    calculate_matrix_A(A);

    // Выводим матрицу A

    print_matrix("Matrix A:", A);

    // Сортировка методом простого выбора

    int assign_count_selection = selection_sort(arr, SIZE);
    printf("Selection sort requires %d assignments.\n", assign_count_selection);

    // Сортировка методом простого обмена

    int assign_count_bubble = bubble_sort(arr, SIZE);
    printf("Simple exchange sort requires %d assignments.\n", assign_count_bubble);

    // Заполнение массива для вставок

    int arr_insertion[SIZE] = {3, 1, 2};
    int assign_count_insertion = insertion_sort(arr_insertion, SIZE);
    printf("Simple insertion sort requires %d assignments.\n", assign_count_insertion);
    return 0;
}
```

### Объяснение программы:

1. **Размер и расчет матриц**:
    
    - Размеры матриц и элементов задаются константой `SIZE`.
    - Функции `calculate_matrix_A` и `print_matrix` используются для вычисления и вывода матриц.
2. **Методы сортировки**:
    
    - **Сортировка методом простого выбора**: Нахождение минимального элемента и обмен с текущим.
    - **Сортировка методом простого обмена** (пузырьковая сортировка): Проход по массиву с обменом соседей, если они в неправильном порядке.
    - **Сортировка методом простых вставок**: Перемещение текущего элемента на правильное место в отсортированной части массива.
3. **Подсчет присваиваний**:
    
    - Для каждого метода сортировки ведется подсчет количества присваиваний.
4. **Функция `main`**:
    
    - Вычисляет и выводит матрицы, выполняет сортировку и выводит количество присваиваний.