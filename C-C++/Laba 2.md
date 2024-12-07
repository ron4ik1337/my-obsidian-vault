**Вариант 16**

Дана целочисленная прямоугольная матрица. Определить:

1) количество отрицательных элементов в тех строках, которые содержат хотя бы один нулевой элемент, вывести номер каждой строки и количество отрицательных элементов в ней;

2) номера строк и столбцов всех седловых точек матрицы;

3) поменять местами строку и столбец , находящиеся на пересечении минимальной седловой точки, если точка находится на главной диагонали.

**ПРИМЕЧАНИЕ**

Матрица _А_ имеет седловую точку Aij, если Aij является минимальным элементом в i-й строке и максимальным в _j-м_ столбце.


**ВЫПОЛНЕНО** 

``` C 
#include <stdio.h>

#include <stdlib.h>

#include <limits.h>

  

// Function to find negative elements in rows with zeros

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
// Function to find saddle points

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

            // Check if maximum in column
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
// Function to swap row and column (if on main diagonal)
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
    // Part 3 - Finding and swapping (needs improvement for multiple saddle points)
    
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