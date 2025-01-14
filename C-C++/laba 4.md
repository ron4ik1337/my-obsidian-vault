15.      Ввести из файла строку, в которой слова разделены одним пробелом. Преобразовать строку следующим образом: после каждого слова добавить в строку два числа – количество гласных и количество согласных букв в слове. Вывести эту строку на экран.

код
```C
#include <stdio.h>

#include <ctype.h>

#include <string.h>

  

#define MAX_LEN 1000

  

// Функция для подсчёта гласных и согласных в слове

void count_vowels_and_consonants(const char* word, int* vowels, int* consonants) {

    *vowels = 0;

    *consonants = 0;

    const char* vowels_list = "AEIOUYaeiouy";

  

    for (int i = 0; word[i] != '\0'; i++) {

        if (isalpha(word[i])) { // Проверяем, что символ - буква

            if (strchr(vowels_list, word[i]) != NULL) {

                (*vowels)++;

            } else {

                (*consonants)++;

            }

        }

    }

}

  

int main() {

    FILE* file = fopen("input.txt", "r");

    if (file == NULL) {

        printf("Error: Failed to open file!\n");

        return 1;

    }

  

    char input[MAX_LEN];

    fgets(input, MAX_LEN, file); // Читаем строку из файла

    fclose(file);

  

    char result[MAX_LEN] = "";  // Строка для хранения результата

    char word[MAX_LEN];

    int vowels, consonants;

  

    char* token = strtok(input, " "); // Разделяем строку на слова

    while (token != NULL) {

        strcpy(word, token);

        word[strcspn(word, "\n")] = '\0'; // Убираем символ переноса строки, если есть

  

        count_vowels_and_consonants(word, &vowels, &consonants); // Считаем гласные и согласные

        // Добавляем слово и числа в результат

        char temp[MAX_LEN];

        sprintf(temp, "%s(%d,%d) ", word, vowels, consonants);

        strcat(result, temp);

  

        token = strtok(NULL, " "); // Переходим к следующему слову

    }

  

    printf("Resulting string: %s\n", result);

  

    return 0;

}
```

---

### Подключение библиотек



```
#include <stdio.h>
#include <ctype.h>
#include <string.h>
```

- `#include <stdio.h>` — библиотека для работы с вводом/выводом (функции `printf`, `fgets`, `fopen` и т. д.).
- `#include <ctype.h>` — библиотека для работы с символами, например, определения, является ли символ буквой (`isalpha`).
- `#include <string.h>` — библиотека для работы со строками C (`strcpy`, `strcat`, `strtok` и другие).

---

### Макрос для ограничения длины строки


```
#define MAX_LEN 1000
```

- Задает максимальную длину строки, например, для входной строки и выходного результата.

---

### Функция для подсчета гласных и согласных



```
void count_vowels_and_consonants(const char* word, int* vowels, int* consonants) {
    *vowels = 0;
    *consonants = 0;
    const char* vowels_list = "AEIOUYaeiouy";

    for (int i = 0; word[i] != '\0'; i++) {
        if (isalpha(word[i])) { // Проверяем, что символ - буква
            if (strchr(vowels_list, word[i]) != NULL) {
                (*vowels)++;
            } else {
                (*consonants)++;
            }
        }
    }
}
```

**Что делает:**

1. Принимает слово на вход (строку `word`) и два указателя (`int*`) для подсчета количества гласных и согласных.
2. Инициализирует счетчики на 0.
3. Для каждого символа в слове:
    - Проверяет, является ли символ буквой (`isalpha`).
    - Если символ находится в списке гласных (`vowels_list`), увеличивает `*vowels`.
    - Иначе увеличивает `*consonants`.

**Результат:** возвращает количество гласных и согласных через указатели.

---

### Открытие файла



```
FILE* file = fopen("input.txt", "r");
if (file == NULL) {
    printf("Error: Failed to open file!\n");
    return 1;
}
```

- Открывает файл `input.txt` в режиме чтения (`"r"`).
- Если файл не найден (вернул `NULL`), выводит ошибку и завершает программу с кодом возврата `1`.

---

### Чтение строки из файла


```
char input[MAX_LEN];
fgets(input, MAX_LEN, file); // Читаем строку из файла
fclose(file);
```

- Объявляет массив `input` длиной `MAX_LEN` для хранения строки из файла.
- Считывает первую строку из файла с помощью `fgets`.
- Закрывает файл (`fclose`).

---

### Объявление переменных для обработки строки


```
char result[MAX_LEN] = "";  // Строка для хранения результата
char word[MAX_LEN];
int vowels, consonants;
```

- `result` — строка для хранения преобразованного результата.
- `word` — временная строка для хранения текущего слова.
- `vowels` и `consonants` — переменные для количества гласных и согласных в текущем слове.

---

### Разделение строки на слова


```
char* token = strtok(input, " "); // Разделяем строку на слова
while (token != NULL) {
    strcpy(word, token);
    word[strcspn(word, "\n")] = '\0';
```

- `strtok` делит строку `input` на слова, используя пробел в качестве разделителя.
- Цикл `while` обрабатывает каждое слово до тех пор, пока не достигнет конца (`token == NULL`).
- Копирует текущее слово в `word`.
- Убирает символ переноса строки (`\n`) в слове (если он есть).

---

### Подсчет гласных и согласных


```
count_vowels_and_consonants(word, &vowels, &consonants); // Считаем гласные и согласные
```

- Вызывает функцию `count_vowels_and_consonants`, подсчитывающую количество гласных и согласных букв в слове.
- Ее результат возвращается через указатели `&vowels` и `&consonants`.

---

### Формирование результата


```
char temp[MAX_LEN];
sprintf(temp, "%s(%d,%d) ", word, vowels, consonants);
strcat(result, temp);
```

- Формирует строку `temp` в формате: `слово(гласные, согласные)`.
- Добавляет `temp` в конец строки `result` (последовательно для каждого слова) с помощью `strcat`.

---

### Переход к следующему слову


```
token = strtok(NULL, " ");
```

- Получает следующее слово, если оно есть.

---

### Вывод результата


```
printf("Resulting string: %s\n", result);
```

- Печатает результирующую строку.

---

### Завершение программы


```
return 0;
```

- Завершает программу с кодом возврата `0` (успешное выполнение).

---

### Пример выполнения

1. Файл `input.txt` содержит строку:
    
    
    
    ```
    Hello world test
    ```
    
2. Программа считает числа для каждого слова:
    - `Hello`: 2 гласные, 3 согласные → `Hello(2,3)`
    - `world`: 1 гласная, 4 согласные → `world(1,4)`
    - `test`: 1 гласная, 3 согласные → `test(1,3)`
3. Вывод в консоль:
    
    
    
    ```
    Resulting string: Hello(2,3) world(1,4) test(1,3)
    ```