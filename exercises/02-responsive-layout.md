# Exercise: Creating a Responsive Layout with Material UI

## Objective

In this exercise, you will create a responsive layout for a blog homepage using Material UI components. This will help you understand how to use Material UI's Grid system, responsive breakpoints, and various components to create a layout that adapts to different screen sizes.

## Prerequisites

- Completion of the "Your First Component" exercise
- Basic understanding of React and Material UI components
- Node.js and npm installed on your machine

## Setup

1. **Create a new React project with TypeScript**:

   ```bash
   npx create-react-app my-blog-layout --template typescript
   cd my-blog-layout
   ```

2. **Install Material UI and its dependencies**:

   ```bash
   npm install @mui/material @emotion/react @emotion/styled @mui/icons-material
   ```

3. **Open the project in your code editor**.

## Part 1: Creating the Basic Layout Structure

### 1. Create the Layout Component

1. Create a new file called `BlogLayout.tsx` in the `src/components` folder.

2. In `BlogLayout.tsx`, import the necessary Material UI components:

   ```typescript
   import React from "react";
   import {
     AppBar,
     Toolbar,
     Typography,
     Container,
     Grid,
     Paper,
   } from "@mui/material";
   ```

3. Create a functional component called `BlogLayout`:

   ```typescript
   const BlogLayout: React.FC = () => {
     return (
       <Container maxWidth="lg">
         <AppBar position="static">
           <Toolbar>
             <Typography variant="h6" component="div" sx={{ flexGrow: 1 }}>
               My Blog
             </Typography>
           </Toolbar>
         </AppBar>
         <Grid container spacing={3} sx={{ marginTop: 2 }}>
           <Grid item xs={12} md={8}>
             <Paper sx={{ padding: 2 }}>Main Content Area</Paper>
           </Grid>
           <Grid item xs={12} md={4}>
             <Paper sx={{ padding: 2 }}>Sidebar</Paper>
           </Grid>
         </Grid>
       </Container>
     );
   };

   export default BlogLayout;
   ```

### 2. Integrate the Layout in App Component

1. In `src/App.tsx`, import and use the `BlogLayout` component:

   ```typescript
   import React from "react";
   import BlogLayout from "./components/BlogLayout";

   const App: React.FC = () => {
     return (
       <div>
         <BlogLayout />
       </div>
     );
   };

   export default App;
   ```

2. Run your app with `npm start` and verify that the layout appears with an AppBar, a main content area, and a sidebar.

## Part 2: Adding Responsive Content

### 1. Create Blog Post Cards

1. Create a new file called `BlogPostCard.tsx` in the `src/components` folder.

2. In `BlogPostCard.tsx`, import the necessary Material UI components:

   ```typescript
   import React from "react";
   import { Card, CardContent, Typography } from "@mui/material";

   interface BlogPostCardProps {
     title: string;
     excerpt: string;
   }

   const BlogPostCard: React.FC<BlogPostCardProps> = ({ title, excerpt }) => {
     return (
       <Card sx={{ marginBottom: 2 }}>
         <CardContent>
           <Typography variant="h5" component="div">
             {title}
           </Typography>
           <Typography variant="body2" color="text.secondary">
             {excerpt}
           </Typography>
         </CardContent>
       </Card>
     );
   };

   export default BlogPostCard;
   ```

### 2. Update the Blog Layout to Include Blog Posts

1. Update the `BlogLayout.tsx` to include multiple `BlogPostCard` components:

   ```typescript
   import BlogPostCard from "./BlogPostCard";

   const BlogLayout: React.FC = () => {
     return (
       <Container maxWidth="lg">
         <AppBar position="static">
           <Toolbar>
             <Typography variant="h6" component="div" sx={{ flexGrow: 1 }}>
               My Blog
             </Typography>
           </Toolbar>
         </AppBar>
         <Grid container spacing={3} sx={{ marginTop: 2 }}>
           <Grid item xs={12} md={8}>
             <Paper sx={{ padding: 2 }}>
               <Typography variant="h4" component="h2" gutterBottom>
                 Blog Posts
               </Typography>
               <BlogPostCard
                 title="Post 1"
                 excerpt="This is the excerpt for post 1."
               />
               <BlogPostCard
                 title="Post 2"
                 excerpt="This is the excerpt for post 2."
               />
               <BlogPostCard
                 title="Post 3"
                 excerpt="This is the excerpt for post 3."
               />
             </Paper>
           </Grid>
           <Grid item xs={12} md={4}>
             <Paper sx={{ padding: 2 }}>Sidebar</Paper>
           </Grid>
         </Grid>
       </Container>
     );
   };
   ```

## Part 3: Adding Responsive Design Features

### 1. Adjusting the Layout for Smaller Screens

1. Modify the `Grid` component in `BlogLayout.tsx` to ensure that it stacks correctly on smaller screens:

   ```typescript
   <Grid container spacing={3} sx={{ marginTop: 2 }}>
     <Grid item xs={12} md={8}>
       <Paper sx={{ padding: 2 }}>
         <Typography variant="h4" component="h2" gutterBottom>
           Blog Posts
         </Typography>
         <BlogPostCard
           title="Post 1"
           excerpt="This is the excerpt for post 1."
         />
         <BlogPostCard
           title="Post 2"
           excerpt="This is the excerpt for post 2."
         />
         <BlogPostCard
           title="Post 3"
           excerpt="This is the excerpt for post 3."
         />
       </Paper>
     </Grid>
     <Grid item xs={12} md={4}>
       <Paper sx={{ padding: 2 }}>Sidebar</Paper>
     </Grid>
   </Grid>
   ```

### 2. Responsive Typography

1. Ensure that typography scales appropriately on different screen sizes:

   ```typescript
   <Typography
     variant="h4"
     component="h2"
     gutterBottom
     sx={{ fontSize: { xs: "1.5rem", md: "2rem" } }}
   >
     Blog Posts
   </Typography>
   ```

## Part 4: Testing Responsiveness

1. **Run your application** and resize the browser window to see how the layout adapts to different screen sizes.

2. **Use the browser's developer tools** to simulate different devices and ensure that the layout remains functional and visually appealing.

## Conclusion

In this exercise, you created a responsive layout for a blog homepage using Material UI and React with TypeScript. You learned how to use the Grid system to create a flexible layout, integrated various components, and ensured that your design is responsive across different screen sizes.

This foundational knowledge will serve you well as you continue to build more complex applications. In the next lesson, we will explore how to customize the appearance of your components through theming and styling.

## [Next: 03-custom-theme](./03-custom-theme.md)
