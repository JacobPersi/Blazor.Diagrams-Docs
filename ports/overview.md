# Ports Overview

Ports are locations/endpoints on your nodes/groups from where a link can be created and/or attached.

## Structure

The internal component `PortRenderer` generates the following structures. The classes that the element can have (beside `diagram-port`) are:

* The alignment (e.g. `top`, `bottom`)
* If the port contains ingoing/outgoing links, `has-links`
* Extra classes you provide using the `Class` parameter

### When the parent is HTML

```html
<div class="diagram-port ..." data-port-id="28e9606d-08dd-47d5-a4c7-b25e541bcf1n">
    <!-- YOUR CONTENT WILL BE HERE -->
</div>
```

### When the parent is SVG

```html
<g class="diagram-port ..." data-port-id="28e9606d-08dd-47d5-a4c7-b25e541bcf1n">
    <!-- YOUR CONTENT WILL BE HERE -->
</g>
```

## Shape

Ports can have a specific shape, which by default is a circle. It is used for two things at the moment:

* `ShapeAnglePositionProvider`: To return a position for the given angle.
* `SinglePortAnchor`: When `UseShapeAndAlignment` is true.

You can change the shape of your node by overriding the `GetShape` method in your custom model.

## Creating a port

```csharp
var port = myNode.AddPort(PortAlignment.Top);

// OR
var port = myNode.AddPort(new PortModel(myNode, PortAlignment.Top));
```