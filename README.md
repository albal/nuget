# TestNuGetPackage

A simple test NuGet package for demonstration purposes.

## Features

- Basic calculator operations (Add, Subtract, Multiply, Divide)
- Fully documented with XML comments
- Built with .NET 8.0

## Installation

```bash
dotnet add package TestNuGetPackage
```

## Usage

```csharp
using TestNuGetPackage;

var calculator = new Calculator();
int sum = calculator.Add(5, 3);        // Returns 8
int difference = calculator.Subtract(10, 4);  // Returns 6
int product = calculator.Multiply(6, 7);      // Returns 42
double quotient = calculator.Divide(10, 2);   // Returns 5.0
```

## License

MIT
