Stack is a linear data structure that follows a particular order in which the operations are performed. The order may be LIFO(Last In First Out) or FILO(First In Last Out). In other words, a _**stack can be defined as a container in which insertion and deletion can be done from the one end known as the top of the stack.**_

![https://media.geeksforgeeks.org/wp-content/cdn-uploads/20221219100314/stack.drawio2.png](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20221219100314/stack.drawio2.png)

**The following are some common operations implemented on the stack:**

- **push():** When we insert an element in a stack then the operation is known as a push. If the stack is full then the overflow condition occurs.
- **pop():** When we delete an element from the stack, the operation is known as a pop. If the stack is empty means that no element exists in the stack, this state is known as an underflow state.
- **isEmpty():** It determines whether the stack is empty or not.
- **isFull():** It determines whether the stack is full or not.'
- **peek():** It returns the element at the given position.
- **count():** It returns the total number of elements available in a stack.
- **change():** It changes the element at the given position.
- **display():** It prints all the elements available in the stack.

**In [[CSHARP|C#]] we have:**

![https://media.geeksforgeeks.org/wp-content/uploads/20190222181540/Untitled-Diagram9.jpg](https://media.geeksforgeeks.org/wp-content/uploads/20190222181540/Untitled-Diagram9.jpg)

### How to create a Stack?

Stack class has _three_ constructors which are used to create a stack which is as follows:

- **Stack():** This constructor is used to create an instance of the Stack class which is empty and having the default initial capacity.
- **Stack(ICollection):** This constructor is used to create an instance of the Stack class which contains elements copied from the specified collection, and has the same initial capacity as the number of elements copied.
- **Stack(Int32):** This constructor is used to create an instance of the Stack class which is empty and having specified initial capacity or the default initial capacity, whichever is greater.

```csharp

using System.Collections;
class GFG {
	static public void Main()
	{
		Stack my_stack = new Stack();

		my_stack.Push("Geeks");
		my_stack.Push("geeksforgeeks");
		my_stack.Push("geeks23");
		my_stack.Push("GeeksforGeeks");

		Console.WriteLine("Total elements present in"+
					" my_stack: {0}",my_stack.Count);												
		// Obtain the topmost element
		// of my_stack Using Pop method
		Console.WriteLine("Topmost element of my_stack"
						+ " is: {0}",my_stack.Pop());						
		Console.WriteLine("Total elements present in"+
					" my_stack: {0}", my_stack.Count);						
		// Obtain the topmost element
		// of my_stack Using Peek method
		Console.WriteLine("Topmost element of my_stack "+
							"is: {0}",my_stack.Peek());
		Console.WriteLine("Total elements present "+
				"in my_stack: {0}",my_stack.Count);						
	}
}
```

### Implementation example
```cs
using System.Text;

namespace Ds.Collections;

public class Pilha
{
  private readonly LinkedList<string> nomes = new LinkedList<string>();

  public void Insere(string nome)
  {
    nomes.AddLast(nome);
  }

  public string Remove()
  {
    var nome = nomes.Last();
    nomes.RemoveLast();
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