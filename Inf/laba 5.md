

``` basic
Function SumEvenOddRowProducts(rng As Variant) As Double
    Dim totalEven As Double
    Dim totalOdd As Double
    Dim i As Long, j As Long
    Dim numRows As Long
    Dim numCols As Long

    totalEven = 0
    totalOdd = 0

    ' Определение границ массива
    numRows = UBound(rng, 1)
    numCols = UBound(rng, 2)

    ' Перебор строк матрицы
    For i = LBound(rng, 1) To UBound(rng, 1)
        Dim rowProduct As Double
        rowProduct = 1

        ' Перебор элементов в строке
        For j = LBound(rng, 2) To UBound(rng, 2)
            rowProduct = rowProduct * rng(i, j)
        Next j

        ' Проверка четности индекса строки
        If (i Mod 2) = 0 Then
            totalEven = totalEven + rowProduct
        Else
            totalOdd = totalOdd + rowProduct
        End If
    Next i

    ' Возвращаем сумму произведений четных и нечетных строк
    SumEvenOddRowProducts = totalEven + totalOdd
End Function

```

### Объяснение кода

1. **Объявление функции**:
    
    basic
    
    Copy
    
    ```
    Function SumEvenOddRowProducts(rng As Variant) As Double
    ```
    
    Здесь мы определяем функцию с названием `SumEvenOddRowProducts`, которая принимает один аргумент — `rng`. Этот аргумент представляет собой диапазон ячеек (матрицу) и имеет тип `Variant`, что позволяет работать с различными типами данных.
    
2. **Переменные**:
    
    basic
    
    Copy
    
    ```
    Dim totalEven As Double
    Dim totalOdd As Double
    Dim i As Long, j As Long
    Dim numRows As Long
    Dim numCols As Long
    ```
    
    Объявляем переменные:
    
    - `totalEven` и `totalOdd` — для хранения сумм произведений четных и нечетных строк соответственно.
    - `i` и `j` — индексы, которые будут использоваться для перебора строк и столбцов.
    - `numRows` и `numCols` — для определения количества строк и столбцов в массиве.
3. **Инициализация сумм**:
    
    basic
    
    Copy
    
    ```
    totalEven = 0
    totalOdd = 0
    ```
    
    Устанавливаем начальные значения сумм для четных и нечетных строк в `0`.
    
4. **Определение границ массива**:
    
    basic
    
    Copy
    
    ```
    numRows = UBound(rng, 1)
    numCols = UBound(rng, 2)
    ```
    
    Используя `UBound`, мы получаем количество строк (`numRows`) и столбцов (`numCols`) в переданном диапазоне. У `UBound(rng, 1)` возвращает верхнюю границу по первому измерению (строки), а `UBound(rng, 2)` — по второму измерению (столбцы).
    
5. **Цикл по строкам матрицы**:
    
    basic
    
    Copy
    
    ```
    For i = LBound(rng, 1) To UBound(rng, 1)
    ```
    
    Мы начинаем цикл, который будет проходить по каждой строке матрицы. `LBound(rng, 1)` возвращает нижнюю границу для строк, обычно это 1 в Calc.
    
6. **Инициализация произведения для строки**:
    
    basic
    
    Copy
    
    ```
    Dim rowProduct As Double
    rowProduct = 1
    ```
    
    Для каждой строки создаем переменную `rowProduct`, которая будет хранить произведение всех элементов строки и инициализируем её значением `1`, так как это нейтральный элемент для умножения.
    
7. **Цикл по столбцам**:
    
    basic
    
    Copy
    
    ```
    For j = LBound(rng, 2) To UBound(rng, 2)
    ```
    
    Внутренний цикл проходит по каждому элементу строки.
    
8. **Вычисление произведения**:
    
    basic
    
    Copy
    
    ```
    rowProduct = rowProduct * rng(i, j)
    ```
    
    Внутри цикла мы умножаем `rowProduct` на текущий элемент строки `rng(i, j)`.
    
9. **Проверка четности строки**:
    
    basic
    
    Copy
    
    ```
    If (i Mod 2) = 0 Then
        totalEven = totalEven + rowProduct
    Else
        totalOdd = totalOdd + rowProduct
    End If
    ```
    
    Здесь мы используем оператор `Mod`, чтобы проверить четность индекса текущей строки. Если индекс четный (например, 0, 2, 4 и т.д. — учитывая, что индекс `i` начинается с 1 в Calc), добавляем значение `rowProduct` к `totalEven`. Если нечетный, добавляем к `totalOdd`.
    
10. **Конец циклов**:
    
    basic
    
    Copy
    
    ```
    Next j
    Next i
    ```
    
    Эти строки завершают циклы по столбцам и строкам.
    
11. **Возврат результата**:
    
    basic
    
    Copy
    
    ```
    SumEvenOddRowProducts = totalEven + totalOdd
    ```
    
    В конце функции мы возвращаем сумму четных и нечетных произведений строк. В целом это значение будет результатом вызова функции.
    

### Примеры использования

- Если у вас есть матрица, например:

text

Copy

```
A1: 1  B1: 2
A2: 3  B2: 4
A3: 5  B3: 6
A4: 7  B4: 8
```

- Четные строки (1 и 3):
    
    - Строка 1: 1 * 2 = 2
    - Строка 3: 5 * 6 = 30
    - `totalEven = 2 + 30 = 32`
- Нечетные строки (2 и 4):
    
    - Строка 2: 3 * 4 = 12
    - Строка 4: 7 * 8 = 56
    - `totalOdd = 12 + 56 = 68`

В итоге функция вернет `32 + 68 = 100`.

### Заключение

Эта функция позволяет вам вычислить сумму произведений элементов по строкам, исходя из четности их индекса. В результате вы получаете удобный и компактный инструмент для анализа данных в таблице. Если у вас есть дополнительные вопросы о коде или хотите рассмотреть другие примеры, дайте знать!

### Пояснение кода

- Функция `SumEvenOddRowProducts` принимает диапазон как двумерный массив.
- `UBound` и `LBound` используются для получения границ массива, что позволяет итерироваться по элементам.
- В каждой строке вычисляется произведение всех элементов.
- В зависимости от четности индекса строки (`i Mod 2`), произведение добавляется к сумме четных или нечетных строк.
- Результат возвращается в виде суммы произведений обоих типов строк.
