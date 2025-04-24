# Navigator Widget

A `NavigatorWidget` (also called a Minimap) is a simplified view of the whole diagram.

## Options

| Name | Type | Default |
|------|------|---------|
| UseNodeShape | bool | true |
| Width | double | 0 |
| Height | double | 0 |
| Margin | double | 5 |
| NodeColor | string | #40babd |
| GroupColor | string | #9fd0d1 |
| ViewStrokeColor | string | #40babd |
| ViewStrokeWidth | double | 4 |
| Class | string | |
| Style | string | |

## Usage

```razor
<CascadingValue Value="_diagram" IsFixed="true">
    <DiagramCanvas>
        <Widgets>
            <NavigatorWidget 
                Width="200" 
                Height="120" 
                Class="border border-black bg-white absolute" 
                Style="bottom: 15px; right: 15px;" />
        </Widgets>
    </DiagramCanvas>
</CascadingValue>
```