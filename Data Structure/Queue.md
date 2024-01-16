_A **Queue** is defined as a linear data structure that is open at both ends and the operations are performed in First In First Out (FIFO) order._

We define a queue to be a list in which all additions to the list are made at one end, and all deletions from the list are made at the other end.  The element which is first pushed into the order, the operation is first performed on that.

![[Queue-Data-Structures.png]]

### Applications of Queue

Due to the fact that queue performs actions on first in first out basis which is quite fair for the ordering of actions. There are various applications of queues discussed as below.

1. Queues are widely used as waiting lists for a single shared resource like printer, disk, CPU.
2. Queues are used in asynchronous transfer of data (where data is not being transferred at the same rate between two processes) for eg. pipes, file IO, sockets.
3. Queues are used as buffers in most of the applications like MP3 media player, CD player, etc.
4. Queue are used to maintain the play list in media players in order to add and remove the songs from the play-list.
5. Queues are used in operating systems for handling interrupts.

### In [[CSHARP|C#]]

![https://media.geeksforgeeks.org/wp-content/uploads/Untitled-Diagram-38.jpg](https://media.geeksforgeeks.org/wp-content/uploads/Untitled-Diagram-38.jpg)

- The Queue class implements the _IEnumerable_, _ICollection_, and _ICloneable_ interfaces.
- When you add an item in the list, it is called **[enqueue](https://www.geeksforgeeks.org/queue-enqueue-method-in-c-sharp/)**.
- when you remove an item, it is called **[dequeue](https://www.geeksforgeeks.org/queue-dequeue-method-in-c-sharp/)**.
- Queue accepts null as a valid value for reference types.
- As elements are added to a Queue, the capacity is automatically increased as required by reallocating the internal array.
- In Queue, you are allowed to store duplicate elements.
- The capacity of a Queue is the number of elements the Queue can hold.

### How to create the Queue?

Queue class has _four constructors_ which are used to create the queue which are as follows:

- **Queue():** This constructor is used to create an instance of Queue class which is empty and having the default initial capacity, and uses the default growth factor.
- **Queue(ICollection):** This constructor is used to create an instance of Queue class which contains elements copied from the specified collection, has the same initial capacity as the number of elements copied, and uses the default growth factor.
- **Queue(Int32):** This constructor is used to create an instance of Queue class which is empty and having specified initial capacity, and uses the default growth factor.
- **Queue(Int32, Single):** This constructor is used to create an instance of Queue class which is empty and having specified initial capacity, and uses the specified growth factor.

```csharp
public class GFG {
	static public void Main()
	{
		Queue my_queue = new Queue();

		my_queue.Enqueue("GFG");
		my_queue.Enqueue(1);
		my_queue.Enqueue(100);
		my_queue.Enqueue(null);
		my_queue.Enqueue(2.4);
		my_queue.Enqueue("Geeks123");

		foreach(var ele in my_queue)
		{
			Console.WriteLine(ele);
		}
	}
}
```

### Implementation example
```cs
using System.Text;

namespace Ds.Collections;
public class Fila
{
  private readonly LinkedList<string> nomes = new LinkedList<string>();

  public void Adiciona(string nome)
  {
    nomes.AddLast(nome);
  }

  public string Remove()
  {
    var nome = nomes.First();
    nomes.RemoveFirst();
    return nome;
  }

  public bool Vazia()
  {
    return nomes.Count() == 0;
  }

  public override string ToString()
  {
    StringBuilder sb = new StringBuilder("[");
    foreach (var item in nomes)
    {
        sb.Append(item);
        sb.Append(",");
    }
    sb.Append("]");
    return sb.ToString();
  }
}

```