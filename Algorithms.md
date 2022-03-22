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
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
**Символьные таблицы:**

```
public class SequentialSearchSt<TKey, TValue>
{
	private class Node
	{
		public TKey Key { get; }
		public TValue Value { get; set; }

		public Node Next { get; set; }

		public Node(TKey key, TValue value, Node next)
		{
			Key = key;
			Value = value;
			Next = next;
		}
	}

	private Node _first;
	private readonly EqualityComparer<TKey> _comparer;

	public int Count { get; private set; }

	public SequentialSearchSt()
	{
		_comparer = EqualityComparer<TKey>.Default;
	}

	public SequentialSearchSt(EqualityComparer<TKey> comparer)
	{
		_comparer = comparer ?? throw new ArgumentNullException();
	}

	public bool TryGet(TKey key, out TValue val)
	{
		for (Node x = _first; x != null; x = x.Next)
		{
			if (_comparer.Equals(key, x.Key))
			{
				val = x.Value;
				return true;
			}
		}

		val = default(TValue);
		return false;
	}

	public void Add(TKey key, TValue val)
	{
		if (key == null)
		{
			throw new ArgumentNullException("Key can't be null.");
		}

		for (Node x = _first; x != null; x = x.Next)
		{
			if (_comparer.Equals(key, x.Key))
			{
				x.Value = val;
				return;
			}
		}

		_first = new Node(key, val, _first);

		Count++;
	}

	public bool Contains(TKey key)
	{
		for (Node x = _first; x != null; x = x.Next)
		{
			if (_comparer.Equals(key, x.Key))
				return true;
		}

		return false;
	}

	public IEnumerable<TKey> Keys()
	{
		for (Node x = _first; x != null; x = x.Next)
		{
			yield return x.Key;
		}
	}

	public bool Remove(TKey key)
	{
		// Null key is not allowed. 
		// Counter should be adjusted properly.
		// It should remove a key - value pair entirely. 
		// It should return false if the requested key was not found, otherwise true.

		if(key==null)
			throw new ArgumentNullException("Key can't be null.");

		if (Count == 1 && _comparer.Equals(_first.Key, key))
		{
			_first = null;
			Count--;
			return true;
		}

		Node prev = null;
		Node current = _first;

		while (current != null)
		{                
			if (_comparer.Equals(current.Key, key))
			{
				if (prev == null)
				{
					_first = current.Next;
				}
				else
				{
					prev.Next = current.Next;
				}

				Count--;
				return true;
			}

			prev = current;
			current = current.Next;
		}

		return false;
	}
}
```

