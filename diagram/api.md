# Diagram API

## Properties

| Name | Type | Default | Description |
|------|------|---------|-------------|
| Options (Read only) | BlazorDiagramOptions | - | |
| Nodes (Read only) | NodeLayer | - | Acts as a list for the nodes |
| Links (Read only) | LinkLayer | - | Acts as a list for the links |
| Groups (Read only) | GroupLayer | - | Acts as a list for the groups |
| Controls (Read only) | ControlsLayer | - | Only way to Get/Add/Remove controls for a model |
| Container (Read only) | Rectangle? | null | Boundaries representing the canvas, retrieved with JS |
| Pan (Read only) | Point? | Zero | |
| Zoom (Read only) | Double | 1 | |
| SuspendRefresh | Boolean | false | Suspends the refreshes related to the diagram (canvas) |
| OrderedSelectables (Read only) | IReadOnlyList<SelectableModel> | - | Ordered list of models using the Order property |

## Events

| Name | Type | Description |
|------|------|-------------|
| PointerDown | Action<Model?, PointerEventArgs>? | |
| PointerMove | Action<Model?, PointerEventArgs>? | |
| PointerUp | Action<Model?, PointerEventArgs>? | |
| PointerEnter | Action<Model?, PointerEventArgs>? | |
| PointerLeave | Action<Model?, PointerEventArgs>? | |
| KeyDown | Action<KeyboardEventArgs>? | |
| Wheel | Action<WheelEventArgs>? | |
| PointerClick | Action<Model?, PointerEventArgs>? | |
| PointerDoubleClick | Action<Model?, PointerEventArgs>? | |
| SelectionChanged | Action<SelectableModel>? | |
| PanChanged | Action? | |
| ZoomChanged | Action? | |
| ContainerChanged | Action? | |
| Changed | Action? | |

## Methods

| Name | Return Type | Description |
|------|-------------|-------------|
| RegisterComponent<TModel, TComponent>(bool replace = false) | void | Register a Blazor component to render for every instance of TModel |
| RegisterComponent(Type modelType, Type componentType, bool replace = false) | void | Register a Blazor component to render for every instance of modelType |
| GetComponent(Type modelType, bool checkSubclasses = true) | Type? | Returns the component Type registered for the modelType |
| GetComponent<TModel>(bool checkSubclasses = true) | Type? | Returns the component Type registered for TModel |
| GetComponent(Model model, bool checkSubclasses = true) | Type? | Returns the component Type registered for typeof(Model) |
| Refresh() | void | |
| Batch(Action action) | void | |
| GetSelectedModels() | IEnumerable<SelectableModel> | |
| SelectModel(SelectableModel model, bool unselectOthers) | void | |
| UnselectModel(SelectableModel model) | void | |
| UnselectAll() | void | |
| RegisterBehavior(Behavior behavior) | void | |
| GetBehavior<T>() where T : Behavior | T? | |
| UnregisterBehavior<T>() where T : Behavior | void | |
| ZoomToFit(double margin) | void | |
| SetPan(double x, double y) | void | |
| UpdatePan(double deltaX, double deltaY) | void | |
| SetZoom(double newZoom) | void | |
| SetContainer(Rectangle newRect) | void | |
| GetRelativeMousePoint(double clientX, double clientY) | Point | |
| GetRelativePoint(double clientX, double clientY) | Point | |
| GetScreenPoint(double clientX, double clientY) | Point | |
| SendToBack(SelectableModel model) | void | |
| SendToFront(SelectableModel model) | void | |
| GetMinOrder() | int | |
| GetMaxOrder() | int | |
| TriggerPointerDown(Model? model, PointerEventArgs e) | void | |
| TriggerPointerMove(Model? model, PointerEventArgs e) | void | |
| TriggerPointerUp(Model? model, PointerEventArgs e) | void | |
| TriggerPointerEnter(Model? model, PointerEventArgs e) | void | |
| TriggerPointerLeave(Model? model, PointerEventArgs e) | void | |
| TriggerKeyDown(KeyboardEventArgs e) | void | |
| TriggerWheel(WheelEventArgs e) | void | |
| TriggerPointerClick(Model? model, PointerEventArgs e) | void | |
| TriggerPointerDoubleClick(Model? model, PointerEventArgs e) | void | |