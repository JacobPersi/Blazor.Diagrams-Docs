# Keyboard Shortcuts

Blazor Diagrams provides a utility behavior to handle keyboard shortcuts: `KeyboardShortcutsBehavior`.

## Default shortcuts

| Keys | Implementation | Description |
|------|---------------|-------------|
| Delete | `KeyboardShortcutsDefaults.DeleteSelection` | Deletes the selected models (nodes, groups and links) |
| Ctrl+Alt+g | `KeyboardShortcutsDefaults.Grouping` | Groups the selected models |

## Adding a shortcut

```csharp
var ksb = _blazorDiagram.GetBehavior<KeyboardShortcutsBehavior>();
ksb.SetShortcut("s", ctrl: true, shift: true, alt: true, SaveToMyServer);

private async ValueTask SaveToMyServer()
{
    await FakeHttpCall();
}
```

## Removing a shortcut

```csharp
var ksb = _blazorDiagram.GetBehavior<KeyboardShortcutsBehavior>();
ksb.RemoveShortcut("s", ctrl: true, shift: true, alt: true);
```