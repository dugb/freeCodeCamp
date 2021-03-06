---
title: Arrays and Strings
localeTitle: Массивы и струны
---
# Массивы в C

Массивы позволяют сгруппировать вместе множество переменных как одну переменную. Это полезно само по себе, но также потому, что строки относятся к этой категории. Строки, которые мы представляем слова и предложения на компьютерных языках, являются просто наборами символьных переменных. Поэтому мы представляем строки, использующие массивы в C.

## Создание массива

Нормальная целочисленная переменная будет объявлена ​​следующим образом:

```C
int my_variable; 
```

Чтобы объявить это как массив и сделать его массивом из 5 целых чисел, его можно объявить следующим образом:

```C
int my_array[5]; 
```

Это создаст массив с именем `my_array` который может содержать 5 целых чисел. Однако ни одна из позиций в массиве не была установлена ​​(пока). Вы можете объявить массив и установить значения в начале:

```C
int my_array[] = {1, 5, 3, 6, 2}; 
```

Обратите внимание, что в этом примере мы не стали указывать число в квадратных скобках. Это связано с тем, что фигурные скобки имеют значения в них, которые будут назначены каждой позиции в массиве. Вы могли бы поместить число в скобки в любом случае, если вы сделали так, чтобы создать достаточное количество мест для хранения значений, которые вы проходите.

При инициализации массива вы можете предоставить меньше значений, чем элементы массива. Например, следующий оператор инициализирует только первые два элемента my\_array:

float my\_array \[5\] = {5.0, 2.5};

Если вы частично инициализируете массив, компилятор устанавливает оставшиеся элементы в ноль.

Теперь, когда массив был объявлен с 5 значениями, он имеет 5 мест памяти. Рассмотрим эту таблицу для наглядного примера:

| Должность | 0 | 1 | 2 | 3 | 4 | | ---------- | --- | --- | --- | --- | --- | | Значение | 1 | 5 | 3 | 6 | 2 |

Обратите внимание, что даже если имеется 5 мест памяти, позиции массива увеличиваются до 4. Это связано с тем, что массивы на C (и большинстве других языков) начинаются с 0, потому что массивы реализуются с помощью указателей. Когда вы вызываете позицию в массиве, вы действительно вызываете эту ячейку памяти и определенное число. Чтобы получить начало массива, переместите 0 мест в памяти, чтобы получить позицию после этого, переместить одно место в памяти и т. Д.

Вот пример установки массива в 9 в позиции 1:

```C
my_array[1] = 9; 
```

Таким образом, он похож на любую другую переменную, за исключением того, что имеет несколько значений для доступа, используя число в квадратных скобках. Значения могут быть возвращены так же:

```C
int variable = my_array[4]; 
```

Это объявит `variable` как целое число, равное значению в позиции 4 `my_array` . Однако, поскольку `variable` - это единственный `int` , а не массив, это **не** код, который будет иметь правильный результат:

```C
// This code will NOT work properly! 
 int variable = my_array; 
```

Любое целое число можно поместить в квадратные скобки, чтобы получить позицию в массиве. Эти целые числа также могут быть переменными. Взгляните на этот пример, который печатает содержимое массива:

```C
#include <stdio.h> 
 
 int main(void) { 
    int my_array[] = {1, 1, 2, 3, 5, 7, 12}; 
 
    for(int count = 0; count < 7; count++) { 
        printf("%i, \n", my_array[count]); 
    } 
 
    return 0; 
 } 
```

## Струны

Массивы - это множество переменных, а строки - это множества символов. В результате мы можем представлять строки с массивом. Вы _можете_ объявить что-то таким же образом, как и раньше, но вам нужно поместить '\\ 0' в качестве одного из ваших значений (подробнее об этом через минуту!):

```C
char hello_world[] = {'H', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd', '!', '\0'}; 
```

Хлоп. Это не очень хорошее решение. К счастью, C обеспечивает лучший способ с учетом строк:

```C
char hello_world[] = "Hello world!"; 
```

Это намного приятнее. Это даже не требует, чтобы вы поместили «\\ 0» в конце. Так что это было?

