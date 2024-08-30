# Core Components in Material UI

In this lesson, we'll explore the essential components that form the backbone of Material UI applications. We'll cover navigation components, input elements, and data display components, providing you with a solid foundation for building complex user interfaces using React with TypeScript.

## 1. Navigation Components

### AppBar

The AppBar component is typically used for displaying the main navigation header of your application.

```typescript
import React from "react";
import { AppBar, Toolbar, Typography, Button, IconButton } from "@mui/material";
import MenuIcon from "@mui/icons-material/Menu";

const MyAppBar: React.FC = () => {
  return (
    <AppBar position="static">
      <Toolbar>
        <IconButton edge="start" color="inherit" aria-label="menu">
          <MenuIcon />
        </IconButton>
        <Typography variant="h6" sx={{ flexGrow: 1 }}>
          My App
        </Typography>
        <Button color="inherit">Login</Button>
      </Toolbar>
    </AppBar>
  );
};

export default MyAppBar;
```

**Key props:**

- `position`: Can be "fixed", "absolute", "sticky", or "static"
- `color`: Sets the color of the AppBar (e.g., "primary", "secondary")

### Drawer

The Drawer component is used for side navigation menus.

```typescript
import React, { useState } from "react";
import { Drawer, List, ListItem, ListItemText, Button } from "@mui/material";

const MyDrawer: React.FC = () => {
  const [open, setOpen] = useState<boolean>(false);

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

export default MyDrawer;
```

**Key props:**

- `anchor`: Determines which side the drawer appears from
- `open`: Controls the open/closed state of the drawer
- `variant`: Can be "permanent", "persistent", or "temporary"

### Buttons and Icons

Buttons are a crucial part of user interaction, while icons enhance visual communication.

```typescript
import React from "react";
import { Button, IconButton } from "@mui/material";
import DeleteIcon from "@mui/icons-material/Delete";

const ButtonsAndIcons: React.FC = () => {
  return (
    <>
      <Button variant="contained" color="primary">
        Primary Button
      </Button>
      <Button variant="outlined" color="secondary">
        Secondary Button
      </Button>
      <IconButton aria-label="delete">
        <DeleteIcon />
      </IconButton>
    </>
  );
};

export default ButtonsAndIcons;
```

**Button key props:**

- `variant`: "text", "contained", or "outlined"
- `color`: "primary", "secondary", "error", etc.
- `size`: "small", "medium", or "large"

## 2. Form Components

### TextField

TextField is used for text input in forms.

```typescript
import React, { useState } from "react";
import { TextField } from "@mui/material";

const MyTextField: React.FC = () => {
  const [value, setValue] = useState<string>("");

  return (
    <TextField
      label="Name"
      variant="outlined"
      value={value}
      onChange={(e) => setValue(e.target.value)}
      error={value === ""}
      helperText={value === "" ? "Name is required" : ""}
    />
  );
};

export default MyTextField;
```

**Key props:**

- `label`: Text label for the input
- `variant`: "outlined", "filled", or "standard"
- `error`: Boolean to indicate error state
- `helperText`: Additional helper text below the input

### Checkbox

Checkboxes allow users to select multiple options from a set.

```typescript
import React, { useState } from "react";
import { Checkbox, FormControlLabel } from "@mui/material";

const MyCheckbox: React.FC = () => {
  const [checked, setChecked] = useState<boolean>(false);

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

export default MyCheckbox;
```

**Key props:**

- `checked`: Controls the checked state
- `color`: Sets the color of the checkbox when checked

### Select

Select components are used for selecting a value from multiple options.

```typescript
import React, { useState } from "react";
import { Select, MenuItem, FormControl, InputLabel } from "@mui/material";

const MySelect: React.FC = () => {
  const [age, setAge] = useState<string>("");

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

export default MySelect;
```

**Key props:**

- `value`: The selected value
- `label`: Label for the select input
- `onChange`: Handler for value changes

## 3. Data Display Components

### Typography

Typography component is used for presenting text with consistent styling.

```typescript
import React from "react";
import { Typography } from "@mui/material";

const TextDisplay: React.FC = () => {
  return (
    <>
      <Typography variant="h1">Heading 1</Typography>
      <Typography variant="body1">
        This is a paragraph of text. It uses the body1 variant.
      </Typography>
      <Typography variant="caption" color="textSecondary">
        This is a caption with secondary color.
      </Typography>
    </>
  );
};

export default TextDisplay;
```

**Key props:**

- `variant`: Defines the text style (e.g., "h1", "body1", "caption")
- `color`: Sets the text color

### Card

Cards are surfaces that display content and actions on a single topic.

```typescript
import React from "react";
import {
  Card,
  CardContent,
  CardActions,
  Button,
  Typography,
} from "@mui/material";

const MyCard: React.FC = () => {
  return (
    <Card>
      <CardContent>
        <Typography variant="h5" component="div">
          Card Title
        </Typography>
        <Typography variant="body2" color="text.secondary">
          This is the content of the card. It can contain various elements.
        </Typography>
      </CardContent>
      <CardActions>
        <Button size="small">Learn More</Button>
      </CardActions>
    </Card>
  );
};

export default MyCard;
```

**Key components:**

- `CardContent`: Wraps the main content of the card
- `CardActions`: Contains action buttons for the card

### Lists

Lists are continuous groups of text or images.

```typescript
import React from "react";
import {
  List,
  ListItem,
  ListItemText,
  ListItemIcon,
  Divider,
} from "@mui/material";
import InboxIcon from "@mui/icons-material/Inbox";
import DraftsIcon from "@mui/icons-material/Drafts";

const MyList: React.FC = () => {
  return (
    <List component="nav">
      <ListItem button>
        <ListItemIcon>
          <InboxIcon />
        </ListItemIcon>
        <ListItemText primary="Inbox" />
      </ListItem>
      <Divider />
      <ListItem button>
        <ListItemIcon>
          <DraftsIcon />
        </ListItemIcon>
        <ListItemText primary="Drafts" />
      </ListItem>
    </List>
  );
};

export default MyList;
```

**Key components:**

- `ListItem`: Individual items in the list
- `ListItemIcon`: Icon for list items
- `ListItemText`: Text content for list items
- `Divider`: Used to separate list items

## Conclusion

These core components form the foundation of most Material UI applications. By mastering these, you'll be able to create complex and interactive user interfaces efficiently. In the next lessons, we'll explore more advanced components and learn how to customize them to fit your specific needs.

Remember to always refer to the official Material UI documentation for the most up-to-date information on component props and usage.

### [Next: 03-layout-and-grids](./03-layout-and-grid.md)
