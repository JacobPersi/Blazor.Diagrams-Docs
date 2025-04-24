# Ports Customization

Unlike for other models, customization in this page refers to the model itself, not the UI. How the ports are represented in the UI is managed by the parent (node or group), no registration is needed.

## Creating a model

Let's assume that we want to create ports that either receive (In) or send (Out). The constraint is that In ports only link to Out ports, you can't link two ports with the same type:

```csharp
public class MyCustomPortModel : PortModel
{
    public bool In { get; set; }

    public MyCustomPortModel(NodeModel parent, bool @in, PortAlignment alignment = PortAlignment.Bottom, Point? position = null, Size? size = null)
        : base(parent, alignment, position, size)
    {
        In = @in;
    }

    public MyCustomPortModel(string id, NodeModel parent, bool @in, PortAlignment alignment = PortAlignment.Bottom, Point? position = null, Size? size = null)
        : base(id, parent, alignment, position, size)
    {
        In = @in;
    }

    public override bool CanAttachTo(ILinkable other)
    {
        if (!base.CanAttachTo(other)) // default constraints
            return false;

        if (other is not MyCustomPortModel otherPort)
            return false;

        // Only link Ins with Outs
        return In != otherPort.In;
    }
}
```

## Using the model

```csharp
var receiverPort = myNode.AddPort(new MyCustomPortModel(myNode, true, PortAlignment.Top));
var senderPort = myNode.AddPort(new MyCustomPortModel(myNode, false, PortAlignment.Top));
```