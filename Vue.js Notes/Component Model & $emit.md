Included some example of component model that how can I change the model value from a component as well by using **$emit** 

**FormField.vue** file
```javascript
<script setup>
const props = defineProps([
    'label', 'modelValue', 'type'
])
const emit = defineEmits(['update:modelValue'])
</script>

<template>
<div class="flex flex-col mx-auto max-w-96 my-3">
    <label class="font-bold">{{ label }}</label>
    <input :type="type" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"  class="border-2 border-blue-400 mt-3 py-2 px-4 rounded">
</div>
</template>

<style scoped>  

</style>
```

**app.vue** file
```js
<script setup>
import {ref} from 'vue'
import FormField from './components/TextComponent.vue';
const name = ref('John Doe')
const email = ref('johndoe@gmail.com')
</script>

<template>
  <section class="mt-10">
    <div class="container">
      <div class="flex justify-center">
        <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
        <h2 class="text-2xl">Vue Component</h2>
      </div>
    </div>
  </section>
  <section class="my-10">
    <div class="container">
      <div class="mt-5">
        <FormField label="Name" type="text" v-model="name" />
        <FormField label="Email" type="email" v-model="email" />
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>
```

You can pass the multiple **v-model** like this way
```js
<Name v-model:fname="fname" v-model:lname="lname" />
```

and accept it this way
``` js
<script setup>
const props = defineProps([
    'fname', 'lname'
])
const emit = defineEmits(['update:fname', 'update:lname'])
</script>

<template>
<div class="flex flex-col mx-auto max-w-96 my-3">
    <label class="font-bold">First Name</label>
    <input type="text" :value="fname" @input="$emit('update:fname', $event.target.value)" class="border-2 border-blue-400 mt-3 py-2 px-4 rounded">
</div>
<div class="flex flex-col mx-auto max-w-96 my-3">
    <label class="font-bold">Last Name</label>
    <input type="text" :value="lname" @input="$emit('update:lname', $event.target.value)" class="border-2 border-blue-400 mt-3 py-2 px-4 rounded">
</div>
</template>

<style scoped>

</style>
```
The example above we are talking about, how to send data from **app.vue** to **component** through **v-model**
Now we see an another example about how to send data through **object** Let's see.....
```js
const person = reactive({
  name: 'John Doe',
  email: 'johndoe@gmail.com',
  password: '34555'
})
```
This a object and I want to send it to my component like this 
```js
<PersonComponent :person="person"/>
```

and this is the simple way to accept through **props**  and setup the **v-model**
```js
<script setup>
import FormField from './FormField.vue';
const props = defineProps(['person'])
</script>

<template>
<FormField label="Name" type="text" v-model="person.name" />
<FormField label="Email" type="email" v-model="person.email" />
<FormField label="Passowrd" type="password" v-model="person.password" />
</template>

<style scoped>

</style>
```

### emit for checkbox
this is how you work with emit for the checkbox
```js
<script setup>
const props = defineProps([
    'label', 'modelValue'
])
const emit = defineEmits(['update:modelValue'])
</script>

<template>
<label>{{ label }}</label>
<input @change="$emit('update:modelValue', $event.target.checked)" class="ml-2" type="checkbox" :checked="modelValue">
</template>

<style scoped>

</style>
```

we need to change two place for work with checkbox.
 * change the **@click** to **@change**
* change the $event.target.value** to **$event.target.checked**