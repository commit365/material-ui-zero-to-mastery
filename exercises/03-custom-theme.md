# Exercise: Customizing a Theme in Material UI

## Objective

In this exercise, you will create a custom theme for a Material UI application. You'll learn how to modify various aspects of the default theme, including colors, typography, spacing, and component styles. You'll also implement a dark mode toggle and create custom component variants.

## Prerequisites

- Completion of the "Creating a Responsive Layout" exercise
- Solid understanding of React hooks and Material UI basics
- Node.js and npm installed on your machine

## Setup

1. **Create a new React project with TypeScript** (if you haven't already):

   ```bash
   npx create-react-app my-custom-theme --template typescript
   cd my-custom-theme
   ```

2. **Install Material UI and its dependencies**:

   ```bash
   npm install @mui/material @emotion/react @emotion/styled
   ```

3. **Open the project in your code editor**.

## Part 1: Creating a Custom Theme

### 1. Define Your Custom Theme

1. Create a new file called `theme.ts` in the `src` folder.

2. In `theme.ts`, import the necessary functions from Material UI:

   ```typescript
   import { createTheme } from "@mui/material/styles";
   ```

3. Create a custom theme:

   ```typescript
   const theme = createTheme({
     palette: {
       primary: {
         main: "#1976d2",
         light: "#42a5f5",
         dark: "#115293",
         contrastText: "#ffffff",
       },
       secondary: {
         main: "#9c27b0",
         light: "#ba68c8",
         dark: "#7b1fa2",
         contrastText: "#ffffff",
       },
       background: {
         default: "#f5f5f5",
         paper: "#ffffff",
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

   export default theme;
   ```

## Part 2: Applying the Theme

### 1. Wrap Your Application with ThemeProvider

1. Open `src/App.tsx` and import the `ThemeProvider` from Material UI:

   ```typescript
   import React from "react";
   import { ThemeProvider, CssBaseline } from "@mui/material";
   import theme from "./theme"; // Import your custom theme
   import MyComponent from "./MyComponent"; // Example component
   ```

2. Wrap your application with `ThemeProvider`:

   ```typescript
   const App: React.FC = () => {
     return (
       <ThemeProvider theme={theme}>
         <CssBaseline />
         <MyComponent />
       </ThemeProvider>
     );
   };

   export default App;
   ```

## Part 3: Implementing Dark Mode

### 1. Adding Dark Mode Toggle

1. Modify `App.tsx` to include a dark mode toggle:

   ```typescript
   import React, { useState, useMemo } from "react";
   import {
     ThemeProvider,
     CssBaseline,
     Switch,
     AppBar,
     Toolbar,
     Typography,
   } from "@mui/material";
   import { createTheme } from "@mui/material/styles";
   import theme from "./theme"; // Import your custom theme

   const App: React.FC = () => {
     const [darkMode, setDarkMode] = useState<boolean>(false);

     const appliedTheme = useMemo(
       () =>
         createTheme({
           ...theme,
           palette: {
             ...theme.palette,
             mode: darkMode ? "dark" : "light",
           },
         }),
       [darkMode]
     );

     return (
       <ThemeProvider theme={appliedTheme}>
         <CssBaseline />
         <AppBar position="static">
           <Toolbar>
             <Typography variant="h6" sx={{ flexGrow: 1 }}>
               My Themed App
             </Typography>
             <Switch
               checked={darkMode}
               onChange={() => setDarkMode(!darkMode)}
             />
           </Toolbar>
         </AppBar>
         <MyComponent />
       </ThemeProvider>
     );
   };

   export default App;
   ```

## Part 4: Customizing Component Styles

### 1. Creating Custom Variants for Components

1. Open `theme.ts` and add custom styles for specific components:

   ```typescript
   const theme = createTheme({
     // ... existing theme configuration
     components: {
       MuiButton: {
         styleOverrides: {
           root: {
             textTransform: "none",
             borderRadius: 8,
           },
           contained: {
             boxShadow: "none",
             "&:hover": {
               boxShadow: "none",
             },
           },
         },
         variants: [
           {
             props: { variant: "gradient" },
             style: {
               background: "linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%)",
               border: 0,
               color: "white",
               height: 48,
               padding: "0 30px",
               boxShadow: "0 3px 5px 2px rgba(255, 105, 135, .3)",
             },
           },
         ],
       },
     },
   });
   ```

## Part 5: Implementing Global Styles

### 1. Using GlobalStyles Component

1. Open `App.tsx` and import the `GlobalStyles` component:

   ```typescript
   import { GlobalStyles } from "@mui/material";
   ```

2. Add the `GlobalStyles` component to your application:

   ```typescript
   const App: React.FC = () => {
     return (
       <ThemeProvider theme={appliedTheme}>
         <CssBaseline />
         <GlobalStyles
           styles={{
             body: { backgroundColor: darkMode ? "#121212" : "#f5f5f5" },
           }}
         />
         <AppBar position="static">
           <Toolbar>
             <Typography variant="h6" sx={{ flexGrow: 1 }}>
               My Themed App
             </Typography>
             <Switch
               checked={darkMode}
               onChange={() => setDarkMode(!darkMode)}
             />
           </Toolbar>
         </AppBar>
         <MyComponent />
       </ThemeProvider>
     );
   };
   ```

## Conclusion

In this exercise, you created a custom theme for your Material UI application using React with TypeScript. You learned how to modify various aspects of the default theme, including colors, typography, spacing, and component styles. Additionally, you implemented a dark mode toggle and created custom component variants.

This foundational knowledge will help you create visually appealing and consistent user interfaces in your applications. In the next lesson, we will explore advanced styling techniques and how to integrate animations into your components.

## [Next: 04-accessibility-audit](./04-accessibility-audit.md)
