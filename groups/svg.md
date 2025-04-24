# SVG Groups

SVG groups are groups that will be rendered in the SVG layer. In this page, we will talk about the differences between them and normal groups.

## Structure

The component `GroupRenderer` generates the following structure:

```html
<g class="diagram-group ..." data-group-id="28e9606d-08dd-47d5-a4c7-b95e541bcf1e" transform="translate(10 10)">
    <rect width="100" height="100" fill="none"></rect>
    <!-- YOUR CONTENT WILL BE HERE -->
</g>
```

The `rect` is there for you to be able to style the background of the group, since we can't style `g` elements.

## Creating a SVG group

### Interactively

First, we will need to change how groups are created:

```csharp
yourDiagram.Options.Groups.Factory = (diagram, children) => new SvgGroupModel(children);
```

By default, users can group selected nodes/groups using the keys `Ctrl+g` (if `Options.Groups.Enabled` is set to `true`). Check out [Keyboard Shortcuts](keyboard-shortcuts.md) in order to change the required keys.

### Programmatically

Assuming we have two nodes, we can simply:

```csharp
var node1 = new SvgNodeModel(new Point(10, 10));
var node2 = new SvgNodeModel(new Point(50, 50));
var group = new SvgGroupModel(new[] { node1, node2 });
```