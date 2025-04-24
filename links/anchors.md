# Anchors

An anchor represents the exact position where on an `ILinkable` (node, group, port, ...) a link should connect. Links have two anchors, `Source` and `Target`.

## Position Anchor

`PositionAnchor` is the most basic anchor. It wraps a `Point` position and is meant to be used for static and/or known positions (without calculations). This anchor was created for internal use, so that links couldn't have `null` as a target, but you can use it if you see fit.

### Usage

```csharp
var paSourceAnchor = new PositionAnchor(new Point(50, 40));
var paTargetAnchor = new PositionAnchor(new Point(300, 70));
Diagram.Links.Add(new LinkModel(paSourceAnchor, paTargetAnchor));
```

## Single Port Anchor

`SinglePortAnchor` calculates a position on the specified port based on the chosen options.

### Options

| Name | Default | Description |
|------|---------|-------------|
| MiddleIfNoMarker | false | If the corresponding side doesn't have a Marker, the center of the port will be used as the position |
| UseShapeAndAlignment | true | Using the port's shape, the point at an angle (depending on the alignment) will be used as the position |

If both options are false, the point at the boundary (depending on the alignment) will be used as the position.

### Usage

For the purpose of this example, the SVG layer will be rendered on top of the HTML one.

```csharp
var spaSourceAnchor = new SinglePortAnchor(spaPort) { 
    MiddleIfNoMarker = false, 
    UseShapeAndAlignment = true 
};
Diagram.Links.Add(new LinkModel(spaSourceAnchor, someTargetAnchor));

// OR
Diagram.Links.Add(new LinkModel(sourcePort, targetPort));
```

## Shape Intersection Anchor

`ShapeIntersectionAnchor` calculates the position as the intersection a line going from the other end to the center of the specified node. This anchor is used to create port-less links that take into account the node's shape.

### Usage

```csharp
var sourceAnchor = new ShapeIntersectionAnchor(firstNode);
var targetAnchor = new ShapeIntersectionAnchor(secondNode);
Diagram.Links.Add(new LinkModel(sourceAnchor, targetAnchor));

// OR
Diagram.Links.Add(new LinkModel(firstNode, secondNode));
```

## Link Anchor

`LinkAnchor` calculates the position along the given link based on the chosen options.

### Usage

```csharp
var sourceAnchor = new LinkAnchor(otherLink, distance: 0.5, offsetX: 0, offsetY: 0);
Diagram.Links.Add(new LinkModel(sourceAnchor, someTargetAnchor));
```

## Dynamic Anchor

`DynamicAnchor` chooses the closest position from the given calculated positions. You can check out the list of position providers [here](https://blazor-diagrams.zhaytam.com/documentation/position-providers).

### Usage

```csharp
var sourceAnchor = new DynamicAnchor(someNode, new[] {
    new BoundsBasedPositionProvider(0.5, 0),   // Center top
    new BoundsBasedPositionProvider(1, 0.5),   // Center right
    new BoundsBasedPositionProvider(0.5, 1),   // Center bottom
    new BoundsBasedPositionProvider(0, 0.5),   // Center left
});
Diagram.Links.Add(new LinkModel(daSourceAnchor, someTargetAnchor));
```