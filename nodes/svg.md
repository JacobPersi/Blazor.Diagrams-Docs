# SVG Nodes

SVG nodes are nodes that will be rendered in the SVG layer. In this page, we will talk about the differences between them and normal nodes.

## Structure

The component `NodeRenderer` generates the following structure:

```html
<g class="diagram-node ..." data-node-id="28e9606d-08dd-47d5-a4c7-b25e541bcf1e" transform="translate(10 10)">
    <!-- YOUR CONTENT WILL BE HERE -->
</g>
```

## Creating a SVG node

```csharp
var node1 = new SvgNodeModel(new Point(10, 10));
BlazorDiagram.Nodes.Add(node1);
```