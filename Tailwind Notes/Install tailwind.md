Install the package.json first
```bash
npm init -y
```
Then run this
```bash
npm install -D tailwindcss
npx tailwindcss init
```
Now add the config file in **tailwind.config.js**
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
Now create a **input.css** and add this
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```