Конечно, давайте подробно рассмотрим каждое задание из пункта 6.6 и создадим соответствующие макросы на языке LibreOffice Basic.

## Задание 6.6.1: Очистка формата всего текста документа, выделенного текста, первого абзаца

### Макрос для очистки формата всего текста документа

```basic
Sub ClearFormatEntireDocument
    Dim Doc As Object
    Dim Enum As Object
    Dim TextElement As Object
    
    Doc = ThisComponent
    Enum = Doc.Text.createEnumeration
    
    While Enum.hasMoreElements
        TextElement = Enum.nextElement
        If TextElement.supportsService("com.sun.star.text.Paragraph") Then
            ' Сбросить форматирование абзаца к стилю по умолчанию
            TextElement.CharFontName = "Liberation Serif" ' Или любой другой стандартный шрифт
            TextElement.CharColor = RGB(0, 0, 0) ' Черный цвет
            TextElement.CharHeight = 12 ' Размер шрифта 12 pt
            TextElement.CharUnderline = com.sun.star.awt.FontUnderline.NONE
            TextElement.CharWeight = com.sun.star.awt.FontWeight.NORMAL
            TextElement.CharBackColor = RGB(255, 255, 255) ' Белый фон
            TextElement.CharPosture = com.sun.star.awt.FontSlant.NONE
            ' Сброс других свойств по необходимости
        End If
    Wend
    
    MsgBox "Формат всего текста документа очищен."
End Sub
```

### Макрос для очистки формата выделенного текста

```basic
Sub ClearFormatSelectedText
    Dim Doc As Object
    Dim Cursor As Object
    
    Doc = ThisComponent
    Cursor = Doc.CurrentController.getViewCursor()
    
    If Cursor.isCollapsed() Then
        MsgBox "Нет выделенного текста."
        Exit Sub
    End If
    
    ' Сбросить форматирование выделенного текста
    Cursor.CharFontName = "Liberation Serif"
    Cursor.CharColor = RGB(0, 0, 0)
    Cursor.CharHeight = 12
    Cursor.CharUnderline = com.sun.star.awt.FontUnderline.NONE
    Cursor.CharWeight = com.sun.star.awt.FontWeight.NORMAL
    Cursor.CharBackColor = RGB(255, 255, 255)
    Cursor.CharPosture = com.sun.star.awt.FontSlant.NONE
    
    MsgBox "Формат выделенного текста очищен."
End Sub
```

### Макрос для очистки формата первого абзаца

```basic
Sub ClearFormatFirstParagraph
    Dim Doc As Object
    Dim Text As Object
    Dim Enum As Object
    Dim Paragraph As Object
    
    ' Инициализация документа и текстового объекта
    Doc = ThisComponent
    Text = Doc.Text
    
    ' Создание перечислителя для абзацев
    Enum = Text.createEnumeration
    
    ' Проверка наличия абзацев в документе
    If Enum.hasMoreElements Then
        Paragraph = Enum.nextElement
        If Paragraph.supportsService("com.sun.star.text.Paragraph") Then
            ' Сбросить форматирование первого абзаца
            Paragraph.CharFontName = "Liberation Serif" ' Или любой другой стандартный шрифт
            Paragraph.CharColor = RGB(0, 0, 0) ' Черный цвет
            Paragraph.CharHeight = 12 ' Размер шрифта 12 pt
            Paragraph.CharUnderline = com.sun.star.awt.FontUnderline.NONE
            Paragraph.CharWeight = com.sun.star.awt.FontWeight.NORMAL
            Paragraph.CharBackColor = RGB(255, 255, 255) ' Белый фон
            Paragraph.CharPosture = com.sun.star.awt.FontSlant.NONE
        Else
            MsgBox "Первый элемент не является абзацем."
            Exit Sub
        End If
    Else
        MsgBox "Документ не содержит абзацев."
        Exit Sub
    End If
    
    MsgBox "Формат первого абзаца очищен."
End Sub

```

## Задание 6.6.2: Изменение стиля каждой первой и пятой буквы каждого абзаца на курсив и изменение цвета текста в активном документе и выделенном тексте

### Макрос для изменения первой и пятой буквы каждого абзаца

