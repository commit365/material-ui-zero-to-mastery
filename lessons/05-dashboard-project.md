# Dashboard Project: Building a Responsive Dashboard with Material UI

In this lesson, we will build a responsive dashboard using Material UI and React with TypeScript. This project will integrate various components learned in previous lessons and implement a dark mode toggle feature using theming. By the end of this lesson, you will have a fully functional dashboard that demonstrates your understanding of Material UI's capabilities.

## Project Overview

### Features

1. Responsive layout using Material UI's Grid system.
2. AppBar with navigation and a dark mode toggle.
3. Sidebar for navigation links.
4. Main content area displaying cards and charts.
5. Dark mode toggle to switch between light and dark themes.

## 1. Setting Up the Project

### Prerequisites

- Ensure you have Node.js and npm installed on your machine.
- Basic knowledge of React and TypeScript.

### Step-by-Step Setup

1. **Create a new React project with TypeScript**:

   ```bash
   npx create-react-app my-dashboard --template typescript
   cd my-dashboard
   ```

2. **Install Material UI and its dependencies**:

   ```bash
   npm install @mui/material @emotion/react @emotion/styled @mui/icons-material recharts
   ```

3. **Set up the project structure**:

   Create the following folder structure:

   ```
   src/
   ├── components/
   │   ├── AppBar.tsx
   │   ├── Sidebar.tsx
   │   ├── Dashboard.tsx
   │   ├── Chart.tsx
   │   └── DataCard.tsx
   ├── theme.ts
   ├── App.tsx
   └── index.tsx
   ```

## 2. Creating the Theme

Create a `theme.ts` file to define your custom theme:

```typescript
// src/theme.ts
import { createTheme } from "@mui/material/styles";

export const createAppTheme = (mode: "light" | "dark") =>
  createTheme({
    palette: {
      mode,
      ...(mode === "light"
        ? {
            primary: {
              main: "#1976d2",
            },
            secondary: {
              main: "#dc004e",
            },
            background: {
              default: "#f5f5f5",
              paper: "#ffffff",
            },
          }
        : {
            primary: {
              main: "#90caf9",
            },
            secondary: {
              main: "#f48fb1",
            },
            background: {
              default: "#303030",
              paper: "#424242",
            },
          }),
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
  });
```

## 3. Creating the AppBar Component

Create an `AppBar.tsx` component for the top navigation:

```typescript
// src/components/AppBar.tsx
import React from "react";
import { AppBar, Toolbar, Typography, IconButton, Switch } from "@mui/material";
import MenuIcon from "@mui/icons-material/Menu";

interface AppBarProps {
  darkMode: boolean;
  toggleDarkMode: () => void;
}

const MyAppBar: React.FC<AppBarProps> = ({ darkMode, toggleDarkMode }) => {
  return (
    <AppBar position="static">
      <Toolbar>
        <IconButton edge="start" color="inherit" aria-label="menu">
          <MenuIcon />
        </IconButton>
        <Typography variant="h6" sx={{ flexGrow: 1 }}>
          My Dashboard
        </Typography>
        <Switch checked={darkMode} onChange={toggleDarkMode} />
      </Toolbar>
    </AppBar>
  );
};

export default MyAppBar;
```

## 4. Creating the Sidebar Component

Create a `Sidebar.tsx` component for navigation links:

```typescript
// src/components/Sidebar.tsx
import React from "react";
import { Drawer, List, ListItem, ListItemText } from "@mui/material";

interface SidebarProps {
  open: boolean;
  onClose: () => void;
}

const MySidebar: React.FC<SidebarProps> = ({ open, onClose }) => {
  return (
    <Drawer anchor="left" open={open} onClose={onClose}>
      <List>
        {["Home", "Profile", "Settings"].map((text) => (
          <ListItem button key={text}>
            <ListItemText primary={text} />
          </ListItem>
        ))}
      </List>
    </Drawer>
  );
};

export default MySidebar;
```

## 5. Creating the Dashboard Component

