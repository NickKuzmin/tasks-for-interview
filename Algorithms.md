**Сортировки:**
- Пузырьковая сортировка
- Сортировка выборкой
- Сортировка вставкой
- Сортировка Шелла
- Сортировка слиянием
- Быстрая сортировка
------------------------------------------------------------------------------------------
- **Устойчивость алгоритма сортировка (устойчивая или неустойчивая сортировка)** - если порядок следования дубликатов сохраняется во всех случаях
- **Хвостовая рекурсия** - ...
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
**Сортировка Шелла:**

```
public static void ShellSort(int[] array)
{
	int gap = 1;
	while (gap < array.Length / 3)
		gap = 3 * gap + 1;

	while (gap >= 1)
	{
		for (int i = gap; i < array.Length; i++)
		{
			for (int j = i; j >= gap && array[j] < array[j - gap]; j -= gap)
			{
				Swap(array, j, j - gap);
			}

		}
		gap /= 3;
	}
}
```
------------------------------------------------------------------------------------------
**Сортировка слияниями:**

```
public static void MergeSort(int[] array)
{
	int[] aux = new int[array.Length];
	Sort(0, array.Length - 1);

	void Sort(int low, int high)
	{
		if (high <= low)
			return;

		int mid = (high + low) / 2;
		Sort(low, mid);
		Sort(mid+1, high);
		Merge(low, mid, high);
	}

	void Merge(int low, int mid, int high)
	{
		if (array[mid] <= array[mid + 1])
			return;

		int i = low;
		int j = mid + 1;

		Array.Copy(array, low, aux, low, high - low + 1);

		for (int k = low; k <= high; k++)
		{
			if (i > mid) array[k] = aux[j++];
			else if (j > high)
				array[k] = aux[i++];
			else if (aux[j] < aux[i])
				array[k] = aux[j++];
			else
				array[k] = aux[i++];
		}
	}
}
```
------------------------------------------------------------------------------------------
**Быстрая сортировка:**

```
public static void QuickSort(int[] array)
{
	Sort(0, array.Length - 1);

	void Sort(int low, int high)
	{
		if (high <= low)
			return;
		int j = Partition(low, high);
		Sort(low, j - 1);
		Sort(j + 1, high);
	}

	int Partition(int low, int high)
	{
		int i = low;
		int j = high + 1;

		int pivot = array[low];
		while (true)
		{
			while (array[++i] < pivot)
			{
				if (i == high)
					break;
			}

			while (pivot < array[--j])
			{
				if (j == low)
					break;
			}

			if (i >= j)
				break;

			Swap(array, i, j);
		}
		Swap(array, low, j);
		return j;
	}
}
```
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
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
**Списки (List):**

```
public class Node<T>
{
	public T Value { get; set; }
	public Node<T> Next { get; set; }

	public Node(T value)
	{
	    Value = value;
	}
}
```

```
public class SinglyLinkedList<T> : IEnumerable<T>
{
	public Node<T> Head { get; private set; }
	public Node<T> Tail { get; private set; }

	public int Count { get; private set; }

	public void AddFirst(T value)
	{
		AddFirst(new Node<T>(value));
	}

	private void AddFirst(Node<T> node)
	{
		//save off the current head
		Node<T> tmp = Head;

		Head = node;

		//shifting the former head
		Head.Next = tmp;

		Count++;

		if (Count == 1)
		{
			Tail = Head;
		}
	}

	public void AddLast(T value)
	{
		AddLast(new Node<T>(value));
	}

	private void AddLast(Node<T> node)
	{
		if (IsEmpty)
			Head = node;
		else
			Tail.Next = node;

		Tail = node;

		Count++;
	}

	public void RemoveFirst()
	{
		if (IsEmpty)
			throw new InvalidOperationException();

		Head = Head.Next;
		if (Count == 1)
			Tail = null;

		Count--;

	}

	public void RemoveLast()
	{
		if (IsEmpty)
			throw new InvalidOperationException();

		if (Count == 1)
		{
			Head = Tail = null;
		}
		else
		{
			//find the penultimate node
			var current = Head;
			while (current.Next != Tail)
			{
				current = current.Next;
			}

			current.Next = null;
			Tail = current;
		}

		Count--;
	}

	public bool IsEmpty => Count == 0;


	public IEnumerator<T> GetEnumerator()
	{
		Node<T> current = Head;
		while (current != null)
		{
			yield return current.Value;
			current = current.Next;
		}
	}

	IEnumerator IEnumerable.GetEnumerator()
	{
		return GetEnumerator();
	}
}
```

