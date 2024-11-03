```js
onBeforeMount(() => {
    fetch(`https://jsonplaceholder.typicode.com/posts/${postId.value}`)
    .then(response => response.json())
    .then((data) => {
        post.value = data
    })
})
```