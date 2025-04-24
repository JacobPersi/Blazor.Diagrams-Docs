# Display

You've created a diagram and populated it, let's display it! First, let's setup our component so that it has a specific width and height. In order for us to display the diagram, a visible parent is mandatory, since the canvas uses 100% width/height.

## MyDiagram.razor
```html
<div class="diagram-container">
</div>
```

Now create a scoped CSS file with the following content:

## MyDiagram.razor.css
```css
.diagram-container {
    width: 100%;
    height: 400px;
    border: 1px solid black; /* Just visual */
}
```

Now that we have a visible container, let's display the diagram:

## MyDiagram.razor
```razor
@using Blazor.Diagrams.Components

<div class="diagram-container">
    <CascadingValue Value="Diagram" IsFixed="true">
        <DiagramCanvas></DiagramCanvas>
    </CascadingValue>
</div>
```

If you used the default styles and did everything correctly, you'll have an interactive diagram where you can move and manipulate the nodes.

Congratulations! You're now ready to move to the interesting stuff.