### Null Termination

Строки в C завершаются нулем, что означает, что они заканчиваются нулевым символом. Таким образом, код компилятора (и вашего и каждого другого) будет знать, где заканчивается строка: после того, как символ равен null, строка завершена.

Конечно, на клавиатуре нет кнопки «нуль», но вам все равно нужно ее ввести. Это то, что делает \\ 0. Всякий раз, когда компилятор C видит \\ 0, он вставляет нулевой символ. Это похоже на то, как \\ n печатает новую строку.

### Печать строк

Еще одна вещь C упрощает для нас печать строк. Вместо того, чтобы заставлять вас печатать каждый символ в массиве, вы можете просто использовать спецификатор формата% s и обрабатывать строку, как и любое значение `int` или `double` . Вот пример приветствия, мировой программы с самого начала, немного сложнее строк:

```C
#include <stdio.h> 
 
 int main(void) { 
    char hello_world[] = "Hello, World!\n"; 
    printf("%s", hello_world); 
 
    return 0; 
 } 
```

### Игра со струнами

Печать строк проста, но другие операции немного сложнее. К счастью, в библиотеке `string.h` есть несколько полезных функций для использования в ряде ситуаций.

#### Копирование: `strcpy`

`strcpy` (из 'string copy') копирует строку. Например, этот фрагмент кода скопирует содержимое строки `second` в строку `first` :

```C
strpy(first, second); 
```

Ниже приведен пример того, как выглядит ручная реализация функции strcpy:

void copy _string (char \[\] первая_ строка, char \[\] second\_string) { int i;
```
for(i = 0; first_string[i] != '\0'; i++) 
 { 
    first_string[i] = second_string[i]; 
 } 
```

}

#### Конкатенация: `strcat`

`strcat` (from 'string concatenate') будет конкатенировать строку, то есть она будет `strcat` содержимое одной строки и поместить ее в конец другой строки. В этом примере содержимое `second` будет конкатенировано на `first` :

```C
strcat(first, second); 
```

Вот пример ручной реализации fuction strcat:

void string\_concatenate (char \[\] s1, char \[\] s2) { int i = strlen (s1), j; for (int j = 0; s2 \[j\]; j ++, i + = 1) { s1 \[i\] = s2 \[j\]; } }

#### Получить длину: `strlen`

`strlen` (from 'string length') вернет целочисленное значение, соответствующее длине строки. В этом примере целому числу `string_length` будет назначена длина `my_string` :

```C
string_length = strlen(my_string); 
```

Вот ручная реализация fuction strlen:

int string\_length (char \[\] string) { int i;
```
for(int i = 0; string[i]; i++); 
 
 return i; 
```

}

#### Сравнить: `strcmp`

`strcmp` (из сравнения строк) сравнивает две строки. Целое число, которое оно возвращает, равно 0, если они одинаковы, но оно также будет возвращать отрицательное значение, если значение первого (путем сложения символов) меньше значения второго и положительное, если первое больше второго , Взгляните на пример того, как это можно использовать:

```C
if(!strcmp(first, second)){ 
    printf("These strings are the same!\n"); 
 } else { 
    printf("These strings are not the same!\n"); 
 } 
```

Обратите внимание `!` , что необходимо, потому что эта функция возвращает 0, если они одинаковы. Размещение восклицательного знака здесь приведет к тому, что сравнение вернется.

#### Разделить строку: `strtok`

`strtok` (из «токена строки») разбивает строку на ряд токенов, используя разделитель. В этом примере strtok разбивает строку str на ряд токенов, используя разделитель delim:

```C
char *strtok(char *str, const char *delim); 
```

# Прежде чем продолжить ...

## Обзор

*   Массивы - это совокупности переменных.
*   Массивы имеют отдельные позиции, которые могут быть объявлены скобками и доступны с квадратными скобками.
*   Строки также являются массивами, но мы можем относиться к ним несколько иначе: их можно объявить с помощью двойных кавычек и напечатать с использованием% s.
*   Строки имеют собственную библиотеку, `string.h` , которая имеет некоторые удобные функции для использования.