# Selection Box Widget

A `SelectionBoxWidget` lets you hold SHIFT and click+drag to show a selection box that selects all models intersecting with it.

## Options

| Name | Type | Default |
|------|------|---------|
| Background | string | rgb(110 159 212 / 25%) |

## Usage

```razor
<CascadingValue Value="_diagram" IsFixed="true">
    <DiagramCanvas>
        <Widgets>
            <SelectionBoxWidget />
        </Widgets>
    </DiagramCanvas>
</CascadingValue>
```