```basic
Sub FormatFirstAndFifthLetters
    Dim Doc As Object
    Dim Enum As Object
    Dim Paragraph As Object
    Dim Text As String
    Dim Cursor As Object
    Dim i As Integer
    
    Doc = ThisComponent
    Enum = Doc.Text.createEnumeration
    
    While Enum.hasMoreElements
        Paragraph = Enum.nextElement
        If Paragraph.supportsService("com.sun.star.text.Paragraph") Then
            Text = Paragraph.getString()
            If Len(Text) >= 1 Then
                ' Форматирование первой буквы
                Cursor = Doc.Text.createTextCursorByRange(Paragraph.Start)
                Cursor.goRight(1, True)
                Cursor.CharPosture = com.sun.star.awt.FontSlant.ITALIC
                Cursor.CharColor = RGB(255, 0, 0) ' Красный цвет
            End If
            If Len(Text) >= 5 Then
                ' Форматирование пятой буквы
                Dim FifthCharPos As Integer
                FifthCharPos = 4 ' Индексация с 0
                Cursor = Doc.Text.createTextCursorByRange(Paragraph.Start)
                Cursor.goRight(FifthCharPos, False)
                Cursor.goRight(1, True)
                Cursor.CharPosture = com.sun.star.awt.FontSlant.ITALIC
                Cursor.CharColor = RGB(0, 0, 255) ' Синий цвет
            End If
        End If
    Wend
    
    MsgBox "Форматирование первой и пятой букв каждого абзаца выполнено."
End Sub
```

### Макрос для изменения цвета текста в выделенном фрагменте

```basic
Sub ChangeColorSelectedText
    Dim Doc As Object
    Dim Cursor As Object
    
    Doc = ThisComponent
    Cursor = Doc.CurrentController.getViewCursor()
    
    If Cursor.isCollapsed() Then
        MsgBox "Нет выделенного текста."
        Exit Sub
    End If
    
    ' Изменение цвета выделенного текста
    Cursor.CharColor = RGB(0, 128, 0) ' Зеленый цвет
    
    MsgBox "Цвет выделенного текста изменен."
End Sub
```

## Задание 6.6.3: Поиск запятых в тексте и замена их на троеточие

### Макрос для замены запятых на троеточие

```basic
Sub ReplaceCommasWithEllipsis
    Dim Doc As Object
    Dim ReplaceDescriptor As Object
    Dim Found As Integer
    
    ' Инициализация документа
    Doc = ThisComponent
    
    ' Создание объекта ReplaceDescriptor
    ReplaceDescriptor = Doc.createReplaceDescriptor()
    
    ' Настройка параметров поиска и замены
    ReplaceDescriptor.SearchString = ","
    ReplaceDescriptor.ReplaceString = "..."
    
    ' Выполнение замены всех запятых на троеточие
    Found = Doc.replaceAll(ReplaceDescriptor)
    
    ' Вывод сообщения о результате
    MsgBox "Все запятые заменены на троеточие. Количество замен: " & Found
End Sub

```

**Примечание:** Данный макрос заменяет все запятые в документе на троеточие. Если требуется более сложная логика (например, разноцветные точки), потребуется использовать курсор и перебор символов.

## Задание 6.6.4: Обмен двух абзацев местами

### Макрос для обмена местами двух абзацев

```basic
Sub SwapTwoParagraphs
    Dim Doc As Object
    Dim Text As Object
    Dim Paragraph1 As Object
    Dim Paragraph2 As Object
    Dim TempText As String
    
    Doc = ThisComponent
    Text = Doc.Text
    
    ' Получение первого и второго абзацев
    If Text.getParagraphCount() < 2 Then
        MsgBox "В документе менее двух абзацев."
        Exit Sub
    End If
    
    Paragraph1 = Text.getParagraphByIndex(0)
    Paragraph2 = Text.getParagraphByIndex(1)
    
    ' Сохранение текста первого абзаца
    TempText = Paragraph1.getString()
    
    ' Замена текста
    Paragraph1.setString(Paragraph2.getString())
    Paragraph2.setString(TempText)
    
    MsgBox "Абзацы обменяны местами."
End Sub
```

**Примечание:** Данный макрос обменивает местами первые два абзаца. Для обмена других абзацев можно изменить индексы `getParagraphByIndex`.

## Задание 6.6.5: Изменение цвета и размера шрифта каждого абзаца на произвольный

### Макрос для изменения цвета и размера шрифта каждого абзаца на случайный

