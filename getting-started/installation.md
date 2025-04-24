# Installation

Let's begin by installing the NuGet package. You can use Visual Studio's Nuget Package Manager, or one of the following commands:

## .NET CLI
```bash
dotnet add package Z.Blazor.Diagrams
```

## Package Manager
```powershell
Install-Package Z.Blazor.Diagrams
```

## Project Setup

Next, we'll setup the project and add the static resources for the library to work.

Add the following to your `wwwroot/index.html` or `Pages/_Host.cshtml`:

```html
<!DOCTYPE html>
<html>
<head>
    <!-- ... -->
    <link href="_content/Z.Blazor.Diagrams/style.min.css" rel="stylesheet" />
    <!-- If you want the default style -->
    <link href="_content/Z.Blazor.Diagrams/default.styles.min.css" rel="stylesheet" />
</head>
<body>
    <!-- ... -->
    <script src="_content/Z.Blazor.Diagrams/script.min.js"></script>
</body>
</html>
```

You're now ready to create your first diagram!