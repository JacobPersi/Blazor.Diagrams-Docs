# Blazor.Diagrams Usage Guide

## Setup

1. Install NuGet package:
```
dotnet add package Z.Blazor.Diagrams
```

2. Add required CSS and JS to `index.html` or `_Host.cshtml`:
```html
<link href="_content/Z.Blazor.Diagrams/style.min.css" rel="stylesheet" />
<script src="_content/Z.Blazor.Diagrams/script.min.js"></script>
```

3. Add using statements in `_Imports.razor`:
```csharp
@using Blazor.Diagrams
@using Blazor.Diagrams.Components
@using Blazor.Diagrams.Components.Widgets
```

## Core Components

### Component Structure
```razor
@page "/diagram"
@inherits DiagramComponent

<div class="diagram-container" style="width: 100%; height: 100vh;">
    <CascadingValue Value="Diagram">
        <DiagramCanvas>
            <Widgets>
                <NavigatorWidget Width="200" Height="150" />
                <SelectionBoxWidget />
            </Widgets>
        </DiagramCanvas>
    </CascadingValue>
</div>

@code {
    private BlazorDiagram Diagram { get; set; }

    protected override void OnInitialized()
    {
        Diagram = new BlazorDiagram();
        InitializeDiagram();
    }

    private void InitializeDiagram()
    {
        var node1 = new NodeModel(new Point(100, 100));
        var node2 = new NodeModel(new Point(300, 300));
        node1.AddPort(PortAlignment.Right);
        node2.AddPort(PortAlignment.Left);
        
        Diagram.Nodes.Add(new[] { node1, node2 });
        Diagram.Links.Add(new LinkModel(node1.GetPort(PortAlignment.Right), 
                                      node2.GetPort(PortAlignment.Left)));
    }
}

## Node Operations

### Create Node
```csharp
var node = new NodeModel(new Point(x, y));
diagram.Nodes.Add(node);
```

### Add Ports
```csharp
node.AddPort(PortAlignment.Top);
node.AddPort(PortAlignment.Right);
node.AddPort(PortAlignment.Bottom);
node.AddPort(PortAlignment.Left);
```

### Create Links
```csharp
var link = new LinkModel(sourceNode.GetPort(PortAlignment.Right), targetNode.GetPort(PortAlignment.Left));
diagram.Links.Add(link);
```

## Customization

### Custom Node Implementation
```csharp
// CustomNode.cs
public class CustomNode : NodeModel
{
    public string Title { get; set; }
    public CustomNode(Point position) : base(position) { }
}

// CustomNodeWidget.razor
@inherits NodeWidget<CustomNode>

<div class="custom-node" style="background: white; border: 2px solid black; padding: 10px;">
    <div>@Node.Title</div>
    @foreach (var port in Node.Ports)
    {
        <PortWidget Port="port" />
    }
</div>

@code {
    protected override void OnInitialized()
    {
        Node.AddPort(PortAlignment.Top);
        Node.AddPort(PortAlignment.Bottom);
    }
}

// Registration in parent component
diagram.RegisterComponent<CustomNode, CustomNodeWidget>();
```

### Custom Link Implementation
```csharp
// CustomLink.cs
public class CustomLink : LinkModel
{
    public string LinkType { get; set; }
    public CustomLink(IPort source, IPort target) : base(source, target) { }
}

// CustomLinkWidget.razor
@inherits LinkWidget<CustomLink>

<g class="@Link.LinkType">
    <path d="@Link.GetPathDefinition()" 
          stroke="@(Link.Selected ? "red" : "black")" 
          stroke-width="2" 
          fill="none" />
    @if (Link.Labels.Any())
    {
        @foreach (var label in Link.Labels)
        {
            <LinkLabelWidget Label="label" />
        }
    }
</g>

@code {
    protected override void OnInitialized()
    {
        Link.Router = new OrthogonalRouter();
        Link.PathGenerator = new StraightPathGenerator();
    }
}

// Registration in parent component
diagram.RegisterComponent<CustomLink, CustomLinkWidget>();
```

### Link Usage
```razor
@code {
    private void CreateCustomLink(IPort source, IPort target)
    {
        var link = new CustomLink(source, target)
        {
            LinkType = "data-flow",
            SourceMarker = LinkMarker.Arrow,
            TargetMarker = LinkMarker.Arrow
        };
        link.Labels.Add(new LinkLabelModel("Data"));
        Diagram.Links.Add(link);
    }
}
```

## Configuration Options

### Diagram Options
```csharp
diagram.Options.AllowPanning = true;
diagram.Options.Zoom.Enabled = true;
diagram.Options.Virtualization.Enabled = true;
diagram.Options.GridSnapEnabled = true;
diagram.Options.GridSize = 20;
```

### Event Handling
```razor
@code {
    protected override void OnInitialized()
    {
        Diagram = new BlazorDiagram();
        
        Diagram.SelectionChanged += OnSelectionChanged;
        Diagram.NodeAdded += OnNodeAdded;
        Diagram.LinkAdded += OnLinkAdded;
        Diagram.PointerDown += OnPointerDown;
    }

    private void OnSelectionChanged(SelectionChangedEventArgs args)
    {
        SelectedNodes = args.Selected.OfType<NodeModel>().ToList();
        StateHasChanged();
    }

    private void OnNodeAdded(NodeModel node)
    {
        node.Changed += (s, e) => 
        {
            // Handle node property changes
            StateHasChanged();
        };
    }

    private void OnLinkAdded(LinkModel link)
    {
        // Validate link
        if (!IsValidConnection(link.Source, link.Target))
        {
            Diagram.Links.Remove(link);
            return;
        }
    }

    private void OnPointerDown(Model model, PointerEventArgs args)
    {
        if (args.Button == 2) // Right click
        {
            ShowContextMenu(args.Position);
        }
    }

    public void Dispose()
    {
        Diagram.SelectionChanged -= OnSelectionChanged;
        Diagram.NodeAdded -= OnNodeAdded;
        Diagram.LinkAdded -= OnLinkAdded;
        Diagram.PointerDown -= OnPointerDown;
    }
}
```

## Diagram Services

### Dependency Injection
```razor
@inject NavigationManager NavigationManager
@inject IDialogService DialogService
@inject IDiagramService DiagramService

@code {
    [Inject] private ISnackbar Snackbar { get; set; }
    
    private async Task SaveDiagram()
    {
        var json = DiagramService.Serialize(Diagram);
        await LocalStorage.SetItemAsync("diagram", json);
    }
    
    private async Task LoadDiagram()
    {
        var json = await LocalStorage.GetItemAsync<string>("diagram");
        if (!string.IsNullOrEmpty(json))
        {
            Diagram = DiagramService.Deserialize(json);
            StateHasChanged();
        }
    }
}
```

## Key Interfaces

### Model Interfaces
- `ILinkable`: Implement for custom port functionality
- `IPositionable`: Implement for objects that can be positioned on canvas
- `IGroupable`: Implement for nodes that can be grouped

### Component Interfaces
```csharp
public interface INodeWidget<TNode> where TNode : NodeModel
{
    TNode Node { get; }
    RenderFragment ChildContent { get; }
}

public interface ILinkWidget<TLink> where TLink : LinkModel
{
    TLink Link { get; }
    string PathDefinition { get; }
}