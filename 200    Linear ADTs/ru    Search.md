## Линейный поиск.

```c++
// Возвращает позицию элемента, если он есть
// в массиве. Возвращает -1, если его нет.
int FindElement(const double* arr, int count, double element)
{
    for (int i = 0; i < count; ++i) 
    {
        if( arr[i] == element) { // Нашли.
            return i;
        }
    }
    return -1;
}
```

Найти максимальный элемент в массиве.
Вернуть его значение.
Решение: Последовательно проверяем все элементы массива, запоминаем текущее значение максимума.
Время работы T(n) = O(n) , где n – количество элементов в массиве.

```c++
// Возвращает максимальный элемент в массиве.
double MaxElement(const double* arr, int count)
{
    // Число элементов должно быть больше 0.
    assert(count > 0);
    double currentMax = arr[0];

    for (int i = 1; i < count; i++) 
    {
        if (arr[i] > currentMax) { // Нашли новый.
            currentMax = arr[i];
        }
    }
    return currentMax;
}
```

Задача (Бинарный поиск = Двоичный поиск).
На отсортированном массиве.
Проверить, есть ли заданный элемент в
упорядоченном массиве. Если он есть, вернуть
позицию его первого вхождения. Если его нет, 
вернуть -1.
Решение. Шаг. Сравниваем элемент в середине
массива (медиану) с заданным элементом. 
Выбираем нужную половинку массива в
зависимости результата сравнения.
Повторяем этот шаг до тех пор, пока размер
массива не уменьшится до 1.

```c++
// Бинарный поиск без рекурсии.
int BinarySearch(double* arr, int count, double element)
{
    int first = 0;
    int last = count; // Элемент в last не учитывается.

    while( first < last ) 
    {
        int mid = (first + last) / 2;

        if (element <= arr[mid]){
            last = mid;
        }
        else {
            first = mid + 1;
        }
    }
    // Все элементы слева от first строго больше искомого.
    return ( first == count || arr[first] != element ) ? -1 : first;
}

// Возвращает позицию вставки элемента на отрезке [first, last).
int FindInsertionPoint(const double* arr, int first, int last, double element)
{
    if (last – first == 1){
        return element <= arr[first] ? first : last;
    }
    int mid = ( first + last ) / 2;
    if (element <= arr[mid]){
        return FindInsertionPoint(arr, first, mid, element);
    }
    else {
        return FindInsertionPoint(arr, mid, last, element);
    }
}
// Возвращает позицию элемента в упорядоченном массиве, если он есть, и -1, если его нет.
int BinarySearch2(const double* arr, int count, double element)
{
    if(count == 0) 
        return -1;
    
    int point = FindInsertionPoint(arr, 0, count, element);
    return (point == count || arr[point] != element) ? -1 : point;
}
```

T(n) = O(log n),
M(n) = O(1).
-> в рекурсивном: M(n) = O(log n),