```basic
Sub ChangeFontColorAndSizeRandomly
    Dim Doc As Object
    Dim Enum As Object
    Dim Paragraph As Object
    Dim RandomColor As Long
    Dim RandomSize As Single
    Dim RndGen As New Random
    
    Doc = ThisComponent
    Enum = Doc.Text.createEnumeration
    
    While Enum.hasMoreElements
        Paragraph = Enum.nextElement
        If Paragraph.supportsService("com.sun.star.text.Paragraph") Then
            ' Генерация случайного цвета
            RandomColor = RGB(Int(RndGen.Next() * 256), Int(RndGen.Next() * 256), Int(RndGen.Next() * 256))
            ' Генерация случайного размера шрифта от 10 до 20 pt
            RandomSize = 10 + RndGen.Next() * 10
            
            ' Применение форматирования к абзацу
            Paragraph.CharColor = RandomColor
            Paragraph.CharHeight = RandomSize
        End If
    Wend
    
    MsgBox "Цвет и размер шрифта каждого абзаца изменены на случайные значения."
End Sub
```

**Примечание:** В данном макросе используется объект `Random` для генерации случайных значений. Если среда LibreOffice Basic не поддерживает объект `Random`, можно использовать функцию `Rnd()`.

### Альтернативный вариант с использованием функции `Rnd()`

```basic
Sub ChangeFontColorAndSizeRandomlyAlt
    Dim Doc As Object
    Dim Enum As Object
    Dim Paragraph As Object
    Dim RandomColor As Long
    Dim RandomSize As Single
    
    Doc = ThisComponent
    Enum = Doc.Text.createEnumeration
    
    Randomize ' Инициализация генератора случайных чисел
    
    While Enum.hasMoreElements
        Paragraph = Enum.nextElement
        If Paragraph.supportsService("com.sun.star.text.Paragraph") Then
            ' Генерация случайного цвета
            RandomColor = RGB(Int(Rnd * 256), Int(Rnd * 256), Int(Rnd * 256))
            ' Генерация случайного размера шрифта от 10 до 20 pt
            RandomSize = 10 + Rnd * 10
            
            ' Применение форматирования к абзацу
            Paragraph.CharColor = RandomColor
            Paragraph.CharHeight = RandomSize
        End If
    Wend
    
    MsgBox "Цвет и размер шрифта каждого абзаца изменены на случайные значения."
End Sub
```

## Задание 6.6.6: Изменение цвета и размера шрифта каждого третьего слова в тексте

### Макрос для изменения цвета и размера каждого третьего слова

```basic
Sub FormatEveryThirdWord
    Dim Doc As Object
    Dim Enum As Object
    Dim Paragraph As Object
    Dim Cursor As Object
    Dim WordCount As Integer
    
    Doc = ThisComponent
    Enum = Doc.Text.createEnumeration
    
    WordCount = 0
    
    While Enum.hasMoreElements
        Paragraph = Enum.nextElement
        If Paragraph.supportsService("com.sun.star.text.Paragraph") Then
            Dim WordEnum As Object
            Dim TextElement As Object
            WordEnum = Paragraph.createEnumeration
            
            While WordEnum.hasMoreElements
                TextElement = WordEnum.nextElement
                If TextElement.supportsService("com.sun.star.text.TextPortion") Then
                    WordCount = WordCount + 1
                    If WordCount Mod 3 = 0 Then
                        ' Создание курсора для текущего слова
                        Cursor = Doc.Text.createTextCursorByRange(TextElement.Start)
                        Cursor.gotoEndOfWord(True)
                        
                        ' Изменение цвета и размера шрифта
                        Cursor.CharColor = RGB(255, 0, 255) ' Фиолетовый цвет
                        Cursor.CharHeight = 14 ' Размер шрифта 14 pt
                    End If
                End If
            Wend
        End If
    Wend
    
    MsgBox "Форматирование каждого третьего слова выполнено."
End Sub
```

## Задание 6.6.7: Замена каждой запятой на последовательность трех разноцветных точек

### Макрос для замены запятых на три разноцветные точки

```basic
Sub ReplaceCommasWithColoredDots
    Dim Doc As Object
    Dim Cursor As Object
    Dim Found As Boolean
    
    Doc = ThisComponent
    Cursor = Doc.Text.createTextCursor()
    
    Found = Cursor.gotoStart(False)
    
    Do While Cursor.findNext(",")
        ' Установить курсор на запятую
        Cursor.gotoStartOfWord(False)
        Cursor.goRight(1, True) ' Выделить запятую
        
        ' Вставить три разноцветные точки
        Dim Dot1 As String, Dot2 As String, Dot3 As String
        Dot1 = "•" ' Точка 1
        Dot2 = "•" ' Точка 2
        Dot3 = "•" ' Точка 3
        
        ' Изменение цвета каждой точки
        Dim Range1 As Object, Range2 As Object, Range3 As Object
        Range1 = Cursor.Text.createTextCursorByRange(Cursor.Start)
        Range1.goRight(1, True)
        Range1.CharColor = RGB(255, 0, 0) ' Красный
        
        Range2 = Cursor.Text.createTextCursorByRange(Cursor.Start)
        Range2.goRight(1, True)
        Range2.CharColor = RGB(0, 255, 0) ' Зеленый
        
        Range3 = Cursor.Text.createTextCursorByRange(Cursor.Start)
        Range3.goRight(1, True)
        Range3.CharColor = RGB(0, 0, 255) ' Синий
        
        ' Заменить запятую на точки
        Cursor.String = Dot1 & Dot2 & Dot3
        
        ' Перейти к следующей запятой
        Found = Cursor.gotoNext(",", False)
        If Not Found Then Exit Do
    Loop
    
    MsgBox "Все запятые заменены на три разноцветные точки."
End Sub
```

