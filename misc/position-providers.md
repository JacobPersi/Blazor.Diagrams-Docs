# Position Providers

Position Providers simply take some input (e.g. a model and some arguments) and return a position (Point) when asked to (by some other features in the library).

## Bounds Based

### Options

| Name | Type | Description |
|------|------|-------------|
| x | double | A number between 0 and 1 that will be multiplied by the width |
| y | double | A number between 0 and 1 that will be multiplied by the height |
| offsetX | double | Any number |
| offsetY | double | Any number |

### Demonstration
![Bounds Based Position Provider](../images/bounds-based-position-provider.png)

## Shape Angle

### Options

| Name | Type | Description |
|------|------|-------------|
| angle | double | In degrees |
| offsetX | double | Any number |
| offsetY | double | Any number |

### Demonstration
![Shape Angle Position Provider](../images/shape-angle-position-provider.png)

## Link Path

### Options

| Name | Type | Description |
|------|------|-------------|
| distance | double | If between 0 and 1, it will be multiplied by the link's length. If less than 0, it will start from the end of the link. If greater than 1, it will start from the beginning of the link |
| offsetX | double | Any number |
| offsetY | double | Any number |

### Demonstration
![Link Path Position Provider](../images/link-path-position-provider.png)