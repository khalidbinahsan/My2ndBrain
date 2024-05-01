## How to install vue router?
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

You can give a name of your `<router-view></router-view>` like this
```html
<router-view name="sidebar"></router-view>
```

In this case you should make some changes on your **router** Ensure that the **component** is plural here **components**
```json
{
   path: '/blog',
   name: 'blog',
   components: {
        default: Blog,
        sidebar: rightSidebar
    }
}
```

## How to create the dynamic router?
Here is a router example for dynamic router
```json
 {
        path: '/blog/category/:name',
        components: {
            default: Blog,
            sidebar: rightSidebar
        },
        name: 'category'
    }
```

As you can see here on the path, the **:name** is the dynamic param. You can put any category name here like `/blog/category/lifestyle` and you can see your category with this code
```javascript
<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute()
const catname = ref(route.params.name)
</script>

<template>
	  <h2>{{ catname }}</h2>
</template>
```

But the problem the component is not loading in this case. The solution is for this issues to modified our `<router-view></router-view` and add **:key** like this way
```html
<router-view :key="$route.fullPath"></router-view>
```

There is another way to get the dynamic category name by using **watch**. In this case we don't need to make any changes on `<router-view></router-view>` Keep as it is and write the following code below
```javascript
<script setup>
import { ref, watch } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute()
const catname = ref('')
watch(()=>route.params.name, (newValue)=>{
    catname.value = newValue
})
</script>

<template>
	  <h2>{{ catname }}</h2>
</template>
```

There is one more easiest way by using **computed** Here is the example
```javascript
<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute()
const catname = computed(()=>{
    return route.params.name
})
</script>

<template>
	  <h2>{{ catname }}</h2>
</template>
```