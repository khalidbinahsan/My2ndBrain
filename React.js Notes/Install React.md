**Install React**

```bash
npm create vite@latest my-project
```

**Install with Tailwind**

```bash
npm install tailwindcss @tailwindcss/vite
```

**Vite Configuration**
Open `vite.config.js` (or `vite.config.ts`) in your root directory. Import the Tailwind plugin and add it to the `plugins` array.
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    react(),
    tailwindcss(),
  ],
})
```

**Import Tailwind in your CSS**
Open your main CSS file (usually `src/index.css`) and replace its entire content with a single import line. In v4, this replaces the old `@tailwind base;` directives.
```css
@import "tailwindcss";
```

**Start Styling!**
Now you can start the development server:
```bash
npm run dev
```

To test if it's working, go to `src/App.jsx` and add some Tailwind classes to an element:
```js
function App() {
  return (
    <h1 className="text-3xl font-bold underline text-blue-600">
      Hello world!
    </h1>
  )
}
```