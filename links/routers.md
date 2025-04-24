# Routers

A `Router` is responsible of creating the route that the link will go through. It takes as input the list of vertices (if any) and outputs a list of new computed points.

## Normal Router

The `NormalRouter` is the default router. It simply returns the list of user-created vertices as is to ensure the link goes through them.

### Usage

```csharp
var link = Diagram.Links.Add(new LinkModel(sourceAnchor, targetAnchor));
link.Router = new NormalRouter();
```

## Orthogonal Router

The `OrthogonalRouter` is a router that ensures an orthogonal path. It will add as many points as necessary to create that route using a simplified A* algorithm.

Limitations:
* Only supports links between 2 ports
* Ignores user-defined Vertices

### Usage

```csharp
var link = Diagram.Links.Add(new LinkModel(sourcePort, targetPort));
link.Router = new OrthogonalRouter();
```