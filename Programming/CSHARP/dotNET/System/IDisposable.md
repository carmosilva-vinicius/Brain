Is an interface of [[System]] namespace that provides a mechanism to clean unmanaged resources. Garbage collector is responsible for release managed objects is no longer used, to free memory allocation. 


`IDisposable` is most commonly encountered with library classes that wrap operating system (unmanaged) resources such as [`System.IO.Stream`](https://docs.microsoft.com/en-us/dotnet/api/system.io.stream) and [`System.IO.TextReader`](https://docs.microsoft.com/en-us/dotnet/api/system.io.textreader). (`Stream`s and `TextReader`s are covered in other exercises). [source](https://exercism.org/tracks/csharp/concepts/resource-cleanup)
```cs
public class TextHandler : IDispoable 
{ 
	private TextReader reader = new TextReader(...);
	
	public void Dispose() 
	{ 
		reader.Dispose(); 
	} 
}
```

If a class you are using implements the `IDispoable` interface then you must ensure that `Dispose()` is called (by use of [`catch` and `finally`](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/try-catch-finally) clauses) when the instance is no longer required. If a class has a member which implements `IDisposable` then it may well need to implement `IDisposable` itself so that `Dispose()` can be called to dispose of the `IDisposble`-implementing member.
```cs
public class Activity : IDisposable {
	private MyResource myResource; 
	
	public Activity() 
	{ 
		myResource = new MyResource(); 
	}
	
	public void Perform() 
	{
		try 
		{
			myResource.BeUseful(); 
		}
		catch (Exception) 
		{
			myResource.Dispose(); 
		} 
	} 
	
	public void Dispose() 
	{
		myResource.Dispose(); 
	} 
}
```

# using statement
This ensures the correct management of disposable objects lifetime in a single block of code:
```csharp
using (var file = new File("my_secrets"))
{
    file.WriteSecret("xxxxxxx");
}
```
In the above example the file system resources associated with `file` will be released back to the operating system when the `using` block is exited.

C# 8 introduces a refinement to the pattern. A using statement can placed at the beginning of a block:
```csharp
using var drawingResource = some_provided_or_new_object;
try
{
    drawingResource.DrawSomething();
}
catch (Exception)
{
    throw;
}
```