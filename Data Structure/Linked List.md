A linked list is a linear data structure in which elements are not stored at contiguous memory locations. The elements in a linked list are linked using pointers as shown in the below image:
![https://media.geeksforgeeks.org/wp-content/uploads/20220712172013/Singlelinkedlist.png](https://media.geeksforgeeks.org/wp-content/uploads/20220712172013/Singlelinkedlist.png)

### **Characteristics of a Linked list:**

A linked list has various characteristics which are as follows:

- A linked list uses extra memory to store links.
- During the initialization of the linked list, there is no need to know the size of the elements.
- Linked lists are used to implement stacks, queues, graphs, etc.
- The first node of the linked list is called the Head.
- The next pointer of the last node always points to NULL.
- In a linked list, insertion and deletion are possible easily.
- Each node of the linked list consists of a pointer/link which is the address of the next node.
- Linked lists can shrink or grow at any point in time easily.

### **Applications of the Linked list:**

Different applications of linked lists are as follows:

- Linked lists are used to implement stacks, queues, graphs, etc.
- Linked lists are used to perform arithmetic operations on long integers.
- It is used for the representation of sparse matrices.
- It is used in the linked allocation of files.
- It helps in memory management.
- It is used in the representation of Polynomial Manipulation where each polynomial term represents a node in the linked list.
- Linked lists are used to display image containers. Users can visit past, current, and next images.
- They are used to store the history of the visited page.
- They are used to perform undo operations.
- Linked are used in software development where they indicate the correct syntax of a tag.
- Linked lists are used to display social media feeds.

```csharp
public class LinkedListExample  
{  
    public static void Main(string[] args)  
    {
        var names = new LinkedList<string>();  
        names.AddLast("Sonoo Jaiswal");  
        names.AddLast("Ankit");  
        names.AddLast("Peter");  
        names.AddLast("Irfan");  
        names.AddFirst("John");//added to first index  
        foreach (var name in names)  
        {  
            Console.WriteLine(name);  
        }  
    }  
}
```

## Implementation of LinkedList in [[CSHARP|C#]]
```cs
public class ListaLigada
{
  private Celula? primeira = null;
  private Celula? ultima = null;
  private int totalDeElementos = 0;

  public void AdicionaNoComeco(Object elemento) { 
    if(totalDeElementos == 0){
      Celula nova = new Celula(elemento);
      this.primeira = nova;
      this.ultima = nova;
    } else {
      Celula nova = new Celula(elemento, this.primeira);
      this.primeira!.Anterior = nova;
      this.primeira = nova;
    }
    this.totalDeElementos++;
  }

  public void Adiciona(Object elemento) { 
    if (this.totalDeElementos == 0) {
      this.AdicionaNoComeco(elemento);
    } else {
      Celula nova = new Celula(elemento);
      this.ultima!.Proximo = nova;
      nova.Anterior = this.ultima;
      this.ultima = nova;
      this.totalDeElementos++;
    }
  }

  private bool PosicaoOcupada(int posicao) { 
    return posicao >= 0 && posicao < this.totalDeElementos;
  }

  private Celula PegaCelula(int posicao) { 
    if (!this.PosicaoOcupada(posicao)) {
      throw new ArgumentException("Posição não existe");
    }

    Celula? atual = primeira;

    for (int i = 0; i < posicao; i++) {
      atual = atual!.Proximo;
    }

    return atual!;
  }

  public void Adiciona(int posicao, Object elemento) { 
    if (posicao == 0) {
      this.AdicionaNoComeco(elemento);
    } else if (posicao == this.totalDeElementos) {
      this.Adiciona(elemento);
    } else {
      Celula anterior = this.PegaCelula(posicao - 1);
      Celula proxima = anterior.Proximo!;

      Celula nova = new Celula(elemento, anterior.Proximo);
      nova.Anterior = anterior;
      anterior.Proximo = nova;
      proxima.Anterior = nova;
      this.totalDeElementos++;
    }
  }

  public Object Pega(int posicao) {
    return this.PegaCelula(posicao).Elemento;
  }

  public void Remove(int posicao) {
    if (posicao == 0) {
      this.RemoveDoComeco();
    } else if (posicao == this.totalDeElementos - 1) {
      this.RemoveDoFim();
    } else {
      Celula anterior = this.PegaCelula(posicao - 1);
      Celula atual = anterior.Proximo!;
      Celula proxima = atual.Proximo!;

      anterior.Proximo = proxima;
      proxima.Anterior = anterior;

      this.totalDeElementos--;
    }
  }

  public void RemoveDoComeco() { 
    if (totalDeElementos == 0) {
      throw new ArgumentException("Lista vazia");
    }

    this.primeira = this.primeira!.Proximo;
    this.totalDeElementos--;

    if (this.totalDeElementos == 0) {
      this.ultima = null;
    }
  }

  public void RemoveDoFim() { 
    if (totalDeElementos == 1) {
      this.RemoveDoComeco();
    } else {
      Celula penultima = this.ultima!.Anterior!;
      penultima.Proximo = null;
      this.ultima = penultima;
      this.totalDeElementos--;
    }
  }

  public int Tamanho() {
    return this.totalDeElementos;
  }

  public bool Contem(Object elemento) {
    Celula? atual = this.primeira;

    while (atual != null) {
      if (atual.Elemento.Equals(elemento)) {
        return true;
      }

      atual = atual.Proximo;
    }

    return false;
  }

  public override string ToString() {
    if (this.totalDeElementos == 0) {
      return "[]";
    }

    Celula? atual = primeira;

    StringBuilder builder = new StringBuilder("[");

    // Percorrendo até o penúltimo elemento.
    for (int i = 0; i < this.totalDeElementos - 1; i++) {
      builder.Append(atual!.Elemento);
      builder.Append(", ");
      atual = atual.Proximo;
    }

    // último elemento
    builder.Append(atual!.Elemento);
    builder.Append("]");

    return builder.ToString();
  }
}
```

```cs
public class Celula
{
  public Object Elemento { get; }
  public Celula? Anterior { get; set; }
  public Celula? Proximo { get; set; }

  public Celula(Object elemento)
  {
    this.Elemento = elemento;
    this.Proximo = null;
  }
  public Celula(Object elemento, Celula? proximo)
  {
    this.Elemento = elemento;
    this.Proximo = proximo;
  }
}
```