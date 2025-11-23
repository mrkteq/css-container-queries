# CSS Container Queries

A responsive component that demonstrates CSS container queries, allowing styles to respond to the size of a containing element rather than the viewport. The heading dynamically changes size and color as the container height increases.

## Features

- **CSS Container Queries**: Uses `@container` queries to respond to container dimensions
- **Resizable Container**: Interactive demo with resize handles for testing

## Container Query Structure

1. **Container Context**: The `.content` element establishes a container context with `container-type: size` and `container-name: box`
2. **Responsive Rules**: The `@container box` queries check the container's height
3. **Dynamic Styling**: When height thresholds are met, different font sizes and colors are applied to the heading

