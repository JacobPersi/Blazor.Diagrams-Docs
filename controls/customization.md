# Controls Customization

Customizing controls is done the same way as any other customization.

* For completely new controls, you create a model class and its accompanying widget.
* For existing controls, you simply register a new widget for them.

In this document, we will only talk about new controls.

## Simple Control

Let's say we want to show some information about a node when we hover on it:

### NodeInformationControl.cs
```csharp
public class NodeInformationControl : Control
{
    public override Point? GetPosition(Model model)
    {
        // We want the information to be under the node
        var node = (model as NodeModel)!;
        if (node.Size == null)
            return null;

        return node.Position.Add(0, node.Size!.Height + 10);
    }
}
```

### NodeInformationControlWidget.razor
```razor
@using Blazor.Diagrams.Core.Models.Base;
@using YourNamespace;

<div style="background-color: #eee; width: @(Node.Size!.Width)px; padding: 5px;">
    <div>Width: @Node.Size.Width</div>
    <div>Height: @Node.Size.Height</div>
    <div>Ports: @Node.Ports.Count</div>
    <div>Links: @(Node.Links.Count + Node.PortLinks.Count())</div>
</div>

@code {
    [Parameter]
    public NodeInformationControl Control { get; set; } = null!;

    [Parameter]
    public Model Model { get; set; } = null!;

    public NodeModel Node => (Model as NodeModel)!;
}
```

## Executable Control

Let's say we want to show an alert button (I'm out of ideas):

### AlertControl.cs
```csharp
public class AlertControl : ExecutableControl
{
    private readonly IJSRuntime _jSRuntime;

    public AlertControl(IJSRuntime jSRuntime)
    {
        _jSRuntime = jSRuntime;
    }

    public override Point? GetPosition(Model model)
    {
        // Fixed at top-right
        var node = (model as NodeModel)!;
        if (node.Size == null)
            return null;

        return node.Position.Add(node.Size.Width + 10, -10);
    }

    public override async ValueTask OnPointerDown(Diagram diagram, Model model, PointerEventArgs e)
    {
        await _jSRuntime.InvokeVoidAsync("alert", "Some Alert??");
    }
}
```

### AlertControl.Widget.razor
```razor
@using Blazor.Diagrams.Core.Models.Base;
@using YourNamespace;

<div class="rounded-full p-1 text-center text-white" style="background-color: red; width: 30px; height: 30px;">
    !
</div>

@code {
    [Parameter]
    public AlertControl Control { get; set; } = null!;

    [Parameter]
    public Model Model { get; set; } = null!;

    public NodeModel Node => (Model as NodeModel)!;
}
```