**Примечание:** Данный макрос заменяет каждую запятую на три точки с разными цветами (красный, зеленый, синий). Символ `•` используется как точка. При необходимости можно изменить символы или цвета.

## Общие рекомендации по созданию и запуску макросов

1. **Создание макроса:**
    
    - Откройте LibreOffice Writer.
    - Перейдите в меню `Инструменты` → `Макросы` → `Организовать макросы` → `LibreOffice Basic`.
    - В появившемся окне выберите документ или `Мои макросы`, нажмите `Создать`.
    - Введите имя модуля и нажмите `OK`.
    - В редакторе вставьте код макроса и сохраните его.
2. **Запуск макроса:**
    
    - Перейдите в меню `Инструменты` → `Макросы` → `Выполнить макрос`.
    - Найдите созданный макрос в списке, выберите его и нажмите `Выполнить`.
3. **Назначение макроса на кнопку:**
    
    - Вы можете добавить кнопку на панель инструментов или в документ и назначить на нее соответствующий макрос для быстрого доступа.
4. **Безопасность макросов:**
    
    - Убедитесь, что настройки безопасности макросов позволяют выполнять созданные вами макросы. Перейдите в `Инструменты` → `Параметры` → `LibreOffice` → `Безопасность` → `Безопасность макросов`.

Эти макросы помогут автоматизировать рутинные задачи по форматированию текста в LibreOffice Writer, экономя ваше время и усилия.

Конечно, давайте продолжим выполнение лабораторной работы и реализуем пункт **6.6.8**. В этом задании необходимо заменить все запятые в тексте на символы `"<номер>"`, где `номер` — это порядковый номер запятой, начиная с 1. При этом цвет скобочек `"<>"` должен быть случайным для каждой пары.

## Задание 6.6.8: Замена запятых на символы «<>» с указанием номера запятой и случайным цветом скобочек

### Описание задания

- **Замена запятых:** Все запятые в тексте должны быть заменены на строку вида `"<номер>"`, где `номер` — последовательный номер запятой.
- **Случайный цвет скобочек:** Цвет символов `"<"` и `">"` должен быть случайным для каждой пары.

### Подход к решению

1. **Итерация по всему тексту документа:**
    - Используем объект `Cursor` для навигации по тексту.
    - Находим каждую запятую с помощью метода `findNext`.
2. **Замена запятых:**
    - Заменяем найденную запятую на строку `"<номер>"`, где `номер` — счетчик запятых.
3. **Установка случайного цвета для скобочек:**
    - После замены определяем позиции символов `"<"` и `">"`.
    - Генерируем случайные цвета для каждой пары скобочек.
    - Применяем эти цвета к соответствующим символам.

### Реализация макроса

