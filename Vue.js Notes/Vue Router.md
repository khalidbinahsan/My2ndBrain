## How to install vue router
First of all run this command on your project
```bash
npm install vue-router@4
```

Now create a **router** folder and **router.js** file and write your router here following the example below
```javascript
import { createRouter, createWebHistory } from 'vue-router'

import Home from '../components/Home.vue'

import About from '../components/About.vue'

import Contact from '../components/Contact.vue'

import Blog from '../components/Blog.vue'

import rightSidebar from '../components/RightSidebar.vue'

const routes = [

    {

        path: '/',

        name: 'home',

        component: Home

    },

    {

        path: '/about',

        name: 'about',

        component: About

    },

    {

        path: '/contact',

        name: 'contact',

        component: Contact

    },

    {

        path: '/blog',

        name: 'blog',

        components: {

            default: Blog,

            sidebar: rightSidebar

        }

    },

    {

        path: '/blog/category/:name',

        components: {

            default: Blog,

            sidebar: rightSidebar

        },

        name: 'category'

    }

]

  

const router = createRouter({

    history: createWebHistory(),

    routes: routes

})

  

export default router
```

Now go to your **main.js** file and make the following changes there
```javascript
import { createApp } from 'vue'

import './style.css'

import App from './App.vue'

import router from './router/router'

createApp(App).use(router).mount('#app')
```

Perfect! Now you can link up your router with the `<router-link></router-link>` like this
```html
<router-link :to="{name: 'home'}">Home</router-link>
```

and you can display it anywhere by `<router-view></router-view>` like this
```html
<router-view></router-view>
```
