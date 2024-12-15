9.  Задать значения элементам массива с клавиатуры. Определить максимальный элемент и его номер в одномерном массиве. Поиск максимального элемента оформить функцией.  
Поменять местами максимальный элемент с элементом, указанным пользователем.

Выполнено.

```C
#include <stdio.h>

#define MAX_SIZE 100

// Функция для поиска максимального элемента и его индекса
void find_max_element(int arr[], int size, int *max_index, int *max_value) {
    *max_value = arr[0];
    *max_index = 0;
    for (int i = 1; i < size; i++) {
        if (arr[i] > *max_value) {
            *max_value = arr[i];
            *max_index = i;
        }
    }
}  

// Функция для обмена элементов местами

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}  
int main() {
    int size;
    int arr[MAX_SIZE];
    
    // Ввод размера массива

    printf("Enter array size (max %d): ", MAX_SIZE);
    scanf("%d", &size);
    
    // Ввод элементов массива

    printf("Enter %d array elements:\n", size);
    for (int i = 0; i < size; i++) {
        scanf("%d", &arr[i]);
    }
    int max_index, max_value;
    
    // Поиск максимального элемента

    find_max_element(arr, size, &max_index, &max_value);
    printf("Max element: %d, index: %d\n", max_value, max_index);

    // Ввод индекса элемента для замены

    int user_index;
    printf("Enter the index of the item to exchange with the maximum (0 to %d): ", size - 1);
    scanf("%d", &user_index);
    
    // Проверка на допустимость индекса

    if (user_index >= 0 && user_index < size) {
    
        // Обмен местами

        swap(&arr[max_index], &arr[user_index]);
        printf("Array after exchange:\n");

        // Вывод обновленного массива

        for (int i = 0; i < size; i++) {
            printf("%d ", arr[i]);
        }
        printf("\n");
    } else {
        printf("Error: Invalid index!\n");
    }
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