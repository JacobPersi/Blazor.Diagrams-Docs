# Blazor Diagrams Quick Reference

## Basic Setup

```csharp
// Add services
builder.Services.AddBlazorDiagram();

// Initialize diagram
private BlazorDiagram Diagram { get; set; } = new();

// Basic display
<CascadingValue Value="@Diagram" IsFixed="true">
    <DiagramCanvas>
        <!-- Optional Widgets -->
    </DiagramCanvas>
</CascadingValue>
```

## Nodes

```csharp
// Add basic node
var node = Diagram.Nodes.Add(new NodeModel(new Point(100, 100)));

// Add SVG node
var svgNode = Diagram.Nodes.Add(new SvgNodeModel(new Point(100, 100)));

// Custom HTML node
public class CustomNode : NodeModel 
{
    public string Title { get; set; }
    public CustomNode(Point position) : base(position) { }
}

// Register custom node component
Diagram.RegisterComponent<CustomNode, CustomNodeWidget>();
```

## Ports

```csharp
// Add port to node
var port = node.AddPort(PortAlignment.Bottom);

// Custom port
public class CustomPort : PortModel 
{
    public CustomPort(NodeModel parent, PortAlignment alignment) 
        : base(parent, alignment) { }
}

// Add custom port
node.AddPort(new CustomPort(node, PortAlignment.Top));
```

## Links

```csharp
// Basic link between nodes
var link = Diagram.Links.Add(new LinkModel(node1, node2));

// Link between ports
var link = Diagram.Links.Add(new LinkModel(port1, port2));

// Configure link appearance
link.SourceMarker = LinkMarker.Arrow;
link.TargetMarker = LinkMarker.Circle;
link.Router = new OrthogonalRouter();
link.PathGenerator = new SmoothPathGenerator();
```

## Groups

```csharp
// Create group with nodes
var group = Diagram.Groups.Add(new GroupModel(new[] { node1, node2 }));

// SVG group
var svgGroup = Diagram.Groups.Add(new SvgGroupModel(new[] { node1, node2 }));

// Configure group factory
Diagram.Options.Groups.Factory = (diagram, children) => new SvgGroupModel(children);
```

## Widgets

```razor
<DiagramCanvas>
    <Widgets>
        <!-- Navigator (minimap) -->
        <NavigatorWidget 
            Width="200" 
            Height="120" 
            Class="border border-black bg-white absolute" 
            Style="bottom: 15px; right: 15px;" />

        <!-- Grid -->
        <GridWidget 
            Size="30" 
            Mode="GridMode.Line" 
            BackgroundColor="white" />

        <!-- Selection Box -->
        <SelectionBoxWidget />
    </Widgets>
</DiagramCanvas>
```

## Controls

```csharp
// Add controls to model
var controls = Diagram.Controls.AddFor(node);
controls.Add(new BoundaryControl());
controls.Add(new RemoveControl(0.5, 0));  // top center
controls.Add(new ArrowHeadControl(source: true));

// Show/Hide controls
controls.Show();
controls.Hide();
```

## Common Options

```csharp
Diagram.Options.Links.DefaultRouter = new OrthogonalRouter();
Diagram.Options.Links.DefaultPathGenerator = new SmoothPathGenerator();
Diagram.Options.Groups.Enabled = true;
Diagram.Options.Constraints = DiagramConstraints.Default | DiagramConstraints.Snapable;

// Layer ordering
Diagram.Options.LinksLayerOrder = 1;
Diagram.Options.NodesLayerOrder = 0;
```

## Event Handling

```csharp
// Node events
node.Changed += (s, e) => Console.WriteLine("Node changed");
node.Selected += (s, e) => Console.WriteLine("Node selected");

// Link events
link.SourceChanged += (s, e) => Console.WriteLine("Source changed");
link.VerticesChanged += (s, e) => Console.WriteLine("Vertices changed");

// Diagram events
Diagram.SelectionChanged += (s, e) => Console.WriteLine("Selection changed");
```

## Position Providers

```csharp
// Bounds based (x,y between 0-1)
new BoundsBasedPositionProvider(0.5, 0);     // top center
new BoundsBasedPositionProvider(1, 0.5);     // right center
new BoundsBasedPositionProvider(0.5, 1);     // bottom center
new BoundsBasedPositionProvider(0, 0.5);     // left center

// Shape angle (in degrees)
new ShapeAnglePositionProvider(45);          // 45 degrees

// Link path
new LinkPathPositionProvider(0.5);           // middle of link
```

## Keyboard Shortcuts (Default)

- `Delete`: Delete selected items
- `Ctrl+C`: Copy selected items
- `Ctrl+V`: Paste copied items
- `Ctrl+Z`: Undo
- `Ctrl+Y`: Redo
- `Ctrl+G`: Group selected items
- `Ctrl+Shift+G`: Ungroup selected items
- `Ctrl+A`: Select all items