```
public class DoublyLinkedNode<T>
{
	public DoublyLinkedNode<T> Next { get; internal set; }
	public DoublyLinkedNode<T> Previous { get; internal set; }

	public T Value { get; set; }

	public DoublyLinkedNode(T value)
	{
		Value = value;
	}
}
```

```
public class DoublyLinkedList<T> : IEnumerable<T>
{
	public DoublyLinkedNode<T> Head { get; private set; }
	public DoublyLinkedNode<T> Tail { get; private set; }

	public void AddFirst(T value)
	{
		AddFirst(new DoublyLinkedNode<T>(value));
	}

	private void AddFirst(DoublyLinkedNode<T> node)
	{
		//save off the Head
		DoublyLinkedNode<T> temp = Head;
		//point Head to node
		Head = node;

		//insert the rest of the list after the head
		Head.Next = temp;

		if (IsEmpty)
		{
			Tail = Head;
		}
		else
		{
			//before: 1(head) <-------> 5 <-> 7 -> null
			//after:  3(head) <-------> 1 <-> 5 <-> 7 -> null

			//update "previous" ref of the former head
			temp.Previous = Head;
		}

		Count++;
	}

	public void AddLast(T value)
	{
		AddLast(new DoublyLinkedNode<T>(value));
	}

	private void AddLast(DoublyLinkedNode<T> node)
	{
		if (IsEmpty)
			Head = node;
		else
		{
			Tail.Next = node;
			node.Previous = Tail;
		}
		Tail = node;
		Count++;
	}

	public void RemoveFirst()
	{
		if (IsEmpty)
			throw new InvalidOperationException();
		//shift head
		Head = Head.Next;

		Count--;

		if (IsEmpty)
			Tail = null;
		else
			Head.Previous = null;
	}

	public void RemoveLast()
	{
		if (IsEmpty)
			throw new InvalidOperationException();

		if (Count == 1)
		{
			Head = null;
			Tail = null;
		}
		else
		{
			Tail.Previous.Next = null; //null the last node
			Tail = Tail.Previous; //shift the Tail (now it is the former penultimate node)
		}

		Count--;
	}

	public IEnumerator<T> GetEnumerator()
	{
		DoublyLinkedNode<T> current = Head;
		while (current != null)
		{
			yield return current.Value;
			current = current.Next;
		}
	}

	IEnumerator IEnumerable.GetEnumerator()
	{
		return GetEnumerator();
	}

	public int Count { get; private set; }
	public bool IsEmpty => Count == 0;
}
```
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
**Stack:**

```
public class ArrayStack<T> : IEnumerable<T>
{
	private T[] _items;

	public ArrayStack()
	{
		const int defaultCapacity = 4;
		_items = new T[defaultCapacity];
	}

	public ArrayStack(int capacity)
	{
		_items = new T[capacity];
	}

	public T Peek()
	{
		if (IsEmpty)
			throw new InvalidOperationException();
		return _items[Count - 1];
	}

	public void Pop()
	{
		if(IsEmpty)
			throw new InvalidOperationException();

		_items[--Count] = default(T);
	}

	public void Push(T item)
	{
		if (_items.Length == Count)
		{
			T[] largerArray = new T[Count * 2];
			Array.Copy(_items, largerArray, Count);

			_items = largerArray;
		}
		_items[Count++] = item;            
	}

	public bool IsEmpty => Count == 0;
	public int Count { get; private set; }
	public int Capacity => _items.Length;

	public IEnumerator<T> GetEnumerator()
	{
		for (int i = Count - 1; i >= 0; i--)
		{
			yield return _items[i];
		}
	}

	IEnumerator IEnumerable.GetEnumerator()
	{
		return GetEnumerator();
	}
}
```

```
public class LinkedStack<T> : IEnumerable<T>
{
	private readonly SinglyLinkedList<T> _list = new SinglyLinkedList<T>();

	public T Peek()
	{
		if (IsEmpty)
			throw new InvalidOperationException();
		return _list.Head.Value;
	}

	public void Pop()
	{
		if (IsEmpty)
			throw new InvalidOperationException();
		_list.RemoveFirst();
	}

	public void Push(T item)
	{
		_list.AddFirst(item);
	}

	public bool IsEmpty => Count == 0;
	public int Count => _list.Count;

	public IEnumerator<T> GetEnumerator()
	{
		return _list.GetEnumerator();
	}

	IEnumerator IEnumerable.GetEnumerator()
	{
		return GetEnumerator();
	}
}
```
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
**Queue (Очередь):**

