# SVG Nodes Customization

Creating a custom SVG node is as easy as a HTML one, let's go!

## Creating a model

Let's assume that we want to create a new node that represents Gingerbread:

### GingerbreadNode.cs
```csharp
using Blazor.Diagrams.Core.Geometry;
using Blazor.Diagrams.Models;

namespace YourNamespace;

public class GingerbreadNode : SvgNodeModel
{
    public GingerbreadNode(Point? position = null) : base(position)
    {
    }
    // Here, you can put whatever you want
}
```

## Creating a component

Let's create a UI component to control how the node looks like:

### GingerbreadWidget.razor
```razor
@using Blazor.Diagrams.Components.Renderers;
@using Site.Models.Nodes;

<g class="gingerbread">
    <circle class="body" cx="60" cy="30" r="30" />
    <circle class="eye" cx="48" cy="25" r="3" />
    <circle class="eye" cx="72" cy="25" r="3" />
    <rect class="mouth" x="50" y="40" width="20" height="5" rx="2" />
    <line class="limb" x1="20" y1="70" x2="100" y2="70" />
    <line class="limb" x1="35" y1="130" x2="60" y2="65" />
    <line class="limb" x1="85" y1="130" x2="60" y2="65" />
    <circle class="button" cx="60" cy="70" r="5" />
    <circle class="button" cx="60" cy="90" r="5" />

    <PortRenderer @key="'l'" Port="Node.GetPort(PortAlignment.Left)">
        <circle class="hand" cx="20" cy="70" r="17.5" />
    </PortRenderer>

    <PortRenderer @key="'r'" Port="Node.GetPort(PortAlignment.Right)">
        <circle class="hand" cx="100" cy="70" r="17.5" />
    </PortRenderer>
</g>

@code {
    // This gets filled by the library
    [Parameter]
    public GingerbreadNode Node { get; set; } = null!;
}
```

Let's also style our component!

### GingerbreadWidget.razor.css
```css
.gingerbread .body {
    fill: #cd803d;
}

.gingerbread .eye {
    fill: white;
}

.gingerbread .mouth {
    fill: none;
    stroke: white;
    stroke-width: 2px;
}

.gingerbread .limb {
    stroke: #cd803d;
    stroke-width: 35px;
    stroke-linecap: round;
}

.gingerbread .hand {
    fill: #cd803d;
}

.gingerbread .hand:hover {
    fill: #75441a;
}
```

## Displaying

All we have to do now is register our new creation!

```csharp
private BlazorDiagram Diagram { get; set; } = new();

protected override void OnInitialized()
{
    base.OnInitialized();
    Diagram.RegisterComponent<GingerbreadNode, GingerbreadWidget>();

    var node = Diagram.Nodes.Add(new GingerbreadNode(new Point(80, 80)));
    node.AddPort(PortAlignment.Left);
    node.AddPort(PortAlignment.Right);
}
```

Grabbing his hands will create a link!