# Albal.TestNuGetPackage

[![Build and Publish](https://github.com/albal/nuget/actions/workflows/nuget-publish.yml/badge.svg)](https://github.com/albal/nuget/actions/workflows/nuget-publish.yml)
[![NuGet](https://img.shields.io/nuget/v/Albal.TestNuGetPackage.svg)](https://www.nuget.org/packages/Albal.TestNuGetPackage/)
[![NuGet Downloads](https://img.shields.io/nuget/dt/Albal.TestNuGetPackage.svg)](https://www.nuget.org/packages/Albal.TestNuGetPackage/)

A test NuGet package demonstrating automated package publishing with GitHub Actions.

## Features

- 🧮 Basic calculator operations (Add, Subtract, Multiply, Divide)
- 📚 Fully documented with XML comments
- 🏗️ Built with .NET 6.0
- 🤖 Automated CI/CD with GitHub Actions
- 📦 Published to both NuGet.org and GitHub Packages

## Installation

### From NuGet.org
```bash
dotnet add package Albal.TestNuGetPackage
```

### From GitHub Packages
```bash
dotnet add package Albal.TestNuGetPackage --source https://nuget.pkg.github.com/albal/index.json
```

## Usage

```csharp
using TestNuGetPackage;

var calculator = new Calculator();

// Basic operations
int sum = calculator.Add(5, 3);              // Returns 8
int difference = calculator.Subtract(10, 4); // Returns 6
int product = calculator.Multiply(6, 7);     // Returns 42
double quotient = calculator.Divide(10, 2);  // Returns 5.0
```

## GitHub Actions Workflow

This package is automatically built and published using GitHub Actions:

- **Build**: Runs on every push and pull request to `main`
- **Publish**: Automatically publishes to NuGet.org and GitHub Packages when a version tag (e.g., `v1.0.3`) is pushed

### Workflow Features
- ✅ Restore dependencies
- ✅ Build project
- ✅ Create NuGet package
- ✅ Upload artifact
- ✅ Publish to NuGet.org (on version tags)
- ✅ Publish to GitHub Packages (on version tags)

## Development

### Build locally
```bash
dotnet build TestNuGetPackage/TestNuGetPackage.csproj --configuration Release
```

### Create package locally
```bash
dotnet pack TestNuGetPackage/TestNuGetPackage.csproj --configuration Release --output ./nupkg
```

### Create a new release
```bash
# Update version in TestNuGetPackage.csproj
git add TestNuGetPackage/TestNuGetPackage.csproj
git commit -m "Bump version to x.y.z"
git push

# Tag and push
git tag vx.y.z
git push origin vx.y.z
```

## License

MIT
