# Groups Customization

Customizing groups in Blazor Diagrams is very easy! This tutorial is based on the Nodes Customization one, make sure you look at that one first.

## Creating a model

Let's assume that we want to create a new group that represents a container of arithmetic operations:

### ArithmeticContainer.cs
```csharp
namespace YourNamespace;

public class ArithmeticContainer : GroupModel
{
    public ArithmeticContainer(IEnumerable<NodeModel> children, byte padding = 30, bool autoSize = true)
        : base(children, padding, autoSize)
    {
    }
}
```

## Creating a component

Let's create a UI component to control how the group looks like:

### ArithmeticContainerWidget.razor
```razor
@using Site.Models.Nodes;

<div class="arithmetic-container">
    <div class="title">
        @Group.Title
    </div>

    @* This is required and it's what renders the children *@
    <GroupNodes Group="Group" />

    @foreach (var port in Group.Ports)
    {
        <PortRenderer Port="port" Class="group-port"></PortRenderer>
    }
</div>

@code {
    // This gets filled by the library
    [Parameter]
    public ArithmeticContainer Group { get; set; } = null!;
}
```

Let's also style our component!

### ArithmeticContainerWidget.razor.css
```css
.arithmetic-container {
    width: 100%;
    height: 100%;
    border: 2px dashed black;
}

.arithmetic-container .title {
    position: absolute;
    right: 0;
    padding: 8px;
    text-align: right;
    border-left: 2px dashed black;
    border-bottom: 2px dashed black;
}

::deep .diagram-port {
    position: absolute;
    width: 30px;
    height: 20px;
    background-color: black;
    left: 50%;
    transform: translate(-50%, -50%);
}

::deep .diagram-port.top {
    border-top-left-radius: 50%;
    border-top-right-radius: 50%;
    top: -10px;
}

::deep .diagram-port.bottom {
    border-bottom-left-radius: 50%;
    border-bottom-right-radius: 50%;
    bottom: -30px;
}
```

## Displaying

All we have to do now is register our new creation!

```csharp
private BlazorDiagram Diagram { get; set; } = new();

protected override void OnInitialized()
{
    base.OnInitialized();
    Diagram.RegisterComponent<AddTwoNumbersNode, AddTwoNumbersWidget>();
    Diagram.RegisterComponent<ArithmeticContainer, ArithmeticContainerWidget>();

    var node1 = Diagram.Nodes.Add(new AddTwoNumbersNode(new Point(120, 140)));
    node1.AddPort(PortAlignment.Top);
    node1.AddPort(PortAlignment.Bottom);

    var node2 = Diagram.Nodes.Add(new AddTwoNumbersNode(new Point(370, 340)));
    node2.AddPort(PortAlignment.Top);
    node2.AddPort(PortAlignment.Bottom);

    var group = Diagram.Groups.Add(new ArithmeticContainer(new[] { node1, node2 }, padding: 50));
    group.AddPort(PortAlignment.Top);
    group.AddPort(PortAlignment.Bottom);
    group.Title = "First Container";
}
```