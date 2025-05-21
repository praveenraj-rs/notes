# css_basics

CSS cheat sheet with some common syntax and properties:

### Syntax

-   CSS is written in a "property: value;" format
-   Multiple properties can be combined in a single rule separated by semicolons
-   Rules are wrapped in curly braces {}

Example:

```css
selector {
  property1: value1;
  property2: value2;
}
```

### Selectors

-   Selectors are used to target specific HTML elements
-   Multiple selectors can be combined to target specific elements

Example:

```css
/* targeting elements with the class "example" */
.example {
  /* styles */
}

/* targeting the element with id "example" */
#example {
  /* styles */
}

/* targeting all h1 elements inside of the element with class "example" */
.example h1 {
  /* styles */
}
```

### Variables

```
:root {
  --main-color: #3498db;
  --accent-color: #e74c3c;
}

body {
  background-color: var(--main-color);
  color: #fff;
}

.accent-box {
  background-color: var(--accent-color);
}
```

### Properties

-   Properties are used to define the appearance of an element
-   Some common properties include:

#### Font Properties

-   font-family
-   font-size
-   font-weight
-   font-style

#### Color Properties

-   color
-   background-color

#### Box Properties

-   width
-   height
-   margin
-   padding
-   border

#### Display Properties

-   display
-   visibility

#### Positioning Properties

-   position
-   top
-   right
-   bottom
-   left

#### Text Properties

-   text-align
-   text-decoration
-   line-height
-   letter-spacing
-   word-spacing

#### Flexbox Properties

-   display: flex;
-   justify-content
-   align-items
-   flex-direction
-   flex-wrap

#### Grid Properties

-   display: grid;
-   grid-template-columns
-   grid-template-rows
-   grid-gap

#### Transition Properties

-   transition-property
-   transition-duration
-   transition-timing-function
-   transition-delay

#### Animation Properties

-   animation-name
-   animation-duration
-   animation-timing-function
-   animation-delay
-   animation-iteration-count
-   animation-direction

### Box Model

-   The CSS box model is used to define the layout and spacing of elements on a web page
-   It consists of the content, padding, border, and margin of an element
-   The content refers to the actual content inside the element, while padding adds space between the content and the border
-   The border surrounds the padding and content, and the margin adds space between the border and other elements on the page

### Display Property

-   The display property determines how an element is displayed on the page
-   Some common values for this property include: block, inline, inline-block, flex, and grid
-   Block elements take up the full width of their parent container and are displayed on a new line
-   Inline elements are displayed within a line of text and do not break the flow of text
-   Inline-block elements are similar to inline elements, but can have padding and margins applied to them
-   Flex and grid are layout models that allow for more


### Pseudo-classes

-   Pseudo-classes are used to apply styles to elements based on their state or position in the DOM
-   Some common pseudo-classes include :hover, :active, :visited, :first-child, :last-child, and :nth-child
-   Pseudo-classes are added to selectors using a colon : before the pseudo-class name

Example:

```css
/* style the link when the user hovers over it */
a:hover {
  color: red;
}

/* style the first child of an element */
li:first-child {
  font-weight: bold;
}
```

### Media Queries

-   Media queries allow you to apply different styles based on the size of the user's screen or device
-   They are written using the @media rule and can include specific styles for different screen sizes or device types
-   Common screen sizes include: mobile, tablet, desktop, and large desktop

Example:

```css
/* apply styles when the screen is smaller than 768px */
@media (max-width: 768px) {
  body {
    font-size: 14px;
  }
}

/* apply styles when the screen is larger than 1200px */
@media (min-width: 1200px) {
  body {
    font-size: 18px;
  }
}
```

### Box Shadow

-   The box-shadow property is used to add a shadow effect to an element
-   It takes values for the horizontal and vertical offset, blur radius, spread radius, and color of the shadow

Example:

```css
/* add a 2px black shadow to an element */
box-shadow: 2px 2px 2px 0px rgba(0, 0, 0, 1);
```

### Transitions and Animations

-   Transitions and animations allow you to create dynamic effects on your web page
-   Transitions are used to create a smooth transition between two states of an element, such as changing its color or position
-   Animations are used to create more complex effects, such as a bouncing ball or a loading spinner
-   Both transitions and animations are defined using CSS keyframes and can be triggered by user actions or automatically

Example:

```css
/* transition the background color of an element over 1 second */
transition: background-color 1s ease;

/* create a bouncing ball animation */
@keyframes bounce {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-50px);
  }
  100% {
    transform: translateY(0);
  }
}
```

### Flexbox

-   Flexbox is a layout model that allows you to easily align and position elements within a container
-   It is based on a flex container and flex items, and uses properties such as display, flex-direction, justify-content, and align-items to control the layout
-   Flexbox can be used for simple or complex layouts, such as creating a navigation bar or a card grid

Example:

### Flex

