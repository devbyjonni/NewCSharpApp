# NewCSharpApp

Follow these steps to create a new **C#** project from scratch using **.NET** in **Visual Studio Code** on **Mac**.

---

## Install C# Extensions in VS Code

Install the following extensions from the VS Code Marketplace:
- **[C# Dev Kit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit)**
(The C# extension and the .NET Install Tool will automatically be installed.)

## 🚀 Quick Setup Script
```bash
#!/bin/bash

# Define project names using best practices
SOLUTION_NAME="DotnetConsoleApp"          # Root solution name
CORE_PROJECT_NAME="DotnetConsoleApp"      # Console application folder
CORE_PROJECT_FILE="DotnetConsoleApp"      # Console application .csproj file
TEST_PROJECT_NAME="DotnetConsoleApp.Tests" # Test project folder
TEST_PROJECT_FILE="DotnetConsoleApp.Tests" # Test project .csproj file

FILE_NAME="Program"                       # Default main file name
TEST_FILE_NAME="ProgramTests"             # Default test file name


# Expected folder structure:
# /Developer
#     /DotnetConsoleApp
#         DotnetConsoleApp.sln
#         /DotnetConsoleApp
#             Program.cs
#             DotnetConsoleApp.csproj
#         /DotnetConsoleApp.Tests
#             ProgramTests.cs
#             DotnetConsoleApp.Tests.csproj


# Navigate to Developer folder
cd ~/Developer

# Step 1: Create the DotnetConsoleApp solution folder
mkdir $SOLUTION_NAME
cd $SOLUTION_NAME

# Step 2: Create the solution file
dotnet new sln -n $SOLUTION_NAME

# Step 3: Create the DotnetConsoleApp console application project
dotnet new console -o $CORE_PROJECT_NAME

# Step 4: Replace the default Program.cs with the correct namespace
echo 'using System;

namespace '"$SOLUTION_NAME"'
{
    public class '"$FILE_NAME"'
    {
        public static void Main()
        {
            Console.WriteLine("Dotnet Console App is Running! 🚀");
        }
    }
}
' > $CORE_PROJECT_NAME/$FILE_NAME.cs

# Step 5: Add the Core project to the solution
dotnet sln add $CORE_PROJECT_NAME/$CORE_PROJECT_FILE.csproj

# Step 6: Create the DotnetConsoleApp.Tests xUnit test project
dotnet new xunit -o $TEST_PROJECT_NAME

# Step 7: Remove default UnitTest1.cs
rm $TEST_PROJECT_NAME/UnitTest1.cs

# Step 8: Create ProgramTests.cs inside the test project with correct namespace
echo 'using Xunit;
using '"$SOLUTION_NAME"';
using System;

namespace '"$TEST_PROJECT_NAME"'
{
    public class '"$TEST_FILE_NAME"'
    {
        [Fact]
        public void Program_Output_ShouldBeCorrect()
        {
            // Arrange
            var expectedOutput = "Dotnet Console App is Running! 🚀";

            using (var sw = new System.IO.StringWriter())
            {
                Console.SetOut(sw); // Redirect Console output to StringWriter

                // Act
                '"$FILE_NAME"'.Main(); // Run the Main method

                // Assert
                var result = sw.ToString().Trim(); // Capture output and trim spaces
                Assert.Equal(expectedOutput, result); // Ensure the output matches
            }
        }
    }
}
' > $TEST_PROJECT_NAME/$TEST_FILE_NAME.cs

# Step 9: Add a reference from DotnetConsoleApp.Tests to DotnetConsoleApp
dotnet add $TEST_PROJECT_NAME/$TEST_PROJECT_FILE.csproj reference $CORE_PROJECT_NAME/$CORE_PROJECT_FILE.csproj

# Step 10: Add the test project to the solution
dotnet sln add $TEST_PROJECT_NAME/$TEST_PROJECT_FILE.csproj

# Step 11: Build the solution
dotnet build

# Step 12: Rename UnitTest1.cs to ProgramTests.cs (Just in case)
mv $TEST_PROJECT_NAME/UnitTest1.cs $TEST_PROJECT_NAME/$TEST_FILE_NAME.cs 2>/dev/null || true

# Step 13: Run the tests
cd $TEST_PROJECT_NAME
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

