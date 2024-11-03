This is very simple to define props and use that.
```js
<script setup>
const props = defineProps([
    'label', 'modelValue', 'type'
])
</script>
<template>
<h1>{{ label }}</h1>
</template>
```
If you pass a object with props then let's see how to access
```js
<script setup>
const props = defineProps(['product'])
</script>
<template>
<h1>{{ product.title }}</h1>
</template>
```

You can mention the data type of props and the default value
```js
<script setup>
	const props = defineProps({
		product: {
			type: string,
			default: "Product 1",
			required: true
		}
	})
</script>
```