# Diagram Options

Here are all the available options in `BlazorDiagramOptions`:

## Main Options

| Name | Type | Default | Description |
|------|------|---------|-------------|
| LinksLayerOrder | Integer | 0 | The order (z-index) of the SVG layer |
| NodesLayerOrder | Integer | 0 | The order (z-index) of the HTML layer |
| Zoom | BlazorDiagramZoomOptions | - | Zoom options |
| Links | BlazorDiagramLinkOptions | - | Link options |
| Groups | BlazorDiagramGroupOptions | - | Group options |
| Constraints | BlazorDiagramConstraintsOptions | - | Constraint options |
| Virtualization | BlazorDiagramVirtualizationOptions | - | Virtualization options |

## Zoom Options

| Name | Type | Default | Description |
|------|------|---------|-------------|
| Enabled | Boolean | true | Enable/disable zoom functionality |
| Inverse | Boolean | false | Invert zoom direction |
| Minimum | Double | 0.1 | Minimum zoom level |
| Maximum | Double | 2 | Maximum zoom level |
| ScaleFactor | Double | 1.05 | Scale factor for each zoom step |

## Link Options

| Name | Type | Default | Description |
|------|------|---------|-------------|
| DefaultColor | String | black | Default link color |
| DefaultSelectedColor | String | rgb(110, 159, 212) | Default selected link color |
| DefaultRouter | Router | NormalRouter | Default router for new links |
| DefaultPathGenerator | PathGenerator | SmoothPathGenerator | Default path generator for new links |
| EnableSnapping | Boolean | false | If true, dragging new links will snap them to the closest ports |
| SnappingRadius | Double | 50 | Used to calculate the distance and decide whether to snap the link |
| RequireTarget | Boolean | true | If false, links can be free (without target) |
| Factory | LinkFactory | - | Delegate to control how a link is instantiated |
| TargetAnchorFactory | AnchorFactory | - | Delegate to control how the target anchor is instantiated |

## Group Options

| Name | Type | Default | Description |
|------|------|---------|-------------|
| Enabled | Boolean | false | Enable/disable group functionality |
| Factory | GroupFactory | - | Delegate to control how a group is instantiated |

## Constraint Options

| Name | Type | Default | Description |
|------|------|---------|-------------|
| ShouldDeleteNode | Func<NodeModel, ValueTask<bool>> | true | Constraint for node deletion |
| ShouldDeleteLink | Func<BaseLinkModel, ValueTask<bool>> | true | Constraint for link deletion |
| ShouldDeleteGroup | Func<GroupModel, ValueTask<bool>> | true | Constraint for group deletion |

## Virtualization Options

| Name | Type | Default | Description |
|------|------|---------|-------------|
| Enabled | Boolean | false | Enable/disable virtualization |
| OnNodes | Boolean | true | Enable virtualization for nodes |
| OnGroups | Boolean | false | Enable virtualization for groups |
| OnLinks | Boolean | false | Enable virtualization for links |