Suppose you route is like this
```js
 {
    path: '/product/:id', 
    components: {
        default: Product,
        LeftSideBar: Sidebar
    },
    name: 'product',
},
```
Let see how you can get the **:id** params
```js
<script setup>
import { useRoute } from "vue-router";
const route = useRoute();
const id = route.params.id;
</script>
```