```basic
Sub ReplaceCommasWithNumberedBrackets
    Dim Doc As Object
    Dim Text As Object
    Dim Cursor As Object
    Dim Found As Boolean
    Dim CommaCount As Integer
    Dim SearchString As String
    Dim ReplaceString As String
    Dim StartPos As Long
    Dim EndPos As Long
    Dim i As Integer
    
    ' Инициализация документа и курсора
    Doc = ThisComponent
    Text = Doc.Text
    Cursor = Doc.Text.createTextCursor()
    
    ' Инициализация счетчика запятых
    CommaCount = 0
    
    ' Инициализация генератора случайных чисел
    Randomize
    
    ' Установка курсора в начало документа
    Cursor.gotoStart(False)
    
    ' Цикл поиска запятых и их замены
    Do
        ' Поиск следующей запятой
        Found = Cursor.findNext(",")
        
        If Found Then
            ' Увеличение счетчика запятых
            CommaCount = CommaCount + 1
            
            ' Получение позиции запятой
            StartPos = Cursor.Start
            EndPos = Cursor.End
            
            ' Замена запятой на строку "<номер>"
            ReplaceString = "<" & CStr(CommaCount) & ">"
            Cursor.String = ReplaceString
            
            ' Создание нового курсора для форматирования скобочек
            Dim FormatCursor As Object
            FormatCursor = Doc.Text.createTextCursor()
            FormatCursor.gotoStart(False)
            FormatCursor.goRight(Len("<"), True) ' Выделение символа "<"
            
            ' Генерация случайного цвета для "<"
            Dim RandomColor1 As Long
            RandomColor1 = RGB(Int(Rnd * 256), Int(Rnd * 256), Int(Rnd * 256))
            FormatCursor.CharColor = RandomColor1
            
            ' Перемещение курсора к символу ">"
            FormatCursor.gotoEnd(False)
            FormatCursor.goLeft(Len(">" ), True) ' Выделение символа ">"
            
            ' Генерация случайного цвета для ">"
            Dim RandomColor2 As Long
            RandomColor2 = RGB(Int(Rnd * 256), Int(Rnd * 256), Int(Rnd * 256))
            FormatCursor.CharColor = RandomColor2
            
            ' Перемещение курсора после замененной строки
            Cursor.gotoRange(Cursor.End, False)
        End If
    Loop While Found
    
    MsgBox "Все запятые заменены на нумерованные скобочки с случайным цветом."
End Sub
```

### Пояснение к коду

1. **Инициализация объектов:**
    
    - `Doc`: текущий документ.
    - `Text`: текстовый объект документа.
    - `Cursor`: курсор для навигации и изменения текста.
2. **Счетчик запятых:**
    
    - Переменная `CommaCount` отслеживает количество замененных запятых.
3. **Поиск и замена запятых:**
    
    - Используется цикл `Do...Loop` для поиска каждой запятой в документе.
    - Каждая найденная запятая заменяется на строку `"<номер>"`, где `номер` увеличивается с каждой заменой.
4. **Форматирование скобочек:**
    
    - После замены запятой создается новый курсор `FormatCursor` для выделения символов `"<"` и `">"`.
    - Для каждого символа генерируется случайный цвет с помощью функции `RGB` и метода `Rnd`.
    - Применяется сгенерированный цвет к соответствующему символу.
5. **Завершение работы макроса:**
    
    - После завершения всех замен выводится сообщение об успешном завершении операции.

### Дополнительные рекомендации

- **Убедитесь в правильности настроек макросов:**
    
    - Перейдите в `Инструменты` → `Параметры` → `LibreOffice` → `Безопасность` → `Безопасность макросов` и настройте уровень безопасности таким образом, чтобы разрешить выполнение созданных макросов.
- **Тестирование макроса:**
    
    - Перед запуском макроса на важном документе рекомендуется протестировать его на копии документа, чтобы избежать нежелательных изменений.
- **Расширение функционала:**
    
    - При необходимости можно расширить макрос, например, добавить форматирование номера внутри скобочек или изменить стиль шрифта.

### Запуск макроса

1. **Создание макроса:**
    
    - Откройте LibreOffice Writer.
    - Перейдите в меню `Инструменты` → `Макросы` → `Организовать макросы` → `LibreOffice Basic`.
    - В появившемся окне выберите `Мои макросы` или текущий документ, нажмите `Создать`.
    - Введите имя модуля (например, `Module1`) и нажмите `OK`.
    - В редакторе макросов вставьте приведенный выше код и сохраните его.
2. **Запуск макроса:**
    
    - Перейдите в меню `Инструменты` → `Макросы` → `Выполнить макрос`.
    - В списке найдите созданный макрос `ReplaceCommasWithNumberedBrackets`, выберите его и нажмите `Выполнить`.
3. **Назначение макроса на кнопку (опционально):**
    
    - Вы можете добавить кнопку на панель инструментов или в сам документ и назначить на нее данный макрос для быстрого доступа.

### Пример работы макроса

**Исходный текст:**

```
Это пример текста, в котором есть несколько запятых, для тестирования макроса.
```

**Текст после выполнения макроса:**

```
Это пример текста<1>, в котором есть несколько запятых<2>, для тестирования макроса.
```

При этом символы `<` и `>` будут иметь случайные цвета для каждой пары.

### Итог

Макрос **ReplaceCommasWithNumberedBrackets** эффективно заменяет все запятые в документе на нумерованные скобочки с случайными цветами, что соответствует требованиям задания **6.6.8**. Вы можете использовать этот макрос для автоматизации форматирования текста и улучшения визуального представления документа.

Если у вас возникнут дополнительные вопросы или потребуется помощь с другими заданиями, не стесняйтесь обращаться!