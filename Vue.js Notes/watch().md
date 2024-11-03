Watch function in vue 3 like a monitoring system. So you can monitor your variable or url with the **watch()** function. If anything of your variable is change the watch will run automatically. Let's see an example below
```js
import { ref, onBeforeMount, watch } from 'vue'
const postId = ref(1)
const fetchPost = () => {
    fetch(`https://jsonplaceholder.typicode.com/posts/${postId.value}`)
    .then(response => response.json())
    .then((data) => {
        post.value = data
    })
}
onBeforeMount(() => {
    fetchPost()
})
watch(postId, () => {
    fetchPost()
})
```
So when the postId value will change the fetchPost() function will call automatically. If you want to call the fetchPost() for the first time when the application is load, you can give a extra option **immediate: true** instead of using **onBeforeMount** 
```js
watch(postId, () => {
    fetchPost()
}, {immediate: true})
```
It will call the fetchPost() when application is load then start to watch your variable
## watchEffect()
**watchEffect()** is more than easier of **watch**. You don't need mention any value or options. Just call the function, it will watch your reactive value. If anyone of it is changed, the function will run.
```js
import { watchEffect } from 'vue'
const fetchPost = () => {
    fetch(`https://jsonplaceholder.typicode.com/posts/${postId.value}`)
    .then(response => response.json())
    .then((data) => {
        post.value = data
    })
}
watchEffect(() => {
	fetchPost()
})
```
## watch array
To watch the array item we need to add an extra options is `deep = true` 
```js
import { ref, computed, watch } from 'vue'
const items = [12, 14, 15]
const total = ref(0)
watch(items, (newItem, oldItem) => {
    total.value = newItem.reduce((acc, item) => acc + item, 0)
}, {deep: true, immediate: true})
```
You can see the how [[JS Functions#reduce()]] **reduce()** function work in js.