# Diagram Behaviors

Behaviors are a way to encapsulate a functionality. They are separated into classes mainly for readability, separation of concerns, and for the library users to be able to remove/replace them. The behaviors inherit from the base class `Behavior` and use the available events to do what they need.

## Example

Here's an example of the built-in selection behavior:

```csharp
using Blazor.Diagrams.Core.Models.Base;
using Blazor.Diagrams.Core.Events;

namespace Blazor.Diagrams.Core.Behaviors
{
    public class SelectionBehavior : Behavior
    {
        public SelectionBehavior(Diagram diagram) : base(diagram)
        {
            Diagram.PointerDown += OnPointerDown;
        }

        private void OnPointerDown(Model? model, PointerEventArgs e)
        {
            var ctrlKey = e.CtrlKey;

            switch (model)
            {
                case null:
                    Diagram.UnselectAll();
                    break;
                case SelectableModel sm when ctrlKey && sm.Selected:
                    Diagram.UnselectModel(sm);
                    break;
                case SelectableModel sm:
                {
                    if (!sm.Selected)
                    {
                        Diagram.SelectModel(sm, !ctrlKey || !Diagram.Options.AllowMultiSelection);
                    }
                    break;
                }
            }
        }

        public override void Dispose()
        {
            Diagram.PointerDown -= OnPointerDown;
        }
    }
}
```

As you can see, the behavior simply uses the `PointerDown` event in order to (un)select stuff.

## Replacing a behavior

Let's say you didn't like how the `SelectionBehavior` works, let's replace it by a simpler one. We just want to keep selecting models without CTRL and only unselect everything once the canvas is clicked.

```csharp
using Blazor.Diagrams.Core.Models.Base;
using Blazor.Diagrams.Core.Events;

namespace Blazor.Diagrams.Core.Behaviors
{
    public class MySelectionBehavior : Behavior
    {
        public SelectionBehavior(Diagram diagram) : base(diagram)
        {
            Diagram.PointerDown += OnPointerDown;
        }

        private void OnPointerDown(Model? model, PointerEventArgs e)
        {
            if (model == null) // Canvas
            {
                Diagram.UnselectAll();
            }
            else if (model is SelectableModel sm)
            {
                Diagram.SelectModel(sm);
            }
        }

        public override void Dispose()
        {
            Diagram.PointerDown -= OnPointerDown;
        }
    }
}
```

A very simple class indeed. Inherting from `Behavior` automatically forces you to have the constructor, in order to have the `Diagram` instance, but also the `Dispose` method in order to remove any event handlers in case the behavior is unregistered.

Let's now replace the old behavior with ours:

```csharp
// In case you want to keep the old behavior intance
var oldSelectionBehavior = Diagram.GetBehavior<SelectionBehavior>()!;
Diagram.UnregisterBehavior<SelectionBehavior>();
Diagram.RegisterBehavior(new MySelectionBehavior(Diagram));
```