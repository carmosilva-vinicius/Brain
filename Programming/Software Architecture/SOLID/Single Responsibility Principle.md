A class must have one reason for change, if there are many reasons, they should be moved to other classes. In other words, each class should focus on a single piece of functionality. By adhering to SRP, your code becomes easier to maintain, test, and extend.

## Example
Suppose we have an application for handling book-related operations. Initially, we have a single class called Book that contains methods for both storing book information and printing its details. This violates the SRP because the Book class has two responsibilities: managing book data and printing it.

```cs
public class Book
{
    public string Title { get; set; }
    public string Author { get; set; }

    public void SaveToDatabase()
    {
        // Code to save the book to the database
        Console.WriteLine("Saving book to database.");
    }

    public void PrintDetails()
    {
        // Code to print book details
        Console.WriteLine($"Title: {Title}, Author: {Author}");
    }
}
```

In this example, the `Book` class handles two responsibilities:

1. Storing book information (`Title`, `Author`)
2. Saving the book to a database (`SaveToDatabase`) and printing the book details (`PrintDetails`).

### Applying SRP

To apply the Single Responsibility Principle, we separate these responsibilities into different classes:

1. **`Book`**: Manages book data (only properties, without methods related to printing or database storage).
2. **`BookPrinter`**: Handles printing the book details.
3. **`BookRepository`**: Manages database operations for the book.

### Example With SRP
```cs
public class Book
{
    public string Title { get; set; }
    public string Author { get; set; }

    public Book(string title, string author)
    {
        Title = title;
        Author = author;
    }
}

public class BookPrinter
{
    public void Print(Book book)
    {
        Console.WriteLine($"Title: {book.Title}, Author: {book.Author}");
    }
}

public class BookRepository
{
    public void SaveToDatabase(Book book)
    {
        // Code to save the book to the database
        Console.WriteLine($"Saving '{book.Title}' by {book.Author} to the database.");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        var book = new Book("The Great Gatsby", "F. Scott Fitzgerald");
        
        var printer = new BookPrinter();
        printer.Print(book);
        
        var repository = new BookRepository();
        repository.SaveToDatabase(book);
    }
}
```
### Explanation

1. **`Book`** class is only responsible for holding book information.
2. **`BookPrinter`** class is responsible for printing the book details.
3. **`BookRepository`** class is responsible for database operations (e.g., saving the book).

By dividing the responsibilities, each class has a single reason to change:

- **Book**: If the structure of book information changes.
- **BookPrinter**: If the format or the way details are printed changes.
- **BookRepository**: If the database or storage mechanism changes.

This separation of concerns makes the code more modular and easier to manage.