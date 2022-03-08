**Сортировки:**
- Пузырьковая сортировка
- Сортировка выборкой
- Сортировка вставкой
- Сортировка Шелла
- Сортировка слиянием
- Быстрая сортировка
------------------------------------------------------------------------------------------
- **Устойчивость алгоритма сортировка (устойчивая или неустойчивая сортировка)** - если порядок следования дубликатов сохраняется во всех случаях
------------------------------------------------------------------------------------------
**Пузырьковая сортировка:**

```
public static void BubbleSort(int[] array)
{
    for (int partIndex = array.Length - 1; partIndex > 0; partIndex--)
    {
        for (int i = 0; i < partIndex; i++)
        {
            if (array[i] > array[i + 1])
            {
                Swap(array, i, i + 1);
            }
        }
    }
}
```

```
private static void Swap(int[] array, int i, int j)
{
	int temp = array[i];
	array[i] = array[j];
	array[j] = temp;
}
```
------------------------------------------------------------------------------------------
**Сортировка выборкой:**

```
public static void SelectionSort(int[] array)
{
	for (int partIndex = array.Length - 1; partIndex > 0; partIndex--)
	{
		int largestAt = 0;
		for (int i = 1; i <= partIndex; i++)
		{
			if (array[i] > array[largestAt])
			{
				largestAt = i;
			}
		}
		Swap(array, largestAt, partIndex);
	}
}
```
------------------------------------------------------------------------------------------
**Сортировка вставкой:**

```
public static void InsertionSort(int[] array)
{
	for (int partIndex = 1; partIndex < array.Length; partIndex++)
	{
		int curUnsorted = array[partIndex];
		int i = 0;
		for (i = partIndex; i > 0 && array[i - 1] > curUnsorted; i--)
		{
		    array[i] = array[i - 1];
		}

		array[i] = curUnsorted;
	}
}
```
------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
**Рекурсия:**

```
private static int RecursiveFactorial(int n)
{
    if (n == 0)
	return 1;

    return n * RecursiveFactorial(n - 1);
}
```

```
private static int IterativeFactorial(int number)
{
	if (number == 0)
		return 1;

	int factorial = 1;
	for (int i = 1; i <= number; i++)
	{
		factorial *= i;
	}

	return factorial;
}
```
