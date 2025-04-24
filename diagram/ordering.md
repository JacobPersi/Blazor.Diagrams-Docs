# Diagram Ordering

Since 3.0, Blazor Diagrams supports ordering between models out of the box!

## Overview

* All selectable models have an `Order` property (number).
* `Diagram` keeps an ordered list of all selectable models called `OrderedSelectables`.
* When a new model is added to the diagram, it's placed at the end of the list with the Order property set to `lastOrder + 1`.
* When the Order property changes on any of the models, everything is re-ordered.

## Demonstration

```csharp
var diagram = new BlazorDiagram();
var node1 = diagram.Nodes.Add(new NodeModel());
var node2 = diagram.Nodes.Add(new NodeModel());

Console.WriteLine(node1.Order); // 1
Console.WriteLine(node2.Order); // 2

node1.Order = 10;
// diagram.OrderedSelectables[0] will be node2 (Order 2)
// diagram.OrderedSelectables[1] will be node1 (Order 10)

diagram.SendToFront(node2);
Console.WriteLine(node1.Order); // 10
Console.WriteLine(node2.Order); // 11

diagram.SendToBack(node2);
Console.WriteLine(node1.Order); // 2
Console.WriteLine(node2.Order); // 1

// Setting the order for 2 models will sort the list twice
// We can avoid that by suspending the sorting until we're finished
diagram.SuspendSorting = true;
node1.Order = 100;
node2.Order = 200;
diagram.SuspendSorting = false;
diagram.RefreshOrders();

// diagram.OrderedSelectables[0] will be node1 (Order 100)
// diagram.OrderedSelectables[1] will be node2 (Order 200)
```