

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

### Пояснение кода

- Функция `SumEvenOddRowProducts` принимает диапазон как двумерный массив.
- `UBound` и `LBound` используются для получения границ массива, что позволяет итерироваться по элементам.
- В каждой строке вычисляется произведение всех элементов.
- В зависимости от четности индекса строки (`i Mod 2`), произведение добавляется к сумме четных или нечетных строк.
- Результат возвращается в виде суммы произведений обоих типов строк.

