# Groups Overview

In Blazor Diagrams, Groups are a way to group nodes together. Groups can also contain other groups, so you can create hierarchies.

## Structure

The internal component `GroupRenderer` generates the following structure:

```html
<div class="diagram-group ..." data-group-id="28e9606d-08dd-47d5-a4c7-b95e541bcf1e" style="top: 10px; left: 10px; width: 100px; height: 100px">
    <!-- YOUR CONTENT WILL BE HERE -->
</div>
```

The classes that the div can have (beside `diagram-group`) are: `locked`, `selected` and `default`.

## Creating a group

### Interactively

By default, users can group selected nodes/groups using the keys `Ctrl+g` (if `Options.Groups.Enabled` is set to `true`). Check out [Keyboard Shortcuts](keyboard-shortcuts.md) in order to change the required keys.

### Programmatically

Assuming we have two nodes, we can simply:

```csharp
var node1 = new NodeModel(new Point(10, 10));
var node2 = new NodeModel(new Point(50, 50));
var group = BlazorDiagram.Groups.Group(node1, node2);
```

## ! Important Note

Most of the time, groups will have a background of some sort (e.g. a color), which will hide all the links beneath it since if you remember, the nodes layer is above the links layer. There are 2 solutions for this:

### SVG Group

If you use svg nodes, then make sure you add your groups first, then your links.

If you're grouping nodes dynamically, make sure to bring links associated to those groups and their nodes to the front (or the created groups to the back) using the ordering methods available.

### Layers order

The `BlazorDiagramOptions` class contains two properties in order to control the order (z-index) of the layers: `LinksLayerOrder` and `NodesLayerOrder`. All you have to do for groups to work properly is to set `LinksLayerOrder` to a bigger value than the other.