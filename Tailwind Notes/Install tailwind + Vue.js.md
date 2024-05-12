Here is the full process to install tailwind and Vue together
```shell
npm create vite@latest my-project
cd my-project
```

Then 
```shell
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Now go to your **tailwind.config.js** file and replace with this code
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

 Go ahead to your **style.css** and add the following code there
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Perfect! now run the dev command
```shell
npm run dev
```