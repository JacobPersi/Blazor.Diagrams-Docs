# Controls Overview

Controls are "extra" UI element that show when models are selected or hovered on. The internal `ControlsLayerRenderer` component is responsible of rendering them in the appropriate layer, which means you can have HTML controls as well as SVG controls based on the parent's layer.

> This feature is still somewhat new and might be improved based on feedback.

## Types

### Control
A `Control` is just a UI element with no behavior (e.g. `BoundaryControl`).

### Executable Control
A `ExecutableControl` is a clickable UI element with some attached behavior (e.g. `RemoveControl`). For now, executable controls work best using `ControlsType.OnSelection`.

## Demonstration

```csharp
// Initialize
var node1Controls = Diagram.Controls.AddFor(Node1); // OnSelection default
var node2Controls = Diagram.Controls.AddFor(Node2, ControlsType.OnHover);

// Add
node1Controls.Add(new SomeControl());
node2Controls.Add(new SomeControl());

// Get the controls whenever
node1Controls = Diagram.Controls.GetFor(Node1);
node2Controls = Diagram.Controls.GetFor(Node2);

// Manually control visibility
node1Controls.Show();
node2Controls.Hide();

// Remove all controls for a model
Diagram.Controls.RemoveFor(Node1);
```

## Out of the box controls

The library comes with a couple of controls:

### Boundary Control

The `BoundaryControl` simply shows a border alongside the boundary of the model based on `GetBounds`.

```csharp
Diagram.Controls.AddFor(SomeModel).Add(new BoundaryControl());
```

### Remove Control

The `RemoveControl` adds a deletion button positioned using [Position Providers](position-providers.md).

```csharp
Diagram.Controls.AddFor(SomeModel)
    .Add(new RemoveControl(0.5, 0)); // BoundsBasedPositionProvider (top center)

// OR
Diagram.Controls.AddFor(SomeModel)
    .Add(new RemoveControl(somePositionProvider));
```

### Arrow Head Control

The `ArrowHeadControl` adds a draggable arrow head on links to enable changing the source and/or target interactively.

```csharp
Diagram.Controls.AddFor(SomeModel).Add(new ArrowHeadControl(source: true));
Diagram.Controls.AddFor(SomeModel).Add(new ArrowHeadControl(source: false)); // Target
Diagram.Controls.AddFor(SomeModel).Add(new ArrowHeadControl(true, customLinkMarker));
```

### Drag New Link Control

The `DragNewLinkControl` adds a link creation button positioned using [Position Providers](position-providers.md). This is mainly for port-less links, the source anchor will be a `ShapeIntersectionAnchor` by default.

```csharp
Diagram.Controls.AddFor(SomeModel).Add(new DragNewLinkControl(1, 0.5, offsetX: 20));
Diagram.Controls.AddFor(SomeModel).Add(new DragNewLinkControl(0, 0.5, offsetX: -20));

// OR
Diagram.Controls.AddFor(SomeModel)
    .Add(new DragNewLinkControl(somePositionProvider));
```