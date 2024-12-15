**Задания для практических занятий по программированию на Си**

Что надо сделать:  
1. Решить задачи №3,5.  
2. Текст кода с комментариями вставить в файл .doc.  
3. Составить блок-схему (фото или картинку), вставить в тот же файл.  
4. Назвать правильно файл, имя файла должно содержать ФИО студента, номер практики, например: ИвановИИ. Практика 1.

Критерии оценки (по каждому критерию 1 балл) :  
1. Алгоритм составлен верно, результат соответствует введенным данным.  
2. Типы данных всех переменных определены верно.  
3. Блок-схема отражает логику алгоритма кода.  
4. Задание сдано преподавателю.  
5. Текст кода программы написан согласно требованиям структурного программирования.

|   |   |
|---|---|
|||

ЗДАНИЕ 3 ВЫПОЛНЕНО 

```C
#include <stdio.h>

int main() {
   int M, N;
    int sum = 0;
    printf("Enter M (even number): ");
    scanf("%d", &M);
    printf("Enter N (even number, greater than M): ");
    scanf("%d", &N);
    if (M % 2 != 0) {
        printf("M must be an even number.\n");
        return 1;
    }
    if (N % 2 != 0) {
        printf("N must be an even number.\n");
        return 1;
    }
    if (M >= N) {
        printf("N must be greater than M.\n");
        return 1;
    }
    for (int i = M; i <= N; i += 2) {
       sum += i;
    }
    printf("Sum of even numbers in an interval [%d, %d]: %d\n", M, N, sum);
    return 0;
}
```


ЗАДАНИЕ 5 ВЫПОЛНЕНО 

```C
#include <stdio.h>
#include <math.h>

double f(int a, int n) {
    double sum1 = 0, sum2 = 0;

    for (int i = 1; i <= n; i++) {
        sum1 += (double)a / i;
        sum2 += (double)a / (i * i);
    }

    return sum1 / fabs(sum2);
}

int main() {
    printf("=================================\n");
    printf("|  a/n  |   5   |   6   |   7   |  8  |\n");
    printf("=================================\n");
    
    for (int a = 1; a <= 2; a++) {
        for (int n = 5; n <= 8; n++) {
            double result = f(a, n);
            printf("|  %d | %.3f |\n", a, result);
        }
    }
    
    printf("=================================\n");
    return 0;
}

```