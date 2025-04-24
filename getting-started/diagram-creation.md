# Diagram Creation

You've installed the library, now let's create a diagram! Blazor.Diagrams is very code/oop oriented at the moment, which means all the diagram information needs to be given to it using code.

## Creating a Diagram

First, we'll start by creating a `BlazorDiagram`, which holds all the data of a diagram, as well as its behaviors. Create a new component and initialize a new diagram:

### MyDiagram.razor.cs
```csharp
using Blazor.Diagrams;

namespace MyNamespace;

public partial class MyDiagram
{
    private BlazorDiagram Diagram { get; set; } = null!;

    protected override void OnInitialized()
    {
        Diagram = new BlazorDiagram();
    }
}
```

## Changing Options

### MyDiagram.razor.cs
```csharp
using Blazor.Diagrams;
using Blazor.Diagrams.Core.PathGenerators;
using Blazor.Diagrams.Core.Routers;
using Blazor.Diagrams.Options;

namespace Site.Components.Documentation;

public partial class MyDiagram
{
    private BlazorDiagram Diagram { get; set; } = null!;

    protected override void OnInitialized()
    {
        var options = new BlazorDiagramOptions
        {
            AllowMultiSelection = true,
            Zoom = { Enabled = false },
            Links = {
                DefaultRouter = new NormalRouter(),
                DefaultPathGenerator = new SmoothPathGenerator()
            },
        };
        Diagram = new BlazorDiagram(options);
    }
}
```

## Adding Nodes

Continuing on our initialization code before, let's create two nodes:

### MyDiagram.razor.cs
```csharp
var firstNode = Diagram.Nodes.Add(new NodeModel(position: new Point(50, 50)) { Title = "Node 1" });
var secondNode = Diagram.Nodes.Add(new NodeModel(position: new Point(200, 100)) { Title = "Node 2" });

var leftPort = secondNode.AddPort(PortAlignment.Left);
var rightPort = secondNode.AddPort(PortAlignment.Right);
```

As you can see, we give the nodes a position and a title, as well as 2 ports for the second node.

## Adding a Link

In Blazor.Diagrams, links are created between 2 anchors (input and output). The library comes with a few out of the box anchors, we'll be using two of them to show how a link can be created from a node to a port.

### MyDiagram.razor.cs
```csharp
// The connection point will be the intersection of
// a line going from the target to the center of the source
var sourceAnchor = new ShapeIntersectionAnchor(firstNode);

// The connection point will be the port's position
var targetAnchor = new SinglePortAnchor(leftPort);

var link = Diagram.Links.Add(new LinkModel(sourceAnchor, targetAnchor));
```

You now have a diagram containing 2 nodes, 2 ports and one link.