```
public class BinarySearchSt<TKey, TValue>
{
	private TKey[] _keys;
	private TValue[] _values;

	public int Count { get; private set; }

	private readonly IComparer<TKey> _comparer;

	public int Capacity => _keys.Length;
	public bool IsEmpty => Count == 0;

	private const int DefaultCapacity = 4;

	public BinarySearchSt(int capacity, IComparer<TKey> comparer)
	{
		_keys = new TKey[capacity];
		_values = new TValue[capacity];
		_comparer = comparer ?? throw new ArgumentNullException("Comparer can't be null.");
	}

	public BinarySearchSt(int capacity): this(capacity, Comparer<TKey>.Default)
	{		
	}

	public BinarySearchSt(): this(DefaultCapacity)
	{		
	}

	public int Rank(TKey key)
	{
		int low = 0;
		int high = Count - 1;

		while (low <= high)
		{
			int mid = low + (high - low) / 2;

			int cmp = _comparer.Compare(key, _keys[mid]);

			if (cmp < 0)
				high = mid - 1;
			else if (cmp > 0)
				low = mid + 1;
			else
				return mid;
		}
		return low;
	}

	public TValue GetValueOrDefault(TKey key)
	{
		if (IsEmpty)
		{
			return default(TValue);
		}

		int rank = Rank(key);
		if (rank < Count && _comparer.Compare(_keys[rank], key) == 0)
		{
			return _values[rank];
		}

		return default(TValue);
	}

	public void Add(TKey key, TValue value)
	{
		if (key == null)
			throw new ArgumentNullException("Key can't be null");

		int rank = Rank(key);
		if (rank < Count && _comparer.Compare(_keys[rank], key) == 0)
		{
			_values[rank] = value;
			return;
		}

		if (Count == Capacity)
			Resize(Capacity * 2);

		for (int j = Count; j > rank; j--)
		{
			_keys[j] = _keys[j - 1];
			_values[j] = _values[j - 1];
		}

		_keys[rank] = key;
		_values[rank] = value;

		Count++;
	}

	public void Remove(TKey key)
	{
		if (key == null)
			throw new ArgumentNullException("Key can't be null");

		if (IsEmpty)
			return;

		int r = Rank(key);
		if (r == Count || _comparer.Compare(_keys[r], key) != 0)
			return;

		for (int j = r; j < Count - 1; j++)
		{
			_keys[j] = _keys[j + 1];
			_values[j] = _values[j + 1];
		}

		Count--;
		_keys[Count] = default(TKey);
		_values[Count] = default(TValue);

		//resize if 1/4 full
		//if(Count > 0 && Count ==keys.Length / 4) Resize(_keys.Length / 2);
	}

	public bool Contains(TKey key)
	{
		int r = Rank(key);
		if (r < Count && _comparer.Compare(_keys[r], key) == 0)
			return true;
		return false;
	}

	public IEnumerable<TKey> Keys()
	{
		foreach (var key in _keys)
		{
			yield return key;
		}
	}

	private void Resize(int capacity)
	{
		TKey[] keysTmp = new TKey[capacity];
		TValue[] valuesTmp = new TValue[capacity];

		for (int i = 0; i < Count; i++)
		{
			keysTmp[i] = _keys[i];
			valuesTmp[i] = _values[i];
		}

		_values = valuesTmp;
		_keys = keysTmp;
	}

	public TKey Min()
	{
		if(IsEmpty)
			throw new InvalidOperationException("Table is empty.");
		return _keys[0];
	}

	public TKey Max()
	{
		if (IsEmpty)
			throw new InvalidOperationException("Table is empty.");
			
		return _keys[Count - 1];
	}

	public void RemoveMin()
	{
		if (IsEmpty)
			throw new InvalidOperationException("Table is empty.");

		Remove(Min());
	}

	public void RemoveMax()
	{
		if (IsEmpty)
			throw new InvalidOperationException("Table is empty.");

		Remove(Max());
	}

	public TKey Select(int index)
	{
		if(index<0 || index>=Count)
			throw new ArgumentException("Can't select since index is out of range.");
			
		return _keys[index];
	}

	public TKey Ceiling(TKey key)
	{
		if(key==null)
			throw new ArgumentNullException("Argument to ceiling() is null.");

		int r = Rank(key);
		if (r == Count) return default(TKey);
		else return _keys[r];
	}

	public TKey Floor(TKey key)
	{
		if (key == null)
			throw new ArgumentNullException("Argument to floor() is null.");

		int r = Rank(key);
		if (r < Count && _comparer.Compare(_keys[r], key)==0) return _keys[r];
		if (r == 0)
			return default(TKey);
		else
			return _keys[r - 1];
	}

	public IEnumerable<TKey> Range(TKey left, TKey right)
	{
		var q = new LinkedQueue<TKey>();

		int low = Rank(left);
		int high = Rank(right);

		for (int i = low; i < high; i++)
		{
			q.Enqueue(_keys[i]);
		}

		if (Contains(right))
			q.Enqueue(_keys[Rank(right)]);

		return q;
	}
}
```

