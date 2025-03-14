# NewCSharpApp

Follow these steps to create a new **C#** project from scratch using **.NET** in **Visual Studio Code** on **Mac**.

---

## Install C# Extensions in VS Code

Install the following extensions from the VS Code Marketplace:
- **[C# Dev Kit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit)**
(The C# extension and the .NET Install Tool will automatically be installed.)

## 🚀 Quick Setup Script
```bash
# Navigate to the Developer folder
cd ~/Developer

# Step 1: Create the main project folder (BankingApp)
mkdir BankingApp
cd BankingApp

# Step 2: Create the solution file
dotnet new sln -n BankingApp

# Step 3: Create the main app project in the 'src' folder
mkdir src
cd src
dotnet new console -o BankingApp

# Step 4: Create the test project in the 'tests' folder
cd ..
mkdir tests
cd tests
dotnet new xunit -n BankingApp.Tests

# Step 5: Add the reference from the test project to the main app project (from top-level folder)
cd ..
dotnet add tests/BankingApp.Tests/BankingApp.Tests.csproj reference src/BankingApp/BankingApp.csproj

# Step 6: Add both projects to the solution
dotnet sln BankingApp.sln add src/BankingApp/BankingApp.csproj
dotnet sln BankingApp.sln add tests/BankingApp.Tests/BankingApp.Tests.csproj

# Step 7: Add custom code to Program.cs in the main app
cd src/BankingApp
echo 'using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("New C# App Running! 🚀");
    }
}' > Program.cs

# Step 8: Rebuild the solution (ensure the projects are correctly linked)
cd ~/Developer/BankingApp
dotnet build

# Step 9: Run the tests
cd tests/BankingApp.Tests
dotnet test
```

Download the recommended .gitignore for C#/.NET projects
```bash
curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/main/VisualStudio.gitignore
```

### Verify Installation

```bash
ls -a
dotnet --version
dotnet run
```

### Initialize Git and commit the setup

```bash
git init
git add .
git commit -m "Initial commit with .NET .gitignore"
git log
git status
```

### (Optional) Force .NET 8 if Needed

If your project is not using .NET 8, manually set the target framework.

Open the project file:

```bash
code MyNewCSharpApp.csproj
```

Ensure the `<TargetFramework>` is set to .NET 8:

```xml
<TargetFramework>net8.0</TargetFramework>
```

Restore dependencies and re-run the project:

```bash
dotnet restore
dotnet run
```

### ⚠️ Force .NET 8 for Future Projects (If Needed)

If `dotnet --version` shows .NET 9, but you want to default to .NET 8, set it globally:

```bash
dotnet new globaljson --sdk-version 8.0.309
dotnet restore
dotnet run
```

Verify:

```bash
dotnet --version
```

Expected output:

```bash
8.0.309
```

Open the new project:
```bash
code .
```

Run the project:
```bash
dotnet run
```

### Commit the update:
```bash
git status
git add .
git commit -m "Update to .NET version 8.0.309"
git log
git status
```


---

✅ **All Set!**

