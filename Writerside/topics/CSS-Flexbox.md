# Flexbox

CSS Flexbox (Flexible Box Layout) is a layout model designed to provide a more efficient way to lay out, align, and distribute space among items in a container, even when their size is unknown or dynamic. It is particularly useful for creating complex layouts with ease and ensuring that elements behave predictably when the page layout must accommodate different screen sizes and devices.

## Key Concepts

### Flex Container

A flex container is an element with `display: flex` or `display: inline-flex`. This container establishes a flex formatting context for its direct children, known as flex items.

```css
.container {
    display: flex;
}
```

### Flex Items

Flex items are the direct children of a flex container. These items can be laid out in any direction and can have flexible dimensions.

### Main Axis and Cross Axis

- **Main Axis**: The primary axis along which flex items are laid out. It can be horizontal or vertical, depending on the `flex-direction` property.
- **Cross Axis**: The axis perpendicular to the main axis.

### Flex Properties

#### Container Properties

1. **`flex-direction`**: Defines the direction in which the flex items are placed in the flex container.
    - `row` (default): Items are placed in a row, from left to right.
    - `row-reverse`: Items are placed in a row, from right to left.
    - `column`: Items are placed in a column, from top to bottom.
    - `column-reverse`: Items are placed in a column, from bottom to top.

    ```css
    .container {
        flex-direction: row;
    }
    ```

2. **`flex-wrap`**: Controls whether the flex container is single-line or multi-line, and the direction of the cross-axis lines.
    - `nowrap` (default): All flex items are on one line.
    - `wrap`: Flex items wrap onto multiple lines, from top to bottom.
    - `wrap-reverse`: Flex items wrap onto multiple lines, from bottom to top.

    ```css
    .container {
        flex-wrap: wrap;
    }
    ```

3. **`flex-flow`**: A shorthand for `flex-direction` and `flex-wrap`.

    ```css
    .container {
        flex-flow: row wrap;
    }
    ```

4. **`justify-content`**: Aligns flex items along the main axis.
    - `flex-start` (default): Items are packed toward the start of the main axis.
    - `flex-end`: Items are packed toward the end of the main axis.
    - `center`: Items are centered along the main axis.
    - `space-between`: Items are evenly distributed; the first item is at the start, the last item is at the end.
    - `space-around`: Items are evenly distributed with equal space around them.
    - `space-evenly`: Items are evenly distributed with equal space between them.

    ```css
    .container {
        justify-content: center;
    }
    ```

5. **`align-items`**: Aligns flex items along the cross axis.
    - `stretch` (default): Items are stretched to fill the container.
    - `flex-start`: Items are aligned toward the start of the cross axis.
    - `flex-end`: Items are aligned toward the end of the cross axis.
    - `center`: Items are centered along the cross axis.
    - `baseline`: Items are aligned such that their baselines align.

    ```css
    .container {
        align-items: center;
    }
    ```

6. **`align-content`**: Aligns flex lines when there is extra space in the cross axis.
    - `stretch` (default): Lines stretch to take up the remaining space.
    - `flex-start`: Lines are packed toward the start of the cross axis.
    - `flex-end`: Lines are packed toward the end of the cross axis.
    - `center`: Lines are centered along the cross axis.
    - `space-between`: Lines are evenly distributed; the first line is at the start, the last line is at the end.
    - `space-around`: Lines are evenly distributed with equal space around them.
    - `space-evenly`: Lines are evenly distributed with equal space between them.

    ```css
    .container {
        align-content: space-between;
    }
    ```

#### Item Properties

1. **`order`**: Controls the order in which flex items appear in the flex container.

    ```css
    .item {
        order: 2;
    }
    ```

2. **`flex-grow`**: Defines the ability of a flex item to grow if necessary. It accepts a unitless value that serves as a proportion.

    ```css
    .item {
        flex-grow: 1;
    }
    ```

3. **`flex-shrink`**: Defines the ability of a flex item to shrink if necessary. It accepts a unitless value that serves as a proportion.

    ```css
    .item {
        flex-shrink: 1;
    }
    ```

4. **`flex-basis`**: Defines the default size of an element before the remaining space is distributed. It can be a length (e.g., `20%`, `5rem`) or `auto`.

    ```css
    .item {
        flex-basis: 100px;
    }
    ```

5. **`flex`**: A shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`.

    ```css
    .item {
        flex: 1 1 100px;
    }
    ```

6. **`align-self`**: Allows the default alignment (or the one specified by `align-items`) to be overridden for individual flex items.

    ```css
    .item {
        align-self: flex-end;
    }
    ```

## Common use cases for CSS Flexbox include:

1. **Centering Elements**: Flexbox makes it easy to center elements both horizontally and vertically.

2. **Creating Responsive Layouts**: Flexbox allows for flexible and responsive layouts that adapt to different screen sizes.

3. **Equal Height Columns**: Flexbox can be used to create columns that are equal in height, regardless of their content.

4. **Navigation Menus**: Flexbox is useful for creating horizontal and vertical navigation menus that are easy to align and distribute.

5. **Reordering Elements**: Flexbox allows for easy reordering of elements without changing the HTML structure.

6. **Distributing Space**: Flexbox can distribute space between items evenly, making it useful for creating grids and galleries.

7. **Sticky Footers**: Flexbox can be used to create sticky footers that stay at the bottom of the page regardless of the content height.

8. **Form Layouts**: Flexbox is useful for creating flexible and responsive form layouts.

These use cases leverage the flexibility and alignment capabilities of Flexbox to create modern, responsive web designs.

## Example

Here is a simple example demonstrating the use of Flexbox:

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .container {
            display: flex;
            flex-direction: row;
            justify-content: space-around;
            align-items: center;
            height: 100vh;
        }
        .item {
            background-color: lightblue;
            padding: 20px;
            margin: 10px;
        }
    </style>
</head>
<body>
<div class="container">
    <div class="item">Item 1</div>
    <div class="item">Item 2</div>
    <div class="item">Item 3</div>
</div>
</body>
</html>
```

In this example:
- The container is a flex container with items laid out in a row.
- The items are evenly distributed along the main axis with space around them.
- The items are centered along the cross axis.