```
public class ChainHashSet<TKey, TValue>
{
	private SequentialSearchSt<TKey, TValue>[] _chains;

	private const int DefaultCapacity = 4;
	public int Count { get; private set; }
	public int Capacity { get; private set; }

	public ChainHashSet():this(Prime.MinPrime)
	{		
	}

	public ChainHashSet(int capacity)
	{
		Capacity = capacity;
		_chains = new SequentialSearchSt<TKey, TValue>[capacity];
		for (int i = 0; i < capacity; i++)
		{
			_chains[i] = new SequentialSearchSt<TKey, TValue>();
		}
	}

	private int Hash(TKey key)
	{
		return (key.GetHashCode() & 0x7fffffff) % Capacity;
	}

	public TValue Get(TKey key)
	{
		if(key==null)
			throw new ArgumentNullException("Key is not allowed to be null");

		int index = Hash(key);
		if (_chains[index].TryGet(key, out TValue val))
		{
			return val;
		}

		throw new ArgumentException("Key was not found.");
	}

	public bool Contains(TKey key)
	{
		if (key == null)
			throw new ArgumentNullException("Key is not allowed to be null");

		int index = Hash(key);
		return _chains[index].TryGet(key, out TValue _);
	}

	public bool Remove(TKey key)
	{
		if (key == null)
			throw new ArgumentNullException("Key is not allowed to be null");

		int index = Hash(key);
		if (_chains[index].Contains(key))
		{
			Count--;
			_chains[index].Remove(key);

			if(Capacity > DefaultCapacity && Count <= 2*Capacity)
				Resize(Prime.ReducePrime(Capacity));

			return true;
		}

		return false;
	}

	public void Add(TKey key, TValue val)
	{
		if (key == null)
			throw new ArgumentNullException("Key is not allowed to be null");

		if (val == null)
		{
			Remove(key);
			return;
		}

		if (Count >= 10 * Capacity) Resize(Prime.ExpandPrime(Capacity));

		int i = Hash(key);
		if (!_chains[i].Contains(key))
			Count++;

		_chains[i].Add(key, val);
	}

	private void Resize(int chains)
	{
		var temp = new ChainHashSet<TKey, TValue>(chains);
		for (int i = 0; i < Capacity; i++)
		{
			foreach (TKey key in _chains[i].Keys())
			{
				if (_chains[i].TryGet(key, out TValue val))
				{
					temp.Add(key, val);
				}
			}
		}

		Capacity = temp.Capacity;
		Count = temp.Count;
		_chains = temp._chains;
	}

	public IEnumerable<TKey> Keys()
	{
		var queue = new LinkedQueue<TKey>();
		for (int i = 0; i < Capacity; i++)
		{
			foreach (TKey key in _chains[i].Keys())
			{
				queue.Enqueue(key);
			}
		}
		return queue;
	}
}
```

```
public class Prime
{
	private static readonly int[] Predefined = {
		3, 7, 11, 17, 23, 29, 37, 47, 59, 71, 89, 107, 131, 163, 197, 239, 293, 353, 431, 521, 631, 761, 919,
		1103, 1327, 1597, 1931, 2333, 2801, 3371, 4049, 4861, 5839, 7013, 8419, 10103, 12143, 14591,
		17519, 21023, 25229, 30293, 36353, 43627, 52361, 62851, 75431, 90523, 108631, 130363, 156437,
		187751, 225307, 270371, 324449, 389357, 467237, 560689, 672827, 807403, 968897, 1162687, 1395263,
		1674319, 2009191, 2411033, 2893249, 3471899, 4166287, 4999559, 5999471, 7199369};

	public static int MinPrime => Predefined[0];

	public static int GetPrime(int min)
	{
		if (min < 0)
			throw new ArgumentException("Min can't be negative");

		for (int i = 0; i < Predefined.Length; i++)
		{
			int prime = Predefined[i];
			if (prime >= min) return prime;
		}

		for (int i = min | 1; i < int.MaxValue; i += 2)
		{
			if (IsPrime(i) && (i - 1) % HashPrime != 0)
				return i;
		}

		return min;
	}

	private const int HashPrime = 101;

	private static bool IsPrime(int candidate)
	{
		if (candidate % 2 != 0)
		{
			int limit = (int)Math.Sqrt(candidate);
			for (int divisor = 3; divisor <= limit; divisor += 2)
			{
				if (candidate % divisor == 0)
					return false;
			}

			return true;
		}

		return candidate == 2;
	}

	public static int ExpandPrime(int oldSize)
	{
		int newSize = 2 * oldSize;
		if ((uint)newSize > MaxPrimeArrayLength && MaxPrimeArrayLength > oldSize)
			return MaxPrimeArrayLength;
		return GetPrime(newSize);
	}

	//= 2146435069
	public const int MaxPrimeArrayLength = 0x7FEFFFFD;

	public static int ReducePrime(int oldSize)
	{
		int newSize = oldSize / 2;
		if (newSize > MaxPrimeArrayLength && MaxPrimeArrayLength > oldSize)
			return MaxPrimeArrayLength;

		return GetPrime(newSize);
	}

	public static IEnumerable<int> Sieve(int max)
	{
		bool[] composite = new bool[max + 1];

		for (int p = 2; p <= max; p++)
		{
			if (composite[p]) continue;

			yield return p;

			for (int i = p * p; i <= max; i+=p)
			{
				composite[i] = true;
			}
		}
	}
}
```