```
public class ArrayQueue<T> : IEnumerable<T>
{
	private T[] _queue;
	private int _head;
	private int _tail;

	public ArrayQueue()
	{
		const int defaultCapacity = 4;
		_queue = new T[defaultCapacity];
	}

	public ArrayQueue(int capacity)
	{
		_queue = new T[capacity];
	}

	public void Enqueue(T item)
	{
		if (_queue.Length == _tail)            
		{
			T[] largerArray = new T[Count * 2];
			Array.Copy(_queue, largerArray, Count);
			_queue = largerArray;
		}

		_queue[_tail++] = item;
	}

	public void Dequeue()
	{
		if (IsEmpty)
			throw new InvalidOperationException();

		_queue[_head++] = default(T);

		if (IsEmpty)
			_head = _tail = 0;
	}

	public T Peek()
	{
		if (IsEmpty)
			throw new InvalidOperationException();
		return _queue[_head];
	}

	public bool IsEmpty => Count == 0;

	public int Count => _tail - _head;
	public int Capacity => _queue.Length;

	public IEnumerator<T> GetEnumerator()
	{
		for (int i = _head; i < _tail; i++)
		{
			yield return _queue[i];
		}
	}

	IEnumerator IEnumerable.GetEnumerator()
	{
		return GetEnumerator();
	}
}
```

```
public class CircularQueue<T> : IEnumerable<T>
{
	private T[] _queue;

	public CircularQueue()
	{
		const int defaultCapacity = 4;
		_queue = new T[defaultCapacity];
	}
	public CircularQueue(int capacity)
	{
		_queue = new T[capacity];
	}

	public void Enqueue(T item)
	{
		if (Count == _queue.Length - 1)
		{
			int countPriorResize = Count;
			T[] newArray = new T[2*_queue.Length];

			Array.Copy(_queue, _head, newArray, 0, _queue.Length - _head);
			Array.Copy(_queue, 0, newArray, _queue.Length - _head, _tail);

			_queue = newArray;

			_head = 0;
			_tail = countPriorResize;
		}

		_queue[_tail] = item;
		if (_tail < _queue.Length - 1)
		{
			_tail++;
		}
		else
		{
			_tail = 0;
		}
	}

	public void Dequeue()
	{
		if (IsEmpty)
			throw new InvalidOperationException();
		_queue[_head++] = default(T);

		if (IsEmpty)
			_head = _tail = 0;
		else if(_head == _queue.Length)
		{
			_head = 0;
		}
	}

	public T Peek()
	{
		if (IsEmpty)
			throw new InvalidOperationException();
		return _queue[_head];
	}

	public bool IsEmpty => Count == 0;

	private int _head;
	private int _tail;
	public int Count => _head <= _tail 
		? _tail - _head 
		: _tail - _head + _queue.Length;

	public int Capacity => _queue.Length;

	public IEnumerator<T> GetEnumerator()
	{
		if (_head <= _tail)
		{
			for (int i = _head; i < _tail; i++)
			{
				yield return _queue[i];
			}
		}
		else
		{
			for (int i = _head; i < _queue.Length; i++)
			{
				yield return _queue[i];
			}

			for (int i = 0; i < _tail; i++)
			{
				yield return _queue[i];
			}
		}
	}

	IEnumerator IEnumerable.GetEnumerator()
	{
		return GetEnumerator();
	}
}
```

```
public class LinkedQueue<T> : IEnumerable<T>
{
	private readonly SinglyLinkedList<T> _list = new SinglyLinkedList<T>();

	public void Enqueue(T item)
	{
		_list.AddLast(item);
	}

	public void Dequeue()
	{
		_list.RemoveFirst();
	}



	public T Peek()
	{
		if(IsEmpty)
			throw new InvalidOperationException();
		return _list.Head.Value;
	}

	public int Count => _list.Count;
	public bool IsEmpty => Count == 0;

	public IEnumerator<T> GetEnumerator()
	{
		return _list.GetEnumerator();
	}

	IEnumerator IEnumerable.GetEnumerator()
	{
		return GetEnumerator();
	}
}
```
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
**Binary Search (бинарный поиск):**

```
public class Searching
{
	public static int RecursiveBinarySearch(int[] array, int value)
	{
		return InternalRecursiveBinarySearch(0, array.Length);
		int InternalRecursiveBinarySearch(int low, int high)
		{
			if (low >= high)
				return -1;

			int mid = (low + high) / 2;
			if (array[mid] == value)
				return mid;
			if (array[mid] < value)
				return InternalRecursiveBinarySearch(mid + 1, high);
			return InternalRecursiveBinarySearch(low, mid);
		}
	}
	public static int BinarySearch(int[] array, int value)
	{
		int low = 0;
		int high = array.Length;

		while (low < high)
		{
			int mid = (low + high) / 2;

			if (array[mid] == value)
				return mid;
			if (array[mid] < value)
				low = mid + 1;
			else
				high = mid;
		}

		return -1;
	}
}
```
