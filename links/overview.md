# Links Overview

Links (also called Edges) are relationships between nodes, groups, ports and even other links! They are always rendered in the SVG layer.

## Structure

The internal component `LinkRenderer` generates the following structure:

```html
<g class="diagram-link" data-link-id="9566f945-cc88-46bc-8d50-1ec15502f6fb">
    <!-- YOUR CONTENT WILL BE HERE -->
</g>
```

The classes that the g can have (beside `diagram-link`) are: `attached`.

## Creating a link

```csharp
var link = Diagram.Links.Add(new LinkModel(node1, node2));

// OR
var link = Diagram.Links.Add(new LinkModel(port1, port2));

// OR
var link = Diagram.Links.Add(new LinkModel(anchor1, anchor2));
```