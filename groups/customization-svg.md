# SVG Groups Customization

Creating a custom SVG group is as easy as a HTML one, let's go! This tutorial is based on the SVG Nodes Customization one, make sure you look at that one first.

## Creating a model

Let's assume that we want to create a new group that represents a house for gingerbreads:

### GingerbreadHouse.cs
```csharp
namespace YourNamespace;

public class GingerbreadHouse : SvgGroupModel
{
    public GingerbreadHouse(IEnumerable<NodeModel> children, byte padding = 30, bool autoSize = true)
        : base(children, padding, autoSize)
    {
    }
}
```

## Creating a component

Let's create a UI component to control how the group looks like:

### GingerbreadHouseWidget.razor
```razor
@using YourNamspace;

@{
    var halfWidth = Group.Size!.Width / 2;
}

<path d="m @halfWidth -100 l @halfWidth 100 l -@Group.Size.Width 0 z" 
      fill="transparent" 
      stroke="black" 
      stroke-width="2" />

<rect width="@Group.Size!.Width" 
      height="@Group.Size!.Height" 
      fill="transparent" 
      stroke="black" 
      stroke-width="2">
</rect>

@* This is required and it's what renders the children *@
<GroupNodes Group="Group" />

@foreach (var port in Group.Ports)
{
    <PortRenderer Port="port" Class="group-port"></PortRenderer>
}

@code {
    // This gets filled by the library
    [Parameter]
    public GingerbreadHouse Group { get; set; } = null!;
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
    Diagram.RegisterComponent<GingerbreadHouse, GingerbreadHouseWidget>();

    var node1 = Diagram.Nodes.Add(new GingerbreadNode(new Point(160, 300)));
    node1.AddPort(PortAlignment.Left);
    node1.AddPort(PortAlignment.Right);

    var node2 = Diagram.Nodes.Add(new GingerbreadNode(new Point(410, 350)));
    node2.AddPort(PortAlignment.Left);
    node2.AddPort(PortAlignment.Right);

    var group = Diagram.Groups.Add(new GingerbreadHouse(new[] { node1, node2 }, padding: 50));
}
```