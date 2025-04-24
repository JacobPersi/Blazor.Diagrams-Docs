# Link Markers

A `LinkMarker` is a SVG path that can be drawn at the beginning and/or at the end of a link. They are automatically rotated to fit the direction.

## Usage

You can simply use the provided markers:

```csharp
yourLink.SourceMarker = LinkMarker.Arrow;
// OR
yourLink.TargetMarker = LinkMarker.Circle;
// OR
yourLink.TargetMarker = LinkMarker.Square;
```

## Customization

You can either customize the predefined shapes:

```csharp
yourLink.SourceMarker = LinkMarker.NewCircle(10);
yourLink.SourceMarker = LinkMarker.NewSquare(20);
yourLink.TargetMarker = LinkMarker.NewArrow(20, 30);
yourLink.TargetMarker = LinkMarker.NewRectangle(20, 30);
```

Or provide your own SVG paths:

Requirements:
* Know the width of your path
* Your path should not go to the negative side

```csharp
yourLink.SourceMarker = new LinkMarker("M 0 -8 L 3 -8 3 8 0 8 z M 4 -8 7 -8 7 8 4 8 z M 8 -8 16 0 8 8 z", 16);
yourLink.TargetMarker = new LinkMarker("M 0 -8 L 8 -8 4 0 8 8 0 8 4 0 z", 8);
```

You can use the [SvgPathEditor](https://yqnn.github.io/svg-path-editor/) app to easily create these.