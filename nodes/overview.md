# Nodes Overview

Nodes are the most important concept in Blazor Diagrams.

## Structure

The internal component `NodeRenderer` generates the following structure:

```html
<div class="diagram-node ..." data-node-id="28e9606d-08dd-47d5-a4c7-b25e541bcf1e" style="top: 10px; left: 10px;">
    <!-- YOUR CONTENT WILL BE HERE -->
</div>
```

The classes that the div can have (beside `diagram-node`) are: `locked`, `selected` and `grouped`.

## Shape

Nodes can have a specific shape, which by default is a rectangle. It is used for two things at the moment:

* `ShapeAnglePositionProvider`: To return a position for the given angle.
* `NavigatorWidget`: To know what to draw.

You can change the shape of your node by overriding the `GetShape` method in your custom model.

## Creating a node

```csharp
var node1 = new NodeModel(new Point(10, 10));
BlazorDiagram.Nodes.Add(node1);
```