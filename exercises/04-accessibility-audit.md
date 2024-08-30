# Exercise: Conducting an Accessibility Audit on a Material UI Application

## Objective

In this exercise, you will conduct a thorough accessibility audit on a Material UI application. You'll learn how to identify and fix common accessibility issues, use automated testing tools, and perform manual checks to ensure your application is usable by people with various disabilities.

## Prerequisites

- Completion of previous Material UI exercises
- Basic understanding of web accessibility principles (WCAG)
- Familiarity with screen readers (e.g., NVDA, VoiceOver)
- Node.js and npm installed on your machine

## Part 1: Automated Accessibility Testing

### 1. Set Up Automated Testing Tools

1. **Install `axe-core` and `react-axe`** for accessibility testing:

   ```bash
   npm install --save-dev axe-core react-axe
   ```

2. **Configure `react-axe`** in your `src/index.tsx` file to enable accessibility checks during development:

   ```typescript
   import React from "react";
   import ReactDOM from "react-dom";
   import App from "./App";

   if (process.env.NODE_ENV !== "production") {
     const axe = require("react-axe");
     axe(React, ReactDOM, 1000);
   }

   ReactDOM.render(
     <React.StrictMode>
       <App />
     </React.StrictMode>,
     document.getElementById("root")
   );
   ```

### 2. Run the Application

Start the application in development mode:

```bash
npm start
```

### 3. Check for Accessibility Violations

1. Open your browser's developer console to view any accessibility violations reported by `react-axe`.

2. Document any issues you find, including the component and the nature of the violation.

## Part 2: Manual Accessibility Audit

### 1. Keyboard Navigation

Test keyboard navigation throughout the application:

- Ensure all interactive elements (buttons, links, form fields) are focusable.
- Use the `Tab` key to navigate through the application and check the focus order.
- Verify that focus indicators are visible.

### 2. Screen Reader Testing

Use a screen reader to navigate the application:

- **For Windows**: Use NVDA or JAWS.
- **For Mac**: Use VoiceOver.

1. Navigate through the application using the screen reader.
2. Ensure that all important content is read aloud and makes sense contextually.
3. Check that form inputs have proper labels and instructions.

### 3. Color Contrast

Use a color contrast checker (e.g., WebAIM Contrast Checker) to verify that text has sufficient contrast with its background:

- Ensure that text color contrasts meet the WCAG AA standard (4.5:1 for normal text, 3:1 for large text).

### 4. Headings and Structure

Check that the page has a logical heading structure:

- Ensure that headings are used correctly (H1, H2, H3, etc.) and follow a hierarchical order.
- Verify that lists are marked up correctly (ul, ol, li).

### 5. ARIA Roles and Attributes

Ensure that ARIA roles and attributes are used appropriately:

- Check that interactive elements have the correct roles (e.g., buttons, links).
- Ensure that ARIA attributes are not misused or conflicting with native HTML semantics.

### 6. Form Validation

Test form submission with invalid data:

- Ensure that error messages are clearly associated with the relevant fields.
- Verify that users receive feedback when they attempt to submit invalid forms.

## Part 3: Fixing Accessibility Issues

### 1. Addressing Automated Violations

For each violation reported by `react-axe`, take the following steps:

- Identify the component that needs fixing.
- Update the component code to resolve the issue. For example, if a button is missing an `aria-label`, add it:

  ```typescript
  <Button aria-label="Submit form">Submit</Button>
  ```

### 2. Enhancing Keyboard Navigation

If you find that certain elements are not focusable or the focus order is incorrect, make adjustments:

- Use `tabIndex` to control focus order where necessary.
- Ensure that all interactive elements are keyboard-accessible.

### 3. Improving Screen Reader Compatibility

Ensure that all images have appropriate alt text:

```typescript
<img src="image.jpg" alt="Description of the image" />
```

### 4. Implementing ARIA Roles

If certain components lack ARIA roles, add them as needed:

```typescript
<div role="alert">This is an important message.</div>
```

## Part 4: Testing for Accessibility

### 1. Re-run Automated Tests

After making changes, re-run the application and check the console for any remaining accessibility violations.

### 2. Manual Testing

Repeat the manual testing steps to ensure that all accessibility issues have been addressed.

## Part 5: Documenting Your Findings

1. Create a document summarizing your accessibility audit findings, including:

   - List of identified issues
   - Steps taken to resolve each issue
   - Recommendations for future accessibility improvements

2. Showcase your completed project in your GitHub repository by pushing your changes:

```bash
git add .
git commit -m "Conducted accessibility audit and fixed issues"
git push origin main
```

## Conclusion

In this exercise, you conducted a thorough accessibility audit on a Material UI application. You learned how to identify and fix common accessibility issues, use automated testing tools, and perform manual checks to ensure your application is usable by people with various disabilities.

Accessibility is an ongoing process, and it's essential to incorporate these practices into your development workflow. By ensuring your applications are accessible, you create a better experience for all users.
