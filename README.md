# .NET Core Interview Questions And Answers

One step solution for all dotnet core interview questions

## Q1: What is .NET Core? ⭐

**Answer:**

The .NET Core platform is a new .NET stack that is optimized for open source development and agile delivery on NuGet.

.NET Core has two major components. It includes a small runtime that is built from the same codebase as the .NET Framework CLR. The .NET Core runtime includes the same GC and JIT (RyuJIT), but doesn’t include features like Application Domains or Code Access Security. The runtime is delivered via NuGet, as part of the ASP.NET Core package.

.NET Core also includes the base class libraries. These libraries are largely the same code as the .NET Framework class libraries, but have been factored (removal of dependencies) to enable to ship a smaller set of libraries. These libraries are shipped as `System.*` NuGet packages on NuGet.org.

🔗 **Source:** [stackoverflow.com](https://stackoverflow.com/questions/26908049/what-is-net-core)

## Q2: What is the difference between .NET Core and Mono? ⭐⭐

**Answer:**

To be simple:

- Mono is third party implementation of .Net Framework for Linux/Android/iOs
- .Net Core is Microsoft's own implementation for same.

🔗 **Source:** [stackoverflow.com](https://stackoverflow.com/questions/37738106/net-core-vs-mono)

## Q3: What are some characteristics of .NET Core? ⭐⭐

**Answer:**

- **Flexible deployment**: Can be included in your app or installed side-by-side user- or machine-wide.

- **Cross-platform**: Runs on Windows, macOS and Linux; can be ported to other OSes. The supported Operating Systems (OS), CPUs and application scenarios will grow over time, provided by Microsoft, other companies, and individuals.

- **Command-line tools**: All product scenarios can be exercised at the command-line.

- **Compatible**: .NET Core is compatible with .NET Framework, Xamarin and Mono, via the .NET Standard Library.

- **Open source**: The .NET Core platform is open source, using MIT and Apache 2 licenses. Documentation is licensed under CC-BY. .NET Core is a .NET Foundation project.

- **Supported by Microsoft**: .NET Core is supported by Microsoft, per .NET Core Support

🔗 **Source:** [stackoverflow.com](https://stackoverflow.com/questions/26908049/what-is-net-core)

## Q4: What is a .NET application domain? ⭐⭐

**Answer:**

It is an isolation layer provided by the .NET runtime. As such, App domains live with in a process (1 process can have many app domains) and have their own virtual address space.

App domains are useful because:

- They are less expensive than full processes
- They are multithreaded
- You can stop one without killing everything in the process
- Segregation of resources/config/etc
- Each app domain runs on its own security level

🔗 **Source:** [stackoverflow.com](https://stackoverflow.com/questions/1094478/what-is-a-net-application-domain)

## Q5: Name some CLR services? ⭐⭐

**Answer:**

**CLR services**

- Assembly Resolver
- Assembly Loader
- Type Checker
- COM marshalled
- Debug Manager
- Thread Support
- IL to Native compiler
- Exception Manager
- Garbage Collector

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/interview-question-on-net-framework-or-clr/)

## Q6: What is CLR? ⭐⭐

**Answer:**

The **CLR** stands for Common Language Runtime and it is an Execution Environment. It works as a layer between Operating Systems and the applications written in .NET languages that conforms to the Common Language Specification (CLS). The main function of Common Language Runtime (CLR) is to convert the Managed Code into native code and then execute the program.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/interview-question-on-net-framework-or-clr/)

## Q7: What is CTS? ⭐⭐

**Answer:**

The **Common Type System (CTS)** standardizes the data types of all programming languages using .NET under the umbrella of .NET to a common data type for easy and smooth communication among these .NET languages.

CTS is designed as a singly rooted object hierarchy with `System.Object` as the base type from which all other types are derived. CTS supports two different kinds of types:

1. **Value Types**: Contain the values that need to be stored directly on the stack or allocated inline in a structure. They can be built-in (standard primitive types), user-defined (defined in source code) or enumerations (sets of enumerated values that are represented by labels but stored as a numeric type).
2. **Reference Types**: Store a reference to the value‘s memory address and are allocated on the heap. Reference types can be any of the pointer types, interface types or self-describing types (arrays and class types such as user-defined classes, boxed value types and delegates).

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/interview-question-on-net-framework-or-clr/)

## Q8: What is Kestrel? ⭐⭐⭐

**Answer:**

## Q9: Is there a way to catch multiple exceptions at once and without code duplication? ⭐⭐⭐

**Questions Details:**

Consider:

```csharp
try
{
    WebId = new Guid(queryString["web"]);
}
catch (FormatException)
{
    WebId = Guid.Empty;
}
catch (OverflowException)
{
    WebId = Guid.Empty;
}
```

Is there a way to catch both exceptions and only call the `WebId = Guid.Empty` call once?

**Answer:**

```csharp
try
{
    WebId = new Guid(queryString["web"]);
}
catch (Exception ex)
{
    if (ex is FormatException || ex is OverflowException)
    {
        WebId = Guid.Empty;
        return;
    }
    throw ex;
}
```

## Q10: Explain the difference between Thread, Task and Parallel in .NET ⭐⭐⭐

**Answers:**

**Thread:**
A thread is the smallest unit of execution within an operating system. It represents a sequence of instructions that can be scheduled and executed independently. In C#, you can create and manage threads using the Thread class from the System.Threading namespace. Threads allow concurrent execution of code and are useful when you need to perform multiple tasks simultaneously.
**Real-time example:** Consider a chat application where you want to receive and send messages concurrently. You can use multiple threads to handle incoming and outgoing messages independently. Each thread can listen for incoming messages or send messages without blocking the main thread, allowing the chat application to handle multiple conversations simultaneously.

**Task:**
A task is a higher-level abstraction introduced in .NET that represents an asynchronous operation or a unit of work. It provides a simplified programming model for concurrent and asynchronous programming. Tasks can run concurrently on different threads, and they allow you to perform operations without blocking the main thread and waiting for the result.
**Real-time example:** Suppose you have a web application that needs to perform multiple database queries simultaneously. Instead of blocking the main thread while waiting for each query to complete, you can create tasks for each query and let them execute concurrently. Once all tasks complete, you can process the results asynchronously, improving the responsiveness of your application.

**Parallel:**
Parallel programming is a technique that involves breaking down a problem into smaller subtasks and executing them concurrently. The Parallel class in C# provides constructs for parallel programming, such as parallel loops and parallel execution of operations on collections.
**Real-time example:** Consider a data processing application that needs to perform a computationally intensive operation on a large collection of data. By using the Parallel.ForEach method, you can distribute the workload across multiple threads and process the data in parallel. This can significantly improve the overall performance of the application by utilizing the available CPU cores effectively.

In summary, threads are the fundamental units of execution, tasks provide a higher-level abstraction for asynchronous operations, and parallel programming allows you to execute tasks concurrently to improve performance. Depending on your requirements, you can choose the appropriate approach to achieve concurrency and optimize the execution of your application.

## Q11: What is FCL? ⭐⭐⭐

**Answers:**

## Q12: What's is BCL? ⭐⭐⭐

**Answers:**

## Q13: What is the difference between .NET Standard and PCL (Portable Class Libraries)? ⭐⭐⭐

**Answers:**

## Q14: What is the difference between Class Library (.NET Standard) and Class Library (.NET Core)? ⭐⭐⭐

**Answers:**

## Q15: When should we use .NET Core and .NET Standard Class Library project types? ⭐⭐⭐

**Answers:**

## Q16: What is the difference between .NET Framework/Core and .NET Standard Class Library project types? ⭐⭐⭐⭐

**Answers:**

## Q17: What's the difference between RyuJIT and Roslyn? ⭐⭐⭐⭐

**Answers:**

## Q18: Explain how does Asynchronous tasks (Async/Await) work in .NET? ⭐⭐⭐⭐

**Questions Details:**

Consider:

```csharp
private async Task<bool> TestFunction()
{
  var x = await DoesSomethingExists();
  var y = await DoesSomethingElseExists();
  return y;
}
```

Does the second `await` statement get executed right away or after the first `await` returns?

**Answers:**

## Q19: What are benefits of using JIT? ⭐⭐⭐⭐

**Answers:**

## Q20: Why does .NET use a JIT compiler instead of just compiling the code once on the target machine? ⭐⭐⭐⭐

**Answers:**

## Q21: What is the difference between CIL and MSIL (IL)? ⭐⭐⭐⭐

**Answers:**

## Q22: What is the difference between AppDomain, Assembly, Process, and a Thread? ⭐⭐⭐⭐

**Answers:**

## Q23: Why does .NET Standard library exist? ⭐⭐⭐⭐

**Answers:**

## Q24: Explain Finalize vs Dispose usage? ⭐⭐⭐⭐⭐

**Answers:**

## Q25: What is the difference between Node.js async model and async/await in .NET? ⭐⭐⭐⭐⭐

**Answers:**
