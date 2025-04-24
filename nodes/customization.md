# Nodes Customization

Customizing nodes in Blazor Diagrams is very easy!

## Creating a model

Most of the time, your nodes will hold more information than just a title, which is why we create a new model to encapsulate all the data and behavior we want. In a perfect world, you would have one node model for each behavior and or UI representation.

Let's assume that we want to create a new node that represents addition:

### AddTwoNumbersNode.cs
```csharp
using Blazor.Diagrams.Core.Geometry;
using Blazor.Diagrams.Core.Models;

namespace YourNamespace;

public class AddTwoNumbersNode : NodeModel
{
    public AddTwoNumbersNode(Point? position = null) : base(position)
    {
    }

    public double FirstNumber { get; set; }
    public double SecondNumber { get; set; }

    // Here, you can put whatever you want, such as a method that does the addition
}
```

## Creating a component

Let's create a UI component to control how the node looks like:

### AddTwoNumbersWidget.razor
```razor
@using Blazor.Diagrams.Components.Renderers;
@using YourNamespace;

<div>
    <h5 class="card-title">Add</h5>
    <input type="number" class="form-control" @bind-value="Node.FirstNumber" placeholder="Number 1" />
    <input type="number" class="form-control" @bind-value="Node.SecondNumber" placeholder="Number 2" />

    @foreach (var port in Node.Ports)
    {
        // In case you have any ports to show
        // IMPORTANT: You are always in charge of rendering ports
        <PortRenderer @key="port" Port="port" />
    }
</div>

@code {
    // This gets filled by the library
    [Parameter]
    public AddTwoNumbersNode Node { get; set; } = null!;
}
```

Let's also style our component!

### AddTwoNumbersWidget.razor.css
```css
div {
    width: 230px;
    outline: 1px solid black;
    padding: 20px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

div > h5 {
    font-weight: 600;
    text-transform: uppercase;
    margin-bottom: 10px;
}

div > input[type=number] {
    padding: 3px;
    border-radius: 3px;
    border: 1px solid black;
    margin-bottom: 8px;
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

    var node = Diagram.Nodes.Add(new AddTwoNumbersNode(new Point(80, 80)));
    node.AddPort(PortAlignment.Top);
    node.AddPort(PortAlignment.Bottom);
}
```