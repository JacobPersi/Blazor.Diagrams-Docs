# Grid Widget

A `GridWidget` is simply a customizable background with a grid pattern. It adjusts itself based on the current panning / zoom.

## Options

| Name | Type | Default |
|------|------|---------|
| Size | double | 20 |
| ZoomThreshold | double | 0 |
| Mode | GridMode (Line or Point) | GridMode.Line |
| BackgroundColor | string | rgb(241 241 241) |

## Usage

```razor
<CascadingValue Value="_diagram" IsFixed="true">
    <DiagramCanvas>
        <Widgets>
            <GridWidget 
                Size="30" 
                Mode="GridMode.Line" 
                BackgroundColor="white" />
        </Widgets>
    </DiagramCanvas>
</CascadingValue>
```