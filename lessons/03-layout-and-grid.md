# Layout and Grid System in Material UI

In this lesson, we'll dive deep into Material UI's layout components and grid system. Understanding these concepts is crucial for creating responsive, well-structured user interfaces using React with TypeScript.

## 1. The Grid Component

Material UI's Grid component uses CSS's Flexbox module for high flexibility. It's a two-dimensional system, meaning it can handle both columns and rows.

### Basic Grid Structure

```typescript
import React from "react";
import { Grid } from "@mui/material";

const BasicGrid: React.FC = () => {
  return (
    <Grid container spacing={2}>
      <Grid item xs={12} sm={6} md={4}>
        <div>Item 1</div>
      </Grid>
      <Grid item xs={12} sm={6} md={4}>
        <div>Item 2</div>
      </Grid>
      <Grid item xs={12} sm={6} md={4}>
        <div>Item 3</div>
      </Grid>
    </Grid>
  );
};

export default BasicGrid;
```

**Key concepts:**

- `container`: Defines a grid container.
- `item`: Defines a grid item.
- `spacing`: Sets the space between grid items.
- `xs`, `sm`, `md`, `lg`, `xl`: Responsive breakpoints.

### Grid Properties

1. **Direction**:

   ```typescript
   <Grid container direction="row" | "row-reverse" | "column" | "column-reverse">
   ```

2. **Justification**:

   ```typescript
   <Grid container justifyContent="flex-start" | "center" | "flex-end" | "space-between" | "space-around">
   ```

3. **Alignment**:

   ```typescript
   <Grid container alignItems="flex-start" | "center" | "flex-end" | "stretch" | "baseline">
   ```

### Responsive Design

```typescript
<Grid item xs={12} sm={6} md={4} lg={3} xl={2}>
  <div>Responsive Item</div>
</Grid>
```

This item will occupy:

- 12 columns on extra-small screens
- 6 columns on small screens
- 4 columns on medium screens
- 3 columns on large screens
- 2 columns on extra-large screens

### Nested Grids

Grids can be nested for complex layouts:

```typescript
<Grid container spacing={2}>
  <Grid item xs={12} sm={6}>
    <Grid container spacing={1}>
      <Grid item xs={6}>
        <div>Nested Item 1</div>
      </Grid>
      <Grid item xs={6}>
        <div>Nested Item 2</div>
      </Grid>
    </Grid>
  </Grid>
  <Grid item xs={12} sm={6}>
    <div>Main Item 2</div>
  </Grid>
</Grid>
```

## 2. Containers

The Container component is used to center your content horizontally. It's the most basic layout element.

```typescript
import React from "react";
import { Container, Typography } from "@mui/material";

const MyContainer: React.FC = () => {
  return (
    <Container maxWidth="sm">
      <Typography variant="h4" component="h1" gutterBottom>
        Centered Content
      </Typography>
      <Typography variant="body1">
        This content is centered within a container with a maximum width of
        'sm'.
      </Typography>
    </Container>
  );
};

export default MyContainer;
```

**Key properties:**

- `maxWidth`: "xs", "sm", "md", "lg", "xl", or false (for full width).
- `fixed`: Boolean. If true, the container will have a fixed max-width for each breakpoint.

## 3. Box Component

The Box component serves as a wrapper component for most of the CSS utility needs. It's highly customizable and can be used for layout, spacing, and more.

```typescript
import React from "react";
import { Box, Typography } from "@mui/material";

const MyBox: React.FC = () => {
  return (
    <Box
      sx={{
        width: 300,
        height: 300,
        backgroundColor: "primary.main",
        "&:hover": {
          backgroundColor: "primary.light",
          opacity: [0.9, 0.8, 0.7],
        },
      }}
    >
      <Typography color="white" p={2}>
        This is a customized box
      </Typography>
    </Box>
  );
};

export default MyBox;
```

The `sx` prop allows you to define custom styles using the theme.

## 4. Spacing and Alignment

Material UI provides a built-in spacing system that can be used with the `sx` prop or with specific spacing props.

### Margin and Padding

```typescript
<Box
  sx={{
    m: 2, // margin: theme.spacing(2)
    p: 2, // padding: theme.spacing(2)
  }}
>
  Content with margin and padding
</Box>
```

You can also use specific directional spacing:

```typescript
<Box
  sx={{
    mt: 2, // margin-top
    mb: 3, // margin-bottom
    pl: 1, // padding-left
    pr: 1, // padding-right
  }}
>
  Content with specific spacing
</Box>
```

### Alignment

For alignment, you can use Flexbox properties:

```typescript
<Box
  sx={{
    display: "flex",
    alignItems: "center",
    justifyContent: "space-between",
  }}
>
  <Typography>Left aligned</Typography>
  <Typography>Right aligned</Typography>
</Box>
```

## 5. Responsive Design Techniques

### Hidden Component

The Hidden component allows you to hide elements based on the current breakpoint:

```typescript
import { Hidden } from "@mui/material";

const MyComponent: React.FC = () => {
  return (
    <Hidden smDown>
      <Typography>This is hidden on small screens and down</Typography>
    </Hidden>
  );
};

export default MyComponent;
```

### useMediaQuery Hook

For more complex responsive logic, use the `useMediaQuery` hook:

```typescript
import React from "react";
import { useMediaQuery } from "@mui/material";
import { useTheme } from "@mui/material/styles";

const ResponsiveComponent: React.FC = () => {
  const theme = useTheme();
  const isSmallScreen = useMediaQuery(theme.breakpoints.down("sm"));

  return (
    <div>
      {isSmallScreen ? (
        <Typography>Small screen content</Typography>
      ) : (
        <Typography>Large screen content</Typography>
      )}
    </div>
  );
};

export default ResponsiveComponent;
```

## Conclusion

Mastering Material UI's layout and grid system is essential for creating responsive and well-structured applications. The Grid component provides a powerful tool for creating complex layouts, while Containers and Boxes offer additional control over spacing and alignment. By combining these components with responsive design techniques, you can create UIs that look great on any device.

Remember to always consider the user experience across different screen sizes when designing your layouts. In the next lesson, we'll explore how to further customize the appearance of your components through theming and styling.

### [Next: 04-styling-and-theming](./04-styling-and-theming.md)
