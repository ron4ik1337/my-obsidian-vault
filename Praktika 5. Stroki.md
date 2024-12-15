Практика 5. Строки

**ЗАДАЧИ ПО СТРОКАМ**

Задание 15 выполнено.

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

