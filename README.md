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

# Step 1: Create the main project folder (MainApp)
mkdir MainApp
cd MainApp

# Step 2: Create the solution file for the project
dotnet new sln -n MainApp

# Step 3: Create the main app project in the 'src' folder
mkdir src
cd src
dotnet new console -o MainApp

# Step 4: Create the test project in the 'tests' folder
cd ..
mkdir tests
cd tests
dotnet new xunit -n MainApp.Tests

# Step 5: Add the reference from the test project to the main app project
cd ..
dotnet add tests/MainApp.Tests/MainApp.Tests.csproj reference src/MainApp/MainApp.csproj

# Step 6: Add both projects to the solution
dotnet sln MainApp.sln add src/MainApp/MainApp.csproj
dotnet sln MainApp.sln add tests/MainApp.Tests/MainApp.Tests.csproj

# Step 7: Update Program.cs to make the Program class public and add a namespace
cd src/MainApp
echo 'using System;

namespace MainApp
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Your C# App is Running! 🚀");
        }
    }
}' > Program.cs

# Step 8: Add a simple unit test to check the output of Program.cs
cd ../../tests/MainApp.Tests
echo 'using Xunit;
using MainApp; // Import the namespace of the MainApp class

public class UnitTestMainApp
{
    [Fact]
    public void Program_Output_ShouldBeCorrect()
    {
        // Arrange
        var expectedOutput = "Your C# App is Running! 🚀";

        using (var sw = new System.IO.StringWriter())
        {
            Console.SetOut(sw); // Redirect Console output to StringWriter

            // Act
            Program.Main(); // Run the Main method in Program.cs

            // Assert
            var result = sw.ToString().Trim(); // Capture the output and trim any extra newlines
            Assert.Equal(expectedOutput, result); // Ensure the output matches
        }
    }
}
' > ProgramTests.cs

# Step 9: Rebuild the solution (ensure the projects are correctly linked)
cd ~/Developer/MainApp
dotnet build

# Step 10: Run the tests
cd tests/MainApp.Tests
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

