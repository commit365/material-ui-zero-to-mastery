# Material UI Comprehensive Cheat Sheet

## Installation and Setup

To get started with Material UI in a React project using TypeScript, follow these steps:

```bash
npm install @mui/material @emotion/react @emotion/styled
# or
yarn add @mui/material @emotion/react @emotion/styled
```

For icons:

```bash
npm install @mui/icons-material
# or
yarn add @mui/icons-material
```

## Basic Usage

Here’s how to use Material UI components in a React application with TypeScript:

```typescript
import React from "react";
import { Button, Typography } from "@mui/material";

const App: React.FC = () => {
  return (
    <div>
      <Typography variant="h1">Hello, Material UI!</Typography>
      <Button variant="contained" color="primary">
        Click me
      </Button>
    </div>
  );
};

export default App;
```

## Theming

You can create and apply a custom theme to your Material UI application:

```typescript
import { createTheme, ThemeProvider } from "@mui/material/styles";

const theme = createTheme({
  palette: {
    primary: {
      main: "#1976d2",
    },
    secondary: {
      main: "#dc004e",
    },
  },
  typography: {
    fontFamily: "Roboto, Arial, sans-serif",
    h1: {
      fontSize: "2.5rem",
      fontWeight: 500,
    },
  },
});

const ThemedApp: React.FC = () => {
  return (
    <ThemeProvider theme={theme}>{/* Your app components */}</ThemeProvider>
  );
};

export default ThemedApp;
```

## Styling Components

### Using the `sx` Prop

The `sx` prop allows you to apply styles directly to Material UI components:

```typescript
<Button
  sx={{
    backgroundColor: "primary.main",
    "&:hover": {
      backgroundColor: "primary.dark",
    },
  }}
>
  Styled Button
</Button>
```

### Using the `styled` API

You can create styled components using the `styled` function:

```typescript
import { styled } from "@mui/material/styles";
import Button from "@mui/material/Button";

const StyledButton = styled(Button)(({ theme }) => ({
  backgroundColor: theme.palette.primary.main,
  "&:hover": {
    backgroundColor: theme.palette.primary.dark,
  },
}));
```

## Layout Components

### Grid

Use the Grid component to create responsive layouts:

```typescript
import { Grid, Paper } from "@mui/material";

const MyGrid: React.FC = () => {
  return (
    <Grid container spacing={2}>
      <Grid item xs={12} sm={6} md={4}>
        <Paper>Content</Paper>
      </Grid>
      <Grid item xs={12} sm={6} md={4}>
        <Paper>Content</Paper>
      </Grid>
      <Grid item xs={12} sm={6} md={4}>
        <Paper>Content</Paper>
      </Grid>
    </Grid>
  );
};
```

### Box

The Box component is a versatile wrapper for layout and styling:

```typescript
import { Box } from "@mui/material";

const MyBox: React.FC = () => {
  return (
    <Box
      sx={{
        display: "flex",
        flexDirection: "column",
        alignItems: "center",
        p: 2,
        m: 1,
        bgcolor: "background.paper",
      }}
    >
      {/* Box content */}
    </Box>
  );
};
```

### Container

The Container component centers your content:

```typescript
import { Container } from "@mui/material";

const MyContainer: React.FC = () => {
  return <Container maxWidth="sm">{/* Contained content */}</Container>;
};
```

## Form Components

### TextField

Use TextField for user input:

```typescript
import { TextField } from "@mui/material";

const MyTextField: React.FC = () => {
  return (
    <TextField
      label="Username"
      variant="outlined"
      fullWidth
      margin="normal"
      error={false} // Set to true if there's an error
      helperText="" // Provide helper text if needed
    />
  );
};
```

### Select

Use Select for dropdown choices:

```typescript
import { FormControl, InputLabel, Select, MenuItem } from "@mui/material";

const MySelect: React.FC = () => {
  const [age, setAge] = React.useState<string>("");

  return (
    <FormControl fullWidth>
      <InputLabel id="age-select-label">Age</InputLabel>
      <Select
        labelId="age-select-label"
        value={age}
        label="Age"
        onChange={(e) => setAge(e.target.value)}
      >
        <MenuItem value={10}>Ten</MenuItem>
        <MenuItem value={20}>Twenty</MenuItem>
        <MenuItem value={30}>Thirty</MenuItem>
      </Select>
    </FormControl>
  );
};
```

### Checkbox

Use Checkbox for boolean options:

```typescript
import { Checkbox, FormControlLabel } from "@mui/material";

const MyCheckbox: React.FC = () => {
  const [checked, setChecked] = React.useState<boolean>(false);

  return (
    <FormControlLabel
      control={
        <Checkbox
          checked={checked}
          onChange={(e) => setChecked(e.target.checked)}
          color="primary"
        />
      }
      label="Agree to terms and conditions"
    />
  );
};
```

## Navigation Components

### AppBar and Toolbar

Create a top navigation bar:

```typescript
import { AppBar, Toolbar, Typography, Button } from "@mui/material";

const MyAppBar: React.FC = () => {
  return (
    <AppBar position="static">
      <Toolbar>
        <Typography variant="h6" sx={{ flexGrow: 1 }}>
          My Application
        </Typography>
        <Button color="inherit">Login</Button>
      </Toolbar>
    </AppBar>
  );
};
```

### Drawer

Create a side navigation menu:

```typescript
import { Drawer, List, ListItem, ListItemText } from "@mui/material";

const MyDrawer: React.FC = () => {
  const [open, setOpen] = React.useState<boolean>(false);

  return (
    <>
      <Button onClick={() => setOpen(true)}>Open Drawer</Button>
      <Drawer anchor="left" open={open} onClose={() => setOpen(false)}>
        <List>
          {["Home", "Profile", "Settings"].map((text) => (
            <ListItem button key={text}>
              <ListItemText primary={text} />
            </ListItem>
          ))}
        </List>
      </Drawer>
    </>
  );
};
```

## Data Display Components

### Table

Create a table to display data:

```typescript
import {
  TableContainer,
  Table,
  TableHead,
  TableRow,
  TableCell,
  TableBody,
  Paper,
} from "@mui/material";

const MyTable: React.FC = () => {
  const rows = [
    { name: "Dessert", calories: 200, fat: 10 },
    { name: "Ice Cream", calories: 300, fat: 15 },
  ];

  return (
    <TableContainer component={Paper}>
      <Table>
        <TableHead>
          <TableRow>
            <TableCell>Dessert</TableCell>
            <TableCell align="right">Calories</TableCell>
            <TableCell align="right">Fat (g)</TableCell>
          </TableRow>
        </TableHead>
        <TableBody>
          {rows.map((row) => (
            <TableRow key={row.name}>
              <TableCell component="th" scope="row">
                {row.name}
              </TableCell>
              <TableCell align="right">{row.calories}</TableCell>
              <TableCell align="right">{row.fat}</TableCell>
            </TableRow>
          ))}
        </TableBody>
      </Table>
    </TableContainer>
  );
};
```

### Card

Display content in a card layout:

```typescript
import { Card, CardContent, Typography } from "@mui/material";

const MyCard: React.FC = () => {
  return (
    <Card>
      <CardContent>
        <Typography variant="h5" component="div">
          Card Title
        </Typography>
        <Typography variant="body2" color="text.secondary">
          This is some content within a card.
        </Typography>
      </CardContent>
    </Card>
  );
};
```

## Feedback Components

### Dialog

Create a modal dialog:

```typescript
import {
  Dialog,
  DialogTitle,
  DialogContent,
  DialogActions,
  Button,
} from "@mui/material";

const MyDialog: React.FC<{ open: boolean; onClose: () => void }> = ({
  open,
  onClose,
}) => {
  return (
    <Dialog open={open} onClose={onClose}>
      <DialogTitle>Dialog Title</DialogTitle>
      <DialogContent>This is the dialog content.</DialogContent>
      <DialogActions>
        <Button onClick={onClose}>Close</Button>
      </DialogActions>
    </Dialog>
  );
};
```

### Snackbar

Display brief messages:

```typescript
import { Snackbar, Button } from "@mui/material";

const MySnackbar: React.FC<{ open: boolean; onClose: () => void }> = ({
  open,
  onClose,
}) => {
  return (
    <Snackbar
      anchorOrigin={{ vertical: "bottom", horizontal: "left" }}
      open={open}
      autoHideDuration={6000}
      onClose={onClose}
      message="This is a snackbar message"
      action={
        <Button color="inherit" onClick={onClose}>
          Close
        </Button>
      }
    />
  );
};
```

## Utility Functions

### useMediaQuery

Use media queries to adapt to screen sizes:

```typescript
import { useMediaQuery } from "@mui/material";
import { useTheme } from "@mui/material/styles";

const MyResponsiveComponent: React.FC = () => {
  const theme = useTheme();
  const isSmallScreen = useMediaQuery(theme.breakpoints.down("sm"));

  return <div>{isSmallScreen ? "Small Screen" : "Large Screen"}</div>;
};
```

### useTheme

Access the theme in your components:

```typescript
import { useTheme } from "@mui/material/styles";

const ThemedComponent: React.FC = () => {
  const theme = useTheme();
  return (
    <div style={{ backgroundColor: theme.palette.primary.main }}>
      Themed Component
    </div>
  );
};
```

## Best Practices

1. **Use the `sx` prop** for one-off styling needs.
2. **Create reusable styled components** using the `styled` API for frequently used custom styles.
3. **Utilize the theme** for consistent styling across your application.
4. **Take advantage of Material UI's responsive utilities** like `useMediaQuery` for creating adaptive layouts.
5. **Always provide accessible labels** and ARIA attributes for components when necessary.
6. **Use Material UI's built-in color palette** and spacing system for consistency.
7. **Leverage the power of composition** by combining Material UI components to create more complex UI elements.

This cheat sheet covers many common use cases, but Material UI offers even more components and features. Always refer to the official documentation for the most up-to-date and detailed information.
