## Практика 3. Рекуррентные алгоритмы

Домащнее задание: решить задачу 7 с использование рекуррентного алгоритма.  
После решения задачи сформируйте файл (файл назовите **_ФамилияПрактика_****_3_**), в который вложите:  
- текст задания;  
- расчёт рекуррентного коэффициента (можно фото);  
- текст кода программы;  
- копию экрана с результатом работы программы;  
- блок-схему алгоритма (можно нарисовать в Word или нарисовать на листе бумаги и сфотографировать).


Задание 7:
![[Pasted image 20241215234519.png]]

Выполнено
`
```C
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX_STRINGS 100
#define MAX_STRING_LENGTH 100

int main() {
    char text[MAX_STRINGS][MAX_STRING_LENGTH];
    int n;
    printf("Enter the number of lines of text: ");
    scanf("%d", &n);
    // Очистим входной буфер
    getchar();
    printf("Enter lines of text:\n");
    for (int i = 0; i < n; i++) {
        fgets(text[i], MAX_STRING_LENGTH, stdin);
        
        // Удаляем символ новой строки, если он есть

        text[i][strcspn(text[i], "\n")] = 0;
    }
    int letterCount = 0;
    int symbolCount = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < strlen(text[i]); j++) {
            if (isalpha(text[i][j])) {
                letterCount++;
            } else if (isdigit(text[i][j]) ||
                       text[i][j] == '+' ||
                       text[i][j] == '-' ||
                       text[i][j] == '*' ||
                       text[i][j] == '/') {
                symbolCount++;
            }
        }
    }

    printf("Number of letters: %d\n", letterCount);
    printf("Number of characters and numbers: %d\n", symbolCount);
    if (letterCount > symbolCount) {
        printf("The text contains more letters than symbols and numbers.\n");
    } else {
        printf("The text contains more symbols and numbers than letters.\n");
    }
    return 0;

}
```



