**Вариант 16**

Дана целочисленная прямоугольная матрица. Определить:

1) количество отрицательных элементов в тех строках, которые содержат хотя бы один нулевой элемент, вывести номер каждой строки и количество отрицательных элементов в ней;

2) номера строк и столбцов всех седловых точек матрицы;

3) поменять местами строку и столбец , находящиеся на пересечении минимальной седловой точки, если точка находится на главной диагонали.

**ПРИМЕЧАНИЕ**

Матрица _А_ имеет седловую точку Aij, если Aij является минимальным элементом в i-й строке и максимальным в _j-м_ столбце.

##### Инициализация многомерных массивов

Значения элементов многомерного массива, как и в одномерном случае, могут быть заданы константными значениями при объявлении, заключенными в фигурные скобки {}. Однако в этом случае указание количества элементов в строках и столбцах должно быть обязательно указано в квадратных скобках [ ].

Пример
``` C
#include <stdio.h>  
int main () {

  int a[2][3]={1, 2, 3, 4, 5, 6};

  printf ("%d %d %d\n", a[0][0], a[0][1], a[0][2]);

  printf ("%d %d %d\n", a[1][0], a[1][1], a[1][2]);

  return 0;  
}
```
Результат выполнения  
![](file:///C:/Users/ron4i/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)  
  

При работе с массива часто используется параметрический цикл, тот же результат выполнения программы будет достигнут следующим программным кодом:

  for (i=0; i<2; i++)  // цикл по строкам
``` C
   {

    for (j=0; j<3; j++) // цикл по столбцам

      printf ("%d ",a[ i][j]);

    printf (“\n”);

  }

```

Массив **а[2][3]** можно инициализировать, явно выделяя строки массива:

  int a[2][3]={{1, 2, 3}, {4, 5, 6}};

Можно инициализировать не все элементы массива, в нижеследующем инициализируются только элементы первого столбца:

 int a[2][3]={{1}, {4}};

Следующее описание формирует «треугольное» заполнение матрицы в целочисленном массиве из 5 строк и 4 столбцов:

int x[5][4]={{1}, {2, 3},{4, 5, 6},{7,8,9,10}};

|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Строка|0|   |   |   |1|   |   |   |2|   |   |   |3|   |   |   |4|   |   |   |
|Столбец|0|1|2|3|0|1|2|3|0|1|2|3|0|1|2|3|0|1|2|3|
|Значение|1||||2|3|||4|5|6||7|8|9|10|||||

  

Однако чаще требуется вводить значения элементов многомерного массива в процессе выполнения программы. С этой целью удобно использовать вложенный [параметрический цикл](http://prog-cpp.ru/c-cycles/#for "Параметрический цикл").

Пример

``` C
#include <stdio.h>  
int main() {

  int a[2][3]; // массив из 2 строк и 3 столбцов

  int i, j;

  // Ввод элементов массива

  for(i=0; i<2; i++)  // цикл по строкам

   {

    for(j=0; j<3; j++) // цикл по столбцам

     {

       printf("a[%d][%d] = ", i,j);

       scanf("%d", &a[i][j]);

    }

  }

```

  // Вывод элементов массива

``` C
  for(i=0; i<2; i++)  // цикл по строкам

  {

     for(j=0; j<3; j++) // цикл по столбцам

       {

         printf("%d ", a[i][j]);

       }

     printf("\n"); // перевод на новую строку

   }

  return 0;  
}
```


Результат выполнения  
![](file:///C:/Users/ron4i/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)


**ВЫПОЛНЕНО** 

``` C 
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

 
// Функция для поиска отрицательных элементов в строках с нулями

void countNegativesInZeroRows(int rows, int cols, int matrix[rows][cols])
{
    for (int i = 0; i < rows; i++)
    {
        int hasZero = 0;
        int negCount = 0;
        for (int j = 0; j < cols; j++)
        {
            if (matrix[i][j] == 0)
            {
               hasZero = 1;
            }
            if (matrix[i][j] < 0)
            {
               negCount++;
            }
        }
        if (hasZero)
        {
            printf("Row %d: %d negative elements\n", i + 1, negCount);
        }
    }
}
// Функция для поиска седловых точек

void findSaddlePoints(int rows, int cols, int matrix[rows][cols])
{
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < cols; j++)
        {
           int isMinRow = 1;
            int isMaxCol = 1;
            // Check if minimum in row
            for (int k = 0; k < cols; k++)
            {
                if (matrix[i][k] < matrix[i][j])
                {
                    isMinRow = 0;
                    break;
                }

            }

            // Проверьте, есть ли максимум в столбце
            for (int k = 0; k < rows; k++)
            {
                if (matrix[k][j] > matrix[i][j])
                {
                    isMaxCol = 0;
                    break;
                }
            }
            if (isMinRow && isMaxCol)
            {
                printf("Saddle point at (%d, %d): %d\n", i + 1, j + 1, matrix[i][j]);

            }
        }

    }

}
// Функция для замены строки и столбца (если они на главной диагонали)
void swapRowCol(int rows, int cols, int matrix[rows][cols], int row, int col)
{
    if (row == col)
    {
        for (int i = 0; i < cols; i++)
        {
            int temp = matrix[row][i];
            matrix[row][i] = matrix[i][col];
            matrix[i][col] = temp;
        }
    }
}

int main()
{
    int rows, cols;
    printf("Enter the number of rows and columns: ");
    if (scanf("%d %d", &rows, &cols) != 2)
    {
        fprintf(stderr, "Invalid input. Please enter integers.\n");
        return 1;
    }
    int matrix[rows][cols];
    printf("Enter the matrix elements:\n");
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < cols; j++)
        {
            if (scanf("%d", &matrix[i][j]) != 1)
            {
                fprintf(stderr, "Invalid input. Please enter integers.\n");
                return 1;
            }
        }
    }
    // Part 1
    printf("Negative elements in rows with zeros:\n");
    countNegativesInZeroRows(rows, cols, matrix);
    // Part 2
    
    printf("\nSaddle points:\n");
    findSaddlePoints(rows, cols, matrix);
    // Part 3 - Поиск и замена (требуется улучшение для нескольких седловых точек)
    
    int minSaddleRow = -1, minSaddleCol = -1, minSaddleVal = INT_MAX;
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < cols; j++)
        {
            int isMinRow = 1;
            int isMaxCol = 1;
            for (int k = 0; k < cols; k++)
            {
                if (matrix[i][k] < matrix[i][j])
                    isMinRow = 0;
            }
            for (int k = 0; k < rows; k++)
            {
                if (matrix[k][j] > matrix[i][j])
                    isMaxCol = 0;
            }
            if (isMinRow && isMaxCol && matrix[i][j] < minSaddleVal)
            {
                minSaddleVal = matrix[i][j];
                minSaddleRow = i;
                minSaddleCol = j;
            }
        }
    }

    if (minSaddleRow != -1)
    {
        printf("\nSwapping row and column for minimal saddle point...\n");
        swapRowCol(rows, cols, matrix, minSaddleRow, minSaddleCol);
        printf("Matrix after swap:\n");
        for (int i = 0; i < rows; i++)
        {
            for (int j = 0; j < cols; j++)
            {
                printf("%d ", matrix[i][j]);
            }
            printf("\n");
        }
    }
    else
    {
        printf("\nNo saddle point found.\n");
    }
    return 0;

}
```