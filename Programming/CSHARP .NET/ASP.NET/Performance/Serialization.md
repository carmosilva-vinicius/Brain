Here are some approaches to serialize data using `System.Text.Json`, this is part of .NET [[CSHARP|C#]] framework that in general it presents better [[Performance and Optimization|performance]] than the popular Newtonsoft package. 

```csharp
// Example 1
Products = JsonSerializer.Deserialize<List<ProductModel>>(jsonContent,
	new JsonSerializerOptions(defaults:JsonSerializerDefaults.Web)); 

// Example 2
Products = await response.Content.ReadFromJsonAsync<List<ProductModel>>();  
```

The first example is similar with the use of Newtonsoft example:

```csharp
Products = JsonConvert.DeserializeObject<List<ProductModel>>(jsonContent)
```


1. `JsonSerializer.Deserialize<List<ProductModel>>(jsonContent, new JsonSerializerOptions(defaults:JsonSerializerDefaults.Web))`:
    - This code uses the `JsonSerializer.Deserialize` method from the `System.Text.Json` namespace.
    - It explicitly specifies the type to deserialize into (`List<ProductModel>`) and provides a `JsonSerializerOptions` object as the second argument.
    - The `JsonSerializerOptions` object is configured with the `JsonSerializerDefaults.Web` option, which applies default settings optimized for web scenarios.
    - This method is suitable for deserializing JSON data in a synchronous manner.
    - It is available in .NET 5 and later versions.
    - [learn.microsoft.com](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/how-to)

2. `response.Content.ReadFromJsonAsync<List<ProductModel>>()`:
    - This code uses the `ReadFromJsonAsync` method from the `System.Net.Http.Json` namespace.
    - It is an extension method provided by the `System.Net.Http.Json` package.
    - This method reads the HTTP content asynchronously and deserializes it into the specified type (`List<ProductModel>`).
    - It automatically uses the default JSON serializer settings.
    - This method is suitable for deserializing JSON data asynchronously, which is often preferred for network requests.
    - It is available in .NET 5 and later versions.
    - [learn.microsoft.com](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.json.httpcontentjsonextensions.readfromjsonasync?view=net-7.0)

In terms of performance, both methods are efficient and have similar performance characteristics. However, the second method (`ReadFromJsonAsync`) is designed for asynchronous operations and is more suitable for scenarios where you want to avoid blocking the main thread while waiting for the deserialization to complete. Asynchronous operations can improve the responsiveness of your application, especially when dealing with network requests.

Another option is to use **Source Generation**, a feature introduced in .NET 6 that allows the compiler to generate serialization and deserialization code at compile-time, resulting in improved performance compared to traditional reflection-based approaches.

```csharp
Products = JsonSerializer.Deserialize(jsonContent, SourceGenerationContext.Default.ListProductModel);

[JsonSourceGenerationOptions(PropertyNamingPolicy = JsonKnownNamingPolicy.CamelCase)]
[JsonSerializable(typeof(List<ProductModel>))]
public partial class SourceGenerationContext : JsonSerializerContext
{
}
```

1. `Products = JsonSerializer.Deserialize(jsonContent, SourceGenerationContext.Default.ListProductModel);`:
    - This code uses the `JsonSerializer.Deserialize` method from the `System.Text.Json` namespace to deserialize JSON content.
    - It deserializes the `jsonContent` into an object of type `List<ProductModel>`.
    - The second argument, `SourceGenerationContext.Default.ListProductModel`, represents the type of the object to deserialize into.
    - The `SourceGenerationContext.Default` provides a default instance of the `SourceGenerationContext` class, which is a subclass of `JsonSerializerContext`.
    - The `JsonSerializerContext` is a base class for customizing the serialization and deserialization behavior.
    - [github.com](https://docs.microsoft.com/en-us/dotnet/api/system.text.json.jsonserializer.deserialize?view=net-7.0)

2. `[JsonSourceGenerationOptions(PropertyNamingPolicy = JsonKnownNamingPolicy.CamelCase)]`:
    - This attribute is applied to the `SourceGenerationContext` class.
    - It specifies the `PropertyNamingPolicy` to use during source generation.
    - In this case, the `JsonKnownNamingPolicy.CamelCase` is used, which applies camel case naming convention to the properties during serialization and deserialization.
    - This ensures that the property names in the JSON match the property names in the `ProductModel` class, following the camel case convention.
    - [devblogs.microsoft.com](https://docs.microsoft.com/en-us/dotnet/api/system.text.json.serialization.jsonsourcegenerationoptions.propertynamingpolicy?view=net-7.0)

3. `[JsonSerializable(typeof(List<ProductModel>))]`:
    - This attribute is applied to the `SourceGenerationContext` class.
    - It indicates that the `SourceGenerationContext` is serializable for the specified type, `List<ProductModel>`.
    - This attribute is used during source generation and provides information to the source generator about the types that should be generated.
    - It helps generate efficient serialization and deserialization code for the specified type.
    - [learn.microsoft.com](https://docs.microsoft.com/en-us/dotnet/api/system.text.json.serialization.jsonserializableattribute?view=net-7.0)