# E-commerce Challenge: Designing a Product Card Component

In this lesson, you will design a product card component using Material UI and React with TypeScript. This component will display product information and will be responsive and accessible. By the end of this challenge, you will have a fully functional product card that you can showcase in your GitHub repository.

## Challenge Overview

### Features

1. Display product image, title, description, price, and an "Add to Cart" button.
2. Ensure the component is responsive across different screen sizes.
3. Implement accessibility features, including ARIA roles and properties.
4. Use TypeScript for type safety and better development experience.

## 1. Setting Up Your Environment

### Prerequisites

- Ensure you have Node.js and npm installed on your machine.
- Basic knowledge of React and TypeScript.

### Step-by-Step Setup

1. **Create a new React project with TypeScript** (if you haven't already):

   ```bash
   npx create-react-app my-ecommerce-app --template typescript
   cd my-ecommerce-app
   ```

2. **Install Material UI and its dependencies**:

   ```bash
   npm install @mui/material @emotion/react @emotion/styled @mui/icons-material
   ```

3. **Create the Product Card Component**:

   Create a new file named `ProductCard.tsx` in the `src/components` directory:

   ```
   src/
   ├── components/
   │   ├── ProductCard.tsx
   ```

## 2. Designing the Product Card Component

### ProductCard Component Structure

Here’s how to structure the `ProductCard` component:

```typescript
// src/components/ProductCard.tsx
import React from "react";
import {
  Card,
  CardMedia,
  CardContent,
  CardActions,
  Typography,
  Button,
} from "@mui/material";

interface ProductCardProps {
  image: string;
  title: string;
  description: string;
  price: number;
  onAddToCart: () => void;
}

const ProductCard: React.FC<ProductCardProps> = ({
  image,
  title,
  description,
  price,
  onAddToCart,
}) => {
  return (
    <Card sx={{ maxWidth: 345, margin: 2 }}>
      <CardMedia component="img" height="140" image={image} alt={title} />
      <CardContent>
        <Typography variant="h5" component="div">
          {title}
        </Typography>
        <Typography variant="body2" color="text.secondary">
          {description}
        </Typography>
        <Typography variant="h6" color="primary">
          ${price.toFixed(2)}
        </Typography>
      </CardContent>
      <CardActions>
        <Button
          size="small"
          onClick={onAddToCart}
          aria-label={`Add ${title} to cart`}
        >
          Add to Cart
        </Button>
      </CardActions>
    </Card>
  );
};

export default ProductCard;
```

### Key Features of the ProductCard Component

- **Props**: The component accepts props for the product image, title, description, price, and a function to handle adding the product to the cart.
- **Accessibility**: The button has an `aria-label` for screen readers, ensuring users with disabilities can understand its purpose.
- **Responsive Design**: The Card component is responsive by default and adapts to different screen sizes.

## 3. Implementing the Product Card in a Dashboard

### Creating a Product List Component

Next, create a `ProductList.tsx` component to showcase multiple product cards.

```typescript
// src/components/ProductList.tsx
import React from "react";
import { Grid } from "@mui/material";
import ProductCard from "./ProductCard";

const products = [
  {
    id: 1,
    image: "https://via.placeholder.com/150",
    title: "Product 1",
    description: "Description for Product 1",
    price: 29.99,
  },
  {
    id: 2,
    image: "https://via.placeholder.com/150",
    title: "Product 2",
    description: "Description for Product 2",
    price: 39.99,
  },
  {
    id: 3,
    image: "https://via.placeholder.com/150",
    title: "Product 3",
    description: "Description for Product 3",
    price: 49.99,
  },
];

const ProductList: React.FC = () => {
  const handleAddToCart = (title: string) => {
    console.log(`${title} added to cart`);
  };

  return (
    <Grid container spacing={2}>
      {products.map((product) => (
        <Grid item xs={12} sm={6} md={4} key={product.id}>
          <ProductCard
            image={product.image}
            title={product.title}
            description={product.description}
            price={product.price}
            onAddToCart={() => handleAddToCart(product.title)}
          />
        </Grid>
      ))}
    </Grid>
  );
};

export default ProductList;
```

### Integrating ProductList in App Component

Finally, integrate the `ProductList` component in your `App.tsx` file:

```typescript
// src/App.tsx
import React from "react";
import { ThemeProvider, CssBaseline } from "@mui/material";
import { createAppTheme } from "./theme"; // Import your custom theme
import ProductList from "./components/ProductList";

const App: React.FC = () => {
  const theme = createAppTheme("light"); // You can change this to "dark" for dark mode

  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <ProductList />
    </ThemeProvider>
  );
};

export default App;
```

## 4. Running Your Project

1. Start your application:

   ```bash
   npm start
   ```

2. Open your browser and navigate to `http://localhost:3000` to see your product cards in action.

## 5. Ensuring Responsiveness and Accessibility

### Responsive Design

The `Grid` component ensures that the product cards are responsive. Each card will stack on smaller screens and arrange in a grid on larger screens.

### Accessibility Considerations

- Ensure all interactive elements are focusable and have appropriate labels.
- Use semantic HTML where possible.
- Test the application with screen readers to ensure that all content is accessible.

## Conclusion

In this challenge, you designed a product card component using Material UI and React with TypeScript. You ensured that the component is responsive and adheres to accessibility standards. This project demonstrates your ability to create functional and user-friendly components in a real-world application.

In the next lesson, we will explore how to further enhance our e-commerce application by implementing additional features and best practices.

### [Next: 08-final-project](./08-final-project.md)
