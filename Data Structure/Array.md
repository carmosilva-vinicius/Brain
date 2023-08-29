Arrays are [[Data Structure#Linear|Linear]] data structure, defined as the collection of similar types of data items stored at contiguous memory locations. It is one of the simplest data structures where each data element can be randomly accessed by using its index number.

- Each element in an array is of the same data type and carries the same size that is 4 bytes.
- Elements in the array are stored at contiguous memory locations from which the first element is stored at the smallest memory location.
- Elements of the array can be randomly accessed since we can calculate the address of each element of the array with the given base address and the size of the data element.

### Why are arrays required?

- Sorting and searching a value in an array is easier.
- Arrays are best to process multiple values quickly and easily.
- **Arrays are good for storing multiple values in a single variable -** In computer programming, most cases require storing a large number of data of a similar type. To store such an amount of data, we need to define a large number of variables. It would be very difficult to remember the names of all the variables while writing the programs. Instead of naming all the variables with a different name, it is better to define an array and store all the elements into it.

Example in [[CSHARP#Array|C#]]
```csharp
//< Data Type > [ ] < Name_Array >
//type [ ] < Name_Array > = new < datatype > [size];

int[] x;  // can store int values
string[] s; // can store string values
double[] d; // can store double values
Student[] stud1; // can store instances of Student class which is custom
```

## Manipulating arrays
### Adding algorithms
We can consider to use this [[Algorithms|algorithm]] to append new object to the end of an array:
```csharp
private Obj[] objects = new Obj[100];

public void Add(Obj obj){
	for (int i = 0; i < objects.Length; i++)
	{
	  if (objects[i] == null)
	  {
		objects[i] = obj;
		break;
	  }
	}
}
```
But this has a [[Algorithms#O(n)|O(n)]] complexity, which means that the number of operation will increase with the size of the array. In this case, the loop for will repeat following the amount of data in the array and it may not be good.
We could solve it including a var that store the current amount of data in the array. This information will allow to know in which position the new data should be appending, without search for it, will be a constant time algorithm. As bonus it also allows to implement the method to get the size off the array easily: 
```csharp
private Obj[] objects = new Obj[100];
private int amountOfObj = 0;

public void Add(Obj obj){
	objects[amountOfObj] = obj;
	amountOfObj++;
}

public int Size(){
	return amountOfObj;
}
```
