# Link Vertices

`LinkVertexModel` are user-defined points for the link to pass through.

## Usage

### Programmatically

```csharp
yourLink.Vertices.Add(new LinkVertexModel(new Point(50, 200)));
// OR
yourLink.AddVertex(new Point(50, 200));
```

### Interactively

```csharp
yourLink.Segmentable = true;
// Clicking a link will now create vertices
// Double clicking a vertex deletes it
```

## Customization

If you need any additional data, feel free to create a separate model (class) and inherit `LinkVertexModel`. In all cases, you will need to register a custom Blazor component to be used.

```csharp
Diagram.RegisterComponent<LinkVertexModel, MyVertexWidget>();
```

### MyVertexWidget.razor
```razor
<circle cx="@Vertex.Position.X" cy="@Vertex.Position.Y" r="5" fill="red"></circle>
<circle cx="@Vertex.Position.X" cy="@Vertex.Position.Y" r="10" fill="none" stroke="red" stroke-width="4"></circle>

@code {
    [Parameter]
    public LinkVertexModel Vertex { get; set; } = null!;

    [Parameter]
    public string Color { get; set; } = null!;
}
```