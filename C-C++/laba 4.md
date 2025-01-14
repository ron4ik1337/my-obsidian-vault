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