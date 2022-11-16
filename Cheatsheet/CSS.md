# Font
Only import font and font weight necessary for optimization
# Variable
```css
/* Global */
:root {
    --text-color: blue;
}

body {
    color: var(--text-color, pink); /* pink is the fallback value */
}

/* Local */
.localDiv {
    --text-color: red;
}
```