```
public class LinearProbingHashSet<TKey, TValue>
{
	private const int DefaultCapacity = 4;

	public int Count { get; private set; }
	public int Capacity { get; private set; }
	private TKey[] _keys;
	private TValue[] _values;

	public LinearProbingHashSet() : this(DefaultCapacity)
	{

	}

	public LinearProbingHashSet(int capacity)
	{
		Capacity = capacity;
		_keys = new TKey[capacity];
		_values = new TValue[capacity];
	}

	private int Hash(TKey key)
	{
		return (key.GetHashCode() & 0x7fffffff) % Capacity;
	}

	public bool Contains(TKey key)
	{
		if (key == null)
			throw new ArgumentNullException("Key is not allowed to be null");

		for (int i = Hash(key); _keys[i] != null; i = (i + 1) % Capacity)
		{
			if (_keys[i].Equals(key))
				return true;
		}

		return false;
	}

	public TValue Get(TKey key)
	{
		if (key == null)
			throw new ArgumentNullException("Key is not allowed to be null");

		for (int i = Hash(key); _keys[i] != null; i = (i + 1) % Capacity)
		{
			if (_keys[i].Equals(key))
			{
				return _values[i];
			}
		}

		throw new ArgumentException("Key was not found.");
	}

	public bool TryGet(TKey key, out int index)
	{
		if (key == null)
			throw new ArgumentNullException("Key is not allowed to be null");

		for (int i = Hash(key); _keys[i] != null; i = (i + 1) % Capacity)
		{
			if (_keys[i].Equals(key))
			{
				index = i;
				return true;
			}
		}

		index = -1;
		return false;
	}

	public void Remove(TKey key)
	{
		if (key == null)
			throw new ArgumentNullException("Key is not allowed to be null");

		if (!TryGet(key, out int index))
			return;

		_keys[index] = default(TKey);
		_values[index] = default(TValue);

		index = (index + 1) % Capacity;

		while (_keys[index] != null)
		{
			TKey keyToRehash = _keys[index];
			TValue valToRehash = _values[index];

			_keys[index] = default(TKey);
			_values[index] = default(TValue);

			Count--;

			Add(keyToRehash, valToRehash);

			index = (index + 1) % Capacity;
		}

		Count--;

		if (Count > 0 && Count <= Capacity / 8)
			Resize(Capacity / 2);
	}

	public void Add(TKey key, TValue value)
	{
		if (key == null)
			throw new ArgumentNullException("Key is not allowed to be null");

		if (value == null)
		{
			Remove(key);
			return;
		}

		if (Count >= Capacity / 2)
			Resize(2 * Capacity);

		int i;
		for (i = Hash(key); _keys[i] != null; i = (i + 1) % Capacity)
		{
			if (_keys[i].Equals(key))
			{
				_values[i] = value;
				return;
			}
		}

		_keys[i] = key;
		_values[i] = value;

		Count++;
	}

	private void Resize(int capacity)
	{
		var temp = new LinearProbingHashSet<TKey, TValue>(capacity);

		for (int i = 0; i < Capacity; i++)
		{
			if (_keys[i] != null)
			{
				temp.Add(_keys[i], _values[i]);
			}
		}

		_keys = temp._keys;
		_values = temp._values;

		Capacity = temp.Capacity;
	}

	public IEnumerable<TKey> Keys()
	{
		var q = new Queue<TKey>();
		for (int i = 0; i < Capacity; i++)
		{
			if(_keys[i]!=null)
				q.Enqueue(_keys[i]);
		}

		return q;
	}
}
```
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
**Trees (деревья):**

