# Diagram Overview

## Structure

The `DiagramCanvas` component generates the following structure:

```html
<div class="diagram-canvas" tabindex="-1">
    <!-- LAYERS -->
</div>
```

You can add your own CSS classes using the `Class` parameter.

## Layers

It is very important to know that in Blazor Diagrams, everything is rendered in 2 layers:

### SVG Layer

```html
<svg class="diagram-svg-layer" style="transform: translate(0px, 0px) scale(1); z-index: 0;">
    <!-- Links, Nodes, Controls, ... -->
</svg>
```

This layer is basically a svg. It is mainly used to render links, since they require the `<path>` element. However, it is also possible to render nodes in it by inherting from `SvgNodeModel` or `SvgGroupModel`. This lets you use any svg elements and features with ease.

### HTML Layer

```html
<div class="diagram-html-layer" style="transform: translate(0px, 0px) scale(1); z-index: 0;">
    <!-- Nodes, Controls, ... -->
</div>
```

This layer is a simple html div. It is mainly used to render nodes. It is very useful since you can re-use any html you might already have in your nodes, as well as include interactivity through inputs for example.

## Additional Content

You can add additional content to each layer using the available render fragments:

```html
<DiagramCanvas>
    <AdditionalHtml>
        <!-- EXTRA HTML -->
    </AdditionalHtml>
    <AdditionalSvg>
        <!-- EXTRA SVG -->
    </AdditionalSvg>
</DiagramCanvas>
```