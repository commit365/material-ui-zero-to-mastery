# Styling and Theming in Material UI

In this lesson, we'll dive deep into Material UI's powerful styling and theming capabilities. We'll explore how to customize components using the `sx` prop, create and apply custom themes, and implement global styles for consistent design across your application using React with TypeScript.

## 1. The `sx` Prop

The `sx` prop is a powerful tool for inline styling in Material UI. It allows you to apply custom styles directly to components using a shorthand syntax.

### Basic Usage

```typescript
import React from "react";
import { Box, Typography } from "@mui/material";

const SxExample: React.FC = () => {
  return (
    <Box
      sx={{
        width: 300,
        height: 100,
        backgroundColor: "primary.main",
        "&:hover": {
          backgroundColor: "primary.light",
        },
      }}
    >
      <Typography sx={{ color: "white", p: 2 }}>Styled with sx prop</Typography>
    </Box>
  );
};

export default SxExample;
```

### Advanced `sx` Usage

The `sx` prop supports various CSS properties, pseudo-selectors, and even responsive styles:

```typescript
<Box
  sx={{
    width: { xs: "100%", sm: "50%", md: "25%" },
    p: 2,
    m: 1,
    textAlign: "center",
    color: (theme) => theme.palette.text.primary,
    border: (theme) => `1px solid ${theme.palette.primary.main}`,
    borderRadius: 2,
    fontSize: "0.875rem",
    fontWeight: 700,
    "&:hover": {
      backgroundColor: "primary.main",
      color: "white",
    },
  }}
>
  Advanced sx styling
</Box>
```

## 2. Creating and Applying Custom Themes

Material UI's theming system allows you to customize the look and feel of your entire application.

### Creating a Custom Theme

```typescript
import { createTheme } from "@mui/material/styles";

const theme = createTheme({
  palette: {
    primary: {
      main: "#1976d2",
      light: "#42a5f5",
      dark: "#1565c0",
      contrastText: "#ffffff",
    },
    secondary: {
      main: "#9c27b0",
      light: "#ba68c8",
      dark: "#7b1fa2",
      contrastText: "#ffffff",
    },
  },
  typography: {
    fontFamily: "Roboto, Arial, sans-serif",
    h1: {
      fontSize: "2.5rem",
      fontWeight: 500,
    },
    body1: {
      fontSize: "1rem",
      lineHeight: 1.5,
    },
  },
  shape: {
    borderRadius: 8,
  },
  spacing: 8,
});
```

### Applying the Theme

To apply the theme to your entire application, use the `ThemeProvider` component:

```typescript
import React from "react";
import { ThemeProvider } from "@mui/material/styles";
import CssBaseline from "@mui/material/CssBaseline";
import App from "./App";
import theme from "./theme"; // Import your custom theme

const ThemedApp: React.FC = () => {
  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <App />
    </ThemeProvider>
  );
};

export default ThemedApp;
```

The `CssBaseline` component normalizes styles across browsers and applies some base styles from your theme.

### Accessing Theme in Components

You can access the theme in your components using the `useTheme` hook:

```typescript
import React from "react";
import { useTheme } from "@mui/material/styles";
import { Typography } from "@mui/material";

const ThemedComponent: React.FC = () => {
  const theme = useTheme();
  return (
    <Typography style={{ color: theme.palette.primary.main }}>
      This text uses the primary color from the theme
    </Typography>
  );
};

export default ThemedComponent;
```

## 3. Implementing Global Styles

Global styles can be implemented using the `GlobalStyles` component or by creating a custom `GlobalStyles` component.

### Using the GlobalStyles Component

```typescript
import React from "react";
import { GlobalStyles } from "@mui/material";

const MyGlobalStyles: React.FC = () => {
  return (
    <GlobalStyles
      styles={{
        body: {
          backgroundColor: "#f0f0f0",
        },
        ".custom-class": {
          color: "red",
          fontSize: "1.2rem",
        },
      }}
    />
  );
};

export default MyGlobalStyles;
```

### Creating a Custom GlobalStyles Component

For more complex global styles, you can create a custom component:

```typescript
import React from "react";
import { Global, css } from "@emotion/react";
import { useTheme } from "@mui/material/styles";

const CustomGlobalStyles: React.FC = () => {
  const theme = useTheme();
  return (
    <Global
      styles={css`
        body {
          background-color: ${theme.palette.background.default};
          color: ${theme.palette.text.primary};
        }
        a {
          color: ${theme.palette.primary.main};
          text-decoration: none;
          &:hover {
            text-decoration: underline;
          }
        }
        .custom-scrollbar {
          &::-webkit-scrollbar {
            width: 8px;
          }
          &::-webkit-scrollbar-thumb {
            background-color: ${theme.palette.primary.main};
            border-radius: 4px;
          }
        }
      `}
    />
  );
};

export default CustomGlobalStyles;
```

## 4. Advanced Theming Techniques

### Theme Nesting

You can nest themes for different sections of your application:

```typescript
import React from "react";
import { ThemeProvider, createTheme } from "@mui/material/styles";
import { Button } from "@mui/material";

const NestedThemeExample: React.FC = () => {
  const outerTheme = createTheme({
    palette: {
      primary: { main: "#1976d2" },
    },
  });

  const innerTheme = createTheme({
    palette: {
      primary: { main: "#9c27b0" },
    },
  });

  return (
    <ThemeProvider theme={outerTheme}>
      <Button color="primary">Outer Theme Button</Button>
      <ThemeProvider theme={innerTheme}>
        <Button color="primary">Inner Theme Button</Button>
      </ThemeProvider>
    </ThemeProvider>
  );
};

export default NestedThemeExample;
```

### Dynamic Theming

You can implement dynamic theming, such as a dark mode toggle:

```typescript
import React, { useState, useMemo } from "react";
import { ThemeProvider, createTheme } from "@mui/material/styles";
import { CssBaseline, Switch, Paper } from "@mui/material";

const DynamicThemeExample: React.FC = () => {
  const [darkMode, setDarkMode] = useState<boolean>(false);

  const theme = useMemo(
    () =>
      createTheme({
        palette: {
          mode: darkMode ? "dark" : "light",
        },
      }),
    [darkMode]
  );

  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <Paper sx={{ height: "100vh", p: 2 }}>
        <Switch checked={darkMode} onChange={() => setDarkMode(!darkMode)} />
        <p>Toggle dark mode</p>
      </Paper>
    </ThemeProvider>
  );
};

export default DynamicThemeExample;
```

## Conclusion

Mastering styling and theming in Material UI allows you to create unique, consistent, and responsive user interfaces. The `sx` prop provides a powerful way to apply styles inline, while custom themes enable you to maintain a consistent look and feel across your entire application. Global styles help you set base styles and create custom utility classes.

Remember that good design is not just about aesthetics but also about usability and accessibility. Always consider how your styling choices affect the user experience across different devices and for users with different needs.

In the next lesson, we'll put these concepts into practice by building a complete dashboard project, integrating various components and applying custom styling and theming.

### [Next: 05-dashboard-project](./05-dashboard-project.md)