```
public class TreeNode<T> where T : IComparable<T>
{
	public T Value { get; set; }
	public TreeNode<T> Left { get; set; }
	public TreeNode<T> Right { get; set; }

	public TreeNode(T value)
	{
		Value = value;
	}

	public void Insert(T newValue)
	{
		int compare = newValue.CompareTo(Value);
		if (compare == 0)
			return;

		if (compare < 0)
		{
			if (Left == null)
			{
				Left = new TreeNode<T>(newValue);
			}
			else
			{
				Left.Insert(newValue);
			}
		}
		else
		{
			if (Right == null)
			{
				Right = new TreeNode<T>(newValue);
			}
			else
			{
				Right.Insert(newValue);
			}
		}        
	}

	public TreeNode<T> Get(T value)
	{
		int compare = value.CompareTo(Value);
		if (compare == 0)
		{
			return this;
		}

		if (compare < 0)
		{
			if (Left != null)
				return Left.Get(value);
		}
		else
		{
			if (Right != null)
				return Right.Get(value);
		}

		return null;
	}

	public IEnumerable<T> TraverseInOrder()
	{
		var list = new List<T>();
		InnerTraverse(list);
		return list;
	}

	private void InnerTraverse(List<T> list)
	{
		if(Left!=null)
			Left.InnerTraverse(list);

		list.Add(Value);

		if (Right != null)
			Right.InnerTraverse(list);
	}

	public T Min()
	{
		if (Left != null)
			return Left.Min();
		return Value;
	}
	public T Max()
	{
		if (Right != null)
			return Right.Max();
		return Value;
	}
}
```

```
public class Bst<T> where T : IComparable<T>
{
	private TreeNode<T> _root;

	public void Remove(T value)
	{
		_root = Remove(_root, value);
	}

	public TreeNode<T> Remove(TreeNode<T> subtreeRoot, T value)
	{
		if (subtreeRoot == null)
			return null;
		int compareTo = value.CompareTo(subtreeRoot.Value);
		if (compareTo < 0)
		{
			subtreeRoot.Left = Remove(subtreeRoot.Left, value);
		}
		else if (compareTo > 0)
		{
			subtreeRoot.Right = Remove(subtreeRoot.Right, value);
		}
		else
		{
			if (subtreeRoot.Left == null)
			{
				return subtreeRoot.Right;
			}

			if (subtreeRoot.Right == null)
			{
				return subtreeRoot.Left;
			}

			subtreeRoot.Value = subtreeRoot.Right.Min();
			subtreeRoot.Right = Remove(subtreeRoot.Right, subtreeRoot.Value);

		}

		return subtreeRoot;
	}

	public TreeNode<T> Get(T value)
	{
		return _root?.Get(value);
	}

	public T Min()
	{
		if(_root==null)
			throw new InvalidOperationException("Empty tree.");
		return _root.Min();
	}

	public T Max()
	{
		if (_root == null)
			throw new InvalidOperationException("Empty tree.");
		return _root.Max();
	}

	public void Insert(T value)
	{
		if(_root==null)
			_root = new TreeNode<T>(value);
		else
		{
			_root.Insert(value);
		}
	}

	public IEnumerable<T> TraverseInOrder()
	{
		if (_root != null)
		{
			return _root.TraverseInOrder();
		}

		return Enumerable.Empty<T>();
	}
}
```
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
**Heap (куча/пирамида):**