##### display
flex
##### justify-content
center, start, end, flex-start, flex-end,
##### align-items
center, start, end, flex-start, flex-end


```css
/* create a flex container and align its items */
.container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

/* create a flex item and set its width */
.item {
  flex-basis: 25%;
}
```

### Grid

-   CSS grid is another layout model that allows you to create complex, multi-dimensional layouts
-   It is based on a grid container and grid items, and uses properties such as display, grid-template-rows, grid-template-columns, and grid-gap to control the layout
-   Grid can be used for creating layouts such as a multi-column article or a pricing table

Example:
```css
/* create a grid container with 3 columns and 2 rows */
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 100px);
  grid-gap: 20px;
}

/* create a grid item and position it within the grid */
.item {
  grid-column: 2 / 3;
  grid-row: 1 / 2;
}
```

### Transforms

-   CSS transforms allow you to change the shape or position of an element, such as rotating, scaling, or translating it
-   Transforms can be applied to both 2D and 3D elements
-   Common transform functions include rotate(), scale(), and translate()

Example:

```css
/* rotate an element by 45 degrees */
transform: rotate(45deg);

/* scale an element by 2 times its original size */
transform: scale(2);

/* translate an element 50 pixels to the right and 20 pixels down */
transform: translate(50px, 20px);
```

Certainly, here are some notes on CSS link styling:

1. **Link Styles Basics:**
   - Links are an essential part of web navigation, connecting different pages and resources together.
   - CSS (Cascading Style Sheets) is used to style the appearance of links on a webpage.

2. **Pseudo-Classes:**
   - Pseudo-classes are used to define different states of a link, such as when it's hovered over, clicked, or unvisited.
   - Common pseudo-classes for links are `:link` (unvisited), `:visited` (visited), `:hover` (hovered over), and `:active` (clicked).

3. **Styling Link States:**
   - You can apply different styles to various link states using these pseudo-classes. For example:
     ```css
     /* Unvisited link */
     a:link {
         color: blue;
         text-decoration: underline;
     }

     /* Visited link */
     a:visited {
         color: purple;
     }

     /* Hovered link */
     a:hover {
         color: red;
         text-decoration: none; /* Removing underline, for example */
     }

     /* Clicked link */
     a:active {
         color: green;
     }
     ```

4. **Text Decoration:**
   - The `text-decoration` property controls whether the link text has an underline or strike-through.
   - Set it to `none` to remove underlines or strike-throughs.

5. **Colors:**
   - The `color` property defines the text color of the link in various states.

6. **Cursor Style:**
   - The `cursor` property can be used to change the cursor appearance when hovering over a link. For example:
     ```css
     a:hover {
         cursor: pointer;
     }
     ```

7. **Background Highlighting:**
   - You can add background color changes to create more interactive link styling:
     ```css
     a:hover {
         background-color: #f0f0f0;
     }
     ```

8. **Text Transformation:**
   - The `text-transform` property can be used to change the capitalization of the link text.

9. **Removing Default Styles:**
   - Browsers usually apply default styles to links. To remove them, you might use a CSS reset or a specific reset for links:
     ```css
     a {
         text-decoration: none;
     }
     ```

10. **Accessibility:**
    - Consider accessibility when styling links. Ensure that there's enough contrast between the link color and the background to make them easily readable.

11. **External Links:**
    - You can style external links differently to distinguish them from internal links:
      ```css
      a[href^="http"]:not([href*="yoursite.com"]) {
          /* Styles for external links */
      }
      ```

12. **Transitions and Animations:**
    - You can add transitions or animations to create smooth effects when link states change. For example, animating color changes.

Remember that these are just some of the basic concepts for styling links using CSS. Link styling can vary based on the design and requirements of your website. Always ensure that your chosen styles align with the overall look and feel of your site while also maintaining good usability and accessibility practices.


### Customizing Scrollbar and Creating Custom Cursor

```css
.page { 
  position: relative;
  width: 100px; 
  height: 200px;
}

.content {
   width: 100%;
}

.wrapper {
  position: relative;
  width: 100%; 
  height: 100%; 
  padding: 0; 
  overflow-y: scroll; 
  overflow-x: hidden; 
  border: 1px solid #ddd;
}

.page::after { 
  content:'';
  position: absolute;
  z-index: -1;
  height: calc(100% - 20px);
  top: 10px;
  right: -1px;
  width: 5px;
  background: #666;
}

.wrapper::-webkit-scrollbar {
    display: block;
    width: 5px;
}
.wrapper::-webkit-scrollbar-track {
    background: transparent;
}
    
.wrapper::-webkit-scrollbar-thumb {
    background-color: red;
    border-right: none;
    border-left: none;
}

.wrapper::-webkit-scrollbar-track-piece:end {
    background: transparent;
    margin-bottom: 10px; 
}

.wrapper::-webkit-scrollbar-track-piece:start {
    background: transparent;
    margin-top: 10px;
}
```
