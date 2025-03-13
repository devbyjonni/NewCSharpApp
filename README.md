# NewCSharpApp

Follow these steps to create a new **C#** project from scratch using **.NET** in **Visual Studio Code** on **Mac**.

---

## Install C# Extensions in VS Code

Install the following extensions from the VS Code Marketplace:

- **[C# Dev Kit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit)**

## 🚀 Quick Setup Script

```bash
cd ~/Developer
dotnet new console -o MyDotNetProject
cd MyDotNetProject
dotnet run
```

### Verify Installation

```bash
ls -l
dotnet --version
```

### (Optional) Force .NET 8 if Needed

If your project is not using .NET 8, manually set the target framework.

Open the project file:

```bash
code MyDotNetProject.csproj
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

---

✅ **All Set!**