```
public class MaxHeap<T> where T : IComparable<T>
{
	private const int DefaultCapacity = 4;
	private T[] _heap;

	public int Count { get; private set; }

	public bool IsFull => Count == _heap.Length;
	public bool IsEmpty => Count == 0;

	public void Insert(T value)
	{
		if (IsFull)
		{
			var newHeap = new T[_heap.Length * 2];
			Array.Copy(_heap, 0, newHeap, 0, _heap.Length);
			_heap = newHeap;
		}

		_heap[Count] = value;

		Swim(Count);

		Count++;
	}

	private void Swim(int indexOfSwimmingItem)
	{
		T newValue = _heap[indexOfSwimmingItem];
		while (indexOfSwimmingItem > 0 && IsParentLess(indexOfSwimmingItem))
		{
			_heap[indexOfSwimmingItem] = GetParent(indexOfSwimmingItem);
			indexOfSwimmingItem = ParentIndex(indexOfSwimmingItem);
		}

		_heap[indexOfSwimmingItem] = newValue;

		bool IsParentLess(int swimmingItemIndex)
		{
			return newValue.CompareTo(GetParent(swimmingItemIndex)) > 0;
		}
	}

	public IEnumerable<T> Values()
	{
		for (var i = 0; i < Count; i++)
		{
			yield return _heap[i];
		}
	}

	private T GetParent(int index)
	{
		return _heap[ParentIndex(index)];
	}

	private int ParentIndex(int index)
	{
		return (index - 1) / 2;
	}

	public T Peek()
	{
		if(IsEmpty)
			throw new InvalidOperationException();
		return _heap[0];
	}

	public T Remove()
	{
		return Remove(0);
	}

	public T Remove(int index)
	{
		if (IsEmpty)
			throw new InvalidOperationException();

		T removedValue = _heap[index];
		_heap[index] = _heap[Count - 1];
		if (index == 0 || _heap[index].CompareTo(GetParent(index)) < 0)
		{
			Sink(index, Count - 1);
		}
		else
		{
			Swim(index);
		}

		Count--;
		return removedValue;
	}

	private void Sink(int indexOfSinkingItem, int lastHeapIndex)
	{
		while (indexOfSinkingItem <= lastHeapIndex)
		{
			int leftChildIndex = LeftChildIndex(indexOfSinkingItem);
			int rightChildIndex = RightChildIndex(indexOfSinkingItem);

			if (leftChildIndex > lastHeapIndex)
				break;

			int childIndexToSwap = GetChildIndexToSwap(leftChildIndex, rightChildIndex);

			if (SinkingIsLessThan(childIndexToSwap))
			{
				Exchange(indexOfSinkingItem, childIndexToSwap);
			}
			else
				break;

			indexOfSinkingItem = childIndexToSwap;
		}

		bool SinkingIsLessThan(int childToSwap)
		{
			return _heap[indexOfSinkingItem].CompareTo(_heap[childToSwap]) < 0;
		}
	   
		int GetChildIndexToSwap(int leftChildIndex, int rightChildIndex)
		{
			int childToSwap;
			if (rightChildIndex > lastHeapIndex)
			{
				childToSwap = leftChildIndex;
			}
			else
			{
				int compareTo = _heap[leftChildIndex].CompareTo(_heap[rightChildIndex]);
				childToSwap = compareTo > 0 ? leftChildIndex : rightChildIndex;
			}

			return childToSwap;
		}
	}

	private int LeftChildIndex(int parentIndex)
	{
		return 2 * parentIndex + 1;
	}

	private int RightChildIndex(int parentIndex)
	{
		return 2 * parentIndex + 2;
	}

	public MaxHeap():this(DefaultCapacity)
	{
		
	}

	private MaxHeap(int capacity)
	{
		_heap = new T[capacity];
	}

	public void Sort()
	{
		int lastHeapIndex = Count - 1;
		for (int i = 0; i < lastHeapIndex; i++)
		{
			Exchange(0, lastHeapIndex - i);
			Sink(0, lastHeapIndex - i - 1);
		}
	}

	private void Exchange(int leftIndex, int rightIndex)
	{
		T tmp = _heap[leftIndex];
		_heap[leftIndex] = _heap[rightIndex];
		_heap[rightIndex] = tmp;
	}
}
```
