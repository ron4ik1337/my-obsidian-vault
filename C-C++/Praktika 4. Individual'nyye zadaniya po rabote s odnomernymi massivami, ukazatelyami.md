
## Практика 4. Индивидуальные задания на работу с одномерными массивами, указатели


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

