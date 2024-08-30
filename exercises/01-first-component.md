# Exercise: Your First Material UI Component

## Objective

In this exercise, you will create your first Material UI component: a customized Button with an icon. This exercise will help you understand the basics of working with Material UI components, styling, and theming using React with TypeScript.

## Prerequisites

- Basic knowledge of React and TypeScript
- Node.js and npm installed on your machine
- A code editor of your choice

## Setup

1. **Create a new React project using Create React App with TypeScript**:

   ```bash
   npx create-react-app my-first-mui-component --template typescript
   cd my-first-mui-component
   ```

2. **Install Material UI and its icon library**:

   ```bash
   npm install @mui/material @emotion/react @emotion/styled @mui/icons-material
   ```

3. **Open the project in your code editor**.

## Part 1: Creating a Basic Button Component

1. **Create a new file called `CustomButton.tsx` in the `src` folder**.

2. **In `CustomButton.tsx`, import the necessary components**:

   ```typescript
   import React from "react";
   import Button from "@mui/material/Button";
   import SendIcon from "@mui/icons-material/Send";
   ```

3. **Create a functional component called `CustomButton`**:

   ```typescript
   interface CustomButtonProps {
     text: string;
     onClick?: () => void;
     disabled?: boolean;
   }

   const CustomButton: React.FC<CustomButtonProps> = ({
     text,
     onClick,
     disabled,
   }) => {
     return (
       <Button
         variant="contained"
         endIcon={<SendIcon />}
         onClick={onClick}
         disabled={disabled}
       >
         {text}
       </Button>
     );
   };

   export default CustomButton;
   ```

4. **In `App.tsx`, import and use your `CustomButton`**:

   ```typescript
   import React, { useState } from "react";
   import CustomButton from "./CustomButton";

   const App: React.FC = () => {
     const [clickCount, setClickCount] = useState<number>(0);

     const handleClick = () => {
       setClickCount(clickCount + 1);
     };

     return (
       <div className="App">
         <CustomButton
           text={`Clicked ${clickCount} times`}
           onClick={handleClick}
         />
       </div>
     );
   };

   export default App;
   ```

5. **Run your app with `npm start` and verify that the button appears with the "Send" text and an icon**.

## Part 2: Customizing the Button

1. **In `CustomButton.tsx`, import the `styled` function from Material UI**:

   ```typescript
   import { styled } from "@mui/material/styles";
   ```

2. **Create a styled version of the Button component**:

   ```typescript
   const StyledButton = styled(Button)(({ theme }) => ({
     backgroundColor: theme.palette.primary.main,
     color: theme.palette.common.white,
     "&:hover": {
       backgroundColor: theme.palette.primary.dark,
     },
     padding: theme.spacing(1, 2),
     borderRadius: theme.shape.borderRadius,
     textTransform: "none",
     "& .MuiButton-endIcon": {
       marginLeft: theme.spacing(1),
     },
   }));
   ```

3. **Update your `CustomButton` component to use the `StyledButton`**:

   ```typescript
   const CustomButton: React.FC<CustomButtonProps> = ({
     text,
     onClick,
     disabled,
   }) => {
     return (
       <StyledButton
         variant="contained"
         endIcon={<SendIcon />}
         onClick={onClick}
         disabled={disabled}
       >
         {text}
       </StyledButton>
     );
   };
   ```

## Part 3: Adding Props and Functionality

1. **Modify your `CustomButton` component to accept additional props**:

   ```typescript
   interface CustomButtonProps {
     text: string;
     onClick?: () => void;
     disabled?: boolean;
     loading?: boolean;
   }

   const CustomButton: React.FC<CustomButtonProps> = ({
     text,
     onClick,
     disabled,
     loading,
   }) => {
     return (
       <StyledButton
         variant="contained"
         endIcon={!loading && <SendIcon />}
         onClick={onClick}
         disabled={disabled || loading}
       >
         {loading ? <CircularProgress size={24} color="inherit" /> : text}
       </StyledButton>
     );
   };
   ```

2. **In `App.tsx`, add a loading state**:

   ```typescript
   import React, { useState } from "react";
   import CustomButton from "./CustomButton";
   import CircularProgress from "@mui/material/CircularProgress";

   const App: React.FC = () => {
     const [clickCount, setClickCount] = useState<number>(0);
     const [loading, setLoading] = useState<boolean>(false);

     const handleClick = () => {
       setLoading(true);
       setTimeout(() => {
         setClickCount(clickCount + 1);
         setLoading(false);
       }, 1000);
     };

     return (
       <div className="App">
         <CustomButton
           text={`Clicked ${clickCount} times`}
           onClick={handleClick}
           disabled={clickCount >= 10}
           loading={loading}
         />
       </div>
     );
   };

   export default App;
   ```

## Part 4: Adding Theming

1. **In `App.tsx`, import necessary theming components**:

   ```typescript
   import { ThemeProvider, createTheme } from "@mui/material/styles";
   ```

2. **Create a custom theme**:

   ```typescript
   const theme = createTheme({
     palette: {
       primary: {
         main: "#1976d2",
         dark: "#115293",
       },
     },
     shape: {
       borderRadius: 8,
     },
   });
   ```

3. **Wrap your app with `ThemeProvider`**:

   ```typescript
   const App: React.FC = () => {
     // ... (previous code)

     return (
       <ThemeProvider theme={theme}>
         <div className="App">
           <CustomButton
             text={`Clicked ${clickCount} times`}
             onClick={handleClick}
             disabled={clickCount >= 10}
             loading={loading}
           />
         </div>
       </ThemeProvider>
     );
   };
   ```

## Part 5: Adding Responsiveness

1. **In `CustomButton.tsx`, modify the `StyledButton` to be responsive**:

   ```typescript
   const StyledButton = styled(Button)(({ theme }) => ({
     // ... (previous styles)
     [theme.breakpoints.down("sm")]: {
       width: "100%",
     },
     [theme.breakpoints.up("md")]: {
       minWidth: 200,
     },
   }));
   ```

## Conclusion

In this exercise, you've created a custom Material UI Button component with the following features:

- Custom styling using the `styled` function
- Icon integration
- Props for text, click handling, and disabled state
- Custom theming
- Responsiveness
- Loading state

This exercise demonstrates how to create, customize, and use Material UI components in a React application with TypeScript. It covers important concepts such as component composition, styling, theming, responsiveness, and state management.

## Further Challenges

1. Add error handling to the button (e.g., change color when in an error state).
2. Implement different variants of the button (e.g., outlined, text) and allow switching between them.
3. Add animations to the button using Material UI's transition components.
4. Create a form that uses multiple Material UI components, including your custom button.

### [Next: 02-responsive-layout](./02-responsive-layout.md)
