Open your main CSS file (where you put `@import "tailwindcss";`) and add your custom breakpoints inside the `@theme` block:

```css
@import "tailwindcss";

@theme {
  /* Max Width 1566px */
  --breakpoint-2xl: 97.875rem; 
  /* Max Width 1350px */
  --breakpoint-xl: 84.375rem;
}
  
/* Manually applying the center logic to the utility */
@utility container {
  margin-inline: auto;
  padding-inline: 0.9375rem;
}
```