Create a `Dashboard.tsx` component to display the main content:

```typescript
// src/components/Dashboard.tsx
import React from "react";
import { Grid } from "@mui/material";
import DataCard from "./DataCard";
import Chart from "./Chart";

const Dashboard: React.FC = () => {
  return (
    <main>
      <Grid container spacing={3}>
        <Grid item xs={12} md={6}>
          <DataCard title="Total Users" value="1,234" />
        </Grid>
        <Grid item xs={12} md={6}>
          <DataCard title="Revenue" value="$5,678" />
        </Grid>
        <Grid item xs={12}>
          <Chart />
        </Grid>
      </Grid>
    </main>
  );
};

export default Dashboard;
```

## 6. Creating the DataCard Component

Create a `DataCard.tsx` component to display individual data metrics:

```typescript
// src/components/DataCard.tsx
import React from "react";
import { Paper, Typography } from "@mui/material";

interface DataCardProps {
  title: string;
  value: string;
}

const DataCard: React.FC<DataCardProps> = ({ title, value }) => {
  return (
    <Paper
      sx={{ p: 2, display: "flex", flexDirection: "column", height: "100%" }}
    >
      <Typography variant="h6" component="h2">
        {title}
      </Typography>
      <Typography variant="h4">{value}</Typography>
    </Paper>
  );
};

export default DataCard;
```

## 7. Creating the Chart Component

Create a `Chart.tsx` component using Recharts for data visualization:

```typescript
// src/components/Chart.tsx
import React from "react";
import {
  LineChart,
  Line,
  XAxis,
  YAxis,
  CartesianGrid,
  Tooltip,
  ResponsiveContainer,
} from "recharts";

const data = [
  { name: "Jan", value: 400 },
  { name: "Feb", value: 300 },
  { name: "Mar", value: 600 },
  { name: "Apr", value: 800 },
  { name: "May", value: 500 },
  { name: "Jun", value: 700 },
];

const Chart: React.FC = () => {
  return (
    <ResponsiveContainer width="100%" height={300}>
      <LineChart data={data}>
        <CartesianGrid strokeDasharray="3 3" />
        <XAxis dataKey="name" />
        <YAxis />
        <Tooltip />
        <Line type="monotone" dataKey="value" stroke="#8884d8" />
      </LineChart>
    </ResponsiveContainer>
  );
};

export default Chart;
```

## 8. Putting It All Together in App Component

Now, integrate all components in the `App.tsx` file:

```typescript
// src/App.tsx
import React, { useState } from "react";
import { ThemeProvider, CssBaseline } from "@mui/material";
import { createAppTheme } from "./theme";
import MyAppBar from "./components/AppBar";
import MySidebar from "./components/Sidebar";
import Dashboard from "./components/Dashboard";

const App: React.FC = () => {
  const [darkMode, setDarkMode] = useState<boolean>(false);
  const [sidebarOpen, setSidebarOpen] = useState<boolean>(false);
  const theme = createAppTheme(darkMode ? "dark" : "light");

  const toggleDarkMode = () => setDarkMode((prev) => !prev);
  const toggleSidebar = () => setSidebarOpen((prev) => !prev);

  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <MyAppBar darkMode={darkMode} toggleDarkMode={toggleDarkMode} />
      <MySidebar open={sidebarOpen} onClose={toggleSidebar} />
      <Dashboard />
    </ThemeProvider>
  );
};

export default App;
```

## 9. Running the Project

1. Start your application:

   ```bash
   npm start
   ```

2. Open your browser and navigate to `http://localhost:3000` to see your responsive dashboard in action.

## Conclusion

In this lesson, you built a responsive dashboard application using Material UI and React with TypeScript. You integrated various components learned in previous lessons, including the AppBar, Sidebar, DataCard, and Chart components. Additionally, you implemented a dark mode toggle feature using theming.

In the next lesson, we will explore accessibility best practices to ensure your dashboard is usable by everyone.

### [Next: 06-accessibility](./06-accessibility.md)
