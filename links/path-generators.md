# Path Generators

A `PathGenerator` is responsible of creating the SVG path for a given route.

## Smooth Path Generator

The `SmoothPathGenerator` generates a Cubic Bezier Curve. It is the default path generator.

### Usage

```csharp
var link = Diagram.Links.Add(new LinkModel(sourceAnchor, targetAnchor));
link.PathGenerator = new SmoothPathGenerator();
```

## Straight Path Generator

The `StraightPathGenerator` generates straight lines. You can also choose a radius for when the path contains vertices or direction changes.

### Usage

```csharp
var link = Diagram.Links.Add(new LinkModel(sourceAnchor, targetAnchor));
link.PathGenerator = new StraightPathGenerator();
```